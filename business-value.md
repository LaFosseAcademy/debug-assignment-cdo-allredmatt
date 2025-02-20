# Business Value

## Micro-services and Cloud resources

#### Pros
- Using cloud based services allows quick increase or reduction in capacity as serves don't need to be physically build and power on premises, and don't have to be tied to physical locations of business premises.
- Seperating the API into small micro-services allows the different services to be managed and updated sperately.
- It allows for mutliple instances to be run of the same service to be run, shutting down or adding ones as demand requires. If one aspect of the application is in more demand this part only can be scaled up and load balanced, if needed, to prevent bottle necks a larger monolith service could create. 
- Running docker hub images hosted on the cloud allows for the rapid deployment of additional servers in different areas, or multiple servers spreading the load to each one.
- Hosting on cloud services allows quick expansion to a quicker or larger server without having to invest in new hardware.
- Further configuration could be made to allow this build and deployment process to be an automated pipeline that is triggered upon successfully testing of updated code. This can improve deployment times and reduce human error.
- Further automation could be introduced to add or remove services that are running based on demand. This could also reduce the cost implication of hosting.


#### Cons
- Cloud services can be expensive to use, if you only have limited users and very predictable traffic a in-house hosted server may be cheaper to run.
- One repository hosting all aspects of the project - a monolith - can be easier to setup and maintain at first, or with a small codebase and simple architechture. Having a lower amount of code to get to a MVP.
- Having local hardware, if configured correctly and managed effectivily, may allow a more secure data store; especially with very sensitive data needs that may need to be kept in house. However if an in house expertise isn't availible then using a cloud provider to facilitate this may result in a more secure setup as they may well have the best expertise.