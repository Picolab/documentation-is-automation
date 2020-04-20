# How to make pull requests

This document is for pull requests of repositories owned by other organizations.
The example used is the [Aries RFCs repository](https://github.com/hyperledger/aries-rfcs).

## Make the fork

While visiting the repository in which you wish to make a pull request,
click the GitHub "Fork" button (near the top-right corner).

This creates a new repository in an organization to which you belong.
Your organization now owns a "fork" of the official repository.
For our running example, this is [Picolab/aries-rfcs](https://github.com/Picolab/aries-rfcs).

## Make a local clone

Before you can actually do a pull request, you need to have a local `git` repository.
Use the Clone button on the forked repo to obtain a URI, and issue commands like these on your local machine:

```
git clone git@github.com:Picolab/aries-rfcs.git
cd aries-rfcs/
```

## Keep your organization fork "even" with the official repo

When you are viewing your organization's fork, you'll see a line which says either
"This branch is even with hyperledger:master." or that it is either "behind" or "ahead"
by a certain number of commits.

Yours won't be "ahead" until after you have prepared changes for a pull request as described later.

When our fork is "behind" we need to bring it up-to-date.

To prepare for this, we must first define the official repo as "upstream" (this has to be done just once):

```
$ git remote add upstream https://github.com/hyperledger/aries-rfcs.git
$ git remote -v #verify
origin	git@github.com:Picolab/aries-rfcs.git (fetch)
origin	git@github.com:Picolab/aries-rfcs.git (push)
upstream	https://github.com/hyperledger/aries-rfcs.git (fetch)
upstream	https://github.com/hyperledger/aries-rfcs.git (push)
```

With "upstream" defined, these three steps will fetch the upstream commits (the ones we are "behind" with),
merge them into the local clone of our repo,
and push them into our organization's forked repository.

```
# to make my fork "even" with hyperledger:master
git fetch upstream
git merge upstream/master
git push
```

Having done these steps, refreshing the page showing our organization's forked repo should show,
"This branch is even with hyperledger:master."

## Make a change and issue a pull request

1. make a change in the local clone
1. do a `git add .` command in prepartion
1. do a `git commit -s -m "<message>"` command to commit the change locally
1. do a `git push` command to make the change in our organization's fork
1. refresh the GitHub page of our organization's fork

Now you should see your changes in the GitHub pages for our organization's fork.

In addition, you would now see that we are "1 commit ahead" of the official repo.

### Click on the Pull Request link

And follow the prompts to complete the request.
You'll have to wait for someone who has authority in the official organization
to approve the request.
