# To do:
===================

* First of all, delivery pipeline must be implemented ([walking skeleton principle](http://alistair.cockburn.us/Walking+skeleton))
  * To make our pipeline simple, consistent and flexible we will use [Scripts To Rule Them All](https://github.com/github/scripts-to-rule-them-all) approach
  * Producing build artefact must me separated from integration testing.
  * Artefact will be immutable (docker image is OK)
  * Project is small enough so unit testing and packaging will be combined in one stage, as soon as it doesn't affects feedback loop time.
  * Build itself will be done in docker containers, using [multi-stage build](https://blog.alexellis.io/mutli-stage-docker-builds/)
* Let's make it more [12-factor](https://12factor.net)
  * Logging to stdout is OK, we will use [docker logging plugins](https://docs.docker.com/engine/admin/logging/plugins/) later to ship logs to ELK
  * Configuration in Java sources will be changed to use environment variables.
* Deployment
  * Will be enchaned incrementally (having skeleton waloking already)
  * Will start from simplest possible docker containers orchestration (probably docker-compose)
  * Depending on production environment, Docker Swarm, Mesos or, most probably, Kubernets will be utilized later. In case of Kubernetes will use [Compose to Docker](https://github.com/kubernetes/kompose) to maximise usage of previous done.
  * Canary, blue green, etc. Will be implemented later (postponed due to limited POC time)
* Other operational features
  * Will be implemented eventauly, according to priority list.
  * Health checks are both easy and high-priority, simple `HTTP GET` will be done at earliest possible time, more sophisticated `/health` endpoint will be implemented in source code by developers (will do smoke testing and testing of dependencies).
  * `/info` endpoint should be implemented, to expose current configuration, version info etc.
  * Monitoring will be implemented, using Prometheus. We can even make it auto-discoverable. JMX can be scraped at first. Application-specific metrics will be exposed to `/metrics` endpoint by developers.
  * Feature-toggling of new features will be also nice to have.
  * Having both feature-toggling and canary releases implemented, we can safely use [tesing and monitoring combined](https://www.theguardian.com/info/developer-blog/2016/dec/05/testing-in-production-how-we-combined-tests-with-monitoring)