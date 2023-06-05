---
layout: post
title: 🔧Sumologic - ngSIEM
subtitle: brief tool write-up
tags: [tracelay-tool-writeup]
odate: 09-01-2023
pdate: 10-03-2023
---
# Sumologic Tool 
> Problem Statement:
> 1. First task it to deploy the agent collector deployment is super easy in system once you follow steps.
> 2. Create a detailed report as per your understanding with screenshot with 3 page report.

### About the company
Sumo Logic, Inc. is a cloud-based machine data analytics company focusing on security, operations and Business Intelligence usecases. It provides log management and analytics services that use machine-generated big data.

Sumo Logic provides best-in-class cloud monitoring, log management, Cloud SIEM tools, and real-time insights for web and SaaS based apps.

### About the tool
Sumo Logic provide a next generation Security Information and Event Management tool for Log Management and analytical services solution that aggregates and analyzes all activities from different resources across entire IT infrastructure.

To enable the log collection for effective management and analytics, a collector is either installed or hosted on Sumo Logic cloud. 

For the activity done, an installed collector is utilised. An Installed Collector is a Java agent that receives logs and metrics from its Sources and then encrypts, compresses, and sends the data to the Sumo service. As its name implies, an Installed Collector is installed in your environment, as opposed to a Hosted Collector, which resides on the Sumo service. After installing a Collector, you add Sources, to which the Collector connects to obtain data to send to the Sumo service. 

A Sumo Source is an object configured for a specific Collector that sends data to Sumo Logic. There are a number of Source types that work with Installed Collectors.

Listed select few are as follows: AWS services (EC2, CloudFront, S3 audit, ELB), Microsoft IIS, Cisco ASA, DropWizard, Linux System, Windows Events, macOS system, MySQL, Nginx, etc.,

As shown in the diagram:

![](../../../assets/images/sumologic_tool_task2/sumologicselectdatatype.png)

Select Windows Events data type Collector gives a exe file to download which installs a collector. 

![](../../../assets/images/sumologic_tool_task2/sumologicsetup.png)

A collection setup part will appear where the given token must be copied to link data from system where collector is installed to retrive data from.

![](../../../assets/images/sumologic_tool_task2/setupcollection.png)

Configure source to all window events

![](../../../assets/images/sumologic_tool_task2/configuresource.png)

finishing the collector installation gives a dashboard where collected data is represented in an analytical cognitive manner.

![](../../../assets/images/sumologic_tool_task2/sumologicdashboard.png)

### Log Collection
Since while log collection, all categories was selected - one of the them being "OAlerts" - Windows Office 15 Alerts

While using Excel Application - there's an alert - while trying to delete charts geenrated from tables in the application.

The alert GUI prompt received:

![](../../../assets/images/sumologic_tool_task2/alert_2.png)

The prompted alert can be seen as recorded log in Sumologic:

![](../../../assets/images/sumologic_tool_task2/log.png)
