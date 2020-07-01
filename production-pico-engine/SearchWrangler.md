# Search Wrangler

Before a deprecated ruleset can be removed from a pico engine, it needs to be unregistered from all picos in the engine. With a large pico engine like the production instance of manifold, this can be difficult.

To help track down rulesets, I wrote a couple of rules that use the scatter-gather pattern to search each pico for a specified ruleset.

To get this to work, I needed each pico to have these rules installed, so I temporarily added them to the io.picolabs.wrangler ruleset that is installed on every pico.

## How it works
The Search rules use the scatter-gather pattern. The pico that starts the search raises an event in each one of its children, using one of its channels as a correlation identifier. Its children raise the event in each one of their children and so on until every pico has received the event.
The event raised in each pico checks to see if it has the ruleset installed. If it does, it uses the correlation identifier to raise an event in the pico that started the search alerting it that it has the sought after ruleset.
The ruleset_find_results function then can be used to check which picos responded.

## How to use it

Add this function to the global block, and be sure to share it:

```
ruleset_find_results = function() {
      ent:ruleset_find.defaultsTo({})
    }
```

and then add the following rules to the ruleset:

```
//==============================================================================
//                          Ruleset Locator
//==============================================================================
rule ruleset_find_scatter {
  select when wrangler ruleset_find_scatter where event:attr("toFind")

  foreach children().append(0) setting (child)
    pre {
      toRet = event:attr("eci").defaultsTo(meta:eci)
      toFind = event:attr("toFind")
      found = installedRulesets() >< toFind
    }
    if child then
    event:send({"eci": child{"eci"}, "domain": "wrangler", "type": "ruleset_find_scatter", "attrs":{ "toFind": toFind, "eci": toRet }})

    always {
      raise wrangler event "ruleset_find_report" attributes { "eci": toRet, "found": found, "toFind": toFind } on final
    }
}

rule ruleset_find_report {
  select when wrangler ruleset_find_report

  pre {
    toFind = event:attr("toFind").klog("RID")
    found = event:attr("found").klog("FOUND")
    toRet = event:attr("eci").klog("RETURN ECI")
    name = visual:dname()+":"+meta:picoId
  }

  if found && toFind && toRet && name then
    event:send({"eci": toRet, "domain": "wrangler", "type": "ruleset_find_gather", "attrs":{ "cid": toFind, "picoName": name }})
}

rule ruleset_find_gather {
  select when wrangler ruleset_find_gather

  pre {
    name = event:attr("picoName")
    cid = event:attr("cid")
  }
  if name && cid then noop();

  fired {
    ent:ruleset_find := ent:ruleset_find.defaultsTo({}).put(cid, ent:ruleset_find.defaultsTo({}){cid}.defaultsTo([]).append(name))
  }
}
```

Then raise the `ruleset_find_scatter` rule with the `toFind` attribute being the rid you are searching for inside the root pico. You can start from any pico, but it will only search that pico and its children. Raising the event in root will search every pico on the engine.
Give the engine some time to raise the event in each pico. Finally, call the `result_find_results` function to view the results.
