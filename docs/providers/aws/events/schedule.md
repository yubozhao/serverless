<!--
title: Serverless Framework - AWS Lambda Events - Scheduled & Recurring
menuText: Schedule
menuOrder: 4
description: Setting up Scheduled, Recurring, CRON Task Events with AWS Lambda via the Serverless Framework
layout: Doc
-->

<!-- DOCS-SITE-LINK:START automatically generated  -->
### [Read this on the main serverless docs site](https://www.serverless.com/framework/docs/providers/aws/events/schedule)
<!-- DOCS-SITE-LINK:END -->

# Schedule

The following config will attach a schedule event and causes the function `crawl` to be called every 2 hours. The configuration allows you to attach multiple schedules to the same function. You can either use the `rate` or `cron` syntax. Take a look at the [AWS schedule syntax documentation](http://docs.aws.amazon.com/AmazonCloudWatch/latest/events/ScheduledEvents.html) for more details.


```yaml
# Unit of the rate must be singular.

functions:
  crawl:
    handler: crawl
    events:
      - schedule: rate(2 hour)
      - schedule: cron(0 12 * * ? *)
```

## Enabling/Disabling functions

This will create and attach a schedule event for the `aggregate` function which is disabled. If enabled it will call
the `aggregate` function every 10 minutes.

```yaml
functions:
  aggregate:
    handler: statistics.handler
    events:
      - schedule:
          rate: rate(10 minute)
          enabled: false
          input:
            key1: value1
            key2: value2
            stageParams:
              stage: dev
      - schedule:
          rate: cron(0 12 * * ? *)
          enabled: false
          inputPath: '$.stageVariables'
```
