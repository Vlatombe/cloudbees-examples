## Datadog

This folder includes:
* `jenkins.yaml` The datadog agent integration file. Specifies what JMX metrics to be imported and maps them to Datadog metrics. Please refer to CloudBees Core documentation 
* `dashboard.json` An example of Datadog dashboard for a CloudBees Core installation on AWS EC2. Can be imported by following the procedure described below

### Import dashboard

The provided `dashbard.json` must first be modified to fit your needs.

* Replace `CLUSTERNAME` with your actual cluster name. All your EC2 resources are tagged with `KubernetesCluster=CLUSTERNAME`.
* Some widgets refer to autoscaling groups, you may need to update the name `autoscaling_group:nodes.CLUSTERNAME` to fit your configuration.

To import the dashboard, you must get your api key and your app key from datadog then provide them in the following script

```
export api_key=xxxx
export app_key=yyyy
curl -X POST -H "Content-type: application/json" -d @dashboard.json "https://app.datadoghq.com/api/v1/dash?api_key=${api_key}&application_key=${app_key}"
```

Then your dashboard will be available in Datadog.