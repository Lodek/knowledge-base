```yml
```

# Intro
The twelve-factor app is a set of practices / principles for building and deploying software-as-a-service apps.
Its original inception is focused on developing software to run on the cloud.

## One codebase tracked in revision control, many deploys
Defines what an "app" is and enforces the use of version control.
One app maps to one repo (ie one codebase per app).
Multiple apps combine into a distributed system.

##  Explcitly declare and list dependencies
This principle enforces the reproducibility of the running environment.
Dependencies *must* be explictly declared or packages alongside the app.
Furthermore, it  enforces the use of environment isolation tools such as pythons venv.

Every 12 factor compliant app must declare or include it's dependencies.
The dependency upon externall shell tools must be packaged along the app.

> A twelve-factor app never relies on implicit existence of system-wide packages.

## Store config in the environment
Ayaya, I like this one.
I am guilty of the mentioned sins.

In fact, this nicely solves a problem that  I've been  having at work.
I should just delegate all values to the environment and setup a script to get the env values from somewhere.

TLDR Make your app read settings and values from the environment.
> A litmus test for whether an app has all config correctly factored out of the code is whether the codebase could be made open source at any moment, without compromising any credentials.

## Treat backing services as attached resources
External platforms / dependencies are treated as resources.
These are dependencies which can be considered apps on their own such as databases, caching, smtp server, log aggregators and etc.

The article proposes that there should be no distinction between a resource hosted locally or one consumed externally.
This practice reinforces the loosely coupled architecture proposed by the paper.



