# Grafana LLM Plugin

    Reference Documentation:
    https://grafana.com/docs/grafana-cloud/machine-learning/llm/

# 1. Enable Pyroscope for profiling in Grafana

Grafana Alloy automates Java process discovery for profiling, streamlining the setup for applications. It enables precise and targeted profiling configurations through the Grafana Alloy settings.

Java profiling via Grafana Alloy is based on a few components:
- `discovery.process` for process discovery
- `discovery.kubernetes` for adding Kubernetes labels (namespace, pod, and more)
- `discovery.relabel` for detecting java processes and setting up labels
- `pyroscope.java` for enabling profiling for specific applications
- `pyroscope.write` for writing the profiles data to a remote endpoint


### async-profiler

The `pyroscope.java` component internally uses the [async-profiler](https://github.com/async-profiler/async-profiler) library.
This approach offers a key advantage over other instrumentation mechanisms in that you can profile applications that are already running without interruptions (code changes, config changes or restarts).

Under the hood, this is achieved by attaching to the application at a process level and issuing commands to control profiling.

# 2. Getting started

To use this example:

1. Create a `pyroscope-java` namespace:
    ```shell
        kubectl create namespace pyroscope-java
    ```
2. Deploy the manifests:
    ```shell
       kubectl apply -n pyroscope-java -f .
    ```

After the deployment is operational, the Grafana Alloy will profile the Java application using the defined configuration.
The example will deploy a Grafana instance in the same cluster, available via the `grafana` service at port 3000.
