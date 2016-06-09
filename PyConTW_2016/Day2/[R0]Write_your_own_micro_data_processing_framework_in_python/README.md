## Talk: Write your own micro data processing framework in python
- Info: https://tw.pycon.org/2016/events/talk/69113918303240246/
- Speaker: David Chen
- [Slides]( https://github.com/lucemia/slides/blob/master/slides/micropipeline.md)

* gliacloud.com
* What is a data processing framework;  what is a taskflow...

* [TaskFlow (OpenStack)](https://wiki.openstack.org/wiki/TaskFlow)
* [Luigi (Spotify)](https://github.com/spotify/luigi)
* [DataFlow (Google)](https://cloud.google.com/dataflow/)
* [Django-p](https://django-pipeline.readthedocs.io/en/latest/)
* [Google Pipeline API](https://github.com/GoogleCloudPlatform/appengine-pipelines)

#### Design of Django-P
* pipe: abstraction of pipline
* future: the return value from pipline would be given in the future
* pipeline: store config to db
* slot: store pipeline execution results
* barrier: to prevent running before its dependent task completed

Implemented by Python generator, thus, *asynchronous* programming can be achieved.