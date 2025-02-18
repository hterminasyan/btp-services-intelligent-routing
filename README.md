# Intelligent Routing for SAP Launchpad service on SAP Business Technology Platform using Google Cloud DNS
<!--- Register repository https://api.reuse.software/register, then add REUSE badge:
[![REUSE status](https://api.reuse.software/badge/github.com/SAP-samples/REPO-NAME)](https://api.reuse.software/info/github.com/SAP-samples/REPO-NAME)
-->

## Description

Many organizations have business-critical applications that are needed to be operational all the time. This includes all of the cloud services which are exposed and extended to business users both internal and external. On SAP Business Technology Platform, the SAP Launchpad service needs to be available at all times and also ensure good latency as this will be the single point of access to business users.

SAP Business Technology Platform services such as SAP Launchpad service supports the concept of the Availability Zones (AZ). These AZs are single failure domains within a single geographical region and are in separate physical locations with independent power, network, and cooling. Multiple AZs exist in one region and are connected with each other through a low-latency network.

![Availability Zones](./images/AZ_concept.png)

This will ensure if there is an issue or an outage in a single region's AZ then the other AZ in the same region will serve the requests.

But an AZ setup might not work in few case like if there is a Natural disaster, which are usually across AZs or in case the user base is across different regions(for instance US & Europe) there can be issues with network latency.

In such cases, to achieve better fault-tolerance, it is recommended to deploy applications and configure services in multiple regions.

![Launchpad service High Availability using Google Cloud DNS](./images/architecture.png)

In this mission, you will learn how to handle the scenarios described above for the SAP Launchpad service on SAP Business Technology Platform, which serves SAP Fiori Apps federated from SAP S/4HANA systems or alike. The same can be achieved for other SAP BTP services as well. In this scenario, you will leverage Google Cloud DNS to route requests to the SAP Launchpad service in different subaccounts in different regions based on the configurations, which can be priority-based, performance-based, weighted or geo-based.

## Challenge

- Manual and Automatic Failover for SAP Launchpad service(disaster recovery or regular SAP Launchpad service maintenance)
- Google Cloud's unique approach to Global VPC and Global Load Balancers automatically minimizes latency to users around the globe by onboarding end user traffic at their closest point of ingress to the high speed Google backbone. Traffic then rides the Google backbone to your applications.
- Load balancing between SAP Launchpad service tenants (increasing throughput of your tenant beyond scale-up capabilities)
  
## Outcome

A cloud native integration pattern that incorporates SAP BTP and Google Cloud to eliminate downtime, reduce global latency and increase throughput. The approach can be applied to other BTP services the same way. Check the [Further Reading Section](./README.md#furtherreading) for SAP Cloud Integration example.

## Solution

- Using your own domain for SAP Launchpd service using the SAP Custom Domain service
- Configuring Google Cloud DNS and different routing policies for the SAP Launchpad service

## Requirements

The required systems and components are:

- SAP BTP enterprise account
- 2 SAP BTP subaccounts: e.g. one in EU, one in US for example or where the ([SAP Launchpad service is available](https://discovery-center.cloud.sap/serviceCatalog/launchpad?region=all&tab=service_plan))
- Google Cloud account
- Your own domain
- 1 S/4HANA system and 1 Cloud connector to expose the Fiori apps from S/4HANA.

Entitlements/Quota required in your SAP Business Technology Platform Account:

| Service                     | Plan             | Number of instances |
| --------------------------- | ---------------- | ------------------- |
| Custom Domain Service       | Custom Domain    | 2                   |

Subscriptions required in your SAP Business Technology Platform Account:

| Subscription               | Plan                                                   |
| -------------------------- | ------------------------------------------------------ |
| Launchpad service          |  Standard (Application)                                |


## Setup and Configuration

[Step 1: Setup SAP Launchpad Service](./01-SetupLaunchpad/)

[Step 2: Configure S/4HANA system for Content Federation](./02-Configuring_S_4HANA_System_for_Content_Federation/)

[Step 3: Provisioning S/4HANA Apps to Launchpad Service](./03-Provisioning_S_4HANA_Apps_to_Launchpad_Service/)

[Step 4: Configure a Custom Domain with Cloud DNS](./04-Cloud_DNS_Configuration/)

[Step 5: Setup optional Monitoring and Alerting](./05-Setup-Cloud-DNS-Monitoring/)



## <a name="furtherreading"></a> Further Reading

Git Hub: [BTP Cloud Integration Intelligent Routing](https://github.com/SAP-samples/btp-cloud-integration-intelligent-routing)

Blogpost: [Architecting Solutions on SAP BTP for High Availability](https://blogs.sap.com/2021/08/17/architecting-solutions-on-sap-btp-for-high-availability/) by [Murali Shanmugham](https://people.sap.com/muralidaran.shanmugham2)

## Considerations
1. Having two SAP Launchpad services will impact the subscription costs.
2. Ensuring synchronization of apps, roles, etc., between the two Launchpad services.
3. SSO to be configured for the two subaccounts for achieving the seamless switch in failover scenarios.
4. Applications native to SAP BTP with DB access specific to the subaccount(e.g., CAP applications with HANA Cloud DB) have limitations and will not work directly. This works well with content federation scenarios like the example used in this step-by-step tutorial.
5. APIs for syncing the Personalization data for the Launchpad is not available currently.


## How to obtain support

[Create an issue](https://github.com/SAP-samples/btp-cloud-integration-intelligent-routing/issues) in this repository if you find a bug or have questions about the content.
 
For additional support, [ask a question in SAP Community](https://answers.sap.com/questions/ask.html).

## Contributing
If you wish to contribute code, offer fixes or improvements, please send a pull request. Due to legal reasons, contributors will be asked to accept a DCO when they create the first pull request to this project. This happens in an automated fashion during the submission process. SAP uses [the standard DCO text of the Linux Foundation](https://developercertificate.org/).

## License
Copyright (c) 2022 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.
