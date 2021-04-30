# crc-clusterlog-forwarding
Setup of CRC instance with CLF to a splunk instance using fluentd


1. Start CRC with correct config:
 
```
3. # - consent-telemetry                     : no
4. # - cpus                                  : 6
5. # - disk-size                             : 100
6. # - enable-cluster-monitoring             : true
7. # - memory                                : 20500
8. # - pull-secret-file                      : /home/evroon/Devoteam/SVB/ClusterLoggingSetup/pull-secret.txt
crc start
```

2. Setup cluster logging:
https://docs.openshift.com/container-platform/4.7/logging/cluster-logging-deploying.html#cluster-logging-deploy-console_cluster-logging-deploying
See files in dir cluster-logging-files/ 

- Create namespaces for elasticsearch operator
- Create namespaces for Cluster Logging Operator
- Install Elasticsearch Operator by creating:
  - Operator Group object
  - Subscription object
- Install Cluster Logging Operator by creating:
  - Operator Group object
  - Subscription object
- Create an Openshift Logging instance


3. Setup Cluster Log Forwarder w/ helm chart
 
- Follow steps from blog: https://www.openshift.com/blog/forwarding-logs-to-splunk-using-the-openshift-log-forwarding-api
- To use a namespace other than `openshift-logging` works, you have to recreate the secret that helm creates in the `openshift-logging` namespaces. Otherwise, the CLF can't reach the forwarder pods.

4. Make changes to CLF pipelines / inputs / outputs

See files in dir cluster-logforwarder/ for example

6. Demo queries in Splunk

- Find route: `echo https://$(oc get routes -n splunk splunk -o jsonpath='{.spec.host}')`




