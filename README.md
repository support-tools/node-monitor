# Node Metrics - Must-Gather image

This repository is used to build an image for use with the OpenShift Must-Gather tool.
This container image deploys a DaemonSet within the cluster that will collect SAR and other Node Metrics.

The plan is to have the list of metrics configurable through arguments or environment variables, however at this stage the collection is defined in the `collect-metrics.sh` script.

# How to Use
Metrics collection tool is split into two parts, deploying and collecting.

## Deploying
To start retaining metrics for Nodes within the cluster, the 'deploy' option is used when running the image as below:
```bash 
$ oc adm must-gather --image quay.io/support-tools/node-monitor -- deploy
```

Adding one of the following labels to the desired Nodes will indicate to the tool which Nodes should be monitored with the respective script.
```bash 
$ oc label nodes/worker-0.dev-cluster.michael-washer.dev collect-node-metrics=""
$ oc label nodes/worker-1.dev-cluster.michael-washer.dev collect-monitor-sh=""
```

## Collecting the Metrics
To bundle and download the metrics from all labeled Nodes, the 'collect' option should be used as below:
```bash 
$ oc adm must-gather --image quay.io/support-tools/node-monitor -- collect
```

# Uninstall
To remove the metrics collectors the 'destroy' option should be used:
```bash 
$ oc adm must-gather --image quay.io/support-tools/node-monitor -- destroy
```
