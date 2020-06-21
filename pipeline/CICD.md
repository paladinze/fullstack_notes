# CICD

## what is real CICD
1. build the right product
2. reduce risk of release
  MTBF vs MTRS
3. real project progress
  really work in production environments, not just local env
what qualifies as continous delivery?
  checks into trunk once a day
  every checkin results in test and build running


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
- setup workflow in .github/workflows

## jenkins

docker network create jenkins

docker volume create jenkins-docker-certs
docker volume create jenkins-data

docker container run --name jenkins-docker --rm --detach \
  --privileged --network jenkins --network-alias docker \
  --env DOCKER_TLS_CERTDIR=/certs \
  --volume jenkins-docker-certs:/certs/client \
  --volume jenkins-data:/var/jenkins_home \
  --volume "$HOME":/home \
  --publish 3000:3000 docker:dind

docker container run --name jenkins-tutorial --rm --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  --volume "$HOME":/home --publish 8080:8080 jenkinsci/blueocean


docker container exec -it jenkins-tutorial bash

docker logs jenkins-tutorial
