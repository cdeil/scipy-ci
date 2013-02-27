# Continuous integration for scientific Python packages

This is an effort to create `scipy-ci`,
a continuous integration (CI) system for the scientific Python package ecosystem.

## The problem

Making and distributing a scientific Python package is easy.
Making it work for most users and avoid breakage of existing functionality over the years is hard,
because of the multitude of user systems:

* Several Linux, Mac OS X and Windows versions
* Python 2.6, 2.7, 3.2, 3.3 (some packages support even more versions)
* Multiple versions of dependencies,
  e.g. packages that are dependent on numpy should work with the numpy releases
  1.5, 1.6 and 1.7 from the past few years.

Up to now each package had their own little CI system ususally testing
only a few combinations, e.g. a lot of packages use https://travis-ci.org to test on Ubuntu Linux.
Other systems / versions were tested "in the field" by users, and the multitude of bug reports
show that things do go wrong quite frequently.

## The solution

Actually this is not *the solution*, but it would certainly if we join forces and set up a central CI
system, i.e. a server with a dashboard summarizing / archiving all builds, and a bunch of build slaves.

The hope is that by pooling resources and knowledge we will achieve that in the end every scientific
Python package is covered by a large test matrix and developers can spend more time on new features
because they have to spend less time on maintenance.

If there is a test error we will (automatically or manually) create an issue in the tracker of that
project and if needed give the developer ssh access to that machine so that he can debug it himself.

Another thing that is important is to (automatically or quick to add manually)
test release candidates to catch problems before the release happens.

## The plan

This project is just starting (Feb 2013), `scipy-ci` doesn't exist yet, we are in the process of
figuring out how to set it up.

We have started by setting up a [jenkins-ci](http://jenkins-ci.org) server on a
[numfocus](http://numfocus.org)-sponsored Mac at TODO.
At the moment there is a small test matrix for numpy and scipy,
which we plan to expand to the [Scipy stack](http://scipy.github.com/stackspec.html)
and eventually include other scientific Python packages.
Please note that this is just to get some experience, whether we will use Jenkins or
[Jetbrains Teamcity](http://www.jetbrains.com/teamcity/) or 
[Atlassian Bamboo](http://www.atlassian.com/software/bamboo/overview) or one of the
other continous integration systems on the market for `scipy-ci` will be discussed,
possibly there will be a trial-and-error phase where we try out a few promising options.

For now we don't have a webpage or mailing list.
Please write to the [numfocus mailing list](https://groups.google.com/forum/?fromgroups#!forum/numfocus)
if you want to help set up and maintain `scipy-ci` or if you might be able to contribute
build machines at your organization / home or money to buy more build machines via Numfocus.

TODO: Announce a google hangout "Kickoff discussion on scipy-ci"

## Existing continous integration systems.

We don't want to re-invent the wheel, so let's first look at the existing continous integration systems.

### travis-ci

A lot of scientific Python packages use [travis-ci](https://travis-ci.org) to automatically test their master
branch and pull requests. It's free, has great github integration, but only tests Ubuntu Linux and has a build
timeout of 15 minutes, i.e. scipy or packages depending on scipy can't use it because the build times out.
Also it's for Ubuntu Linux only and probably isn't flexible enough to set up `scipy-ci` as we describe it above.

Examples:
* [numpy](https://travis-ci.org/numpy/numpy)
* [ipython](https://travis-ci.org/ipython/ipython)
* [matplotlib](https://travis-ci.org/matplotlib/matplotlib)
* [astropy](https://travis-ci.org/astropy/astropy)

### shiningpanda-ci

[shiningpanda-ci](https://jenkins.shiningpanda.com/astropy/) is a low-cost (was free when they started up)
hosted continous integration system.
They run a Jenkins server for you and offer Linux and Windows build machines, and let you add other build machines
if you want more build power or e.g. also test on Macs.

Given that we have a numfocus-sponsored server for `scipy-ci` where we have root access and can set up whatever
we like, I don't think we want to use shiningpanda-ci, but it is a good example to look at.

Examples:

* [ipython](https://jenkins.shiningpanda.com/ipython/)
* [astropy](https://jenkins.shiningpanda.com/astropy/)

### Scientific Python CI systems

Here are links to the CI dashboards for the [Scipy stack](http://scipy.github.com/stackspec.html) packages:

* Numpy: [travis-ci](https://travis-ci.org/numpy/numpy), ??
* Scipy: [buildbot](http://buildbot.scipy.org)
* matplotlib: [travis-ci](https://travis-ci.org/matplotlib/matplotlib)
* IPython: [travis-ci](https://travis-ci.org/ipython/ipython)
* Pandas: 
* Sympy: 

Other scientific Python packages:

* Nipy: [buildbot](http://nipy.bic.berkeley.edu/builders)
* Astropy: [travis-ci](https://travis-ci.org/astropy/astropy)

It's good to make this more complete, feel free add links and make a pull request.

### Non-Python CI systems

The following projects could also be useful to look at, because they are similar in spirit to what
we want to do, even if they are not for Python:

* http://openbuildservice.org (for testing / packaging on multiple Linuxes)
* http://upstream-tracker.org (an example of testing for API breakage of C / C++ / Java libraries)
