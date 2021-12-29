# How to publish a new version of pico-engine

From Matthew, on slack:

sure, I can walk you though a publish again. do a 
```
npm run clean-setup
```
then 
```
npm run build
```
then do a 
```
git status
```
to make sure there are no pending changes. Then 
```
npm run publish
```
will ask you what version you want to publish

## Preparation

### Step 1

Make a clean clone of the [pico engine](https://github.com/Picolab/pico-engine.git).

### Step 2

Update the [change log](https://github.com/Picolab/pico-engine/blob/master/CHANGELOG.md) first,
by making a note of all the changes since the previous version.

### Step 3

Follow Matthew's instructions above.
