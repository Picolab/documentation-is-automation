# How to publish a new version of pico-engine

### Step 0

You'll need to have the `npm` cli on your machine and be signed in to an account with permission to publish.

https://docs.npmjs.com/packages-and-modules/contributing-packages-to-the-registry

Use `npm whoami` to see if you're logged in. 

### Step 1

Update the [change log](https://github.com/Picolab/pico-engine/blob/master/CHANGELOG.md),
by making a note of all the changes since the previous version.

### Step 2

Make sure you have the master or main branch checked out and up to date. npm publish doesn't know anything about branches so you need to make sure you have the correct code checked out b/c it will simply publish what's checked out in your folder.

A reliable way to make sure you have a clean checkout is to make a clean clone of the [pico engine](https://github.com/Picolab/pico-engine.git).

### Step 3

Make sure your dependencies are up to date.

From the repository root run:

```sh
npm i && npm run clean-setup
```

### Step 4

Make sure any generated files are not different than what is in git.

From the repository root run:

```sh
npm run build
git status
```

You should see no changes i.e. "working tree clean"

If there are new/changed files from the build, add them to git and push it.

### Step 5

Make sure you don't have any extra files. This is important b/c npm publish doesn't know or care about git. It simply will publish whatever files are in the folder. So this is why you want to make sure you have a clean checkout.

From the repository root run:

```sh
git status
```

You should see no changes i.e. "working tree clean"

Then run:

```sh
git clean -ndx
```

You should only see `node_modules` and `dist` folders.

For example, the following output is good, and we are ready to publish.

```
Would remove node_modules/
Would remove packages/krl-compiler/node_modules/
Would remove packages/krl-generator/node_modules/
Would remove packages/krl-parser/dist/test/
Would remove packages/krl-parser/node_modules/
Would remove packages/krl-stdlib/dist/
Would remove packages/krl-stdlib/node_modules/
Would remove packages/pico-engine-core/dist/
Would remove packages/pico-engine-core/node_modules/
Would remove packages/pico-engine-ui/node_modules/
Would remove packages/pico-engine/dist/
Would remove packages/pico-engine/node_modules/
```

If we see any other files in there, they should be removed before publishing.

### Step 5½

Be sure that you are logged in to `npm` before proceeding. Otherwise a commit will occur and have to be reverted.

To determine that you are logged in to `npm` run this command:

```
npm whoami
```

If you need to login, run this command:

```
npm adduser
```

and follow instructions. Once logged in to `npm` proceed to step 6.

### Step 6

Now we are ready to publish!

From the repository root run:

```sh
npm run publish
```

NOTE: `run` i.e. we are using `npm run publish` NOT `npm publish`

`npm run publish` will run our script in the package.json that under the hood uses [lerna](https://lerna.js.org/). Lerna will ask you which version you want to publish, and then do a series of checks. It will update your package.json files and commit them to git. Finally it will do `npm publish` in each package.

#### Troubleshooting

If lerna blows up it will likely leave a commit with those version number changes but the files may not have been published to npm.

First check npm to see what is published. You can do that by viewing the packages on the npm website. Or use the cli:

```sh
npm view krl-compiler version
npm view krl-generator version
npm view krl-parser version
npm view krl-stdlib version
npm view pico-engine version
npm view pico-engine-core version
```

If it didn't publish anything, you can undo lerna's commit. Resolve the issue. Then try again.

Here's one way to undo a single git commit: `git reset --soft HEAD~ && git reset -- .`
You may also need to remove the git tag: `git tag -l` to view your tags, and `git tag -d v1.2.0` to remove one

If it's too much of a hassle to undo the git stuff, you can try publishing again but increment the patch version.
