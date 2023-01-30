## AWS container insight with Fluent bit


[CloudwatchContainerInsights](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/ContainerInsights.html) is used to collect, aggregate, and summarize metrics and logs from your containerized applications and microservices. Container Insights is available for Amazon Elastic Container Service, Amazon Elastic Kubernetes Service, and Kubernetes platforms on Amazon EC2. The metrics include utilization for resources such as CPU, memory, disk, and network. Container Insights also provides diagnostic information, such as container restart failures, to help you isolate issues and resolve them quickly. You can also set CloudWatch alarms on metrics that Container Insights collects.

The metrics that Container Insights collects are available in CloudWatch automatic dashboards. You can analyze and troubleshoot container performance and logs data with CloudWatch Logs Insights. 

## Helm Does,

This helm is based on AWS blog to extract logs. Since there is no concrete steps in helm i wrote this. [Blog](https://aws.amazon.com/premiumsupport/knowledge-center/cloudwatch-stream-container-logs-eks/)

## Prerequisites

Kubernetes 1.4+:

* the fluent bit Agent supports Kubernetes 1.4+
* The fluent bit Agent chart's defaults are tailored to Kubernetes 1.7.6+

## Quick start

By default, the Container Insight Agent runs in a DaemonSet. It can alternatively run inside a Deployment for special use cases.

**Note:** simultaneous DaemonSet + Deployment installation within a single release will be deprecated in a future version, requiring two releases to achieve this.


## Installing
First add Helm repo to Helm
```console
$ helm repo add custom https://anupash147.github.io/helm-charts/
$ helm repo update
```

Create values.yaml file with the parameters specified  

Run Helm command:  
```console
$ helm install nginx-headless custom/aws-container-insight-fluent-bit --set cluster.name=<MyEksClusterName> -f myValues.yaml --version 0.1.0
```
## Configuration
The following table, lists the configurable parameters.

Parameter | Description                                                                                                                                                                                                                                                                                    | Example
--- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| ---
**[Required]** |
`cluster.name` | Sets the cluster name to sync the logs to cloudwatch                                                                                                                                                                                                                                                                 | 
**[Optional]**
`http.port` | Default fluent-bit port to poll to                                                                                                                                                                                                                                | `2020`
`http.server` | Default server value                                                                                                                                                                                                                                | `On`
`logs.region` | Provide the aws-region, this is the default installation region                                                                                                                                                                                                                               | `us-east-2`
`logs.readhead` | Read the logs from, adviced to keep this off                                                                                                                                                                                                                                | `Off`
`logs.readtail` | Read the logs from, adviced to keep this on                                                                                                                                                                                                                               | `On`
`image.repository` | The image repository to pull from                                                                                                                                                                                                                                | `amazon/aws-for-fluent-bit`
`image.pullPolicy` | Image pull policy | `"IfNotPresent"` 
`image.tag` | The image tag to pull | `"latest"` 
`imagePullSecrets` | Image pull secrets | `[]` 
`fullnameOverride` | Override the default name | `""` 
`nameOverride` | Just the name override | `""` 
`nodeSelector` | Node selectors | `{}`
`resources` | Specify the resource limits | limits:<br> &nbsp;&emsp; memory: 200Mi <br>requests: <br> &emsp; cpu: 500m <br> &emsp; memory: 100Mi
`securityContext` | Allows you to overwrite the default securityContext applied to the container | `{}` 
`serviceAccount.annotations` | Annotations to add to the Service account | `{}` 
`serviceAccount.create` | If true, create & use serviceAccoun | `true`
`serviceAccount.name` | If not set & create is true, use template fullname | `""` 
`tolerations` | List of node taints to tolerate (requires Kubernetes >= 1.6) | - key: node-role.kubernetes.io/master <br> &emsp; operator: Exists <br> &emsp; effect: NoSchedule <br> - operator: "Exists" <br> &emsp; effect: "NoExecute" <br> - operator: "Exists" <br> &emsp;  effect: "NoSchedule" 
`affinity` | Node affinities | avoid running pods on the same node








## Releases

0.1.0 - Initial Release
