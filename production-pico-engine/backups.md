# How to backup the production pico-engine

## On the pico-engine machine

`ssh` to the machine where it is running

`mkdir backups` in the home folder (needs to be done once)

`tar czf backups/$(date +%F-%H%M%S).tgz .pico-engine/db/` with a name of current date and time

### Note

As of June 2021, the production pico engine `db` folder is in `~/huh/.pico-engine/db` so the command to create a backup file would be
```
tar  czf  ~/backups/$(date +%F-%H%M%S).tgz  ~/huh/.pico-engine/db/
```

`exit`

## On the machine where backups will be kept

`scp -i <path to certificate> <machine>:<path from root>/backups/*.tgz .`

### Ensuring the backup works

`mkdir huh` make a test folder

`cd huh` and go into it

`tar -xvzf ../2020-02-06-143125.tgz` using the name of the latest backup file

This will recreate the data from the production pico-engine:

```
$ tree -a huh
huh
└── .pico-engine
    └── db
        ├── 005195.ldb
        ├── 005210.ldb
        ├── 005211.ldb
        ├── 005214.ldb
        ├── 005217.log
        ├── 005218.ldb
        ├── 005219.ldb
        ├── 005220.ldb
        ├── CURRENT
        ├── LOCK
        ├── LOG
        ├── LOG.old
        └── MANIFEST-005215
```

`PICO_ENGINE_HOME=<path from root>/huh/.pico-engine node packages/pico-engine/src/cli.js`

This will allow you to work with the snapshot of the production pico-engine.

