# Using Git
Version Control Systems are very important when collaborating with a team. They make it easy to view changes, rollback errors, and work in parallel with your coworkers.

## Commits

### How often should I commit?
You should commit quite often. Each commit should include the changes made to implement a single feature or fix a single bug. The more often you commit, the easier it is to find and fix errors and bugs.

### What should a commit message look like?
Clean and readable commit messages are essential for a better Git experience. Each commit must stand by itself, so its commit message also needs to stand by itself. You don't need to explain every change that is made, but include enough information so that we understand what the main goal of that commit was.

### How do I make a commit?
1. Stage all files using the `git add .` command. Alternatively only add specific files that you want to be staged.
1. Use the 'git commit' command.
1. Your text editor should open up. Write a short, descriptive commit message. Reference the issue by typing `See #<issue number>` on the next line after the commit message

## Branches
Branches will keep your code separate from production code until it has been reviewed and is ready to be added to the development branch.

### How many branches should I have?
Locally, you can have as many branches as you like. On Github, however, there should only be two branches: Master and Development. There may be a few other branches that appear temporarily, but once they are merged with development they should be deleted.

### How do I make a new branch?
1. Use

## Merging

### Merging with Development

### Merging with Master
