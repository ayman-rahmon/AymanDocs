# Background Processes


## Services:

* services : are meant for long running background tasks that don't need a visual component.
* runs even if the Activity/app is closed.
* Loader is used when:
  1. tied to the Activity life cycle.
  2. easy to make user interface changes  and communicatte with activities.
* service is used when:
1. de coupled from the user interface.
2. exists even when there is no user interface.

* ways to start a service:
1. start.
2. scheduale.
3. bind.

* JobService : is a service that executes at some point in the future or when some condition is met.
* Schedualer : defines when a JobService should run.
* bound services 	can easily comunicate back to the component(components like ui sound controlers).E.g: sound data .
