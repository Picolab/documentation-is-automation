Every year the code for calculating daylight savings time needs to be adjusted.
This can be done anytime _after_ the first Sunday in November of the current year.

Open the Wovyn Pico and its Rulesets tab.

Edit the `wovyn_probe_temp_recorder` ruleset.

Find the internal function bound to the name `makeMT` (whose job is convert GMT to Mountain Time).

```
    makeMT = function(ts){
      MST = time:add(ts,{"hours": -7});
      MDT = time:add(ts,{"hours": -6});
      MDT > "2020-11-01T02" => MST |
      MST > "2020-03-08T02" => MDT |
                               MST
    }
```

In the line that says "if MDT after yyyy-11-dd at 2 a.m. then use MST" 
(i.e. "Fall back")
put in the date of the first Sunday in November of the new year.

In the line that says "if MST after yyyy-03-dd at 2 a.m. then use MDT"
(i.e. "Spring forward")
put in the date of the second Sunday in March of the new year.

Register the ruleset.

At the time you make the change, MST is being used. After the change it will continue to be used
because of the default. But when 2 a.m. comes around on the second Sunday of March,
MDT will be used from then until 2 a.m. of the first Sunday of November.

Important to make this code change _before_ the Saturday preceeding the second Sunday of March
of the new year.
