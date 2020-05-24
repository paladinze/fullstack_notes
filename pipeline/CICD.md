# CICD

## 12-Factor of DevOps
- once code base
- Explicitly declare and isolate dependencies
- Store config in the environment, not in code
- backing service should be swappable
- strictly seperate build, release and run stage
- run app as stateless process, use db for state, redis for cache
- export service via port binding
- scale out using the process model
- allows fast startup and graceful shutdown
- dev and prod should be the same
- Logs should be written to stdout app, collected by execution env
- allows to run one-time script for admin task


## pipeline environments
- 
- User Acceptance Test: user requirement is met or not

## value stream

## Travis workflow
- add code to branch
- merge new code to master
- travis: tigger test
- travis: build docker image
- travis: push docker image to the registry
- travis: deploy docker image to the server

## GoCD
- repo: material
  - trigger pipeline
- pipeline > jobs > task
  - jobs run in parallel
  - job runs tasks sequntially
- user store configurations in a repo
  - GoCD server watches for changes 
    - then create/update pipeline from configurations

## Bamboo
- project
  - one or more plans
  - reporting across all plans
    wallboard
- plan
  - has a single state
  - group jobs into multiple stages
  - run sequntial stages on same repo
  - specify 
    - default repo
    - how build is triggered
    - trigger dependencies between plans
    - notifications and build result
    - permission to configure plan and jobs
    - define plan varaibles
- stage
  - single job or multiple jobs
  - process jobs in parallel, on multiple agents
  - must complete all its jobs before the next can be processed
- job 
  - process tasks senquentially on the same agent
  - control the orders of task
  - match task requirement with agent capability
  - define build artificats
  - can only artifact from a previous stage
  - tag build result
- task
  - small and discrete
    - source code checkout
    - run a script
    - parse test result
  - run sequentially within a job


## github actions