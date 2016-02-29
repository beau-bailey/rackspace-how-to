---
node_id: 6001
title: Use enum metrics support
type: article
created_date: '2015-03-03'
created_by: Kyle Laffoon
last_modified_date: '2016-02-24'
last_modified_by: Kyle Laffoon
product: Rackspace Metrics
product_url: rackspace-metrics
---

### Use Enum Metrics Support

The enum metrics release will allow you to push state based metrics (enums) and get the report from API on the frequency of occurrence of the values. For example, a common report for the IT teams to provide the uptime report based on the occurrences of the response codes from the server, or the state of the alerts during a period of time. Enum support is a stepping stone by providing the data to be used in report or visualization.

#### Detailed Information

Many of our users want to be able to keep track of the number of times a particular string appears. The classic example is for state change messages/status code strings. As metrics are typically defined to be numbers, a metric system has no good way of tracking/displaying such values. The purpose of Enum Metrics is to provide a mechanism for doing so.

The same concepts of raw metrics data and roll-up management still apply with the same retention policy.  It is the just roll-ups are doing served in a way that applies to enum values:

Instead of calculating the min/max/average values that only apply to numeric values, the enum roll-ups will be calculated by counting the occurrence of each value.

Again, this is assuming that there is limited number of values. Violating that assumption can cause uncertain behavior from the system and would not be supported. Rackspace Metrics team will put monitoring in place to detect and catch cases where a metrics is containing too many values.

#### Ingesting Enum Data through API
For api commands and additional information on sending enum metrics, see [Sending enum metrics](https://developer.rackspace.com/docs/metrics/v2/developer-guide/#sending-enum-metrics) in the API documentation.

#### Retrieving Enum Data from API

For api command and additional information on retrieving enum metrics, see [Retrieving enum metrics](https://developer.rackspace.com/docs/metrics/v2/developer-guide/#retrieving-enum-metrics) in the API documentation.


### Enum Support in Search API

You can now retrieve the ingested enum values through glob search by adding the parameter "include\_enum\_values=true".

Note: there is a five minutes delay before any newly ingested enum\_values show up with glob searching

Applying the above example:

    curl -X GET 'https://global.metrics.api.rackspacecloud.com/v2.0/737305/metrics/search?query=example.*.*&include_enum_values=true'

Which will then return:
    [
    {
      "metric":"example.enums.value",
      "enum_values":["five","four","one","three","two"]
    },
    {
     "metric":"example.enums.alarm","enum_values":["CRITICAL","OK"]
    },
    {"metric":"example.enums.http","enum_values":["200","404","500"]}
    ]


### Grafana Support

The customer can use the existing Grafana support to visualize the enum data in the form of stacked percent bar chart.

The following are the screen shots of steps to create dashboard based on enum values. Engineer is working on fixes to make it easier. We will update it once that is done.

 1. Enter the metric name manually:

  ![](https://b9002618969a676fa5e9-329656694c46da9401f89a96a819e8df.ssl.cf5.rackcdn.com/rackspace-metrics/Enumsupport-manually.png)

 2. Click **Off** and the drop down option will appear:         

  ![](https://b9002618969a676fa5e9-329656694c46da9401f89a96a819e8df.ssl.cf5.rackcdn.com/rackspace-metrics/Enumsupport-click-off.png)

 3. Select a value:

  ![](https://b9002618969a676fa5e9-329656694c46da9401f89a96a819e8df.ssl.cf5.rackcdn.com/rackspace-metrics/Enumsupport-select-value.png)

 4. Click **duplicate** :

  ![](https://b9002618969a676fa5e9-329656694c46da9401f89a96a819e8df.ssl.cf5.rackcdn.com/rackspace-metrics/Enumsupport-clickduplicate.png)

 5. Select all values

  ![](https://b9002618969a676fa5e9-329656694c46da9401f89a96a819e8df.ssl.cf5.rackcdn.com/rackspace-metrics/Enumsupport-selectall.png)

 6. Change graph style to be bar chart, stack and 100%:

  ![](https://b9002618969a676fa5e9-329656694c46da9401f89a96a819e8df.ssl.cf5.rackcdn.com/rackspace-metrics/Enumsupport-graphstyle.png)


### FAQ

#### How many values are too many for an enum metric?

100

#### Where is the public documentation for this feature?

 - Ingest: [https://developer.rackspace.com/docs/metrics/v2/developer-guide/#send-aggregated-enum-metrics](https://developer.rackspace.com/docs/metrics/v2/developer-guide/#send-aggregated-enum-metrics)
 - Query: [https://developer.rackspace.com/docs/metrics/v2/developer-guide/#retrieve-an-aggregated-set-of-enum-metrics](https://developer.rackspace.com/docs/metrics/v2/developer-guide/#retrieve-an-aggregated-set-of-enum-metrics)
 - Grafana Support:  (To be Updated)

#### How can I learn more about Rackspace Metrics product?

 - Product Overview:  [http://bit.ly/rax-metrics-overview](http://bit.ly/rax-metrics-overview)
 - Getting Started: [https://developer.rackspace.com/docs/metrics/v2/developer-guide/#getting-started](https://developer.rackspace.com/docs/metrics/v2/developer-guide/#getting-started)
 - Grafana support article: [https://support.rackspace.com/how-to/create-a-grafana-dashboard-for-rackspace-metrics/](https://support.rackspace.com/how-to/create-a-grafana-dashboard-for-rackspace-metrics/)

#### How do I sign up an account for EAP?

Sign up at [https://developer.rackspace.com/docs/metrics/v2/developer-guide/#getting-started](https://developer.rackspace.com/docs/metrics/v2/developer-guide/#getting-started).