# Go-Live Assessment - Application View

# Navigation Menu

- [Design Principles](#design-principles)
- [Definition of Workload](#Workload-Definition)
- [Application Assessment Checklist](#Application-Assessment-Checklist)
  - [Application Design](#Application-Design)
    - [Design](#Design)
    - [Failure Mode Analysis](#Failure-Mode-Analysis)
    - [Targets &amp; Non-Functional Requirements](#Targets--Non-Functional-Requirements)
    - [Key Scenarios](#Key-Scenarios)
    - [Dependencies](#Dependencies)
    - [Application Composition](#Application-Composition)
    - [Threat Analysis](#Threat-Analysis)
    - [Security Criteria &amp; Data Classification](#Security-Criteria--Data-Classification)
    - [Transactional](#Transactional)
  - [Health Modelling &amp; Monitoring](#Health-Modelling--Monitoring)
    - [Application Level Monitoring](#Application-Level-Monitoring)
    - [Resource and Infrastructure Level Monitoring](#Resource-and-Infrastructure-Level-Monitoring)
    - [Monitoring and Measurement](#Monitoring-and-Measurement)
    - [Dependencies](#Dependencies)
    - [Data Interpretation &amp; Health Modelling](#Data-Interpretation--Health-Modelling)
    - [Dashboarding](#Dashboarding)
    - [Alerting](#Alerting)
  - [Capacity &amp; Service Availability Planning](#Capacity--Service-Availability-Planning)
    - [Scalability &amp; Capacity Model](#Scalability--Capacity-Model)
    - [Service Availability](#Service-Availability)
    - [Service SKU](#Service-SKU)
    - [Efficiency](#Efficiency)
  - [Application Platform Availability](#Application-Platform-Availability)
    - [Service SKU](#Service-SKU)
    - [Compute Availability](#Compute-Availability)
  - [Data Platform Availability](#Data-Platform-Availability)
    - [Service SKU](#Service-SKU)
    - [Consistency](#Consistency)
    - [Replication and Redundancy](#Replication-and-Redundancy)
  - [Networking &amp; Connectivity](#Networking--Connectivity)
    - [Connectivity](#Connectivity)
    - [Zone-Aware Services](#Zone-Aware-Services)
    - [Endpoints](#Endpoints)
    - [Data flow](#Data-flow)
  - [Application Performance Management](#Application-Performance-Management)
    - [Data Size/Growth](#Data-SizeGrowth)
    - [Data Latency and Throughput](#Data-Latency-and-Throughput)
    - [Network Throughput and Latency](#Network-Throughput-and-Latency)
    - [Elasticity](#Elasticity)
  - [Security &amp; Compliance](#Security--Compliance)
    - [Compliance](#Compliance)
    - [Separation of duties](#Separation-of-duties)
    - [Control-plane RBAC](#Control-plane-RBAC)
    - [Authentication and authorization](#Authentication-and-authorization)
    - [Security Center](#Security-Center)
    - [Network Security](#Network-Security)
    - [Encryption](#Encryption)
  - [Operational Procedures](#Operational-Procedures)
    - [Recovery &amp; Failover](#Recovery--Failover)
    - [Configuration &amp; Secrets Management](#Configuration--Secrets-Management)
    - [Operational Lifecycles](#Operational-Lifecycles)
    - [Patch &amp; Update Process (PNU)](#Patch--Update-Process-PNU)
    - [Incident Response](#Incident-Response)
  - [Deployment &amp; Testing](#Deployment--Testing)
    - [Application Code Deployments](#Application-Code-Deployments)
    - [Application Infrastructure Provisioning](#Application-Infrastructure-Provisioning)
    - [Build Environments](#Build-Environments)
    - [Testing &amp; Validation](#Testing--Validation)
  - [Operational Model &amp; DevOps](#Operational-Model--DevOps)
    - [General](#General)
    - [Roles &amp; Responsibilities](#Roles--Responsibilities)
  - [Performance Testing](#Performance-Testing)
    - [Tools &amp; Planning](#Tools--Planning)
    - [Benchmarking](#Benchmarking)
    - [Load Capacity](#Load-Capacity)
    - [Troubleshooting](#Troubleshooting)
  - [Governance](#Governance)
    - [Standards](#Standards)
    - [Financial Management &amp; Cost Models](#Financial-Management--Cost-Models)
    - [Culture &amp; Dynamics](#Culture--Dynamics)
    - [Licensing](#Licensing)


# Design Principles

The following Design Principles provide context for questions, why a certain aspect is important and how is it applicable to Go-Live.

These critical design principles are used as lenses to assess the Go-Live of an application deployed on Azure, providing a framework for the application assessment questions that follow.


## Optimize build and release processes


  From provisioning with Infrastructure as Code, to build and releases with CI/CD pipelines, to automated testing, embrace software engineering disciplines across your entire environment. This approach ensures the creation and management of environments throughout the software development lifecycle is consistent, repeatable, and enables early detection of issues.



## Dynamically allocate and de-allocate resources to match performance needs


  Identify idle or underutilised resources (e.g. through Azure Advisor or other tools) and reconfigure, consolidate or shut down.



## Set up budgets and keep within cost constraints


  Consider the budget constraints as part of the architectural design, identifying acceptable boundaries pertaining to scale, redundancy, and performance against cost. After initial estimations, set budgets and alerts at different scopes to continuously measure the cost.



## Choose the correct resources for your business goals


  Choose the right resources that are aligned with business goals and can handle the performance needs of the workload. When onboarding new workloads explore the possibility of modernization and cloud native offerings where possible. Using the PaaS or SaaS layer as opposed to IaaS is typically more cost effective.



## Model and test against potential threats


  Establish procedures to identify and mitigate known threats. Use penetration testing to verify threat mitigation, as well as static code analysis and code scanning to detect and prevent future vulnerabilities.



## Protect against code level vulnerabilities


  Identify and mitigate code-level vulnerabilities (e.g. cross-site scripting, SQL injection). Regularly incorporate security fixes and patching of all parts of the codebase, including dependencies, into the operational lifecycle.



## Identify and protect endpoints


  Monitor and protect the network integrity of internal and external endpoints through security appliances, such as firewalls or web application firewalls. Use industry standard approaches to protect against common attack vectors, such as DDoS (e.g. SlowLoris).



## Monitor security of entire system and plan incident responses


  Correlate security and audit events to model application health and identify active threats. Establish automated and manual procedures to respond to incidents leveraging SIEM tooling for tracking.



## Classify and encrypt Data


  Classify data according to risk and apply industry standard encryption at rest and in transit holistically, ensuring keys and certificates are stored securely and managed properly.



## Automate and use least privilege


  Implement least privilege throughout the application and control plane to protect against data exfiltration and malicious actor scenarios. Drive automation through DevSecOps to minimize the need for human interaction.



## Optimise your workloads and aim for scalable costs


  Consider the usage metrics and performance to determine the number of instances used as your workload cost should scale linearly with demand. The cost management process should be rigorous, iterative and a key principle of responsible cloud optimization.



## Plan resources and determine how to harden them


  Ensure that security is taken into account when resources used by this workload are planned, and that it's understood how individual cloud services are protected. Use a service enablement framework to evaluate.



## Design for Self-Healing


  Self Healing describes a system's ability to deal with failures automatically through pre-defined remediation protocols connected to failure modes within the solution. It is an advanced concept that requires a high level of system maturity with monitoring and automation, but should be an aspiration from inception to maximize reliability.



## Drive Automation


  One of the leading causes of application downtime is human error, whether that be due to the deployment of insufficiently tested software to misconfiguration. To minimize the possibility and impact of human errors, it is vital to strive for automation in all aspects of a cloud solution to improve reliability; automated testing, deployment, and management.



## Observe Application Health


  Before issues impacting application reliability can be mitigated, they must first be detected. By monitoring the operation of an application relative to a known healthy state it becomes possible to detect or even predict reliability issues, allowing for swift remedial action to be taken.



## Design for Failure


  Failure is impossible to avoid in a highly distributed multi-tenant environment like Azure. By anticipating failures, from individual components to entire Azure regions, a solution can be developed in a resilient way to increase reliability.



## Design for Business Requirements


  Reliability is a subjective concept and for an application to be appropriately reliable it must reflect the business requirements surrounding it. For example, a mission-critical application with a 99.999% SLA requires a higher level of reliability that another application with an SLA of 95%. There are obvious financial and opportunity cost implications for introducing greater reliability and high availability, and this trade-off should be carefully considered.



## Use loosely coupled architecture


  Enable teams to independently test, deploy, and update their systems on demand without depending on other teams for support, services, resources, or approvals.



## Embrace continuous operational improvement


  Continuously evaluate and refine operational procedures and tasks, while striving to reduce complexity and ambiguity. This approach enables an organization to evolve processes over time, optimizing inefficiencies and learning from failures.



## Rehearse recovery and practice failure


  Run DR drills on regular cadence and use chaos engineering practices to identify and remediate weak points in application reliability. Regular rehearsal of failure will validate the effectiveness of recovery processes and ensure teams are familiar with their responsibilities.



## Understand operational health through focused and assertive monitoring


  Implement systems and processes to monitor build and release processes, infrastructure health, and application health. Telemetry is critical to understanding the health of a workload and whether the service is meeting the business goals.



## Design for Scale-out


  Scale-out is a concept that focuses on a system's ability to respond to demand through horizontal growth. This means that as traffic grows, _more_ resource units are added in parallel instead of increasing the size of the existing resources. A systems ability to handle expected and unexpected traffic increases through scale-units is essential to overall reliability and further reduces the impact of a single resource failure.



## Continuously monitor and optimise your cost management


  Conduct regular cost reviews, measure and forecast the capacity needs so that you can provision resources dynamically and scale with demand.




---



# Definition of Workload

To ensure a successful assessment it is important to scope it to the right customer *workload*. We realize that the term is quite ambiguous and used in various contexts, so for the Well Architected assessments, we define it as:

*A "workload" or "application" is a resource or collection of resources that provide end-to-end functionality to one or multiple clients (humans or systems). Another way to think of it: A workload is an end-to-end scenario (a process) and the IT infrastructure supporting it. It can be one application, it can be multiple apps, APIs and databases working together to deliver a specific functionality.*

Some examples:
* The Azure part of ticket ordering workload would be 1) the client web application, used by consumers to book tickets, 2) the payment gateway used to process credit card transactions, 3) the backend API handling communication, 4) the database where everything is stored, 5) the gateway to on-premises systems handling capacities and available seats, 5) the admin web application, 6) the shared AAD supporting authentication for administrators across the organization... etc.
* A data processing pipeline, which every night 1) ingests data from SAP and other on-premises systems, 2) runs data analytics workbooks on Azure Databricks, 3) stores results into Storage Accounts, 4) is accessed by a desktop application, 5) only for authenticated users from the organization.

Compared to reviewing the whole Azure landscape of an organization, this focus allows us to go deeper into the workload and architecture and provide more relevant recommendations, which are quite often transferrable to other workloads within the same customer as well. 

# Application Assessment Checklist
## Application Design
    
### Design
            
* Was the application built natively for the cloud or was an existing on-premises system migrated?

  _Understanding if the application is cloud-native or not provides a very useful high-level indication about potential technical debt for operability and cost efficiency._
  > While cloud-native workloads are preferred, migrated or modernized applications are reality and they might not utilize the available cloud functionality like auto-scaling, platform notifications etc. Make sure to understand the limitations and implement workarounds if available.
* Does the organization use cloud native security controls for this workload?

  _Native security controls are maintained and supported by the service provider, eliminating, or reducing effort required to integrate external security tooling and update those integrations over time._
  > Use native security capabilities in application services
* Does the workload hide detailed error messages / verbose information from the end user / client?

  _Providing unnecessary information to end users in case of application failure should be avoided. Revealing detailed error information (call stack, SQL queries, out of range errors...) can provide attackers with valuable information about the internals of the application. Error handlers should make the application fail gracefully and log the error._
  > Do not expose security details in error messages. Handle exceptions and failures gracefully (with retry logic) and log them for further inspection.
* Does this workload use cloud services for well-established functions instead of building custom service implementations?

  _Developers should use services available from a cloud provider for well-established functions like databases, encryption, identity directory, and authentication instead of writing custom versions or third-party solutions that must be integrated into the cloud provider._
  > Use services available from a cloud provider for well-established functions like databases, encryption, identity directory, and authentication
* Has a Business Continuity Disaster Recovery (BCDR) strategy been defined for the application and/or its key scenarios?

  _A disaster recovery strategy should capture how the application responds to a disaster situation such as a regional outage or the loss of a critical platform service, using either a re-deployment, warm-spare active-passive, or hot-spare active-active approach. To drive cost down consider splitting application components and data into groups. For example: 1) must protect, 2) nice to protect, 3) ephemeral/can be rebuilt/lost, instead of protecting all data with the same policy._
    - If you have a disaster recovery plan in another region, have you ensured you have the needed capacity quotas allocated?

      _Quotas and limits typically apply at the region level and, therefore, the needed capacity should also be planned for the secondary region._
* Is an availability strategy defined? i.e. multi-geo, full/partial

  _An availability strategy should capture how the application remains available when in a failure state and should apply across all application components and the application deployment stamp as a whole such as via multi-geo scale-unit deployment approach. There are cost implications as well: More resources need to be provisioned in advance to provide high availability. Active-active setup, while more expensive than single deployment, can balance cost by lowering load on one stamp and reducing the total amount of resources needed._
* Is the application deployed across multiple Azure subscriptions?

  _Understanding the subscription landscape of the application and how components are organized within or across subscriptions is important when analyzing if relevant subscription limits or quotas can be navigated._
* Has the application been designed to scale-out?

  _Azure provides elastic scalability, however, applications must leverage a scale-unit approach to navigate service and subscription limits to ensure that individual components and the application as a whole can scale horizontally. Don't forget about scale in as well, as this is important to drive cost down. For example, scale in and out for App Service is done via rules. Often customers write scale out rule and never write scale in rule, this leaves the App Service more expensive._
  > Design your solution with scalability in mind, leverage PaaS capabilities to [scale out](https://docs.microsoft.com/azure/architecture/guide/design-principles/scale-out) and in by adding additional instances when needed
  
    Additional resources:
    - [Design to scale out](https://docs.microsoft.com/azure/architecture/guide/design-principles/scale-out)
* Is the application designed to use managed services?

  _Platform-as-a-Service (PaaS) services provide native resiliency capabilities to support overall application reliability and native capabilities for scalability, monitoring and disaster recovery._
  > Where possible prefer Platform-as-a-Service (PaaS) offerings to leverage their advanced capabilities and to avoid managing the underlying infrastructure
  
    Additional resources:
    - [Use managed services](https://docs.microsoft.com/azure/architecture/guide/design-principles/managed-services)
  
    - [What is PaaS?](https://azure.microsoft.com/overview/what-is-paas/)
* Is platform-specific information (e.g. web server version) removed from server-client communication channels in this workload?

  _Information revealing the application platform, such as HTTP banners containing framework information ("`X-Powered-By`", "`X-ASPNET-VERSION`"), are commonly used by malicious actors when mapping attack vectors of the application. HTTP headers, error messages, website footers etc. should not contain information about the application platform. Azure CDN or Cloudflare can be used to separate the hosting platform from end users, Azure API Management offers [transformation policies](https://docs.microsoft.com/azure/api-management/api-management-transformation-policies) that allow to modify HTTP headers and remove sensitive information._
  > Remove platform-specific information from HTTP headers, error messages, and web site content
    - Does the workload use API Management or Azure Front Door to modify HTTP headers and remove sensitive information?

      _Azure API Management and Azure Front Door offers transformation policies that allow to modify HTTP headers and remove sensitive information._
      > Remove sensitive information from HTTP headers with Azure API Management or Azure Front Door
* Can the application operate with reduced functionality or degraded performance in the presence of an outage?

  _Avoiding failure is impossible in the public cloud, and as a result applications require resilience to respond to outages and deliver reliability. The application should therefore be designed to operate even when impacted by regional, zonal, service or component failures across critical application scenarios and functionality._
* Is component proximity required for application performance reasons?

  _If all or part of the application is highly sensitive to latency it may mandate component co-locality which can limit the applicability of multi-region and multi-zone strategies._
  > Consider using the same datacenter region, Availability Zone and [Proximity Placement Groups](https://azure.microsoft.com/blog/announcing-the-general-availability-of-proximity-placement-groups/) and other options to bring latency sensitive components closer together. Keep also in mind that additional charges may apply when chatty workloads are spread across zones and region.
* Is there a plan to modernize the workload?

  _Is there a plan to change the execution model to Serverless? To move as far as you can up the stack towards cloud-native. When the workload is serverless, it’s charged only for actual use, whereas whith traditional infrastructure there are many underlying things that need to be factored into the price. By applying an end date to the application it encourages you to discuss the goal of re-designing the application to make even better use of the cloud. It might be more expensive from an Azure cost point of view but factoring in other things like licenses, people, time to deploy can drive down cost._
* Is the application implemented with strategies for resiliency and self-healing?

  _Strategies for resiliency and self-healing include retrying transient failures and failing over to a secondary instance or even another region._
  > Consider implementing strategies and capabilities for resiliency and self-healing needed to achieve workload availability targets. Programming paradigms such as retry patterns, request timeouts, and circuit breaker patterns can improve application resiliency by automatically recovering from transient faults.
  
    Additional resources:
    - [Designing resilient Azure applications](https://docs.microsoft.com/azure/architecture/framework/resiliency/app-design)
  
    - [Error handling for resilient applications](https://docs.microsoft.com/azure/architecture/framework/resiliency/app-design-error-handling)
* Is the application architecture designed to use Availability Zones within a region?

  _[Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview#availability-zones) can be used to optimize application availability within a region by providing datacenter level fault tolerance. However, the application architecture must not share dependencies between zones to use them effectively. It is also important to note that Availability Zones may introduce performance and cost considerations for applications which are extremely 'chatty' across zones given the implied physical separation between each zone and inter-zone bandwidth charges. That also means that AZ can be considered to get higher Service Level Agreement (SLA) for lower cost. Be aware of [pricing changes](https://azure.microsoft.com/pricing/details/bandwidth/) coming to Availability Zone bandwidth starting February 2021._
  > Use Availability Zones where applicable to improve reliability and optimize costs
  
    Additional resources:
    - [Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview#availability-zones)
* Was your application architected based on prescribed architecture from the Azure Architecture Center or a Cloud Design Pattern?

  _Starting with a prescribed, proven architecture may help with alleviating some basic performance issues. It is suggested to check out the Azure Architecture Center and Cloud Design Patterns to determine if the application's architecture is similar._
* What datastores are you using? Were you able to choose the datastore during the design phase?

  _Your application will most likely require more than one type of datastore depending on business requirements. Choosing the right mix and correct implementation is extremely important for optimizing application performance._
* When designing the application, which of the following design considerations were considered? (Latency between layers, Request time, Payload sizes, High Availability)

  _When designing a new application or reviewing and existing one, there are three concepts to think about: 1) reducing latency; 2) reducing total request time; and, 3) reducing overall payload sizes. Implementing any combination of these concepts can dramatically improve overall application performance._
* Is the workload deployed across multiple regions?

  _Multiple regions should be used for failover purposes in a disaster state, as part of either re-deployment, warm-spare active-passive, or hot-spare active-active strategies. Additional cost needs to be taken into consideration - mostly from compute, data and networking perspective, but also services like [Azure Site Recovery (ASR)](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)._
  > Deploy across multiple regions for higher availability
  > 
  > *The ultimate goal is to set up the infrastructure in a way that it's able to automatically react to regional disasters. While active-active configuration would be the north star, not every workload requires two regions running simultaneously at all times, some don't even support it due to technical limitations. Depending on the availability, performance and cost requirements, passive or warm standby can be viable alternatives too.*
    - Were regions chosen based on location and proximity to your users or based on resource types that were available?

      _Not only is it important to utilize regions close to your audience, but it is equally important to choose regions that offer the SKUs that will support your future growth. Not all regions share the same parity when it comes to product SKUs._
      > Plan your growth, then choose regions that will support those plans
  
      Additional resources:
        - [Products available by region](https://azure.microsoft.com/global-infrastructure/services/)
    - Are paired regions used?

      _[Paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) exist within the same geography and provide native replication features for recovery purposes, such as Geo-Redundant Storage (GRS) asynchronous replication. In the event of planned maintenance, updates to a region will be performed sequentially only._
  
      Additional resources:
        - [Business continuity with Azure Paired Regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)
    - Have you ensured that both (all) regions in use have the same performance and scale SKUs that are currently leveraged in the primary region?

      _When planning for scale and efficiency, it is important that regions are not only paired, but homogenous in their service offerings. Additionally, you should make sure that, if one region fails, the second region can scale appropriately to sufficiently handle the influx of additional user requests._
  
      Additional resources:
        - [Products available by region](https://azure.microsoft.com/en-us/global-infrastructure/services/)
  
    Additional resources:
    - [Failover strategies](https://docs.microsoft.com/azure/availability-zones/az-overview#availability-zones)
  
    - [About Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview)
* Does the application have components on-premises or in another cloud platform?

  _Hybrid and cross-cloud workloads with components on-premises or on different cloud platforms, such as AWS or GCP, introduce additional operational considerations around achieving a 'single pane of glass' for operations._
  > Make sure that any hybrid or cross cloud relationships and dependencies are well understood
* Is the workload designed to scale independently?

  _If the workload contains multiple components and one component requires scale, this triggers scale-out/up of the entire infrastructure. It needs to be evaluated if the application scale is monolithic or each component is scaled independently and for example how the database scales with the rest of the workload._
* Would you consider the application design to be a microservice architecture?

  _As compared to a monolithic architecture--an application that is tightly coupled with synchronous communication and often a single datastore--microservices leverage concepts such as asynchronous communication, service discovery, various resiliency strategies, and each service has its own datastore._
    - Are your microservices using independent datastores or sharing the same datastore (e.g. a single database server that has multiple databases/tables is still considered a single datastore)?

      _One of the fundamental concepts of a microservice is that it uses its own datastore. Not only does this help with resiliency, but can also improve performance by reducing load on a single source, thus eliminating bottlenecks due to long-running queries._
    - Are the datastores&#39; access restricted only to their respective service or can multiple microservices access the datastores directly?

    - Are you minimizing the load on datastore?

### Failure Mode Analysis
            
* Have all fault-points and fault-modes been identified?

  _Fault-points describe the elements within an application architecture which are capable of failing, while fault-modes capture the various ways by which a fault-point may fail. To ensure an application is resilient to end-to-end failures, it is essential that all fault-points and fault-modes are understood and operationalized._
  
    Additional resources:
    - [Failure Mode Analysis for Azure applications](https://docs.microsoft.com/azure/architecture/resiliency/failure-mode-analysis)
* Have all single points of failure been eliminated?

  _A single point of failure describes a specific fault-point which if it where to fail would bring down the entire application. Single points of failure introduce significant risk since any failure of this component will cause an application outage._
  > Make sure that all single points of failure are identified and wherever possible eliminated. Single point of failures that cannot be avoided need special attention during operations and with regards to resiliency.
  
    Additional resources:
    - [Make all things redundant](https://docs.microsoft.com/azure/architecture/guide/design-principles/redundancy)
* Have all 'singletons' been eliminated?

  _A 'singleton' describes a logical component within an application for which there can only ever be a single instance. It can apply to stateful architectural components or application code constructs. Ultimately, singletons introduce a significant risk by creating single points of failure within the application design._
* Has pathwise analysis been conducted to identify key flows within the application?

  _Pathwise analysis can be used to decompose a complex application into key flows to which business impact can be attached. Frequently, these key flows can be used to identify business critical paths within the application to which reliability targets are most applicable._
### Targets &amp; Non-Functional Requirements
            
* Are recovery targets such as Recovery Time Objective (RTO) and Recovery Point Objective (RPO) defined for the application and/or key scenarios?

  _Understanding customer reliability expectations is vital to reviewing the overall reliability of the application. For instance, if a customer is striving to achieve an application RTO of less than a minute then back-up based and active-passive disaster recovery strategies are unlikely to be appropriate<br />**Recovery time objective (RTO)**: The maximum acceptable time the application is unavailable after a disaster incident<br />**Recovery point objective (RPO)**: The maximum duration of data loss that is acceptable during a disaster event_
  > Recovery targets should be defined in accordance to the required RTO and RPO targets for the workloads
  
    Additional resources:
    - [Protect and recover in cloud management](https://docs.microsoft.com/azure/cloud-adoption-framework/manage/considerations/protect)
* Are you able to predict general application usage?

  _It is important to understand application and environment usage. The customer may have an understanding of certain seasons or incidents that increase user load (e.g. a weather service being hit by users facing a storm, an e-commerce site during the holiday season)._
  > Traffic patterns should be identified by analyzing historical traffic data and the effect of significant external events on the application
    - If typical usage is predictable, are your predictions based on time of day, day of week, or season (e.g. holiday shopping season)?

      _Dig deeper and document predictable periods. By doing so, you can leverage resources like Azure Automation and Autoscale to proactively scale the application and its underlying environment._
    - Do you understand why your application responds to its typical load in the ways that it does?

      _Identifying a typical load helps you determine realistic expectations for performance testing. A "typical load" can be measured in individual users, web requests, user sessions, or transactions. When documenting typical loads, also ensure that all predictable periods have typical loads documented._
    - Are you able to reasonably predict when these peaks will occur?

    - Are you able to accurately predict the amount of load your application will experience during these peaks?

* Are there well-defined performance requirements for the application and/or key scenarios?

  _Non-functional performance requirements, such as those relating to end-user experiences (e.g. average and maximum response times) are vital to assessing the overall health of an application, and is a critical lens required for assessing operations._
  > Identify sensible non-functional requirements
  > 
  > *Work with stakeholders to identify sensible non-functional requirements based on business requirements, research and user testing.*
    - Are there any targets defined for the time it takes to perform scale operations?

      _Scale operations (horizontal - changing the number of identical instances, vertical - switching to more/less powerful instances) can be fast, but usually take time to complete. It's important to understand how this delay affects the application under load and if degraded performance is acceptable._
      > The application should be designed to scale to cope with spikes in load in-line with what is an acceptable duration for degraded performance
    - Is there a strategy in place to manage events that may cause a spike in load?

    - What is the maximum traffic volume the application is expected to serve without performance degradation?

      _Scale requirements the application must be able to effectively satisfy, such as the number of concurrent users or requests per second, is a critical lens for assessing operations. From the cost perspective, it's recommended to set a budget for extreme circumstances and indicate upper limit for cost (when it's not worth serving more traffic due to overall costs)._
      > Traffic limits for the application should be defined in quantified and measurable manner
    - Are these performance targets monitored and measured across the application and/or key scenarios?

      _Monitoring and measuring end-to-end application performance is vital to qualifying overall application health and progress towards defined targets._
      > Automation and specialized tooling (such as Application Insights) should be used to orchestrate and measure application performance
* Are availability targets such as Service Level Agreements (SLAs), Service Level Indicators (SLIs), and Service Level Objectives (SLOs) defined for the application and/or key scenarios?

  _Understanding customer availability expectations is vital to reviewing overall operations for the application. For instance, if a customer is striving to achieve an application SLO of 99.999%, the level of inherent operational activity required by the application is going to be far greater than if an SLO of 99.9% was the aspiration._
  > Have clearly defined availability targets
  > 
  > *Having clearly defined availability targets is crucial in order to have a goal to work and measure against. This will also determine which services an application can leverage vs. those which do not qualify in terms of the Service Level Agreement (SLA) they offer.*
    - Are SLAs/SLOs/SLIs for all leveraged dependencies understood?

      _If the application is depending on external services, their availability targets/commitments should be understood and ideally aligned with application targets._
      > Make sure SLAs/SLOs/SLIs for all leveraged dependencies are understood
    - Has a composite Service-Level Agreement (SLA) been calculated for the application and/or key scenarios using Azure SLAs?

      _A [composite SLA](https://docs.microsoft.com/azure/architecture/framework/resiliency/business-metrics#understand-service-level-agreements) captures the end-to-end SLA across all application components and dependencies. It is calculated using the individual SLAs of Azure services housing application components and provides an important indicator of designed availability in relation to customer expectations and targets._
      > Make sure the composite SLA of all components and dependencies on the critical paths are understood
  
      Additional resources:
        - [Composite Service Level Agreement (SLA)](https://docs.microsoft.com/azure/architecture/framework/resiliency/business-metrics#understand-service-level-agreements)
    - Are availability targets considered while the system is running in disaster recovery mode?

      _The above defined targets might or might not be applied when running in Disaster Recovery (DR) mode. This depends from application to application._
      > Consider availability targets for disaster recovery mode
      > 
      > *If targets must also apply in a failure state, then an N+1 model should be used to achieve greater availability and resiliency, where N is the capacity needed to deliver required availability. There's also a cost implication, because a more resilient infrastructure usually means more costs being involved. This has to be accepted by business.*
    - Are availability targets monitored and measured?

      _Monitoring and measuring application availability is vital to qualifying overall application health and progress towards defined targets._
      > Measure and monitor key availability targets
      > 
      > *Make sure you measure and monitor key targets such as **Mean Time Between Failures (MTBF)** which denotes the average time between failures of a particular component.*
  
      Additional resources:
        - [Mean Time Between Failures](https://en.wikipedia.org/wiki/Mean_time_between_failures)
    - What are the consequences if availability targets are not satisfied?

      _Are there any penalties, such as financial charges, associated with failing to meet Service Level Agreement (SLA) commitments? Additional measures can be used to prevent penalties, but that also brings additional cost to operate the infrastructure. This has to be factored in and evaluated._
      > Understand the consequences of missing availability targets
      > 
      > *It should be fully understood what are the consequences if availability targets are not satisfied. This will also inform when to initiate a failover case.*
### Key Scenarios
            
* Are there any application components which are less critical and have lower availability or performance requirements?

  _Some less critical components or paths through the application may have lower expectations around availability, recovery, and performance. This can result in cost reduction by choosing lower SKUs with less performance and availability._
  > Identify if there are components with more relaxed performance requirements
* Have critical system flows through the application been defined for all key business scenarios?

  _Understanding critical system flows is vital to assessing overall operational effectiveness, and should be used to inform a health model for the application. It can also tell if areas of the application are over or under-utilized and should be adjusted to better meet business needs and cost goals._
  > Path-wise analysis should be used to define critical system flows for key business scenarios, such as the checkout process for an eCommerce application
    - Do these critical system flows have distinct availability, performance, or recovery targets?

      _Critical sub-systems or paths through the application may have higher expectations around availability, recovery, and performance due to the criticality of associated business scenarios and functionality. This also helps to understand if cost will be affected due to these higher needs._
      > Targets should be specific and measurable
### Dependencies
            
* Are all platform-level dependencies identified and understood?

  _The usage of platform level dependencies such as Azure Active Directory must also be understood to ensure that their availability and recovery targets align with that of the application._
* Can the application operate in the absence of its dependencies?

  _If the application has strong dependencies which it cannot operate in the absence of, then the availability and recovery targets of these dependencies should align with that of the application itself. Effort should be taken to [minimize dependencies](https://docs.microsoft.com/azure/architecture/guide/design-principles/minimize-coordination) to achieve control over application reliability._
  
    Additional resources:
    - [Minimize dependencies](https://docs.microsoft.com/azure/architecture/guide/design-principles/minimize-coordination)
* Is the lifecycle of the application decoupled from its dependencies?

  _If the application lifecycle is closely coupled with that of its dependencies it can limit the operational agility of the application, particularly where new releases are concerned._
* Does the application team maintain a list frameworks and libraries used by this workload?

  _As part of the workload inventory the application team should maintain a framework and library list, along with versions in use. Understanding of the frameworks and libraries (custom, OSS, 3rd party, etc.) used by the application and the resulting vulnerabilities is important. There are automated solutions on the market that can help with this assessment: [OWASP Dependency-Check](https://owasp.org/www-project-dependency-check/), [NPM audit](https://docs.npmjs.com/cli/v6/commands/npm-audit) or [WhiteSource Bolt](https://www.whitesourcesoftware.com/free-developer-tools/bolt/)._
  > Maintain a list of frameworks and libraries as part of the application inventory
  
    Additional resources:
    - [Dependencies, frameworks, and libraries](https://docs.microsoft.com/azure/architecture/framework/security/design-app-dependencies#dependencies-frameworks-and-libraries)
  
    - [OWASP Dependency-Check](https://owasp.org/www-project-dependency-check/)
  
    - [NPM audit](https://docs.npmjs.com/cli/v6/commands/npm-audit)
  
    - [WhiteSource Bolt](https://www.whitesourcesoftware.com/free-developer-tools/bolt/)
* Are frameworks and library updates included into the workload lifecycle?

  _Application frameworks are frequently provided with updates (e.g. security), released by the vendor or communities. Critical and important security patches need to be prioritized._
  > Update frameworks and libraries as part of the application lifecycle
* Are Service Level Agreement (SLA) and support agreements in place for all critical dependencies?

  _Service Level Agreement (SLA) represents a commitment around performance and availability of the application. Understanding the Service Level Agreement (SLA) of individual components within the system is essential in order to define reliability targets. Knowing the SLA of dependencies will also provide a justification for additional spend when making the dependencies highly available and with proper support contracts._
  > The operational commitments of all external and internal dependencies should be understood to inform the broader application operations and health model
* Is the organization using a Landing Zone concept for this workload and how was it implemented?

  _Landing Zone refers to components that are already defined and in place before the workloads are getting deployed by the workload owners, e.g. network topology with Hub/Spoke concept. The purpose of the “Landing Zone” is to ensure that when a workload lands on Azure, the required “plumbing” is already in place, providing greater agility and compliance with enterprise security and governance requirements. This is crucial, that a Landing Zone will be handed over to the workload owner with the security guardrails deployed._
  > Implement a landing zone concept with Azure Blueprints and Azure Policies
    - Does the organization use Azure Blueprints to consistently deploy environments of this workload that comply with organizational policies?

      _Automation of deployment and maintenance tasks reduces security and compliance risk by limiting opportunity to introduce human errors during manual tasks._
      > Use Azure Blueprints to consistently deploy environments that comply with organizational policies
* Are all internal and external dependencies identified and categorized as either weak or strong?

  _Internal dependencies describe components within the application scope which are required for the application to fully operate, while external dependencies capture required components outside the scope of the application, such as another application or third-party service._
  > Categorize dependencies as either weak or strong
  > 
  > *Dependencies may be categorized as either strong or weak based on whether or not the application is able to continue operating in a degraded fashion in their absence.*
    - Do you maintain a complete list of application dependencies?

      _Examples of typical dependencies include platform dependencies outside the remit of the application, such as Azure Active Directory, Express Route, or a central NVA (Network Virtual Appliance), as well as application dependencies such as APIs which may be in-house or externally owned by a third-party. For cost it’s important to understand the price for these services and how they are being charged, this makes it easier to understanding an all-up cost. For more details see cost models._
      > Map application dependencies either as a simple list or a document (usually this is part of a design document or reference architecture)
    - Is the impact of an outage with each dependency well understood?

      _Strong dependencies play a critical role in application function and availability meaning their absence will have a significant impact, while the absence of weak dependencies may only impact specific features and not affect overall availability. This reflects the cost that is needed to maintain the HA relationship between the service and its dependencies. It would explain why certain measures needs to be maintained in order to hold a given Service Level Agreement (SLA)._
      > Classify dependencies either as strong or weak. This will help identify which components are essential to the application
  
    Additional resources:
    - [Twelve-Factor App: Dependencies](https://12factor.net/dependencies)
### Application Composition
            
* How do you ensure that cloud resources are appropriately provisioned?

  _Deliberate selection of resources and sizing is important to maintain efficiency and optimal cost._
  > Automate based on the application lifespan, use DevOps and deployment automation, configure auto-scale policies for the workload (both in and out), select the right resource offering size (VM, disk, database), choose appropriate services that match business requirements
* Do you monitor and regularly review new features and capabilities?

  _Azure is continuously evolving, with new features and services becoming available which may be beneficial for the application._
  > Keep up to date on newest developments and feature updates, at least for services most relevant to your application
    - Do you subscribe to Azure service announcements for new features and capabilities?

      _Service announcements provide insights into new features and services, as well as features or services which become deprecated._
      > Use announcement subscriptions to stay up to date
* Are components hosted on shared application or data platforms which are used by other applications?

  _Do application components leverage shared data platforms, such as a central data lake, or application hosting platforms, such as a centrally managed Azure Kubernetes Service (AKS) or App Service Environment (ASE) cluster? Shared platforms drive down cost, but the workload needs to maintain the expected performance._
  > Make sure you understand the design decisions and implications of using shared hosting platforms
* What technologies and frameworks are used by the application?

  _It is important to understand what technologies are used by the application and must be managed, such as .NET Core, Spring, or Node.js._
  > Identify technologies and frameworks used by the application
  > 
  > *All technologies and frameworks should be identified. Vulnerabilities of these dependencies must be understood (there are automated solutions on the market that can help: [OWASP Dependency-Check](https://owasp.org/www-project-dependency-check/) or [NPM audit](https://docs.npmjs.com/cli/audit).*
  
    Additional resources:
    - [OWASP Dependency-Check](https://owasp.org/www-project-dependency-check/)
  
    - [NPM audit](https://docs.npmjs.com/cli/audit)
* What Azure services are used by the application?

  _It is important to understand what Azure services, such as App Services and Event Hubs, are used by the application platform to host both application code and data. In a discussion around cost, this can drive decisions towards the right replacements (e.g. moving from Virtual Machines to containers to increase efficiency, or migrating to .NET Core to use cheaper SKUs etc.)._
  > All Azure services in use should be identified
    - What operational features/capabilities are used for leveraged services?

      _Operational capabilities, such as auto-scale and auto-heal for App Services, can reduce management overheads, support operational effectiveness and reduce cost._
      > Make sure you understand the operational features/capabilities available and how they can be used in the solution
### Threat Analysis
            
* Has the workload been threat modeled?

  _Threat modeling is an engineering technique which can be used to help identify threats, attacks, vulnerabilities and countermeasures that could affect an application. Threat modeling consists of: defining security requirements, identifying threats, mitigating threats, validating threat mitigation. Microsoft uses [STRIDE](https://docs.microsoft.com/azure/security/develop/threat-modeling-tool-threats) for threat modeling.  This might be the right time to talk through the STRIDE methodology and then the tools available to help them with Threat Modeling. There are tools like [Microsoft Threat Modeling Tool](https://docs.microsoft.com/azure/security/develop/threat-modeling-tool-getting-started) which can help._
  > Adopt threat modeling processes
    - Are identified threats ranked based on organizational impact?

      _Ranked threats improves the understanding of risks associated with security issues._
      > Rank identified threats based on organizational impact
    - Does the organization track threat modeling or vulnerability scan results with a management system?

      _Effectively tracking and prioritizing discovered application threats is a vital component of vulnerability management._
      > Centralize threat modeling results
    - Are identified threats mapped to mitigations?

      _Mitigations are controls to help protect, detect and respond to a certain type of threat._
      > Map threats to mitigations
    - Are identified threats communicated to stakeholders? E.g., business, IT, application users

      _After defining and analyzing the risks, identify risk owners which are the roles that are responsible for mitigating the risk. They need to be aware of the risks so that they can start the mitigation process by allocating resources (e.g. financial or people)._
      > Establish communication processes for identified threats
  
    Additional resources:
    - [STRIDE](https://docs.microsoft.com/azure/security/develop/threat-modeling-tool-threats)
  
    - [Microsoft Threat Modeling Tool](https://docs.microsoft.com/azure/security/develop/threat-modeling-tool-getting-started)
* Does the organization evaluate the security posture of this workload using standard benchmarks?

  _[Benchmarking](https://docs.microsoft.com/azure/architecture/framework/Security/governance#evaluate-security-using-benchmarks) enables security program improvement by learning from external organizations. It lets the organization know how its current security state compares to that of other organizations. As an example, the Center for Internet Security (CIS) has created security benchmarks for Azure that map to the CIS Control Framework. Another reference example is the MITRE ATT&CK™ framework that defines the various adversary tactics and techniques based on real-world observations._
  > Establish security benchmarking using Azure Security Benchmark to align with industry standards
  
    Additional resources:
    - [Azure Security Benchmark](https://docs.microsoft.com/azure/security/benchmarks/overview)
* Does the organization have a defined set of security requirements for this workload?

  _Azure resources should be blocked that do not meet the proper security requirements defined during service enablement._
  > Define security requirements for the workload
* Has the organization addressed threat protection for the workload?

  _Enterprise workloads are subjected to many threats that can jeopardize confidentiality, availability, or integrity and should be protected with advanced security solutions._
  > Implement threat protection for the workload
* Has the organization identified and classified business critical workloads which may adversely affect operations if they are compromised or become unavailable?

  _Enterprise organizations typically have a large application portfolio. Have key business applications been identified and classified? This should include applications that have a high business impact if affected. Examples would be business critical data, regulated data, or business critical availability. These applications also might include applications which have a high exposure to attack such as public facing websites key to organizational success._
  > Identify and classify business critical applications
* How are threats addressed once found?

  _The threat modeling tool will produce a report of all the threats identified. This report is typically uploaded into a tracking tool or work items that can be validated and addressed by the developers. Cyber security teams can also use the report to determine attack vectors during a penetration test.  As new features are added to the solution, the threat model should be updated and integrated into the code management process.  If a security issue is found, there should be a process to triage the issue into the next release cycle or a faster release, depending on the severity._
  > Develop and implement a process to track, triage, and address threats into the application development lifecycle
* Does the organization have established processes and timelines to deploy security fixes for this workload?

  _Fixing identified vulnerabilities in a timely manner helps staying secure and preventing additional attack vectors._
  > Implement established processes and timelines to deploy mitigations for identified threats
    - How long does it typically take to deploy a security fix into production?

      _It's important to understand how the customer is updating when a security vulnerability is discovered in their workload: the process and tools, approvals, who is made aware and if there's executive sponsorship to bypass lengthy processes when it comes to security._
### Security Criteria &amp; Data Classification
            
* Does the organization consider containing attacker access to Azure workloads when making investments in security solutions?

  _The actual security risk for an organization is heavily influenced by how much access an adversary can or does obtain to valuable systems and data. For example, when each user only has a focused scope of permissions assigned to them, the impact of compromising an account will be limited._
  > Implement security strategy to contain attacker access
* Does the organization build the appropriate level of resilience into the security infrastructure of this workload?

  _Building cybersecurity resilience into an organization requires balancing investments across the security lifecycle, diligently applying maintenance, vigilantly responding to anomalies and alerts to prevent security assurance decay, and designing to defense in depth and least privilege._
  > Implement holistic security resilience strategy
* Has the organization developed and maintained a security plan in support of the workload?

  _A security plan should be part of the main planning documentation for the cloud. It should include several core elements including organizational functions, security skilling, technical security architecture and capabilities roadmap._
  > Develop a security plan
* Does the organization prioritize security best practices by reviewing guidance based on industry recommendations and apply those settings proactively and completely to all systems as the cloud workload is implemented?

  _Security best practices are ideally applied proactively and completely to all systems as the cloud workload is implemented._
  > Review, prioritize, and proactively apply security best practices to cloud resources
* Does the organization consider balancing attacker vs. defender cost for this workload?

  _Cybersecurity attacks are planned and conducted by human attackers that must manage their return on investment into attacks (return could include profit or achieving an assigned objective)._
  > Implement defenses that detect and prevent commodity attacks
### Transactional
            
* Does your application have any long-running tasks or workflow scenarios?

  _You can offload a long-running task or a multi-step workflow process to a separate, dedicated workers instead of using the application's resources to handle it. To handle this scenario, you can add tasks (messages) to a queue and have a dedicated worker listening to the queue to pick up a message and process it._
    - Where possible, have tasks been configured to execute in parallel?

      _There are many ways to handle long-running tasks. The common way is to use parallel execution threads and leverage WaitAll or WaitAny process waits. However, using these methods introduce blocking on threads and can have large, detrimental performance hits on applications, especially distributed applications. Additionally, the blocks can prevent the execution of other tasks that may not have a dependency on the data at the current code position. Instead, it is better to follow asynchronous models and leverage message queuing for long-running tasks. In this pattern, tasks publish and subscribe to data on the queue and tasks can execute as soon as the data is made available._
    - Are long-running tasks and workflows leveraging durable functions?

* Can you measure the efficiency of the connections that are created to external services and datastores?

  _It is important to be able to determine the total time for a round-robin between your application and its data source. This enables you to establish a baseline in which to measure against future changes along with calculating the cumulative effect of a single request to a service. It may help to leverage connection pooling or a connection multiplexer in order to reduce the need to create and close connections each time you need to communicate with a service. This helps to reduce the CPU overhead on the server that maintains all of those connections. When communicating with a service using an HttpClient or similar type of object, always create this object once and reuse it for subsequent requests. Ways to instantiate an object once can use the Singleton pattern of Dependency Injection or storing the object in a static variable._
* Is the application code written using asynchronous patterns?

  _When calling a service, this is a request that will take time to complete (return). The time for the caller to receive a response could range from milliseconds to minutes and during that time the thread is held by the process until the response comes back (or an exception happens). This means that, while the thread was waiting for a response, it was blocked from processing any other requests. Using an asynchronous pattern, the thread is released and available to process other requests while the initial request is still being processed in the background._
* Does your application batch requests?

  _Creating a lot of individual requests has a tremendous amount of overhead for the producer and consumer of those requests. This will also increase bandwidth as certain elements of data are included in each request. If an API supports batching, you can batch all of the requests (the batch size varies by API and payload size) into a single request. The server will receive the one batched request and process all of the contained, individual requests. This better leverages the server's resources so that the requests can be processed much faster._
## Health Modelling &amp; Monitoring
    
### Application Level Monitoring
            
* Is Personally identifiable information (PII) detected and removed/obfuscated automatically for this workload?

  _Extra care should be taken around logging of sensitive application areas. PII (contact information, payment information etc.) should not be stored in any application logs and protective measures should be applied (such as obfuscation). Machine learning tools like [Cognitive Search PII detection](https://docs.microsoft.com/azure/search/cognitive-search-skill-pii-detection) can help with this._
  > Automatically remove/obfuscate personally identifiable information (PII)
  
    Additional resources:
    - [Cognitive Search PII detection](https://docs.microsoft.com/azure/search/cognitive-search-skill-pii-detection)
* Are application events correlated across all application components?

  _[Distributed tracing](https://docs.microsoft.com/azure/architecture/microservices/logging-monitoring#distributed-tracing) provides the ability to build and visualize end-to-end transaction flows for the application._
  > Events coming from different application components or different component tiers of the application should be correlated to build end-to-end transaction flows
  > 
  > *For instance, this is often achieved by using consistent correlation IDs transferred between components within a transaction.<br /><br />Event correlation between the layers of the application will provide the ability to connect tracing data of the complete application stack. Once this connection is made, you can see a complete picture of where time is spent at each layer. This will typically mean having a tool that can query the repositories of tracing data in correlation to a unique identifier that represents a given transaction that has flowed through the system.*
  
    Additional resources:
    - [Distributed tracing](https://docs.microsoft.com/azure/architecture/microservices/logging-monitoring#distributed-tracing)
* Does the organization actively monitor identity related risk events related to potentially compromised identities of this workload?

  _Most security incidents take place after an attacker initially gains access using a stolen identity. These identities can often start with low privileges, but attackers then use that identity to traverse laterally and gain access to more privileged identities. This repeats as needed until the attacker controls access to the ultimate target data or systems. Reported risk events for Azure AD can be viewed in Azure AD reporting, or Azure AD Identity Protection. Additionally, the Identity Protection risk events API can be used to programmatically access identity related security detections using Microsoft Graph._
  > Establish a detection and response strategy for identity risks
* Is an Application Performance Management (APM) tool used collect application level logs?

  _In order to successfully maintain the application it's important to 'turn the lights on' and have clear visibility of important metrics both in real-time and historically._
  > Use Application Performance Management tools
  > 
  > *An APM technology, such as [Application Insights](https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview), should be used to manage the performance and availability of the application, aggregating application level logs and events for subsequent interpretation. It should be considered what is the appropriate level of logging, because too much can incur significant costs.*
  
    Additional resources:
    - [What is Application Insights?](https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview)
* Do you have detailed instrumentation in the application code?

  _Instrumentation of your code allows precise detection of underperforming pieces when load or stress tests are applied. It is critical to have this data available to improve and identify performance opportunities in the application code. Application Performance Monitoring (APM) tools, such as Application Insights, should be used to manage the performance and availability of the application, along with aggregating application level logs and events for subsequent interpretation._
* Are application logs collected from different application environments?

  _Application logs support the end-to-end application lifecycle. Logging is essential in understanding how the application operates in various environments and what events occur and under which conditions._
  > Collect application logs across application environments
  > 
  > *Application logs and events should be collected across all major environments. Sufficient degree of separation and filtering should be in place to ensure non-critical environments do not convolute production log interpretation. Furthermore, corresponding log entries across the application should capture a correlation ID for their respective transactions.*
* Are log messages captured in a structured format?

  _Structured format, following well-known schema can help in parsing and analyzing logs._
  > Application events should be captured as a structured data type with machine-readable data points rather than unstructured string types
  > 
  > *Structured data can easily be indexed and searched, and reporting can be greatly simplified.*
* Does the organization have a central SecOps teams which monitors security related telemetry data for this workload?

  _Organization is monitoring the security posture across workloads and central SecOps team is monitoring security-related telemetry data and investigating security breaches._
  > Establish a SecOps team and monitor security related events
    - Does the organization have an established process for communication, investigation &amp; hunting activities that is aligned with the workload team?

      _Development team needs to be aware of those activities to align their security improvement  activities with the outcome of those activities._
      > Define a process for aligning communication, investigation and hunting activities with the application team
* How is security monitored in this workload?

  _Organization is monitoring the security posture across workloads and central SecOps team is monitoring security-related telemetry data and investigating security breaches. Communication, investigation and hunting activities need to be aligned with the application team._
* Are log levels used to capture different types of application events?

  _Different log levels, such as INFO, WARNING, ERROR, and DEBUG can be used across environments (such as DEBUG for development environment)._
  > Configure appropriate log levels for environments
  > 
  > *Different log levels, such as INFO, WARNING, ERROR, and DEBUG should be pre-configured and applied within relevant environments. The approach to change log levels should be simple configuration change to support operational scenarios where it is necessary to elevate the log level within an environment.*
* Is it possible to evaluate critical application performance targets and non-functional requirements (NFRs)?

  > Application level metrics should include end-to-end transaction times of key technical functions, such as database queries, response times for external API calls, failure rates of processing steps, etc.
    - Is the end-to-end performance of critical system flows monitored?

      _To fully assess the health of key scenarios in the context of targets and NFRs, application log events across critical system flows should be correlated._
      > Correlate application log events across critical system flows, such as user login
### Resource and Infrastructure Level Monitoring
            
* Does the security team have access to and monitor all subscriptions and tenants that are connected to the existing cloud environment, relative to this workload?

  _Ensure the security organization is aware of all enrollments and associated subscriptions connected to the existing environment and is able to monitor those resources as part of the overall enterprise security posture._
  > Ensure all Azure environments that connect to your production environment/network apply your organization’s policy and IT governance controls for security
* Is resource-level monitoring enforced throughout the application?

  _Resource- or infrastructure-level monitoring refers to the used platform services such as Azure VMs, Express Route or SQL Database. But also covers 3rd-party solutions like an NVA._
  > All application resources should be configured to route diagnostic logs and metrics to the chosen log aggregation technology. Azure Policy should also be used as a device to ensure the consistent use of diagnostic settings across the application, to enforce the desired configuration for each Azure service.
* Are logs and metrics available for critical internal dependencies?

  _To be able to build a robust application health model it is vital that visibility into the operational state of critical internal dependencies, such as a shared NVA or Express Route connection, be achieved._
  > Collect and store logs and key metrics of critical components
* Is there an overall monitoring strategy for scalability and performance?

* Which log aggregation technology is used to collect logs and metrics from Azure resources?

  _Log aggregation technologies, such as Azure Log Analytics or Splunk, should be used to collate logs and metrics across all application components for subsequent evaluation. Resources may include Azure IaaS and PaaS services as well as 3rd-party appliances such as firewalls or anti-malware solutions used in the application. For instance, if Azure Event Hub is used, the [Diagnostic Settings](https://docs.microsoft.com/azure/event-hubs/event-hubs-diagnostic-logs) should be configured to push logs and metrics to the data sink. Understanding usage helps with right-sizing of the workload, but additional cost for logging needs to be accepted and included in the cost model._
  > Use log aggregation technology, such as Azure Log Analytics or Splunk, to gather information across all application components
* Are scaling policies configured to use appropriate metrics?

* Are you collecting Azure Activity Logs within the log aggregation tool?

  _Azure Activity Logs provide audit information about when an Azure resource is modified, such as when a virtual machine is started or stopped. Such information is extremely useful for the interpretation and troubleshooting of operational and performance issues, as it provides transparency around configuration changes._
  > Azure Activity Logs should be collected and aggregated
* Are you tracking when resources scale in and out?

### Monitoring and Measurement
            
* Are error budgets used to track service reliability?

  _An error budget describes the maximum amount of time that the application can fail without consequence, and is typically calculated as 1-Service Level Agreement (SLA). For example, if the SLA specifies that the application will function 99.99% of the time before the business has to compensate customers, the error budget is 52 minutes and 35 seconds per year. Error budgets are a device to encourage development teams to minimize real incidents and maximize innovation by taking risks within acceptable limits, given teams are free to ‘spend’ budget appropriately._
* Is black-box monitoring used to measure platform services and the resulting customer experience?

  _Black-box monitoring tests externally visible application behavior without knowledge of the internals of the system. This is a common approach to measuring customer-centric SLIs/SLOs/SLAs._
  
    Additional resources:
    - [Azure Monitor Reference](https://docs.microsoft.com/azure/azure-monitor/app/monitor-web-app-availability)
* Is there an policy that dictates what will happen when the error budget has been exhausted?

  _If the application error budget has been met or exceeded and the application is operating at or below the defined Service Level Agreement (SLA), a policy may stipulate that all deployments are frozen until they reduce the number of errors to a level that allows deployments to proceed._
* Is the application instrumented to measure the customer experience?

  _Effective instrumentation is vital to detecting and resolving performance anomalies that can impact customer experience and application availability._
  
    Additional resources:
    - [Monitor performance](https://docs.microsoft.com/azure/azure-monitor/app/web-monitor-performance)
* Is white-box monitoring used to instrument the application with semantic logs and metrics?

  _Application level metrics and logs, such as current memory consumption or request latency, should be collected from the application to inform a health model and detect/predict issues._
  
    Additional resources:
    - [Instrumenting an application with Application Insights](https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview)
* Are there known gaps in application observability that led to missed incidents and/or false positives?

  _What you cannot see, you cannot measure. What you cannot measure, you cannot improve._
### Dependencies
            
* Are critical external dependencies monitored?

  _It's common for applications to depend on other services or libraries. Despite these are external, it is still possible to monitor their health and availability using probes._
  > Monitor critical external dependencies
  > 
  > *Critical external dependencies, such as an API service, should be monitored to ensure operational visibility of dependency health. For instance, a probe could be used to measure the availability and latency of an external API.*
* Is the application instrumented to track calls to dependent services?

  _[Dependency tracking](https://docs.microsoft.com/azure/azure-monitor/app/asp-net-dependencies) and measuring the duration/status of dependency calls is vital to measuring overall application health and should be used to inform a health model for the application._
  
    Additional resources:
    - [Dependency tracking](https://docs.microsoft.com/azure/azure-monitor/app/asp-net-dependencies)
### Data Interpretation &amp; Health Modelling
            
* Are long-term trends analyzed to predict performance issues before they occur?

  _Analytics can and should be performed across long-term operational data to help inform on the history of application performance and detect if there have been any regressions. For instance, if the average response times have been slowly increasing over time and getting closer to maximum target._
* Have retention times for logs and metrics been defined and with housekeeping mechanisms configured?

  > Clear retention times should be defined to allow for suitable historic analysis but also control storage costs. Suitable housekeeping tasks should also be used to archive data to cheaper storage or aggregate data for long-term trend analysis.
* Are application and resource level logs aggregated in a single data sink, or is it possible to cross-query events at both levels?

  _To build a robust application health model it is vital that application and resource level data be correlated and evaluated together to optimize the detection of issues and troubleshooting of detected issues._
  > Implement a unified solution to aggregate and query application and resource level logs, such as Azure Log Analytics
* Are long-term trends analyzed to predict operational issues before they occur?

  _Are Operations and/or analytics teams using the stored events for machine learning or similar to make predictions for the future?_
  > Analytics can and should be performed across long-term operational data to help inform operational strategies and also to predict what operational issues are likely to occur and when. For instance, if the average response times have been slowly increasing over time and getting closer to the maximum target.
* Are application level events automatically correlated with resource level metrics to quantify the current application state?

  _The overall health state can be impacted by both application-level issues as well as resource-level failures. [Telemetry correlation](https://docs.microsoft.com/azure/azure-monitor/app/correlation) should be used to ensure transactions can be mapped through the end-to-end application and critical system flows, as this is vital to root cause analysis for failures. Platform-level metrics and logs such as CPU percentage, network in/out, and disk operations/sec should be collected from the application to inform a health model and detect/predict issues. This can also help to distinguish between transient and non-transient faults._
  
    Additional resources:
    - [Telemetry correlation](https://docs.microsoft.com/azure/azure-monitor/app/correlation)
* Is the transaction flow data used to generate application/service maps?

  _Is there a correlation between events in different services and are those visualized?_
  > An [Application Map](https://docs.microsoft.com/azure/azure-monitor/app/app-map?tabs=net) can help spot performance bottlenecks or failure hotspots across components of a distributed application
  
    Additional resources:
    - [Application Map](https://docs.microsoft.com/azure/azure-monitor/app/app-map?tabs=net)
* Is a health model used to qualify what 'healthy' and 'unhealthy' states represent for the application?

  > Implement a health model
  > 
  > *A holistic application health model should be used to quantify what 'healthy' and 'unhealthy' states represent across all application components. It is highly recommended that a 'traffic light' model be used to indicate a green/healthy state when key non-functional requirements and targets are fully satisfied and resources are optimally utilized, e.g. 95% of requests are processed in <= 500ms with Azure Kubernetes Service (AKS) node utilization at x% etc. Once established, this health model should inform critical monitoring metrics across system components and operational sub-system composition. It is important to note that the health model should clearly distinguish between expected-transient but recoverable failures and a true disaster state.*
    - Are critical system flows used to inform the health model?

      > The health model should be able to surface the respective health of critical system flows or key subsystems to ensure appropriate operational prioritization is applied. For example, the health model should be able to represent the current state of the user login transaction flow.
    - Can the health model distinguish between transient and non-transient faults?

      _Is the health model treating all failures the same?_
      > The health model should clearly distinguish between expected transient but recoverable failures and a true disaster state
    - Can the health model determine if the application is performing at expected performance targets?

      _The health model should have the ability to evaluate application performance as a part of the application's overall health state_
### Dashboarding
            
* What technology is used to visualize the application health model and encompassed logs and metrics?

  _Visualization, often also called Dashboarding, refers to how data is presented to operations teams and other interested users._
  > Dashboarding tools, such as Azure Monitor or [Grafana](https://grafana.com/), should be used to visualize metrics and events collected at the application and resource levels, to illustrate the health model and the current operational state of the application.
  
    Additional resources:
    - [Azure Monitor overview](https://docs.microsoft.com/azure/azure-monitor/overview)
  
    - [Grafana](https://grafana.com/)
* Are dashboards tailored to a specific audience?

  _Is there just one big dashboard or do you build individualized solutions for different teams (e.g. networking teams might have a different interest focus than the security team)?_
  > Dashboards should be customized to represent the precise lens of interest of the end-user. For example, the areas of interest when evaluating the current state will differ greatly between developers, security and networking. Tailored dashboards make interpretation easier and accelerates time to detection and action.
* Is Role Based Access Control (RBAC) used to control access to operational and financial dashboards and underlying data?

  _Are the dashboards openly available in your organization or do you limit access based on roles etc.? For example: developers usually don't need to know the overall cost of Azure for the company, but it might be good for them to be able to watch a particular workload._
  > Access to operational and financial data should be tightly controlled to align with segregation of duties, while making sure that it doesn't hinder operational effectiveness; i.e. scenarios where developers have to raise an ITSM (IT service management) ticket to access logs should be avoided.
* Is there a dashboard showing cost related KPIs for this workload which gives a transparent view of the current situation?

  _Single pane of glass which can be shown during weekly ops meetings and instills accountability within everyone whilst also allowing you to understand where you are in terms of budget through every stage._
* Are you using Azure Cost Management (ACM) to track spending in this workload?

  _In order to track spending an ACM tool can help with understanding how much is spent, where and when. This helps to make better decisions about how and if cost can be reduced._
  > Use ACM or other cost management tools to understand if savings are possible
### Alerting
            
* Do all alerts require an immediate response from an on-call engineer?

  _Alerts only deliver value if they are actionable and effectively prioritized by on-call engineers through defined operational procedures._
* Are operational events prioritized based on business impact?

  _Are all alerts being treated the same or do you analyze the potential business impact when defining an alert?_
  > Tagging events with a specific severity or urgency helps operational teams prioritize in cases where multiple events require intervention at the same time. For example, alerts concerning critical system flows might require special attention.
* Are push notifications enabled to inform responsible parties of alerts in real time?

  _Do teams have to actively monitor the systems and dashboard or are alerts sent to them by email etc.? This can help identify not just operational incidents but also budget overruns._
  > Send reliable alert notifications
  > 
  > *It is important that alert owners get reliably notified of alerts, which could use many communication channels such as text messages, emails or push notifications to a mobile app.*
* Are Azure notifications sent to subscriptions owners received and if necessary, properly routed to relevant technical stakeholders?

  _Subscription notification emails can contain important service notifications or security alerts._
  > Make sure that subscription notification emails are routed to the relevant technical stakeholders
  
    Additional resources:
    - [Azure account contact information](https://docs.microsoft.com/azure/cost-management-billing/manage/change-azure-account-profile#service-and-marketing-emails)
* Are there alerts defined for cost thresholds and limits?

  _This is to ensure that if any budget is close to threshold, the cost owner gets notified to take appropriate actions on the change._
  > Set up alerts for cost limits and thresholds
* Have Azure Resource Health alerts been created to respond to Resource-level events?

  _Azure Resource Health provides information about the health of individual resources such as a specific virtual machine, and is highly useful when diagnosing unavailable resources._
  > Azure Resource Health Alerts should be configured for specific resource groups and resource types, and should be adjusted to maximize signal to noise ratios, i.e. only distribute a notification when a resource becomes unhealthy according to the application health model or due to an Azure platform-initiated event. It is therefore important to consider transient issues when setting an appropriate threshold for resource unavailability, such as configuring an alert for a virtual machine with a threshold of 1 minute for unavailability before an alert is triggered.
* Have Azure Service Health alerts been created to respond to Service-level events?

  _Azure Service Health provides a view into the health of Azure services and regions, as well as issuing service impacting communications about outages, planned maintenance activities, and other health advisories._
  > [Azure Service Health](https://docs.microsoft.com/azure/service-health/overview) Alerts should be configured to operationalize Service Health events. However, Service Health alerts should not be used to detect issues due to associated latencies; there is a 5 minute Service Level Objectives (SLOs) for automated issues, but many issues require manual interpretation to define an RCA (Root Cause Analysis). Instead, they should be used to provide extremely useful information to help interpret issues that have already been detected and surfaced via the health model, to inform how best to operationally respond.
  
    Additional resources:
    - [Azure Service Health](https://docs.microsoft.com/azure/service-health/overview)
* Is alerting integrated with an IT Service Management (ITSM) system?

  > ITSM systems, such as ServiceNow, can help to document issues, notify and assign responsible parties, and track issues. For example,  operational alerts from the application could for be integrated to automatically create new tickets to track resolution.
* Are specific owners and processes defined for each alert type?

  _Having well-defined owners and response playbooks per alert is vital to optimizing operational effectiveness. Alerts don't have to be only technical, for example the budget owner should be made aware of capacity issues so that budgets can be adjusted and discussed._
  > Define a process for alert reaction
  > 
  > *Instead of treating all alerts the same, there should be a well-defined process which determines what teams are responsible to react to which alert type.*
* What technology is used for alerting?

  _Alerts from tools such as Splunk or Azure Monitor proactively notify or respond to operational states that deviate from norm. Alerts can also enable cost-awareness by watching budgets and limits and helping workload teams to scale appropriately._
  > Use automated alerting solution
  > 
  > *You should not rely on people to actively look for issues. Instead, an alerting solution should be in place that can push notifications to relevant teams. For example, by email, SMS or into a mobile app.*
## Capacity &amp; Service Availability Planning
    
### Scalability &amp; Capacity Model
            
* Is the process to provision and deprovision capacity codified?

  _Codifying and automating the process helps to avoid human error, varying results and to speed up the overall process._
  > Fluctuation in application traffic is typically expected. To ensure optimal operation is maintained, such variations should be met by automated scalability. The significance of automated capacity responses underpinned by a robust capacity model was highlighted by the COVID-19 crisis where many applications experienced severe traffic variations. While Auto-scaling enables a PaaS or IaaS service to scale within a pre-configured (and often times limited) range of resources, is provisioning or de-provisioning capacity a more advanced and complex process of for example adding additional scale units like additional clusters, instances or deployments. The process should be codified, automated and the effects of adding/removing capacity should be well understood.
* Is auto-scaling enabled for supporting PaaS and IaaS services?

  _Are built-in capabilities for automatic scale being used vs. scaling being always a manual decision?_
  > Leveraging built-in Auto-scaling capabilities can help to maintain system reliability in times of increased demand while not needing to overprovision resources up-front, by letting a service automatically scale within a pre-configured range of resources. It greatly simplifies management and operational burdens. However, it must take into account the capacity model, else automated scaling of one component can impact downstream services if those are not also automatically scaled accordingly.
* Is there a capacity model for the application?

  _A capacity model should describe the relationships between the utilization of various components as a ratio, to capture when and how application components should scale-out._
  > A capacity model should describe the relationships between the utilization of various components as a ratio, to capture when and how application components should scale-out. For instance, scaling the number of Application Gateway v2 instances may put excess pressure on downstream components unless also scaled to a degree. When modelling capacity for critical system components it is therefore recommended that an N+1 model be applied to ensure complete tolerance to transient faults, where N describes the capacity required to satisfy performance and availability requirements. This also prevents cost-related surprises when scaling out and realizing that multiple services need to be scaled at the same time.
  
    Additional resources:
    - [Performance Efficiency - Capacity](https://docs.microsoft.com/azure/architecture/framework/scalability/capacity)
* Is capacity utilization monitored and used to forecast future growth?

  _Predicting future growth and capacity demands can prevent outages due to insufficient provisioned capacity over time._
  > Especially when demand is fluctuating, it is useful to monitor historical capacity utilization to derive predictions about future growth. Azure Monitor provides the ability to collect utilization metrics for Azure services so that they can be operationalized in the context of a defined capacity model. The Azure Portal can also be used to inspect current subscription usage and quota status.
  
    Additional resources:
    - [Supported metrics with Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/platform/metrics-supported)
* Are you confident that the correct SKUs and configurations have been applied to the services in order to support your anticipated loads?

  _Understand which SKUs you have selected and ensure that they are the correct size. Additionally, ensure you understand the configuration of those SKUs (e.g. auto-scale settings for Application Gateways and App Services)._
* Is the impact of changes in application health on capacity fully understood?

  _For example, if an outage in an external API is mitigated by writing messages into a retry queue, this queue will get sudden spikes in load which it will need to be able to handle._
  > Any change in the health state of application components can influence the capacity demands on other components. Those impacts need to be fully understood and measures such as auto-scaling need to be in place to handle those.
* Is the required capacity (initial and future growth) within Azure service scale limits and quotas?

  _Due to physical and logical resource constraints within the platform, Azure must apply [limits and quotas](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits) to service scalability, which may be either hard or soft._
  > The application should take a scale-unit approach to navigate within service limits, and where necessary consider multiple subscriptions which are often the boundary for such limits. It is highly recommended that a structured approach to scale be designed up-front rather than resorting to a 'spill and fill' model.
    - Is the required capacity (initial and future growth) available within targeted regions?

      _While the promise of the cloud is infinite scale, the reality is that there are finite resources available and as a result situations can occur where capacity can be constrained due to overall demand._
      > If the application requires a large amount of capacity or expects a significant increase in capacity then effort should be invested to ensure that desired capacity is attainable within selected region(s). For applications leveraging a recovery or active-passive based disaster recovery strategy, consideration should also be given to ensure suitable capacity exists in the secondary region(s) since a regional outage can lead to a significant increase in demand within a paired region due to other customer workloads also failing over. To help mitigate this, consideration should be given to pre-provisioning resources within the secondary region.
  
      Additional resources:
        - [Azure Capacity (internal)](https://aka.ms/AzureCapacity)
  
    Additional resources:
    - [Azure subscription and service limits, quotas, and constraints](https://docs.microsoft.com/azure/azure-resource-manager/management/azure-subscription-service-limits)
### Service Availability
            
* Are all APIs/SDKs validated against target runtime/languages for required functionality?

  _While there is a desire across Azure to achieve API/SDK uniformity for supported languages and runtimes, the reality is that capability deltas exist. For instance, not all CosmosDB APIs support the use of direct connect mode over TCP to bypass the platform HTTP gateway. It is therefore important to ensure that APIs/SDKs for selected languages and runtimes provide all of the required capabilities_
* Are any preview services/capabilities required in production?

  _If the application has taken a dependency on preview services or SKUs then it is important to ensure that the level of support and committed Service Level Agreement (SLA) are in alignment with expectations and that roadmap plans for preview services to go<br />Generally Available (GA) are understood<br />Private Preview : SLAs do not apply and formal support is not generally provided <br />Public Preview : SLAs do not apply and formal support may be provided on a best-effort basis_
* Are Azure Availability Zones available in the required regions?

  _Not all regions support [Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview#availability-zones) today, so when assessing the suitability of availability strategy in relation to targets it is important to confirm if targeted regions also provide zonal support. All net new Azure regions will conform to the 3 + 0 datacenter design, and where possible existing regions will expand to provide support for [Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-region)._
  
    Additional resources:
    - [Regions that support Availability Zones in Azure](https://docs.microsoft.com/azure/availability-zones/az-region)
* Are Azure services available in the required regions?

  _All Azure services and SKUs are not available within every Azure region, so it is important to understand if the selected regions for the application offer all of the required capabilities. Service availability also varies across sovereign clouds, such as China ("Mooncake") or USGov, USNat, and USSec clouds. In situations where capabilities are missing, steps should be taken to ascertain if a roadmap exists to deliver required services._
  
    Additional resources:
    - [Azure Products by Region](https://azure.microsoft.com/global-infrastructure/services/)
* Is the required capacity (initial and future growth) available within targeted regions?

  _While the promise of the cloud is infinite scale, the reality is that there are finite resources available and as a result situations can occur where capacity can be constrained due to overall demand. If the application requires a large amount of capacity or expects a significant increase in capacity then effort should be invested to ensure that desired capacity is attainable within selected region(s). For applications leveraging a recovery or active-passive based disaster recovery strategy, consideration should also be given to ensure suitable capacity exists in the secondary region(s) since a regional outage can lead to a significant increase in demand within a paired region due to other customer workloads also failing over. To help mitigate this, consideration should be given to pre-provisioning resources within the secondary region._
  
### Service SKU
            
* Have you deployed a Hub and Spoke Design or Virtual WAN?

  _Virtual Wide Area Network (WAN) has costs that are different in hub and spoke design. The cost of the peering network or other service routing has to be included. If Private Link is deployed, peering is not billed - only private link._
  > Consider whether to deploy Hub and Spoke or Virtual WAN for this workload
* Is Azure Advisor being used to optimize SKUs discovered in this workload?

  _Azure Advisor helps to optimize and improve efficiency of the workload by identifying idle and under-utilized resources. It analyzes your configurations and usage telemetry and consolidates it into personalized, actionable recommendations to help you optimize your resources._
  > Use Azure Advisor to identify SKUs for optimization
    - Are the Advisor recommendations being reviewed weekly or bi-weekly for optimization?

      _Your underutilised resources need to be reviewed often in order to be identified and dealt with accordingly, in addition to ensuring that your actionable recommendations are up-to-date and fully optimized. For example, Azure Advisor monitors your virtual machine (VM) usage for 7 days and then identifies low-utilization VMs._
      > Review Azure Advisor recommendation periodically
* Do you know your scale limits and what is most likely to be your bottleneck?

  _An application is made up of many different components, services, and frameworks within both infrastructure and application code. The design and choices in each area will incur unique limits and scale options. Knowing how your application behaves under different kinds of load allows you to be better prepared. It can also help you recognize which individual services to scale, if necessary, versus scaling your entire infrastructure. This can help increase performance efficiency without sacrificing costs._
* Is the required peak capacity aligned with the subscription quotas and limits?

  _Limitless scale requires dedicated design and one of the important design considerations is the limits and quotas of Azure subscriptions. Some services are almost limitless, others require more planning. Some services have 'soft' limits that can be increased by contacting support._
### Efficiency
            
* Are cost-effective regions considered as part of the deployment selection?

  _Is there a technical/legal reason for deploying in a particular region? If not, it might be worth looking at another region to decrease cost. Also depending on the workload and data processing model, choosing a cheaper region might make more financial sense._
  > Choose appropriate region for workload deployment to optimize cost
* Is the price model of this workload clear? Do the consumers understand why they are paying the price per month?

  _As part of driving a good behavior it's important that the consumer has understood why they are paying the price for a service and also that the cost is transparent and fair to the user of the service or else it can drive wrong behavior._
* Is the distribution of the cost done in accordance with the usage of the service?

  _In order to drive down cost it can be advised to incentivize the user of driving the use of a service that helps put less burden on the platform and via this drive down cost as it falls back on the user if a good behavior is followed in order to drive down the price._
* Is the workload using the right operating system for its servers?

  _Analyze the technology stack and identify which workloads are capable of running on Linux and which require Windows. Linux-based VMs and App Services are significantly cheaper, but require the app to run on supported stack (.NET Core, Node.js etc.)._
  > Make sure the optimal operating systems are used for this workload
* Are the right sizes and SKUs used for workload services?

  _The required performance and infrastructure utilization are key factors which define the 'size' of Azure resources to be used, but there can be hidden aspects that affect cost too. Watch for cost variations between different SKUs - for example App Service Plans S3 cost the same as P2v2, but have worse performance characteristics. Once the purchased SKUs have been identified, determine if they purchased resources have the capabilities of supporting anticipated load. For example, if you expect the load to require 30 instances of an App Service, yet you are currently leveraging a Standard App Service Plan SKU (maximum of 10 instances supported), then you will need to upgrade your App Service Plan in order to accommodate the anticipated load._
  > Make sure the optimal service SKUs are used for this workload
* Is it possible to benefit from higher density in this workload?

  _When running multiple applications (typically in multi-tenant or microservices scenarios) density can be increased by deploying them on shared infrastructure and utilizing it more. For example: Containerization and moving to Kubernetes (Azure Kubernetes Services) enables pod-based deployment which can utilize underlying nodes efficiently. Similar approach can be taken with App Service Plans. To prevent the 'noisy neighbour' situation, proper monitoring must be in place and performance analysis must be done (if possible)._
## Application Platform Availability
    
### Service SKU
            
* Are all application platform services running in a High Availability (HA) configuration/SKU?

  _Azure application platform services offer resiliency features to support application reliability, though they may only be applicable at a certain SKU. For instance, [Service Bus Premium SKU](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-premium-messaging) provides predictable latency and throughput to mitigate noisy neighbor scenarios, as well as the ability to automatically scale and replicate metadata to another Service Bus instance for failover purposes._
  
    Additional resources:
    - [Azure Service Bus Premium SKU](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-premium-messaging)
### Compute Availability
            
* Is the underlying application platform service Availability Zone aware?

  _Platform services that can leverage Availability Zones are deployed in either a zonal manner within a particular zone, or in a zone-redundant configuration across multiple zones._
  
    Additional resources:
    - [Building solutions for high availability using Availability Zones](https://docs.microsoft.com/azure/architecture/high-availability/building-solutions-for-high-availability)
* Is the application hosted across 2 or more application platform nodes?

  _To ensure application platform reliability, it is vital that the application be hosted across at least two nodes to ensure there are no single points of failure. Ideally An n+1 model should be applied for compute availability where n is the number of instances required to support application availability and performance requirements. It is important to note that the higher [SLAs provided for virtual machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_9/) and associated related platform services, require at least two replica nodes deployed to either an Availability Set or across two or more [Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview#availability-zones)._
    - Does the application platform use Availability Zones or Availability Sets?

      _An **Availability Set (AS)** is a logical construct to inform Azure that it should distribute contained virtual machine instances across multiple fault and update domains within an Azure region. **Availability Zones (AZ)** elevate the fault level for virtual machines to a physical datacenter by allowing replica instances to be deployed across multiple datacenters within an Azure region. While zones provide greater resiliency than sets, there are performance and cost considerations where applications are extremely 'chatty' across zones given the implied physical separation and inter-zone bandwidth charges. Ultimately, Azure Virtual Machines and Azure PaaS services, such as Service Fabric and Azure Kubernetes Service (AKS) which use virtual machines underneath, can leverage either AZs or an AS to provide application resiliency within a region._
  
      Additional resources:
        - [Business continuity with data resiliency](https://azurecomcdn.azureedge.net/cvt-27012b3bd03d67c9fa81a9e2f53f7d081c94f3a68c13cdeb7958edf43b7771e8/mediahandler/files/resourcefiles/azure-resiliency-infographic/Azure_resiliency_infographic.pdf)
  
    Additional resources:
    - [Service Level Agreement (SLA) for Virtual Machines](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_9/)
* How is the client traffic routed to the application in the case of region, zone or network outage?

  _In the event of a major outage, client traffic should be routable to application deployments which remain available across other regions or zones. This is ultimately where cross-premises connectivity and global load balancing should be used, depending on whether the application is internal and/or external facing. Services such as [Azure Front Door](https://docs.microsoft.com/azure/frontdoor/front-door-overview), [Azure Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview), or third-party CDNs can route traffic across regions based on application health solicited via health probes._
  
    Additional resources:
    - [Traffic Manager endpoint monitoring](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-monitoring)
## Data Platform Availability
    
### Service SKU
            
* Are all data and storage services running in a High Availability (HA) configuration/SKU?

  _Azure data platform services offer resiliency features to support application reliability, though they may only be applicable at a certain SKU. For instance, [Azure SQL Database Business Critical SKUs](https://docs.microsoft.com/azure/azure-sql/database/service-tier-business-critical), or [Azure Storage Zone Redundant Storage (ZRS)](https://docs.microsoft.com/azure/storage/common/storage-redundancy) with three synchronous replicas spread across Availability Zones._
  
    Additional resources:
    - [Business Critical tier - Azure SQL Database and Azure SQL Managed Instance](https://docs.microsoft.com/azure/azure-sql/database/service-tier-business-critical)
  
    - [Azure Storage redundancy](https://docs.microsoft.com/azure/storage/common/storage-redundancy)
### Consistency
            
* How does CAP theorem apply to the data platform and key application scenarios?

  _[CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem) proves that it is impossible for a distributed data store to simultaneously provide more than two guarantees across 1) Consistency (every read receives the most recent write or an error), 2) Availability (very request receives a non-error response, without the guarantee that it contains the most recent write), and 3) Partition tolerance (a system continues to operate despite an arbitrary number of transactions being dropped or delayed by the network between nodes). Determining which of these guarantees are most important in the context of application requirements is critical._
  
    Additional resources:
    - [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem)
* Are data types categorized by data consistency requirements?

  _Data consistency requirements, such as strong or eventual consistency, should be understood for all data types and used to inform data grouping and categorization, as well as what data replication/synchronization strategies can be considered to meet application reliability targets._
### Replication and Redundancy
            
* How is application traffic routed to data sources in the case of region, zone, or network outage?

  _Understanding the method used to route application traffic to data sources in the event of a major failure event is critical to identify whether failover processes will meet recovery objectives. Many Azure data platform services offer native reliability capabilities to handle major failures, such as Cosmos DB Automatic Failover or Azure SQL DB Active Geo-Replication. However, it is important to note that some capabilities such as Azure Storage RA-GRS and Azure SQL DB Active Geo-Replication require application-side failover to alternate endpoints in some failure scenarios, so application logic should be developed to handle these scenarios._
* Has a data restore process been defined and tested to ensure a consistent application state?

  _Regular testing of the data restore process promotes operational excellence and confidence in the ability to recover data in alignment with defined recovery objectives for the application._
* Is data replicated across paired regions and/or Availability Zones

  _Replicating data across zones or paired regions supports application availability objectives to limit the impact of failure scenarios._
  
    Additional resources:
    - [Azure Storage redundancy](https://docs.microsoft.com/azure/storage/common/storage-redundancy)
## Networking &amp; Connectivity
    
### Connectivity
            
* Are you using Microsoft backbone or MPLS network?

  _Are you closer to your users or on-prem? If users are closer to the cloud you should use MSFT (i.e. egress traffic). MPLS is when another service provider gives you the line._
* Is a global load balancer used to distribute traffic and/or failover across regions?

  _Azure Front Door, Azure Traffic Manager, or third-party CDN (Content Delivery Network) services can be used to direct inbound requests to external-facing application endpoints deployed across multiple regions. It is important to note that Traffic Manager is a DNS based load balancer, so failover must wait for DNS propagation to occur. A sufficiently low TTL (Time To Live) value should be used for DNS records, though not all ISPs (Internet Service Providers) may honor this. For application scenarios which only need HTTP(S) support and are requiring transparent failover, Azure Front Door should be used._
  
    Additional resources:
    - [Disaster Recovery using Azure Traffic Manager](https://docs.microsoft.com/azure/networking/disaster-recovery-dns-traffic-manager)
  
    - [Azure Frontdoor routing architecture](https://docs.microsoft.com/azure/frontdoor/front-door-routing-architecture)
* For cross-premises connectivity (ExpressRoute or VPN) are there redundant connections from different locations?

  _At least two redundant connections should be established across two or more Azure regions and peering locations to ensure there are no single points of failure. An active/active load-shared configuration provides path diversity and promotes availability of network connection paths._
  
    Additional resources:
    - [Cross-network connectivity](https://docs.microsoft.com/azure/expressroute/cross-network-connectivity)
* Has a failure path been simulated to ensure connectivity is available over alternative paths?

  _The failure of a connection path onto other connection paths should be tested to validate connectivity and operational effectiveness. Using [Site-to-Site VPN connectivity as a backup path for ExpressRoute](https://docs.microsoft.com/azure/expressroute/use-s2s-vpn-as-backup-for-expressroute-privatepeering) provides an additional layer of network resiliency for cross-premises connectivity._
  
    Additional resources:
    - [Using site-to-site VPN as a backup for ExpressRoute private peering](https://docs.microsoft.com/azure/expressroute/use-s2s-vpn-as-backup-for-expressroute-privatepeering)
* Have all single points of failure been eliminated from the data path (on-premises and Azure)?

  _Single-instance Network Virtual Appliances (NVAs), whether deployed in Azure or within an on-premises datacenter, introduce significant connectivity risk and should be deployed [highly available](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha)._
  
    Additional resources:
    - [Deploy highly available network virtual appliances](https://docs.microsoft.com/azure/architecture/reference-architectures/dmz/nva-ha)
* Do health probes assess critical application dependencies?

  _Custom health probes should be used to assess overall application health including downstream components and dependent services, such as APIs and datastores, so that traffic is not sent to backend instances that cannot successfully process requests due to dependency failures._
  
    Additional resources:
    - [Health Endpoint Monitoring Pattern](https://docs.microsoft.com/azure/architecture/patterns/health-endpoint-monitoring)
* Does the organization restrict access to the workload backend infrastructure (APIs, databases, etc.) by only a minimal set of public IP addresses - only those who really need it?

  _Web applications typically have one public entrypoint and don't expose subsequent APIs and database servers over the internet. When using gateway services like [Azure Front Door](https://docs.microsoft.com/azure/frontdoor/) it's possible to restrict access only to a set of Front Door IP addresses and lock down the infrastructure completely._
  > Expose only a minimal set of public IP addresses based on need
* Does the organization identify and isolate groups of resources from other parts of the organization to aid in detecting and containing adversary movement within the enterprise?

  _A unified [enterprise segmentation strategy](https://docs.microsoft.com/azure/architecture/framework/Security/governance#enterprise-segmentation-strategy) will guide all technical teams to consistently segment access using networking, applications, identity, and any other access controls._
  > Establish a unified enterprise segmentation strategy
    - Does the organization align the cloud network segmentation strategy with the enterprise segmentation model?

      _Aligning cloud network segmentation strategy with the enterprise segmentation model reduces confusion and resulting challenges with different technical teams (networking, identity, applications, etc.) each developing their own segmentation and delegation models that don’t align with each other._
      > Align cloud network segmentation strategy with the enterprise segmentation model
* Does the workload use network security groups (NSG) to isolate and protect traffic within the workload's VNet?

  _If NSGs are being used to isolate and protect the application, the rule set should be reviewed to confirm that required services are not unintentionally blocked._
  > Use NSG or Azure Firewall to protect and control traffic within VNETs
    - Does the organization have configured NSG flow logs to get insights about incoming and outgoing traffic of this workload?

      _NSG flow logs should be captured and analyzed to monitor performance and security. The NSG flow logs enables Traffic Analytics to gain insights into internal and external traffic flows of the application._
      > Configure and collect network traffic logs
* Does the organization use Azure Firewall or any 3rd party next generation Firewall for this workload to control outgoing traffic of Azure PaaS services (data exfiltration protection) where Private Link is not available?

  _NVA solutions and Azure Firewall (for supported protocols) can be leveraged as a reverse proxy to restrict access to only authorized PaaS services for services where Private Link is not yet supported._
  > Use Azure Firewall or a 3rd party next generation firewall to protect against data exfiltration
* Are the services of this workload, which should not be accessible from public IP addresses, protected with network restrictions / IP firewall rules?

  _Azure provides networking solutions to restrict access to individual application services. Multiple levels (such as IP filtering or firewall rules) should be explored to prevent application services from being accessed by unauthorized actors._
  > Protect non-public accessible services with network restrictions / IP firewall
* Does the workload use Service Endpoints or Private Link for accessing Azure PaaS services?

  _[Service Endpoints](https://docs.microsoft.com/azure/virtual-network/virtual-network-service-endpoints-overview) and [Private Link](https://docs.microsoft.com/azure/private-link/private-endpoint-overview) can be leveraged to restrict access to PaaS endpoints only from authorized virtual networks, effectively mitigating data intrusion risks and associated impact to application availability. Service Endpoints provide service level access to a PaaS service, while Private Link provides direct access to a specific PaaS resource to mitigate data exfiltration risks (e.g. malicious admin scenarios). Don’t forget that Private Link is a paid service and has meters for inbound and outbound data processed. Private Endpoints are charged as well._
  > Use service endpoints and private links where appropriate
### Zone-Aware Services
            
* Are health probes configured for Azure Load Balancer(s)/Azure Application Gateway(s)?

  _[Health probes](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview) allow Azure Load Balancers to assess the health of backend endpoints to prevent traffic from being sent to unhealthy instances._
  
    Additional resources:
    - [Load Balancer health probes](https://docs.microsoft.com/azure/load-balancer/load-balancer-custom-probe-overview)
* Is Azure Load Balancer Standard being used to load-balance traffic across Availability Zones?

  _Azure Load Balancer Standard is zone-aware to distribute traffic across [Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview#availability-zones) and [can also be configured in a zone-redundant configuration](https://docs.microsoft.com/azure/load-balancer/load-balancer-standard-availability-zones) to improve reliability and ensure availability during failure scenarios impacting a datacenter within a region._
  
    Additional resources:
    - [Standard Load Balancer and Availability Zones](https://docs.microsoft.com/azure/load-balancer/load-balancer-standard-availability-zones)
* If used, is Azure Application Gateway v2 deployed in a zone-redundant configuration?

  _Azure Application Gateway v2 can be deployed in a [zone-redundant configuration](https://docs.microsoft.com/azure/application-gateway/application-gateway-autoscaling-zone-redundant) to deploy gateway instances across zones for improved reliability and availability during failure scenarios impacting a datacenter within a region._
  
    Additional resources:
    - [Zone-redundant Application Gateway v2](https://docs.microsoft.com/azure/application-gateway/application-gateway-autoscaling-zone-redundant)
* Are zone-redundant ExpressRoute/VPN Gateways used?

  _[Zone-redundant virtual network gateways](https://docs.microsoft.com/azure/vpn-gateway/about-zone-redundant-vnet-gateways) distribute gateway instances across [Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview#availability-zones) to improve reliability and ensure availability during failure scenarios impacting a datacenter within a region._
  
    Additional resources:
    - [Zone-redundant Virtual Network Gateways](https://docs.microsoft.com/azure/vpn-gateway/about-zone-redundant-vnet-gateways)
  
    - [Availability Zones](https://docs.microsoft.com/azure/availability-zones/az-overview#availability-zones)
### Endpoints
            
* Are you using Azure Front Door, Azure App Gateway or Web Application Firewall?

  _There are cost implications to using Front Door with Web Application Firewall enabled, but it can save costs compared to using a 3rd party solution. Front Door has a good latency, because it uses unicast. If only 1 or 2 regions are required, Application Gateway can be used. There are cost implications of having a WAF – you should check pricing of hours and GB/s._
* Do workload virtual machines running on premises or in the cloud have direct internet connectivity for users that may perform interactive logins, or by applications running on virtual machines?

  _Attackers constantly scan public cloud IP ranges for open management ports and attempt “easy” attacks like common passwords and known unpatched vulnerabilities. Limiting internet access from within an application server can prevent data exfiltration or stop the attacker from downloading additional tools._
  > Prohibit direct internet access of virtual machines with policy, logging, and monitoring
  
    Additional resources:
    - [Remove Virtual Machine (VM) direct internet connectivity](https://docs.microsoft.com/azure/architecture/framework/Security/governance#remove-virtual-machine-vm-direct-internet-connectivity)
* Are you using any Content Delivery Networks (CDN)?

  _CDNs store static files in locations that are typically geographically closer to the user than the data center. This increases overall application performance as latency for delivery and downloading these artifacts is reduced. Also, from a security point of view, CDNs can be used to separate the hosting platform from end users. Azure CDN contains a rule engine to remove platform-specific information and headers. The use of Azure CDN or 3rd party CDN will have different cost implications depending on what is chosen for the workload._
  > Use CDN to optimize delivery performance to users and obfuscate hosting platform from users/clients
* Are you using SSL offloading?

  _SSL offloading places the SSL certificate at an appliance that sits in front of the web server, instead of on the web server itself. This is beneficial for two reasons. First, the verification of the SSL certificate is conducted by the appliance instead of the web server, which reduces the taxation on the server. Second, SSL offloading increases operational efficiency as it can often eliminate the need to manage certificates across microservices._
* Are you using authentication/token verification offloading?

  _Like SSL offloading, authentication/token verification offloading on an appliance can reduce taxation on the server. Additionally, authentication verification offloading can greatly reduce development complication as developers no longer need to worry with the complications of SAML or OAuth tokens and, instead, can focus specifically on the business logic._
* Does the organization have the capability and plans in place to mitigate DDoS attacks for this workload?

  _DDoS attacks can be very debilitating and completely block access to your services or even take down the services, depending on the type of DDoS attack._
  > Mitigate DDoS attacks
  > 
  > *Use Azure DDoS Protection Standard for critical workloads where outage would have business impact. Also consider CDN as another layer of protection.*
* Does the organization protect publishing methods for the workload (e.g FTP, Web Deploy)?

  _Application resources allowing multiple methods to publish app content (e.g FTP, Web Deploy) should have the unused endpoints disabled. For Azure Web Apps SCM is the recommended endpoint and it can be protected separately with network restrictions for sensitive scenarios._
  > Protect workload publishing methods and restrict those not in use
    - Does the organization have an CI/CD process for publishing code in this workload?

      _Developers shouldn't publish their code directly to app servers - automated and gated CI/CD process should manage this._
      > Implement an automated and gated CI/CD deployment process
* Are all public endpoints of this workload protected / secured?

  _External application endpoints should be protected against common attack vectors, such as Denial of Service (DoS) attacks like Slowloris, to prevent potential application downtime due to malicious intent. Azure-native technologies such as Azure Firewall, Application Gateway/Azure Front Door Web Application Firewall (WAF), and DDoS Protection Standard Plan can be used to achieve requisite protection._
  > Protect all public endpoints with appropriate controls
    - Are public endpoints of this workload protected with firewall or WAF (Web Application Firewall)?

      _[Azure Firewall](https://docs.microsoft.com/azure/firewall/features) is a managed, cloud-based network security service that protects Azure Virtual Network resources. [Web Application Firewall](https://docs.microsoft.com/azure/web-application-firewall/ag/ag-overview) (WAF) mitigates the risk of an attacker being able to exploit commonly known security application vulnerabilities like cross-site scripting or SQL injection._
      > Use web application firewall
  
    Additional resources:
    - [Azure DDoS Protection](https://docs.microsoft.com/azure/virtual-network/ddos-protection-overview)
  
    - [Azure Web Application Firewall](https://docs.microsoft.com/azure/web-application-firewall/ag/ag-overview)
### Data flow
            
* Are you moving data between regions?

  _Moving data between regions can add additional cost - both on the storage layer or networking layer. It's worth reviewing if this cost is can be replaced via re-architecture or justified due to e.g. disaster recovery (DR)._
  > Consider if the cost of data transfer is acceptable
* How are Azure resources connecting to the internet? Via NSG or via on-prem internet?

  _Tunnelling internet traffic through on-premises can add extra cost as data has to go back to local network before it reaches the internet, this cost should be acknowledged._
* How is the workload connected between regions? Is it using network peering or gateways?

  _VNET Peering has additional cost. Peering within the same region is cheaper than peering between regions or Global regions. Inbound and outbound traffic is charged at both ends of the peered networks._
  > Make sure the workload works with cross-region peering efficiently and be aware of additional costs
* Does the organization leverage a Cloud Application Security Broker (CASB) for this workload?

  _CASBs provide rich visibility, control over data travel, and sophisticated analytics to identify and combat cyberthreats across all Microsoft and third-party cloud services._
  > Leverage a Cloud Application Security Broker (CASB)
* Is the traffic between subnets, Azure components and tiers of the workload managed and secured?

  _Data filtering between subnets and other Azure resources should be protected. Network Security Groups, PrivateLink, and Private Endpoints can be used for traffic filtering._
  > Control network traffic between subnets (east/west) and application tiers (north/south)
* Are there controls in place for this workload to detect and protect from data exfiltration?

  _Data exfiltration occurs when an internal/external malicious actor performs an unauthorized data transfer. The solution should leverage a layered approach such as hub/spoke for network communications with deep packet inspection to detect/protect from data exfiltration attack. Azure Firewall, UDR (User-defined Routes), NSG (Network Security Groups), Key Protection, Data Encryption, PrivateLink, and Private Endpoints are layered defenses for a data exfiltration attack. Azure Sentinel and Azure Security Center can be used to detect data exfiltration attempts and alert incident responders._
  > Adopt a zero trust approach
  
    Additional resources:
    - [Adopt a zero trust approach](https://docs.microsoft.com/azure/security/fundamentals/network-best-practices#adopt-a-zero-trust-approach)
## Application Performance Management
    
### Data Size/Growth
            
* Are target data sizes and associated growth rates calculated per scenario or service?

  _Scale limits and recovery options should be assessed in the context of target data sizes and growth rates to ensure suitable capacity exists._
* Are there any mitigation plans defined in case data size exceeds limits?

  _Mitigation plans such as purging or archiving data can help the application to remain available in scenarios where data size exceeds expected limits._
  > Make sure that data size and growth is monitored, proper alerts are configured and develop (automated and codified, if possible) mitigation plans to help the application to remain available - or to recover if needed
* Are the plans for data growth and retention documented?

* Do you know the growth rate of your data?

  _Your solution might work great in the first week or month, but what happens when data just keeps increasing? Will the solution slow down, or will it even break at a particular threshold? Planning for data growth, data retention, and archiving is essential in capacity planning. Without adequately planning capacity for your datastores, performance will be negatively affected._
* Is the workload data designed for eventual consistency?

* Is the workload's data normalized appropriately?

### Data Latency and Throughput
            
* Are throughput targets defined, tested, and validated for key scenarios?

  _Throughput targets, which are commonly defined in terms of IOPS, MB/s and Block Size, should be defined and measured for key application scenarios, as well as each individual component, to validate overall application performance and health. Available throughput typically varies based on SKU, so defined targets should be used to inform the use of appropriate SKUs._
* Are you using database replicas and data partitioning?

  _Database replicas and data partitioning can improve application performance by providing multiple copies of the data and/or reducing the taxation of database operations. Both mechanisms involve conversations and planning between developers and database administrators._
* Are latency targets defined, tested, and validated for key scenarios?

  _Latency targets, which are commonly defined as first byte in to last byte out, should be defined and measured for key application scenarios, as well as each individual component, to validate overall application performance and health._
### Network Throughput and Latency
            
* Does the application require long running TCP connections?

  _If an application is initiating many outbound TCP or UDP connections it may exhaust all available ports leading to [SNAT port exhaustion](https://docs.microsoft.com/azure/load-balancer/troubleshoot-outbound-connection#snatexhaust) and poor application performance. Long-running connections exacerbate this risk by occupying ports for sustained durations. Effort should be taken to ensure that the application can scale within the port limits of the chosen application hosting platform._
  
    Additional resources:
    - [Managing SNAT port exhaustion](https://docs.microsoft.com/azure/load-balancer/troubleshoot-outbound-connection#snatexhaust)
* Have gateways (ExpressRoute or VPN) been sized accordingly to the expected cross-premises network throughput?

  _Azure Virtual Network Gateways throughput varies based on SKU._
  > Consider sizing gateways according to required throughput based on the available [VPN Gateway SKUs](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku)
  
    Additional resources:
    - [VPN Gateway SKUs](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-about-vpn-gateway-settings#gwsku)
* Does the application require dedicated bandwidth?

  _Applications with stringent throughput requirements may require dedicated bandwidth to remove the risks associated with noisy neighbor scenarios._
* If NVAs are used, has expected throughput been tested?

  _Maximum potential throughput for third-party NVA (Network Virtual Appliance) solutions is based on a combination of the leveraged VM SKU size, support for Accelerated Networking, support for HA (Highly Available) ports, and more generally the NVA technology used. Expected throughput should be tested to ensure optimal performance, however, it is best to confirm throughput requirements with the NVA vendor directly._
    - Is autoscaling enabled based on throughput

      _Autoscaling capabilities can vary between NVA solutions, but ultimately help to mitigate common bottle-neck situations._
* Are there any components/scenarios that are very sensitive to network latency?

  _Components or scenarios that are sensitive to network latency may indicate a need for co-locality within a single Availability Zone or even closer using [Proximity Placement Groups](https://docs.microsoft.com/azure/virtual-machines/windows/co-location#proximity-placement-groups) with Accelerated Networking enabled._
  
    Additional resources:
    - [Proximity Placement Groups](https://docs.microsoft.com/azure/virtual-machines/windows/co-location#proximity-placement-groups)
### Elasticity
            
* Has the time to scale in/out been measured?

  _Time to scale-in and scale-out can vary between Azure services and instance sizes and should be assessed to determine if a certain amount of pre-scaling is required to handle scale requirements and expected traffic patterns, such as seasonal load variations._
* Is autoscaling enabled and integrated within Azure Monitor?

  _Autoscaling can be leveraged to address unanticipated peak loads to help prevent application outages caused by overloading._
    - Has autoscaling been tested under sustained load?

      _The scaling on any single component may have an impact on downstream application components and dependencies. Autoscaling should therefore be tested regularly to help inform and validate a capacity model describing when and how application components should scale._
    - Is autoscaling configured with automatic schedule to add resources based on time of day trends?

* Can the workload scale horizontally in response to changing load?

  _A scale-unit approach should be taken to ensure that each application component and the application as a whole can scale effectively in response to changing demand. A robust capacity model should be used to define when and how the application should scale._
## Security &amp; Compliance
    
### Compliance
            
* Are Azure policies used to enforce security, compliance and organizational standards of this workload?

  _Azure Policy should be used to enforce and report a compliant configuration of Azure services. Azure policies can be used on multiple levels. It is recommended to apply organizational wide security controls on Azure platform level. These policies build the guardrails of a landing zone._
  > Define a set of Azure Policies which enforce organizational standards and are aligned with the governance team
* Does the organization periodically perform external and/or internal workload audits?

  _Compliance is important for several reasons. Aside from signifying levels of standards, like ISO 27001 and others, noncompliance with regulatory guidelines may bring sanctions and penalties._
  > Periodically perform external and/or internal workload security audits
    - How often do you have internal and external audits of this workload?

      _Determine the process the customer uses for auditing the solution. Is it done internally, external, or both. How are findings reflected back to the application? Is everyone aware of the audit and involved or is it done in a silo. This will help reduce the firefighting mentality when there is a finding and stress of performing updates._
      > Perform regular internal and external compliance audits
* How do you monitor and maintain your compliance of this workload?

  _Find out how they make sure they maintain compliance as the Azure Platform evolves and they update their application. Are there things preventing them from adopting new features in the platform because it will knock them out of compliance?_
    - Does the organization have a process for regulatory or governance compliance attestation for this workload?

      _Knowing whether your cloud resources are in compliance with standards mandated by governments or industry organizations is essential in today's globalized world (e.g. GDPR)._
      > Perform regulatory compliance attestation
    - Has the organization established a monitoring and assessment solution for compliance?

      _Continuously monitoring and assessing the workload increases the overall security and compliance of your workload in Azure. For example Azure Security Center provides a regulatory compliance dashboard._
      > Continuously assess and monitor compliance
### Separation of duties
            
* Has a designated point of contact been assigned for this workload to receive Azure incident notifications from Microsoft?

  _Security alerts need to reach the right people in your organization. It is important to ensure a security contact receives Azure incident notifications, or alerts from Microsoft / Azure Security Center, such as a notification that your resource is compromised and/or attacking another customer._
  > Establish a designated point of contact to receive Azure incident notifications from Microsoft
* Has the organization established a lifecycle management policy for critical accounts in this workload?

  _A compromise of an account in a role that is assigned privileges with a business-critical impact can be detrimental to organizational information systems and should therefore be closely monitored including a lifecycle process._
  > Establish lifecycle management policy for critical accounts
    - Does the organization regularly review access from accounts that have privileges to this workload?

      _It is important to monitor the usage of high privilege accounts and set up a recurring review pattern to ensure that accounts are removed from permissions as roles change._
      > Regularly review access for critical roles
    - Are all roles (critical and non-critical) assigned only to accounts which really need them and reviewed regularly?

      _All access should be assigned only when really needed. Even the Reader role, especially with wide scope (subscription, resource group level), can provide an attack vector, because if attacker compromises such user account or service principal, they get access to information such as source code of Azure Automation runbooks, Azure Logic Apps definitions, virtual network structure and other configuration properties of various services._
      > Assign all roles only as needed and review access periodically
* Does the application team have a clear view on responsibilities and individual/group access levels for this workload?

  _Application roles and responsibility model need to be defined covering the different access level of each operational function (e.g publish production release, access customer data, manipulate database records). It's in the interest of the application team to include central functions (e.g. SecOps, NetOps, IAM) into this view._
* Are there any processes and tools leveraged in this workload to manage privileged activities?

  _Zero-trust principle comes with the requirement of no standing access to an environment. Native and 3rd party solution can be used to elevate access permissions for at least highly privileged if not all activities. [Azure AD Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure) (Azure AD PIM) is the recommended and Azure native solution._
  > Establish processes and use tools to manage priviliged access
* Does the organization assign the appropriate level of privileges for managing the Azure environment for this workload based on a clearly documented strategy built with the principle of least privilege and based on operational needs?

  _Microsoft recommends starting from the Core Services Reference Permissions model and Segment Reference Permissions model to provide clear guidance for technical teams implementing these permissions._
  > Establish process and tools to manage privileged access with just-in-time capabilities
### Control-plane RBAC
            
* Does the organization conduct periodic & automated access reviews of the workload to make sure only authorized people have access?

  _As people in the organization and on the project change, it is crucial to make sure that only the right people have access to the application infrastructure. Auditing and reviewing access reduces the attack vector to the application. Azure control plane depends on Azure AD and access reviews are often centrally performed often as part of internal or external audit activities. For the application specific access it is recommended to do the same at least twice a year._
  > Conduct periodic access reviews for the workload
* Does the organization use a single identity provider for cross-platform identity management of this workload?

  _A single identity provider such as Azure Active Directory (AAD) for all enterprise assets and cloud services will simplify management and security, minimizing the risk of oversights or human mistakes. Ideally this provider should span across platforms (Windows, Linux, Azure, AWS, Google...)._
  > Use single identity provider for cross-platform IDM
* Does the organization leverage resource locks in this workload to protect critical infrastructure?

  _Critical infrastructure typically doesn't change often. To prevent accidental/undesired modification of resources, Azure offers the locking functionality where only specific roles and users with permissions are able to delete/modify resources. Locks can be used on critical parts of the infrastructure, but special care needs to be taken in the DevOps process - modification locks can sometimes block automation (see [Considerations before applying locks](https://review.docs.microsoft.com/azure/azure-resource-manager/management/lock-resources#considerations-before-applying-locks) for more information)._
  > Implement resource locks to protect critical infrastructure
* Is the identity provider and associated dependencies highly available?

  _It is important to confirm that the identity provider (e.g. Azure AD, AD, or ADFS) and its dependencies (e.g. DNS and network connectivity to the identity provider) are designed in a way and provide an Service Level Agreement (SLA)/Service Level Objectives (SLOs) that aligns with application availability targets._
* Does the organization have a well-defined identity strategy for controlling access to cloud-based workloads?

  _Identity provides the basis of a large percentage of security assurances and a well-defined identity strategy is effective in protecting the organization from cybersecurity threats._
  > Implement a well-defined identity strategy
* Does the organization assign permissions to Azure workloads based on individual resources or use custom permissions?

  _Custom resource-based permissions are often not needed and can result in increased complexity and confusion as they do not carry the intention to new similar resources. This then accumulates into a complex legacy configuration that is difficult to maintain or change without fear of "breaking something" – negatively impacting both security and solution agility. Higher level permissions sets - based on resource groups or management groups - are usually more efficient._
  > Assign permissions based on management or resource groups
* Does the organizational security team have read-only access into all cloud environment resources for this workload?

  _Provide [security teams](https://docs.microsoft.com/azure/architecture/framework/Security/governance#security-team-visibility) read-only access to the security aspects of all technical resources in their purview. Security organizations require visibility into the technical environment to perform their duties of assessing and reporting on organizational risk. Without this visibility, security will have to rely on information provided from groups, operating the environment, who have a potential conflict of interest (and other priorities).<br />Note that security teams may separately be granted additional privileges if they have operational responsibilities or a requirement to enforce compliance on Azure resources.<br />For example in Azure, assign security teams to the Security Readers permission that provides access to measure security risk (without providing access to the data itself).<br />Because security will have broad access to the environment (and visibility into potentially exploitable vulnerabilities), you should consider them critical impact accounts and apply the same protections as administrators._
  > Ensure security team has Security Reader or equivalent to support all cloud resources in their purview
* Has role-based and/or resource-based authorization been configured within Azure AD?

  _[Role-based and resource-based authorization](https://docs.microsoft.com/azure/architecture/multitenant-identity/authorize) are common approaches to authorize users based on required permission scopes._
  > Implement role-based access control for application infrastructure
    - Does the application write-back to Azure AD?

      _The Azure AD Service Level Agreement (SLA) includes authentication, read, write, and administrative actions.  In many cases, applications only require authentication and read access to Azure AD, which aligns with a much higher operational availability due to geographically distributed read replicas._
  
      Additional resources:
        - [Azure AD Architecture](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-architecture)
    - Are authentication tokens cached and encrypted for sharing across web servers?

      _Application code should first try to get tokens silently from a cache before attempting to acquire a token from the identity provider, to optimize performance and maximize availability._
  
      Additional resources:
        - [Acquire and cache tokens](https://docs.microsoft.com/azure/active-directory/develop/msal-acquire-cache-tokens)
  
    Additional resources:
    - [Role-based and resource-based authorization](https://docs.microsoft.com/azure/architecture/multitenant-identity/authorize)
* Does the organization use the root management group and carefully consider any changes that are applied using this group?

  _The [root management group](https://docs.microsoft.com/azure/architecture/framework/security/design-management-groups#use-root-management-group-with-caution) ensures consistency across the enterprise by applying policies, permissions, and tags across all subscriptions. This group can affect all resources in Azure and incorrect use can impact the security of all workloads in Azure._
  > Add planning, testing, and validation rigor to the use of the root management group
### Authentication and authorization
            
* How is the workload authenticated when communicating with Azure platform services?

  _Try to avoid authentication with keys (connection strings, API keys etc.) and always prefer Managed Identities (formerly also known as Managed Service Identity, MSI). Managed identities enable Azure Services to authenticate to each other without presenting explicit credentials via code. Typical use case is a Web App accessing Key Vault credentials or a Virtual Machine accessing SQL Database. [Managed identities](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/)_
  > Use managed identites for authentication to other Azure platform services
* Does the organization synchronize current on-premises Active Directory with Azure AD, or other cloud identity systems?

  _Consistency of identities across cloud and on-premises will reduce human errors and resulting security risk. Teams managing resources in both environments need a consistent authoritative source to achieve security assurances._
  > Synchronize on-premises directory with Azure AD
    - Does the organization synchronize on-premises admin accounts to Azure Active Directory, or to another cloud identity provider?

      _Synchronizing on-premises admin accounts to Azure Active Directory creates a pivot point that allows an on-premsise compromise to impact Azure workloads._
      > Avoid synchronizing on-premises admin accounts to AAD
    - Does the organization use cloud provider identity services designed to host non-employee rather than including vendors, partners, and customers into a corporate directory?

      _Using a cloud identity provider reduces risk by granting the appropriate level of access to external entities instead of the full default permissions given to full-time employees. This least privilege approach and clear differentiation of external accounts from company staff makes it easier to prevent and detect attacks coming in from these vectors._
      > Use cloud provider identity services for non-employees
* Are authentication tokens cached securely and encrypted when sharing across web servers in this workload?

  _OAuth tokens are usually cached after they've been acquired. Application code should first try to get tokens silently from a cache before attempting to acquire a token from the identity provider, to optimize performance and maximize availability. Tokens should be stored securely and handled as any other credentials. When there's a need to share tokens across application servers (instead of each server acquiring and caching their own) encryption should be used._
  > Configure web apps to reuse authentication tokens securely and handle them like other credentials
    - Is trusted state information protected when stored on untrusted client (such as cookie in a web browser)?

      _State data can contain not just session identifier, but also account and claims information, which can get exploited by the client. In a situation where the application needs to round-trip trusted state via an untrusted client (which can be session cookie in a web browser), it has to ensure that the information isn't tampered with. See [ASP.NET Core Data Protection](https://docs.microsoft.com/aspnet/core/security/data-protection/introduction?view=aspnetcore-5.0) for more details on how to use .NET APIs._
      > Implement Data Protection for trusted state information
  
    Additional resources:
    - [Acquire and cache tokens](https://docs.microsoft.com/azure/active-directory/develop/msal-acquire-cache-tokens)
* Does the organization prioritize authentication via identity services for this workload vs. cryptographic keys?

  _Consideration should always be given to authenticating with identity services rather than cryptographic keys when available. Managing keys securely with application code is difficult and regularly leads to mistakes like accidentally publishing sensitive access keys to code repositories like GitHub. Identity systems (such as Azure Active Directory) offer secure and usable experience for access control with built-in sophisticated mechanisms for key rotation, monitoring for anomalies, and more._
  > Use identity services instead of cryptographic keys when available
  
    Additional resources:
    - [Key and secret management considerations in Azure](https://docs.microsoft.com/azure/architecture/framework/security/design-storage-keys)
* Does the organization enforce conditional access for this workload?

  _Modern cloud-based applications are often accessible over the internet and location-based networking restrictions don't make much sense, but it needs to be mapped and understood what kind of restrictions are required. Multi-factor Authentication (MFA) is a necessity for remote access, IP-based filtering can be used to enable ad-hoc debugging, but VPNs are preferred._
  > Implement Conditional Access Policies
    - Does the organization enforce password less or multi-factor authentication for users of this workload?

      _Attack methods have evolved to the point where passwords alone cannot reliably protect an account.  Modern authentication solutions including password-less and multi-factor authentication increase security posture through strong authentication._
      > Enforce password-less or Multi-factor Authentication (MFA)
* How is user authentication handled in this workload?

  _If possible, applications should utilize Azure Active Directory or other managed identity providers (such as Microsoft Account, Azure B2C...) to avoid managing user credentials with custom implementation. Modern protocols like OAuth 2.0 use token-based authentication with limited timespan, identity providers offer additional functionality like multi-factor authentication, password reset etc._
  > Use managed identity providers to authenticate to this workload
  
    Additional resources:
    - [Use identity-based authentication](https://docs.microsoft.com/azure/architecture/framework/security/design-identity-authentication#use-identity-based-authentication)
* Do all APIs for this workload require authentication?

  _API URLs used by client applications are exposed to attackers (JavaScript code on a website can be viewed, mobile application can be decompiled and inspected) and should be protected. For internal APIs, requiring authentication can increase the difficulty of lateral movement if an attacker obtains network access. Typical mechanisms include API keys, authorization tokens, IP restrictions or Azure Managed identities._
  > Require API authentication for all workloads
    - Does this workload leverage modern (OAuth 2.0, OpenID) authentication protocols?

      _Modern authentication protocols support strong controls such as Multi-factor Authentication (MFA) and should be used instead of legacy._
      > Standardize on modern authentication protocols
### Security Center
            
* Is Azure Defender enabled for all subscriptions and reporting to centralized workspaces?

  _Azure Security Center is a unified infrastructure security management system that strengthens the security posture of your data centers, and provides advanced threat protection across your workloads. It has two offerings Azure Security Center free and Azure Defender._
  > Use Azure Defender with automatic provisioning for all subscriptions and configure reporting to centralized workspaces
  
    Additional resources:
    - [What is Azure Security Center?](https://docs.microsoft.com/azure/security-center/security-center-introduction)
  
    - [Configure auto provisioning for agents and extensions from Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-enable-data-collection)
  
    - [Security Center Data Collection](https://docs.microsoft.com/azure/security-center/security-center-enable-data-collection)
* Is Azure Security Center's [Secure Score](https://docs.microsoft.com/azure/security-center/secure-score-security-controls)) being formally reviewed and improved on a regular basis?

  > Formally review Azure Security Center's Secure Score on a regular basis and take actions out of it
  
    Additional resources:
    - [Security Center Secure Score](https://docs.microsoft.com/azure/security-center/secure-score-security-controls)
* Are contact details set in security center to the appropriate email distribution list?

  > Set correct contact details in Azure Security Center to appropriate email distribution lists and review them on a regular basis
  
    Additional resources:
    - [Security Center Contact Details](https://docs.microsoft.com/azure/security-center/security-center-provide-security-contact-details)
* Does the organization use tools to discover and remediate common risks within Azure tenants?

  _Identifying and remediating common security hygiene risks significantly reduces overall risk to the organization by increasing cost to attackers. [Azure Secure Score](https://docs.microsoft.com/azure/security-center/security-center-secure-score) in Azure Security Center monitors the security posture of machines, networks, storage and data services, and applications to discover potential security issues (internet connected VMs, or missing security updates, missing endpoint protection or encryption, deviations from baseline security configurations, missing Web Application Firewall (WAF), and more)._
  > Discover and remediate common risks to improve Secure Score in Azure Security Center
### Network Security
            
* Does the organization have cloud virtual networks that are designed for growth based on an intentional subnet security strategy?

  _Most organizations end up adding more resources to networks than initially planned. When this happens, IP addressing and subnetting schemes need to be refactored to accommodate the extra resources. This is a labor-intensive process. There is limited security value in creating a very large number of small subnets and then trying to map network access controls (such as security groups) to each of them._
  > Design virtual networks for growth
* If data exfiltration concerns exist for services where Private Link is not yet supported, is filtering via Azure Firewall or an NVA being used?

  _NVA (Network Virtual Appliance) solutions and [Azure Firewall](https://docs.microsoft.com/azure/firewall/features) (for supported protocols) can be leveraged as a reverse proxy to restrict access to only authorized PaaS services for services where Private Link is not yet supported._
  
    Additional resources:
    - [Azure Firewall](https://docs.microsoft.com/azure/firewall/features)
* Is communication to Azure PaaS services secured using VNet Service Endpoints or Private Link?

  _Service Endpoints and Private Link can be leveraged to restrict access to PaaS endpoints from only authorized virtual networks, effectively mitigating data intrusion risks and associated impact to application availability. Service Endpoints provide service level access to a PaaS service, while Private Link provides direct access to a specific PaaS resource to mitigate data exfiltration risks (e.g. malicious admin scenarios)._
* Does the organization have a designated group responsible for centralized network management and security of this workload?

  _Centralizing network management and security can reduce the potential for inconsistent strategies that create potential attacker exploitable security risks. Because all divisions of the IT and development organizations do not have the same level of network management and security knowledge and sophistication, organizations benefit from leveraging a centralized network team’s expertise and tooling._
  > Establish a designated group responsible for central network management
* Does the organization have controls in place to ensure that security extends past the network boundaries of the workload in order to effectively prevent, detect, and respond to threats?

  _Traditional network controls based on a “trusted intranet” approach will not be able to effectively provide security assurances for cloud applications._
  > Evolve security beyond network controls
* Are Network Security Groups (NSGs) being used?

  _If NSGs are being used to isolate and protect the application, the rule set should be reviewed to confirm that required services are not unintentionally blocked._
    - Are NSG flow logs being collected?

      _Network Security Group (NSG) flow logs is a feature of Azure Network Watcher that allows you to log information about IP traffic flowing through an NSG. Flow data is sent to Azure Storage accounts from where you can access it as well as export it to any visualization tool, SIEM, or IDS of your choice._
      > Capture and analyze NSG flow logs to monitor performance and security
  
      Additional resources:
        - [Network security groups](https://docs.microsoft.com/en-gb/azure/virtual-network/network-security-groups-overview)
  
        - [Why use NSG flow logs](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview#why-use-flow-logs)
  
    Additional resources:
    - [Azure Platform Considerations for NSGs](https://docs.microsoft.com/azure/virtual-network/security-overview#azure-platform-considerations)
* Has the organization enabled enhanced network visibility by integrating network logs into a Security Information and Event Management (SIEM) solution or similar technology?

  _Integrating logs from the network devices, and even raw network traffic itself, will provide greater visibility into potential security threats flowing over the wire._
  > Integrate network logs into a Security Information and Event Management (SIEM)
* Does the organization have a security containment strategy that blends existing on-premises security controls and practices with native security controls available in Azure, and uses a zero-trust approach?

  _Assume breach is the recommended cybersecurity mindset and the ability to contain an attacker is vital to protect information systems._
  > Build a security containment strategy
* What kind of Data Loss Prevention (DLP) is used for this workload?

  _Network-based Data Loss Prevention (DLP) is decreasingly effective at identifying both inadvertent and deliberate data loss. The reason for this is that most modern protocols and attackers use network-level encryption for inbound and outbound communications. While the organization can use “SSL-bridging” to provide an “authorized man-in-the-middle” that terminates and then reestablishes encrypted network connections, this can also introduce privacy, security and reliability challenges._
  > Deprecate legacy network security controls
### Encryption
            
* Is there any portion of the workload that does not secure data in transit?

  _When data is being transferred between components, locations, or programs, it’s in transit. Data in transit should be encrypted using a common encryption standard at all points to ensure data integrity. For example: web applications and APIs should use HTTPS/SSL for all communication with clients and also between each other (in micro-services architecture). Determine if all components in the solution are using a consistent standard. There are times when encryption is not possible due to technical limitations, but the reason needs to be clear and valid._
  > Data in transit should be encrypted at all points to ensure data integrity
* How is data at rest protected in this workload?

  _This includes all information storage objects, containers, and types that exist statically on physical media, whether magnetic or optical disk.  All data should be classified and encrypted with an encryption standard. It should also be tagged so that it can be audited._
  > Classify your data at rest and use encryption
* Does the workload use industry standard encryption algorithms instead of creating own?

  _Organizations should rarely develop and maintain their own encryption algorithms. Secure standards already exist on the market and should be preferred. AES should be used as symmetric block cipher, AES-128, AES-192 and AES-256 are acceptable. Crypto APIs built into operating systems should be used where possible, instead of non-platform crypto libraries. For .NET make sure you follow the [.NET Cryptography Model](https://docs.microsoft.com/dotnet/standard/security/cryptography-model)._
  > Use standard and recommended encryption algorithms
* Does the organization use identity-based storage access controls for this workload?

  _Protecting data at rest is required to maintain confidentiality, integrity, and availability assurances across all workloads. Cloud service providers make multiple methods of access control available - shared keys, shared signatures, anonymous access, identity provider-based. Identity provider methods (such as AAD and RBAC) are the least liable to compromise and enable more fine-grained role-based access controls._
  > Implement identity-based storage access controls
* Does the organization encrypt virtual disk files for virtual machines which are associated with this workload?

  _Encrypting the virtual disk files helps prevent attackers from gaining access to the contents of the disk files in the event an attacker is able to download the files and mount the disk files offline on a separate system._
  > Use tools like Azure Disk Encryption, BitLocker or DM-Crypt to encrypt virtual disks
* Does the workload use secure modern hash algorithms?

  _Applications should use the **SHA-2** family of hash algorithms (SHA-256, SHA-384, SHA-512)._
  > Use only secure hash algorithms (SHA-2 family)
* What TLS version is used in this workload?

  _All Microsoft Azure services fully support TLS 1.2. It is recommended to migrate solutions to support **TLS 1.2** and use this version by default. TLS 1.3 is not available on Azure yet, but should be the preferred option once implemented on the platform._
  > Use TLS 1.2 or TLS 1.3 where possible
* Does the workload communicate over encrypted (TLS / HTTPS) network channels only?

  _Any network communication between client and server where man-in-the-middle attack can occur, needs to be encrypted. All website communication should use HTTPS, no matter the perceived sensitivity of transferred data (man-in-the-middle attacks can occur anywhere on the site, not just on login forms)._
  > Use encrypted network channels (TLS / HTTPS) for all client/server communication
* Are customer managed keys (CMK) for this workload stored in Azure Key Vault and protected with identity-based access control?

  _In many industries, regulations and compliance obligations require the use of workloads (typically databases) that not only encrypt data at rest, but do so by using encryption keys that end-users can control. The use of CMK exposes the workload to additional management responsibilities around key rotation and renewal, which in-turn can expose the workload to realiability risks, if not handled properly. Keys must be stored in a secure location with identity-based access control and audit policies. Data encryption keys are often encrypted with a key encryption key in Azure Key Vault to further limit access._
  > Store customer managed keys in Azure Key Vault.
  > 
  > *For general use, it is recommended to adopt platform managed keys, unless there are specific business reasons (like regulatory requirements) to use customer managed keys. Those keys should be always stored in Azure Key Vault.*
    - Are customer managed keys (CMK) in this workload protected with an additional key encryption key (KEK)?

      _More than one encryption key should be used in an encryption at rest implementation. Storing an encryption key in Azure Key Vault ensures secure key access and central management of keys._
      > Use an additional key encryption key (KEK) to protect your data encryption key (DEK)
## Operational Procedures
    
### Recovery &amp; Failover
            
* Are critical manual processes defined and documented for manual failure responses?

  _While full automation is attainable, there might be cases where manual steps cannot be avoided._
  > Operational runbooks should be defined to codify the procedures and relevant information needed for operations staff to respond to failures and maintain operational health
    - Are these manual operational runbooks tested and validated on a regular basis?

      > Manual operational runbooks should be tested frequently as part of the normal application lifecycle to ensure appropriateness and efficiency
* Are automated recovery procedures in place for common failure event?

  _Is there at least some automation for certain failure scenarios or are all those depending on manual intervention?_
  > Automated responses to specific events help to reduce response times and limit errors associated with manual processes. Thus, wherever possible, it is recommended to have automation in place instead of relying on manual intervention.
    - Are these automated recovery procedures tested and validated on a regular basis?

      > Automated operational responses should be tested frequently as part of the normal application lifecycle to ensure operational effectiveness
* Are recovery steps defined for failover and failback?

  _Is there a clearly defined playbook or disaster recovery plan for failover and failback procedures?_
  > The steps required to recover or fail over the application to a secondary Azure region in failure situations should be codified, preferably in an automated manner, to ensure capabilities exist to effectively respond to an outage in a way that limits impact. Similar codified steps should also exist to capture the process required to failback the application to the primary region once a failover triggering issue has been addressed.
    - Has the failover and failback approach been tested/validated at least once?

      _Only plans and playbooks that have been executed successfully at least once can be considered working._
      > The precise steps required to failover and failback the application must be tested to validate the effectiveness of the defined disaster recovery approach. Testing of the disaster recovery strategy should occur according to a reasonably regular cadence, such as annually, to ensure that operational application changes do not impact the applicability of the selected approach.
    - How is a failover decided and initiated?

      _Regional failovers are significant operational activities and may incur some downtime, degraded functionality, or data loss depending on the recovery strategy used. The failover process should be fully automated and tested, or at least the process should be clearly documented._
      > Document and understand the failover process
      > 
      > *The failover process itself and also the decision process as to what constitutes a failover should be clearly understood.*
    - Is the health model being used to classify failover situations?

      _It is important to know if a formal procedure is used to classify failover situations._
      > A platform service outage in a specific region will likely require a failover to another region, whereas the accidental change of a firewall rule can be mitigated by a recovery process. The health model and all underlying data should be used to interpret which operational procedures should be triggered.
    - Does the playbook or disaster recovery plan consider every process, component and every category of data that can&#39;t afford unlimited loss or downtime?

      _Different components of an application might have different priorities and impact and therefore different priorities in case of a disaster._
      > When a disaster that affects multiple application components occurs, it's critical that the recovery plan can be used to take a complete inventory of what needs attention and how to prioritize each item. Each major process or workload that's implemented by an app should have separate RPO and RTO values. Each one should be generated through a separate analysis that examines disaster scenario risks and potential recovery strategies for each respective process.
    - Can individual processes and components of the application failover independently?

      _For example, is it possible to failover the compute cluster to a secondary region while keeping the database running in the primary region?_
      > Ideally failover can happen on a component-level instead of needing to failover the entire system together, when, for instance, only one service experiences an outage
### Configuration &amp; Secrets Management
            
* Is the application stateless or stateful? If it is stateful, is the state externalized in a data store?

  _[Stateless services](https://docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices) and processes can easily be hosted across multiple compute instances to meet scale demands, as well as helping to reduce complexity and ensure high cacheability._
  > Use externalized data store for stateful applications
  > 
  > *Strive to design stateless services for scalability. If state must be maintained server side, consider an out-of-process caching service where all application instances can access.*
  
    Additional resources:
    - [Stateless web services](https://docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices)
* Is the session state (if any) non-sticky and externalized to a data store?

  _Sticky session state limits application scalability because it is not possible to balance load. With sticky sessions all requests from a client must be sent to the same compute instance where the session state was initially created, regardless of the load on that compute instance. Externalizing session state allows for traffic to be evenly distributed across multiple compute nodes, with required state retrieved from the external data store._
  
    Additional resources:
    - [Avoid session state](https://docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#sessionstate)
* Are the expiry dates of SSL/TLS certificates monitored and are processes in place to renew them?

  _Expired SSL/TLS certificates are one of the most common yet avoidable causes of application outages; even Azure and more recently Microsoft Teams have experienced outages due to expired certificates._
  > Implement lifecycle management process for SSL/TLS certificates
  > 
  > *Tracking expiry dates of SSL/TLS certificates and renewing them in due time is therefore highly critical. Ideally the process should be automated, although this often depends on leveraged CA. If not automated, sufficient alerting should be applied to ensure expiry dates do not go unnoticed.*
  
    Additional resources:
    - [Configure certificate auto-rotation in Key Vault](https://docs.microsoft.com/azure/key-vault/certificates/tutorial-rotate-certificates)
* Is Soft-Delete enabled for Key Vaults and Key Vault objects?

  _The [Soft-Delete feature](https://docs.microsoft.com/azure/key-vault/general/overview-soft-delete) retains resources for a given retention period after a DELETE operation has been performed, while giving the appearance that the object is deleted. It helps to mitigate scenarios where resources are unintentionally, maliciously or incorrectly deleted._
  > Enable Key Vault Soft-Delete
  
    Additional resources:
    - [Azure Key Vault Soft-Delete](https://docs.microsoft.com/azure/key-vault/general/overview-soft-delete)
* Are keys and secrets backed-up to geo-redundant storage?

  _Keys and secrets must still be available in a failover case._
  > Keys and secrets should be backed up to geo-redundant storage so that they can be accessed in the event of a regional failure and support recovery objectives. In the event of a regional outage, the Key Vault service will automatically be failed over to the secondary region in a read-only state.
    - Are certificate/key backups and data backups stored in different geo-redundant storage accounts?

      > Encryption keys and data should be backed up separately to optimize the security of underlying data
  
    Additional resources:
    - [Azure Key Vault availability and reliability](https://docs.microsoft.com/azure/key-vault/general/disaster-recovery-guidance)
* Does the application use Managed Identities?

  _[Managed Identities](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview) in Azure can be used to securely access Azure services while removing the need to store the secrets or certificates of Service Principals._
  > Use Managed Identities for authentication to other Azure platform services
  > 
  > *Wherever possible Azure Managed Identities (either system-managed or user-managed) should be used since they remove the management burden of storing and rotating keys for service principles. Thus, they provide higher security as well as easier maintenance.*
  
    Additional resources:
    - [Managed Identities](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview)
* Do you have procedures in place for secret rotation?

  _In the situation where a key or secret becomes compromised, it is important to be able to quickly act and generate new versions. Key rotation reduces the attack vectors and should be automated and executed without any human interactions._
  > Establish a process for key management and automatic key rotation
  > 
  > *Secrets (keys, certificates etc.) should be replaced once they have reached the end of their active lifetime or once they have been compromised. Renewed certificates should also use a new key. A process needs to be in place for situations where keys get compromised (leaked) and need to be regenerated on-demand. Tools, such as Azure Key Vault should ideally be used to store and manage application secrets to help with [rotation processes](https://docs.microsoft.com/azure/key-vault/secrets/tutorial-rotation-dual).*
  
    Additional resources:
    - [Secret rotation process tutorial](https://docs.microsoft.com/azure/key-vault/secrets/tutorial-rotation-dual)
* How are passwords and other secrets managed?

  _API keys, database connection strings and passwords are all sensitive to leakage, occasionally require rotation and are prone to expiration. Storing them in a secure store and not within the application code or configuration simplifies operational tasks like key rotation as well as improving overall security._
  > Store keys and secrets outside of application code in Azure Key Vault
  > 
  > *Tools like Azure Key Vault or [HashiCorp Vault](https://www.vaultproject.io/) should be used to store and manage secrets securely rather than being baked into the application artefact during deployment, as this simplifies operational tasks like key rotation as well as improving overall security. Keys and secrets stored in source code should be identified with static code scanning tools. Ensure that these scans are an integrated part of the continuous integration (CI) process.*
  
    Additional resources:
    - [HashiCorp Vault](https://www.vaultproject.io/)
* Can configuration settings be changed or modified without rebuilding or redeploying the application?

  > Application code and configuration should not share the same lifecycle to enable operational activities that change and update specific configurations without developer involvement or redeployment
* Is there a defined access model for keys and secrets for this workload?

  _Permissions to keys and secrets have to be controlled with an [access model](https://docs.microsoft.com/azure/key-vault/general/secure-your-key-vault)._
  > Define an access model for keys and secrets
  > 
  > *Use Azure Key Vault as the secure store and protect the keys/secrets with Azure RBAC.*
* Does the organization have a clear guidance or requirement on what type of keys (PMK - Platform Managed Keys vs CMK - Customer Managed Keys) should be used for this workload?

  _Different approaches can be used by the workload team. Decisions are often driven by security, compliance and specific data classification requirements. Understanding these requirements is important to determine which key types are best suitable (MMK - Microsoft-managed Keys, CMK - Customer-managed Keys or BYOK - Bring Your Own Key)._
  > Provide guidance for either platform managed keys (PMK) or customer managed keys (CMK), based on security or compliance requirements of this workload
* Where is application configuration information stored and how does the application access it?

  _Application configuration information can be stored together with the application itself or preferably using a dedicated configuration management system like Azure App Configuration or Azure Key Vault._
  > Consider storing application configuration in a dedicated management system like Azure App Configuration or Azure Key Vault
  > 
  > *Storing application configuration outside of the application code makes it possible to update it separately and have tighter access control.*
* Does the organization define clear responsibility / role concept for managing keys and secrets for this workload?

  _Central SecOps team should provide guidance on how keys and secrets are managed (governance), application DevOps team is responsible to manage the application related keys and secrets._
  > Define a role & responsibility concept for managing keys and secrets
### Operational Lifecycles
            
* How are operational shortcomings and failures analyzed?

  > Reviewing operational incidents where the response and remediation to issues either failed or could have been optimized is vital to improving overall operational effectiveness. Failures provide a valuable learning opportunity and in some cases these learnings can also be shared across the entire organization.
* Are operational procedures reviewed and refined frequently?

  > Operational procedures should be updated based on outcomes from frequent testing
* Does every environment have a target date for migrating to PaaS or serverless to bring all up cost and transfer risk?

  _To bring down cost the goal should be to get as many applications to only consume resources when they are used, this goes as an evolution from IaaS to PaaS to serverless where you only pay when a service I triggered. The PaaS and serverless might appear more expensive, but risk and other operational work is transferred to the cloud provider which should also be factored in as part of the cost (e.g. patching, monitoring, licenses)._
  > Utilize the PaaS pay-as-you-go consumption model where relevant
* Does every environment have a target end date?

  _If your workload or environment isn't needed then you should be able to decommission it. The same should occur if you are introducing a new service or new feature._
### Patch &amp; Update Process (PNU)
            
* Is the Patch & Update Process (PNU) process defined and for all relevant application components?

  _The PNU process will vary based on the type of Azure service used (i.e. Virtual Machines, Virtual Machine Scale Sets, Containers on Azure Kubernetes Service). Applications using IaaS will typically require more investment to define a PNU process_
  > The PNU process should be fully defined and understood for all relevant application components
    - Is the Patch &amp; Update Process (PNU) process automated?

      > Ideally the PNU process should be fully or partially automated to optimize response times for new updates and also to reduce the risks associated with manual intervention
    - Are Patch &amp; Update Process (PNU) operations performed &#39;as-code&#39;?

      > Performing operations should be defined 'as-code' since it helps to minimize human error and increase consistency
* How are patches rolled back?

  > It is recommended to have a defined strategy in place to rollback patches in case of an error or unexpected side effects
* What is the strategy to keep up with changing dependencies?

  > Changing dependencies, such as new versions of packages, updated Docker images, should be factored into operational processes; the application team should be subscribed to release notes of dependent services, tools, and libraries
* Does the organization reduce the count and potential severity of security vulnerabilities for this workload by implementing security practices and tools during the development lifecycle?

  _Security vulnerabilities can result in an application disclosing confidential data, allowing criminals to alter data/records, or the data/application becoming unavailable for use by customers and employees. Applications will almost always contain logic errors, so it is important to discover, evaluate, and correct them to avoid damage to the organization’s reputation, revenue, or margins. This is made easier by discovering these vulnerabilities in the early stages of the development cycle._
  > Implement security practices and tools during development lifecycle
  
    Additional resources:
    - [Develop Secure Applications on Azure whitepaper](https://azure.microsoft.com/resources/develop-secure-applications-on-azure/)
* Does the organization have a formal policy for this workload to apply security updates to VMs in a timely manner, and do strong passwords exist on those VMs for any local administrative accounts that may be in use?

  _Attackers constantly scan public cloud IP ranges for open management ports and attempt “easy” attacks like common passwords and unpatched vulnerabilities._
  > Put a solution in place that ensures all VMs are patched in a timely manner and that ensures strong local administrative password management
* Are emergency patches handled differently than normal updates?

  _Emergency patches might contain critical security updates that cannot wait till the next maintenance or release window._
### Incident Response
            
* Does the organization have a Security Operations Center (SOC) that leverages a modern security approach?

  _A SOC has a critical role in limiting the time and access an attacker can get to valuable systems and data.  In addition, it provides the vital role of detecting the presence of adversaries, reacting to an alert of suspicious activity, or proactively hunting for anomalous events in the enterprise activity logs._
  > Establish a Security Operations Center (SOC)
* Are operational processes for incident response defined and tested for this workload?

  _Actions executed during an incident and response investigation could impact application availability or performance. It is recommended to define these processes and align them with the responsible (and in most cases central) SecOps team. The impact of such an investigation on the application has to be analyzed._
  > Establish an incident response plan and perform periodically a simulated execution
* Are there playbooks built to help incident responders quickly understand the workload and components to mitigate an attack and investigate?

  _Incident responders are part of a central SecOps team and need to understand security insights of an application. Playbooks can help to understand the security concepts and cover the typical investigation activities. These procedures can and should be automated as much as possible (while maintaining confidence and security)._
  > Implement security playbooks for incident response
  > 
  > *It is recommended to automate as many steps of the investigation and response procedures as you can. Automation reduces overhead. It can also improve your security by ensuring the process steps are done quickly, consistently, and according to your predefined requirements.*
## Deployment &amp; Testing
    
### Application Code Deployments
            
* Can N-1 or N+1 versions be deployed via automated pipelines where N is current deployment version in production?

  _N-1 and N+1 refer to roll-back and roll-forward. Automated deployment pipelines should allow for quick roll-forward and roll-back deployments to address critical bugs and code updates outside of the normal deployment lifecycle._
  > Implement automated deployment process with rollback/roll-forward capabilities
* Is there a defined hotfix process which bypasses normal deployment procedures?

  > In some scenarios there is an operational need to rapidly deploy changes, such as critical security updates. Having a defined process for how such changes can be safely and effectively performed helps greatly to prevent 'heat of the moment' issues.
* Does the application deployment process leverage blue-green deployments and/or canary releases?

  _Blue/green or canary deployments are a way to gradually release new feature or changes without impacting all users at once._
  > Blue-green deployments and/or canary releases can be used to deploy updates in a controlled manner that helps to minimize disruption from unanticipated deployment issues. For example, Azure uses canary regions to test and validate new services and capabilities before they are more broadly rolled out to other Azure regions. Where appropriate the application can also use canary environments to validate changes before wider production rollout. Moreover, certain large application platforms may also derive benefit from leveraging Azure canary regions as a basis for validating the potential impact of Azure platform changes on the application.
  
    Additional resources:
    - [Stage your workloads](https://docs.microsoft.com/azure/architecture/framework/devops/deployment#stage-your-workloads)
* How does the development team manage application source code, builds, and releases?

  _It is important to understand whether there is a systematic approach to the development and release process._
  > The use of source code control systems, such as [Azure Repos](https://azure.microsoft.com/services/devops/) or GitHub, and build and release systems, such as Azure Pipelines or GitHub Actions, should be understood, including the corresponding processes to access, review and approve changes
    - If Git is used for source control, what branching strategy is used?

      _While there are various valid ways, a clearly defined strategy should be in place and understood_
      > To optimize for collaboration and ensure developers spend less time managing version control and more time developing code, a clear and simple branching strategy should be used, such as Trunk-Based Development which is employed internally [within Microsoft Engineering](https://docs.microsoft.com/azure/devops/learn/devops-at-microsoft/use-git-microsoft)
  
    Additional resources:
    - [Azure DevOps](https://azure.microsoft.com/services/devops/)
* Are branch policies used in source control management of this workload? How are they configured?

  _Branch policies provide additional level of control over the code which is commited to the product. It is a common practice to not allow pushing against the main branch and require pull-request (PR) with code review before merging the changes by at least one reviewer, other than the change author. Different branches can have different purposes and access levels, for example: feature branches are created by developers and are open to push, integration branch requires PR and code-review and production branch requires additional approval from a senior developer before merging._
  > Implement a branch policy strategy to enhance DevOps security
* Are code scanning tools an integrated part of the continuous integration (CI) process for this workload?

  _Credentials should not be stored in source code or configuration files, because that increases the risk of exposure. Code analyzers (such as Roslyn analyzers for Visual Studio) can prevent from pushing credentials to source code repository and pipeline addons such as [GitHub Advanced Security](https://docs.github.com/en/github/getting-started-with-github/about-github-advanced-security) or CredScan (part of Microsoft Security Code Analysis) help to catch credentials during the build process._
  > Integrate code scanning tools within CI/CD pipeline
    - Are dependencies and framework components included in the code scanning process of this workload?

      _As part of the continuous integration process it is crucial that every release includes a scan of all components in use. Vulnerable dependencies should be flagged and investigated. This can be done in combination with other code scanning tasks (e.g. code churn, test results/coverage)._
      > Include code scans into CI/CD process that also covers 3rd party dependencies and framework components
  
    Additional resources:
    - [GitHub Advanced Security](https://docs.github.com/github/getting-started-with-github/about-github-advanced-security)
  
    - [OWASP source code analysis tools](https://owasp.org/www-community/Source_Code_Analysis_Tools)
* How long does it take to deploy an entire production environment?

  _The time it takes for a full deployment needs to align with recovery targets._
  > The entire end-to-end deployment process should be understood and align with recovery targets
* What is the process to deploy application releases to production?

  > The entire end-to-end CI/CD deployment process should be understood
    - How long does it take to deploy an entire production environment?

      _The time it takes to perform a complete environment deployment should align with recovery targets. Automation and agility also lead to cost savings due to the reduction of manual labor and errors._
      > The time it takes to perform a complete environment deployment should be fully understood as it needs to align with the recovery targets
* Can the application be deployed automatically from scratch without any manual operations?

  _Manual deployment steps introduce significant risks where human error is concerned and also increases overall deployment times._
  > Automated end-to-end deployments, with manual approval gates where necessary, should be used to ensure a consistent and efficient deployment process
    - Is there a documented process for any portions of the deployment that require manual intervention?

      _Without detailed release process documentation, there is a much higher risk of an operator improperly configuring settings for the application._
      > Any manual steps that are required in the deployment pipeline must be clearly documented with roles and responsibilities well defined
  
    Additional resources:
    - [Deployment considerations for DevOps](https://docs.microsoft.com/azure/architecture/framework/devops/deployment)
* How often are changes deployed to production?

  _Are numerous releases deployed each day or do releases have a fixed cadence, such as every quarter?_
### Application Infrastructure Provisioning
            
* Is application infrastructure defined as code?

  _[Infrastructure as Code](https://docs.microsoft.com/azure/devops/learn/what-is-infrastructure-as-code) (IaC) is the management of infrastructure (networks, virtual machines, load balancers, and connection topology) in a descriptive model, using the same versioning as the team uses for application source code. Like the principle that the same source code generates the same binary, an IaC model generates the same environment every time it is applied._
  > It is highly recommended to describe the entire infrastructure as code, using either ARM Templates, Terraform, or other tools. This allows for proper versioning and configuration management, encouraging consistency and reproducibility across environments.
    - How does the application track and address configuration drift?

      _Configuration drift occurs when changes are applied outside of IaC processes such as manual changes._
      > Tools like Terraform offer a 'plan' command that helps to identify changes and monitor configuration drift, with Azure as the ultimate source of truth
  
    Additional resources:
    - [What is Infrastructure as Code?](https://docs.microsoft.com/azure/devops/learn/what-is-infrastructure-as-code)
* Is direct write access to the infrastructure possible and are any resources provisioned or configured outside of IaC processes?

  _Are any resources provisioned or operationally configured manually through user tools such as the Azure Portal or via Azure CLI?_
  > It is recommended that even small operational changes and modifications be implemented as-code to track changes and ensure they are fully reproducible and revertible. No infrastructure changes should be done manually outside of IaC.
* Is the process to deploy infrastructure automated?

  _Manual changes via for example the Azure Portal or Azure CLI are difficult to test, document and introduce significant risks where human error is concerned and might also increase the overall deployment and recovery times._
  > It is recommended to define infrastructure deployments and changes as code and to use build and release tools to develop automated pipelines for their deployment
* How are credentials, certificates and other secrets managed in CI/CD pipelines for this workload?

  _Secrets need to be managed in a secure manner inside of the CI/CD pipeline. Secrets need to be stored either in a secure store inside the pipeline or externally in Azure Key Vault. When deploying application infrastructure (e.g. with Azure Resource Manager or Terraform), credentials and keys should be generated during the process, stored directly in Key Vault and referenced by deployed resources. Hardcoded credentials should be avoided._
  > Store keys and secrets outside of deployment pipeline in Azure Key Vault or in secure store for the pipeline
### Build Environments
            
* Are mocks/stubs used to test external dependencies in non-production environments?

  _Mocks/stubs can help to test and validate external dependencies, to increase test coverage, when accessing those external dependencies is not possible due to for example IP restrictions._
  > The use of dependent services should be appropriately reflected in test environments
* Does the organization apply security controls (e.g. IP firewall restrictions, update management, etc.) to self-hosted build agents for this workload?

  _When the organization uses their own build agents it adds management complexity and can become an attack vector. Build machine credentials must be stored securely and file system needs to be cleaned of any temporary build artifacts regularly. Network isolation can be achieved by only allowing outgoing traffic from the build agent, because it's using pull model of communication with Azure DevOps._
  > Apply security controls to self-hosted build agents in the same manner as with other Azure IaaS VMs
* Is the application deployed to multiple environments with different configurations?

  _Understand the scope of the solution and distinguish between SKUs used in production and non-production environments. To drive down cost, it might be possible to for example consolidate environments for applications that are not as critical to the business and don't need the same testing._
    - What is the ratio of cost of production and non-production environments for this workload?

      _When the customer is spending more money on testing than production, it usually means they have too many non-production environments. Consider ratio of non-production to production environments and if ratio is substantially higher you should consider merging testing environments or re-visit why the cost is so much higher._
    - How many production vs. non-production environments do you have?

      _Provisioning non-production environments (like development, test, integration...) each on a separate infrastructure is not always necessary. E.g. using shared App Service Plans and consolidating Web Apps for development and testing environments can save costs._
* Do critical test environments have 1:1 parity with the production environment?

  _Do test environment differ from production in more than just smaller SKUs being used, e.g. by sharing components between different environments?_
  > To completely validate the suitability of application changes, all changes should be tested in an environment that is fully reflective of production, to ensure there is no potential impact from environment deltas
* Are releases to production gated by having it successfully deployed and tested in other environments?

  _Deploying to other environments and verifying changes before going into production can prevent bugs getting in front of end users._
  > It is recommended to have a staged deployment process which requires changes to have been validated in test environments first before they can hit production
* Are feature flags used to test features before rolling them out to everyone?

  > To test new features quickly and without bigger risk, [Feature flags](https://docs.microsoft.com/azure/architecture/framework/devops/development#feature-flags) are a technique to help frequently integrate code into a shared repository, even if incomplete. It allows for deployment decisions to be separated from release decisions
  
    Additional resources:
    - [Feature Flags](https://docs.microsoft.com/azure/architecture/framework/devops/development#feature-flags)
### Testing &amp; Validation
            
* Does the organization perform penetration testing or have a third-party entity perform penetration testing of this workload to validate the current security defenses?

  _Real world validation of security defenses is critical to validate a defense strategy and implementation. Penetration tests or red team programs can be used to simulate either one time, or persistent threats against an organization to validate defenses that have been put in place to protect organizational resources._
  > Use penetration testing and red team exercises to validate security defenses for this workload
* Is the application tested for performance, scalability, and resiliency?

  _**Performance testing** is the superset of both load and stress testing. The primary goal of performance testing is to validate benchmark behavior for the application.<br />**Load Testing** validates application scalability by rapidly and/or gradually increasing the load on the application until it reaches a threshold/limit.<br />**Stress Testing** is a type of negative testing which involves various activities to overload existing resources and remove components to understand overall resiliency and how the application responds to issues._
  > Define a testing strategy
    - How does your team perceive the importance of performance testing?

      _It is critical that your team understands the importance of performance testing. Additionally, the team should be committed to providing the necessary time and resources for adequately executing performance testing proven practices._
    - When do you do test for performance, scalability, and resiliency?

      _Regular testing should be performed as part of each major change and if possible on a regular basis to validate existing thresholds, targets and assumptions, as well as ensuring the validity of the health model, capacity model and operational procedures._
    - Are any tests performed in production?

      _While the majority of testing should be performed within the testing and staging environments, it is often beneficial to also run a subset of tests against the production system._
    - Is the application tested with injected faults?

      _It is a common "chaos monkey" practice to verify the effectiveness of operational procedures using artificial faults. For example, taking dependencies offline (stopping API apps, shutting down VMs, etc.), restricting access (enabling firewall rules, changing connection strings, etc.) or forcing failover (database level, Front Door, etc.) is a good way to validate that the application is able to handle faults gracefully._
  
    Additional resources:
    - [Testing strategies](https://docs.microsoft.com/azure/architecture/checklist/dev-ops#testing)
* Does the organization have a method to carry out simulated attacks on users of this workload?

  _People are a critical part of your defense, especially those with elevated permissions, so ensuring they have the knowledge and skills to avoid and resist attacks will reduce your overall organizational risk. Simulating attacks for educational purposes helps to enforce understanding of the various means that an attacker may use to compromise accounts. Tools such as Office 365 Attack Simulation or similar may be used._
  > Simulate attack against users and critical accounts. Ensure proper follow-up to educate users about the various means that an attacker may use
* Does the organization use Azure Defender (Azure Security Center) or any third-party solution to scan containers in this workload for vulnerabilities?

  _Azure Security Center is the Azure-native solution for securing containers. Security Center can protect virtual machines that are running Docker, Azure Kubernetes Service clusters, Azure Container Registry registries. ASC is able to scan container images and identify security issues, or provide real-time threat detection for containerized environments._
  > Scan container workloads for vulnerabilities
  
    Additional resources:
    - [Container Security in Security Center](https://docs.microsoft.com/azure/security-center/container-security)
* Are Dev/Test offerings used correctly for the workload?

  _Special SKUs and subscription offers for development and testing purposes can save costs, but have to be used properly. Dev SKUs are not meant for production deployments._
  > Use developer SKUs for dev/test purposes
* Are smoke tests performed during application deployments?

  _[Smoke tests](https://docs.microsoft.com/azure/architecture/framework/devops/testing#smoke-testing) are a lightweight way to perform high-level validation of changes. For instance, performing a ping test immediately after a deployment._
  
    Additional resources:
    - [Smoke Testing](https://docs.microsoft.com/azure/architecture/framework/devops/testing#smoke-testing)
* Are these tests automated and carried out periodically or on-demand?

  _Testing should be fully automated where possible and performed as part of the deployment lifecycle to validate the impact of all application changes. Additionally, manual explorative testing may also be conducted._
* What degree of security testing is performed?

  _Security and penetration testing, such as scanning for open ports or known vulnerabilities and exposed credentials, is vital to ensure overall security and also support operational effectiveness of the system._
* Do you perform Business Continuity 'fire drills' to test regional failover scenarios?

  _Business Continuity 'fire drills' help to ensure operational readiness and validate the accuracy of recovery procedures ready for critical incidents._
* What happens when a test fails?

  _Failed tests should temporarily block a deployment and lead to a deeper analysis of what has happened and to either a refinement of the test or an improvement of the change that caused the test to fail._
* Are tests and test data regularly validated and updated to reflect necessary changes?

  _Tests and test data should be evaluated and updated after each major application change, update, or outage._
* Are test-environments deployed automatically and deleted after use? Use of tagging for end date?

  _Automating test cases reduces time, cost and helps inefficient resource utilization. It also provides a structured approach to testing with test scripts. Test environments can quickly become overhead if not monitored properly, therefore stopping these resources when they are not in use enables cost saving. In order to drive down cost a good place to look is test environments that might not be used anymore. Implementing a process can help by tagging all test environments with an end date and an owner and after this date follow up with the owner if the environment is still needed and if so set a new end-of-life date._
  > Make sure to delete/deallocate resources used in test environments
* Is unit testing performed to validate application functionality?

  _[Unit tests](https://docs.microsoft.com/azure/architecture/framework/devops/testing#unit-testing) are typically run by each new version of code committed into version control. Unit Tests should be extensive and quick to verify things like syntax correctness of application code, Resource Manager templates or Terraform configurations, that the code is following best practices, or that they produce the expected results when provided certain inputs._
  
    Additional resources:
    - [Unit Testing](https://docs.microsoft.com/azure/architecture/framework/devops/testing#unit-testing)
* When is integration testing performed?

  _[Integration tests](https://docs.microsoft.com/azure/architecture/framework/devops/testing#integration-testing) should be applied as part of the application deployment process, to ensure that different application components  interact with each other as they should. Integration tests typically take longer than smoke testing, and as a consequence occur at a latter stage of the deployment process so they are executed less frequently._
  
    Additional resources:
    - [Integration Testing](https://docs.microsoft.com/azure/architecture/framework/devops/testing#integration-testing)
## Operational Model &amp; DevOps
    
### General
            
* Does the organization leverage DevOps security guidance based on industry lessons-learned, and available automation tools (OWASP guidance, Microsoft toolkit for Secure DevOps etc.)?

  _Organizations should leverage a control framework such as NIST, CIS or [Azure Security Benchmarks (ASB)](https://docs.microsoft.com/azure/security/benchmarks/) for securing applications on the cloud rather than starting from zero._
  > Follow DevOps security guidance and automation for securing applications
  
    Additional resources:
    - [Azure Security Benchmarks](https://docs.microsoft.com/azure/security/benchmarks/)
* Has the organization adopted a formal DevOps approach to building and maintaining software in this workload to ensure security and feature enhancements can be deployed in rapid fashion?

  _The DevOps approach increases the organization’s ability to rapidly address security concerns without waiting for a longer planning and testing cycle of traditional waterfall model. Key attributes are: automation, close integration of infra and dev teams, testability and reliability and repeatability of deployments.* [Adopt the DevOps approach](https://docs.microsoft.com/azure/architecture/framework/Security/applications-services#adopt-the-devops-approach)_
  > Adopt a formal DevSecOps approach to building and maintaining software
* Are specific methodologies, like DevOps, used to structure the development and operations process?

  _The contraction of “Dev” and “Ops” refers to replacing siloed Development and Operations to create multidisciplinary teams that now work together with shared and efficient practices and tools. [Essential DevOps practices](https://docs.microsoft.com/azure/devops/learn/what-is-devops) include agile planning, continuous integration, continuous delivery, and monitoring of applications._
  
    Additional resources:
    - [What is DevOps?](https://docs.microsoft.com/azure/devops/learn/what-is-devops)
* Is the current development and operations process connected to a Service Management framework like ISO or ITIL?

  _[ITIL](https://en.wikipedia.org/wiki/ITIL) is a set of detailed [IT service management (ITSM)](https://en.wikipedia.org/wiki/IT_service_management) practices that can complement DevOps by providing support for products and services built and deployed using DevOps practices._
  
    Additional resources:
    - [ITIL](https://en.wikipedia.org/wiki/ITIL)
  
    - [IT service management (ITSM)](https://en.wikipedia.org/wiki/IT_service_management)
### Roles &amp; Responsibilities
            
* Does the organization clearly define CI/CD roles and permissions for this workload?

  _Defining CI/CD permissions properly ensures that only users responsible for production releases are able to initiate the process and that only developers can access the source code. Azure DevOps offers pre-defined roles which can be assigned to individual users of groups. Using them properly can make sure that for example only users responsible for production releases are able to initiate the process and that only developers can access the source code. Variable groups often contain sensitive configuration information and can be protected as well._
  > Clearly define CI/CD roles and permissions
* Are Billing account names and structure consistent with reference to or use of Departments or Services, or Organization?

  _Transparency and traceability when it comes to cost in order to ensure that any discrepancies are able to be followed back to the source and be dealt with accordingly._
* Has the organization clearly defined lines of responsibility and designated responsible parties for specific functions in Azure?

  _Clearly documenting and sharing the contacts responsible for each of these functions will create consistency and facilitate communication. Examples of such contact groups include network security, network management, server endpoint security, incident response, policy management, identity..._
  > Designate the parties responsible for specific functions in Azure
* Does the organization have the appropriate emergency access accounts configured for this workload in case of an emergency?

  _While rare, sometimes extreme circumstances arise where all normal means of administrative access are unavailable and for this reason emergency access accounts (also refered to as 'break glass' accounts) should be available. These accounts are strictly controlled in accordance with best practice guidance, and they are closely monitored for unsanctioned use to ensure they are not compromised or used for nefarious purposes._
  > Configure emergency access accounts
  > 
  > *The impact of no administrative access can be mitigated by creating two or more [emergency access accounts](https://docs.microsoft.com/azure/active-directory/roles/security-emergency-access) in Azure AD.*
  
    Additional resources:
    - [Emergency Access Accounts](https://docs.microsoft.com/azure/active-directory/roles/security-emergency-access)
* Has the organization developed and maintained a security training program to ensure technical staff of this workload are well-informed and equipped with the appropriate skills?

  _Cybersecurity threats are always evolving and therefore those responsible for organizational information security require specialized, continual, and relevant training to ensure staff maintains the level of competency required to protect, detect, and respond._
  > Develop security training program
* Are tools or processes in place to grant access on a just-in-time basis?

  _Minimizing the number of people who have access to secure information or resources reduces the chance of a malicious actor gaining access or an authorized user inadvertently impacting a sensitive resource. For example, Azure AD [Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-configure) provides time-based and approval-based role activation to mitigate the risks of excessive, unnecessary, or misused access permissions on resources that you care about._
  > Implement just-in-time privileged access management
    - Does anyone have long-standing write-access to production environments?

      _Regular, long-standing write access to production environments by user accounts can pose a security risk and manual intervention is often prone to errors._
      > Limit long-standing write access to production environments only to service principals
  
      Additional resources:
        - [No standing access / Just in Time privileges](https://docs.microsoft.com/azure/architecture/framework/security/design-admins#no-standing-access--just-in-time-privileges)
  
    Additional resources:
    - [No standing access / Just in Time privileges](https://docs.microsoft.com/azure/architecture/framework/security/design-admins#no-standing-access--just-in-time-privileges)
* Are manual approval gates or workflows required to release to production?

  _Even with an automated deployment process there might be a requirement for manual approvals to fulfil regulatory compliance, and it is important to understand who owns any gates that do exist._
* How are development priorities managed for the application?

  _It is important to understand how business features are prioritized relative to engineering fundamentals, especially if operations is a separate function._
* Are any broader teams responsible for operational aspects of the application?

  _Different teams such as Central IT, Security, or Networking may be responsible for aspects of the application which are controlled centrally, such as a shared network virtual appliance (NVA)._
* Is there a separation between development and operations?

  _A true DevOps model positions the responsibility of operations with developers, but many customers do not fully embrace DevOps and maintain some degree of team separation between operations and development, either to enforce clear segregation of duties for regulated environments, or to share operations as a business function._
    - Does the development team own production deployments?

      _It is important to understand if developers are responsible for production deployments end-to-end, or if a handover point exists where responsibility is passed to an alternative operations team, potentially to ensure a strict segregation of duties such as Sarbanes-Oxley Act where developers cannot touch financial reporting systems._
    - How do development and operations teams collaborate to resolve production issues?

      _It is important to understand how operations and development teams collaborate to address operational issues, and what processes exist to support and structure this collaboration. Moreover, mitigating issues might require the involvement of different teams outside of development or operations, such as networking, and in some cases external parties as well. The processes to support this collaboration should also be understood._
    - Is the workload isolated to a single operations team?

      _The goal of [workload isolation](https://docs.microsoft.com/azure/architecture/framework/devops/app-design#workload-isolation) is to associate an application's specific resources to a team, so that the team can independently manage all aspects of those resources._
  
      Additional resources:
        - [Workload isolation](https://docs.microsoft.com/azure/architecture/framework/devops/app-design#workload-isolation)
* Has the application been built and maintained in-house or by an external partner?

  _Exploring where technical delivery capabilities reside helps to qualify operational model boundaries and estimate the cost of operating the application as well as defining a budget and cost model._
  > Explore where technical delivery capabilities reside
* Does the organization have release gate approvals configured in their DevOps release process of this workload?

  _Pull Requests and code reviews serve as the first line of approvals during development cycle. Before releasing new code to production (new features, bugfixes etc.), security review and approval should be required._
  > Configure quality gate approvals in DevOps release process
* Is the security team involved in the planning, design and overall DevOps process of this workload, so that they can implement security controls, auditing and response processes?

  _There should be a process for onboarding service securely to Azure. The onboarding process should include reviewing the configuration options to determine what logging/monitoring needs to be established, how to properly harden a resource before it goes into production.  For a list of common criteria for onboarding resoruces, see the [Service Enablement Framework](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/enterprise-scale/security-governance-and-compliance#service-enablement-framework)_
  > Involve the security team in the development process
## Performance Testing
    
### Tools &amp; Planning
            
* Are you currently using tools for conducting performance testing?

  _There are various performance testing tools available for DevOps. Some tools like JMeter only perform testing against endpoints and tests HTTP statuses. Other tools like K6 and Selenium can perform tests that also check data quality and variations. Application Insights, while not necessarily designed to test server load, can test the performance of an application within the user's browser. When determining what testing tools you will implement, it is always important to remember what type of performance testing you are attempting to execute._
    - What types of performance testing are you currently executing (or looking to execute) against your application?

      _Most people think of load testing as the only form of performance testing. However, there are different types of performance testing--load testing, stress testing, API testing, client-side/browser testing, etc. It is important that you understand and are able to articulate the different types of tests, along with their pro's and con's. With a solid understanding shared amongst your team members, you can identify a path forward to leveraging existing tests or the creation of new tests._
    - How much of your application is currently tested for performance?

      _Performance testing can be initiated within the client's browser, full integration testing (e.g. testing the response of multiple endpoints required to comprise the data of a single page), or testing the performance of a single API endpoint. As stated under the previous question, having a clear vision of the areas you are attempting to test will help identify the tools you will need._
    - Considering the three major application layers of frontend, services, and database, what parts of the application are being tested for performance?

* Have you identified the required human and environment resources needed to create performance tests?

  _Successfully implementing meaningful performance tests requires a number of resources. If is not just a single developer or QA Analyst running some tests on their local machine. Instead, performance tests need a test environment (also known as a test bed) that tests can be executed against without interfering with production environments and data. Performance testing requires input and commitment from developers, architects, database administrators, and network administrators. In short, solid performance testing is a team responsibility.<br />Additionally, to run scaled tests, a machine with enough resources (e.g. memory, processors, network connections, etc.) needs to be made available. While this machine can be located within a data center or on-premises, it is often advantageous to perform performance testing from instances located from multiple geographies. This better simulates what an end-user can expect._
* Have you identified all services being utilized in Azure (and on-prem) that need to be measured?

  _Your assessment may already be complete, but it helps to identify some currently utilized systems to being measuring load capacity. Once these environments have been identified, created benchmarks should include these systems._
### Benchmarking
            
* How do you know when you have reached acceptable efficiency?

  _There is almost no limit to how much an application can be performance-tuned. How do you know when you have tuned an application enough? It really comes down to the 80/20 rule--generally, 80% of the application can be optimized by focusing on just 20%. While you can continue optimizing certain elements of the application, after optimizing the initial 20%, a company typically sees a diminishing return on any further optimization. The question the customer must answer is how much of the remaining 80% of the application is worth optimizing for the business. In other words, how much will optimizing the remaining 80% help the business reach its goals (e.g. customer acquisition/retention, sales, etc.)? The business must determine their own realistic definition of "acceptable."_
* Do you have goals for database queries?

  _Ensuring the data operations are optimized is a key component to any performance assessment. It is important to understand what data is being queried and when. The data life-cycle, if abused, can adversely affect the performance of any application (or microservice). Confirm that a database administrator (a data architect is preferred) is part of the assessment as they will have the necessary tools for monitoring and optimizing a database and its queries._
    - What are your goals for an individual database query execution and response?

    - How often are you achieving your goals for database query execution?

* Do you have goals for latency between systems/microservices?

  _Performance should not only be monitored within the application itself, but response times between service tiers should also be noted. While this is important for n-Tier applications, it is especially crucial for microservices. Most microservices leverage some type of pub-sub architecture where communication is asynchronous. However, validation for sending and receiving messages should still take place. In these instances, understanding the routing and latency between services is imperative to improving performance._
    - What are your goals for a complete response from a given microservice?

    - How often are you achieving your microservice response goals?

* Do you have goals defined for server response times?

  _Similar to previous questions regarding the initial connection to a service, you will also want to understand how long it takes for the server to receive, process, and then return data. This round-trip can also help ensure that enough hardware resources have been assigned to the environment. Additionally, it is possible to identify "noisy neighbors", applications running on the same disk (typically in a virtualized environment) or sharing the same network, that are consuming available resources. Finally, another bottleneck in many environments is traffic on a network that is being shared with a data store (e.g. SQL). If an application server and its database server share the same network as general traffic, then the overall performance of the application can be greatly affected._
    - What are your goals for a full server response?

    - How often are you achieving your server response goals?

* Have you identified goals or baselines for application performance?

  _There are many types of goals when determining baselines for application performance. Perhaps baselines center around a certain number of visitors within a given time period, the time it takes to render a page, type  required for executing a stored procedure, or a desired number of transactions if your site conducts some type of e-commerce. It is important to identify and maintain a shared understanding of these baselines so that you can architect a system that meets them.<br />Baselines can vary based on types of connections or platforms that a user may leverage for accessing the application. It may be important to establish baselines that address the diversity of connections, platforms, and other elements (like time of day, or weekday versus weekend)._
    - Are your goals based on device and/or connectivity type, or are they considered the same across the board?

      _It is important to identify how users are connecting to your application. Are they primarily connecting via a wired connection, wireless, or by using a mobile device? Additionally, you should seek to understand the targeted device types, whether that a mobile device, a tablet or laptop/desktop PC. All of these factors play a major role in performance as it relates to data transmission (e.g. sending data to and receiving data from a remote service) and processing (e.g. displaying that data to a user via a graph, table, etc.). For example, if the site has a large amount of widgets, it may be advantageous to create an experience that is optimized for mobile devices since these devices tend to have smaller processors and less memory._
* Do you have goals defined for establishing an initial connection to a service?

  _It would be helpful to determine a goal that is based upon from when the connection reaches the server, to when the service spins/cycles up, to providing a response. By establishing this baseline, you and your customer can determine if adequate resources have been assigned to the machine. These resources can included, but are not limited to processors, RAM, and disk IOPS. Finally, creating rules for "Always-On" or properly configuring idle time-outs (e.g. IIS, containers, etc.) will be especially helpful for optimizing response times._
* Do you have goals defined for a complete page load?

  _What are your goals for a completed page load? When formulating this metric, it is important to note the varying thresholds that can be deemed acceptable. Some companies, whose primary audience is internal and are salary-based, may base their thresholds on the user's mental capacity to sit at the application screen. Other customers that have service-related users (i.e. users who are paid for performance) may base their thresholds on the ability to keep the user working as fast as possible (mental state is not the primary motivator) because increased productivity typically increases revenue. Typically, most industry standards target page load times to 1-2 seconds, while 3-5 seconds is "acceptable," and more than 5 is unacceptable. If applications are being hosted in Azure App Services, there are a number of tactics that can increase page performance._
    - What are your goals for a completed page load?

    - How often are you achieving your page load goals?

* Do you have goals defined for an API (service) endpoint complete response?

  _Data-centric applications are comprised of pulling data from various API endpoints. For a single page, this could mean many server requests. The page is only as fast as the slowest endpoint. It is important for you to test the performance of your APIs to quickly identify bottlenecks in the application that impede user experience. As an example, if a dashboard page requires data from ten API endpoints and one of those endpoints requires 6.0 seconds to return data while the remaining endpoints only a few hundred milliseconds, this is a good indicator that the single endpoint needs to be inspected and targeted for optimization._
    - What are your goals for a complete response from a given API?

    - How often are you achieving your API response goals?

### Load Capacity
            
* How much of the application is involved in serving an immediate, single request?

  _When understanding load and demands on the application, it is necessary to understand how the application is architected - whether monolithic, n-Tier, or microservice-based - and then understand how load is distributed across the application. This is crucial for focusing on the testing of individual components and identifying bottlenecks._
* Have you determined an acceptable operational margin between your peak utilization and the applications maximum load?

  _What is the maximum taxation you wish to place on resources? Factors such as memory, CPU, and disk IOPS should all be considered. Once a stress test has been performed resulting in the maximum supported load and an operational margin has been chosen, it is best to determine an operational threshold. Then, environment scaling (automatic or manual) can be performed once the threshold has been reached._
    - What are the metrics of a performance test under standard loads?

      _A true performance test measures how the application performs under a standard load. It is critical to understand how your application operates--including CPU utilization and memory consumption--under a standard load. First, this will help you plan accordingly as you anticipate future user growth. Second, this gives you a baseline for performance regression testing._
    - Given your determination of acceptable operational margin and response under standard levels of load, has the environment been configured adequately?

      _Determine if the environment is rightly configured to handle "standard" loads. (e.g. Are the correct SKUs selected based on desired margins?) Over allocation can unnecessarily increase costs and maintenance; under allocation can result in poor user experience._
    - How well does the application respond under fluctuating increased levels of loads?

      _Typically, there is a stair step model to determining load capacity. The stair step model considers various levels of users for various time periods. Running a load test helps to determine how well the application scales as load increases on the application._
    - Given your determination of acceptable operational margin and response under increased levels of load, have you configured the environment to scale out to sustain performance efficiency?

      _Determine if the environment is rightly configured to scale in order to handle increased loads. (e.g. Does the environment scale effectively at certain times of day or at specific performance counters?) If you have identified specific times in which load increases (e.g. holidays, marketing drives, etc.), then the environment can be configured to proactively scale prior to the actual increase in load._
* Has caching and queuing been considered to handle varying load?

  _Caching and queuing offers ways to handle heavy load in read and write scenarios, respectively. However, their usage must be carefully considered as this may mean that data is not fresh and writes to not happen instantly. This could create a scenario of eventual consistency and stale data._
    - Are you using any caching mechanisms?

      _Use caching whenever possible, whether it is client-side caching, view caching, or data caching. Caching can also be configured on the browser, the server, or on an appliance in-between (e.g. Azure Frontdoor). Incorporating caching can help reduce latency and server taxation by eliminating repetitive class to microservices, APIs, and data stores._
    - Are you using static or page caching mechanisms?

      _Available static and page caching mechanisms are for example:<br />- Browser<br />- Azure CDN<br />- Azure Front Door<br />- Other<br />There are various types of caching mechanisms that can be configured with a web page and its components. Such examples include expiry dates, tags, modification dates, content, or other variances like IP addresses or encoding types._
    - What technology are you using for data caching?

      _Available data caching technologies are for example:<br />- Azure Redis Cache<br />- IIS Caching Server<br />- SQL Caching Server<br />- Disk<br />- Other solution_
      > Azure Cache for Redis is a preferred solution for data caching as it improves performance by storing data in memory instead of on disk like SQL Server. Certain development frameworks like .NET also have mechanisms for caching data at the server level.
### Troubleshooting
            
* Do you profile the application code with any profiling tools?

  _Application profiling will involve tooling like Visual Studio Performance Profile, AQTime, dotTrace, and others. These tools will give you in-depth analysis of individual code paths._
* Do you profile the network with any traffic capturing tools?

  _Network capture tooling can capture the network traffic and dive deeper into the interactions at the network layer that may affect your application due to network configuration and/or other network traffic issues._
* Does the application spend a lot of time in the database?

  _Applications that spend a lot of execution time in the database layers can benefit from a database tuning analysis. This analysis will only focus on the data tier components and may require special resources such as DBA's to tune queries, indexes, execution plans, and more._
* Does the application response times increase while not using all the CPU or memory allocated to the system regardless of the load?

  _When the system response times increase without any increase in the CPU or memory, this is an indicator that there is a resource that is time-blocked. This can mean many things such as thread sleep, connection wait, message queueing, etc. The list can go on. The bottom line is there is something that is consuming time but not compute resources. Try to locate these issues with tracing data that can deliver time spans for each layer of the application architecture that is correlated to an application transaction._
    - Have you identified the length of time it takes before response times increase?

    - How long does it take for response times to return to &#34;normal?&#34;

* Does the application have high CPU or memory utilization?

  _If the application has very high CPU or memory utilization, then consider scaling the application either horizontal or vertical. Scaling horizontal to more compute resources will spread the load across more machines. This will, however, increase the network complexity as there will be more machines to support the system. Scaling the application vertical to a larger machine this is optimized for higher CPU or memory workloads may also be considered. Profiling the application code can be useful to find code structures that may be sub-optimal and replace them with better-optimized code. These decisions are a balance of several factors that can include cost, system complexity, and time to implement._
    - Have you identified the length of time it takes before CPU or memory increases?

    - How long does it take for system resources to return to &#34;normal?&#34;

## Governance
    
### Standards
            
* Are tools and processes in place to govern available services, enforce mandatory operational functionality and ensure compliance?

  _Proper standards for naming, tagging, the deployment of specific configurations such as diagnostic logging, and the available set of services and regions is important to drive consistency and ensure compliance. Solutions like [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) can help to enforce and assess compliance at-scale._
* Does the application have a well-defined naming standard for Azure resources?

  _A well-defined naming convention is important for overall operations to be able to easily determine the usage of certain resources and help understand owners and cost centers responsible for the workload. Naming conventions allow the matching of resource costs to particular workloads._
  > Implement a naming convention
  > 
  > *Having a well-defined [naming convention](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/naming-and-tagging) is important for overall operations, particularly for large application platforms where there are numerous resources.*
  
    Additional resources:
    - [Naming Conventions](https://docs.microsoft.com/azure/cloud-adoption-framework/ready/azure-best-practices/naming-and-tagging)
* Is the choice and desired configuration of Azure services centrally governed or can the developers pick and choose?

  _Many customers govern service configuration through a catalogue of allowed services that developers and application owners must pick from._
* Are Azure Tags used to enrich Azure resources with operational metadata?

  _Using tags can help to manage resources and make it easier to find relevant items during operational procedures._
  > Enforce naming conventions and resource tagging for all Azure resources
  > 
  > *[Azure Tags](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources) provide the ability to associate critical metadata as a name-value pair, such as billing information (e.g. cost center code), environment information (e.g. environment type), with Azure resources, resource groups, and subscriptions. See [Tagging Strategies](https://docs.microsoft.com/azure/cloud-adoption-framework/decision-guides/resource-tagging) for best practices.*
  
    Additional resources:
    - [Use tags to organize your Azure resources and management hierarchy](https://docs.microsoft.com/azure/azure-resource-manager/management/tag-resources)
  
    - [Tagging Strategies](https://docs.microsoft.com/azure/cloud-adoption-framework/decision-guides/resource-tagging)
* Are standards, policies, restrictions and best practices defined as code?

  _Policy-as-Code provides the same benefits as Infrastructure-as-Code in regards to versioning, automation, documentation as well as encouraging consistency and reproducibility. Available solutions in the market are [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview) or [HashiCorp Sentinel](https://www.hashicorp.com/resources/introduction-sentinel-compliance-policy-as-code/)._
  
    Additional resources:
    - [Azure Policy](https://docs.microsoft.com/azure/governance/policy/overview)
  
    - [HashiCorp Sentinel](https://www.hashicorp.com/resources/introduction-sentinel-compliance-policy-as-code/)
* Has the organization implemented or considered implementing elevated security capabilities such as dedicated Hardware Security Modules (HSMs) or the use of Confidential Computing?

  _Careful consideration is necessary on whether to utilize specialized security capabilities in the workload architecture. These capabilities include dedicated [Hardware Security Modules](https://docs.microsoft.com/azure/key-vault/managed-hsm/overview) and [Confidential Computing](https://azure.microsoft.com/solutions/confidential-compute/)._
  > Review and consider elevated security capabilities for Azure workloads
* Are there any regulatory or governance requirements for this workload?

  _Regulatory requirements may mandate that operational data, such as application logs and metrics, remain within a certain geo-political region. This has obvious implications for how the application should be operationalized._
  > Make sure that all regulatory requirements are known and well understood
  > 
  > *Create processes for obtaining attestations and be familiar with the [Microsoft Trust Center](https://www.microsoft.com/trust-center). Regulatory requirements like data sovereignty and others might affect the overall architecture as well as the selection and configuration of specific PaaS and SaaS services.*
  
    Additional resources:
    - [Microsoft Trust Center](https://www.microsoft.com/trust-center)
### Financial Management &amp; Cost Models
            
* How is your organization modeling cloud costs for this workload?

  _Estimate and track costs, educate the employees about the cloud and various pricing models, have appropriate governance about expenditure._
* Is there any weekly review process to follow up on budget overrun or signs of spend that should be dealt with?

  _During a weekly review a key area to discuss is high spending on SKUs or workloads that has a high cost, which might cause a budget overrun. Discussing these spendings early and plan for next step enables the business to be pro-active about spending._
  > Perform regular reviews focused on cost and spending for this workload
* Do shared services have an owner and is all up cost with the distribution model defined and communicated by the owner to the service subscribers?

* Is spending forecast to ensure it aligns with budget?

  _In order to predict costs and trends it’s recommended to use forecasting to be proactive for any spending that might be going up due to higher demand than anticipated._
  > Use cost forcasting as a tool to estimate if the workload is aligned with budget
* Is there a cost owner for every service used by this workload?

  _Every service should have a cost owner that is tracking and is responsible for cost. This drives responsibility and awareness on who owns the cost tracking._
  > Establish a cost owner for each service used by the workload
* Do all services used in this workload have a budget assigned to them?

  _For cost management it is recommended to have a budget even for the smallest services operated as that allows to track and understand the flow of the spend and also understand the impact of a smaller service in a bigger picture._
  > Assign a budget and spend limit to the workload
* What actions are you taking to optimize cloud costs of this workload?

  _Identify opportunities to reduce overall cost, use cost management tools to plan and track costs, tag resources and track that back to costs._
### Culture &amp; Dynamics
            
* What happens to the money that you’ve saved? If you go over budget do you have to save somewhere else?

* Are you allowed to exceed budget, if there is proven business justification for it?

* Is there an ongoing conversation between the app owner and the business?

  _Is what’s delivered from IT and what the business is expecting from IT mapped to the cost of the application?_
* When new applications are introduced to the company, how is the budget defined?

  _It is important to have a clear understanding how an IT budget is defined. This is especially true for applications that are not built in-house, where IT budget has to be factored in as part of the delivery._
  > Understand how is the budget defined
* Is there a yearly or monthly meeting where you are able to re-negotiate budget or is it given to you?

  _As Azure changes and new services are introduced, it’s recommended that key services are revisited to see if any new services offered in Azure can help drive down cost or if new SKUs can help drive down cost. It’s recommended that this is done 1-4 times a year._
  > Revisit key Azure services to see if there were any updates which could reduce the spend
* When you build new workloads, are you factoring the budget into the building phase? (Is the cost associated to the criticality to the business?)

  _When building new applications it’s a good practice to have a discussion with the business regarding expectations and build a budget as early as possible and document assumptions of how the IT budget for the service was calculated._
### Licensing
            
* Is A-HUB (Azure Hybrid Use Benefit) used to drive cost down in order to re-use licenses to drive cost down in cloud?

  _Understanding your current spending on licenses can help you drive down cost in the cloud. A-HUB allows you to reuse licenses that you purchased for on-premises in Azure and via this drive down the cost as the license is already paid._
  > See if you can use the hybrid use benefit to reuse licensing
* Are any special discounts given to services or licenses that should be factored in when calculating new cost models for services being moved to the cloud?

  _When alternative cost options are considered it should be understood first if any special offers or deals are given for the existing SKUs to verify that the correct prices are being used to build a business case._
  > Learn if there are any discounts available for the services already in use
* Is there an owner for licensing and is this owner aware of any benefits that can be driven for hybrid license models?

  _Having a go to person in the company who understands the rules and knows what has been bought helps making sure that the right licenses are being used before building a business case for a new workload / application in Azure._
