---
canonical: https://grafana.com/docs/alloy/latest/get-started/install/docker/
description: Learn how to install Grafana Alloy on Docker
menuTitle: Docker
title: Run Grafana Alloy in a Docker container
weight: 100
---

# Run {{% param "PRODUCT_NAME" %}} in a Docker container

{{< param "PRODUCT_NAME" >}} is available as a Docker container image on the following platforms:

* [Linux containers][] for AMD64 and ARM64.
* [Windows containers][] for AMD64.

## Before you begin

* Install [Docker][] on your computer.
* Create and save a {{< param "PRODUCT_NAME" >}} River configuration file on your computer, for example:

  ```river
  logging {
    level  = "info"
    format = "logfmt"
  }
  ```

## Run a Linux Docker container

To run {{< param "PRODUCT_NAME" >}} as a Linux Docker container, run the following command in a terminal window:

```shell
docker run \
  -v <CONFIG_FILE_PATH>:/etc/alloy/config.river \
  -p 12345:12345 \
  grafana/alloy:latest \
    run --server.http.listen-addr=0.0.0.0:12345 /etc/alloy/config.river
```

Replace the following:

- _`<CONFIG_FILE_PATH>`_: The path of the configuration file on your host system.

You can modify the last line to change the arguments passed to the {{< param "PRODUCT_NAME" >}} binary.
Refer to the documentation for [run][] for more information about the options available to the `run` command.

{{< admonition type="note" >}}
Make sure you pass `--server.http.listen-addr=0.0.0.0:12345` as an argument as shown in the example above.
If you don't pass this argument, the [debugging UI][UI] won't be available outside of the Docker container.
{{< /admonition >}}

## Run a Windows Docker container

To run {{< param "PRODUCT_NAME" >}} as a Windows Docker container, run the following command in a terminal window:

```shell
docker run \
  -v <CONFIG_FILE_PATH>:C:\etc\grafana-alloy\config.river \
  -p 12345:12345 \
  grafana/alloy:latest-windows \
    run --server.http.listen-addr=0.0.0.0:12345 C:\etc\grafana-alloy\config.river
```

Replace the following:

- _`<CONFIG_FILE_PATH>`_: The path of the configuration file on your host system.

You can modify the last line to change the arguments passed to the {{< param "PRODUCT_NAME" >}} binary.
Refer to the documentation for [run][] for more information about the options available to the `run` command.

{{< admonition type="note" >}}
Make sure you pass `--server.http.listen-addr=0.0.0.0:12345` as an argument as shown in the example above.
If you don't pass this argument, the [debugging UI][UI] won't be available outside of the Docker container.
{{< /admonition >}}

## Verify

To verify that {{< param "PRODUCT_NAME" >}} is running successfully, navigate to <http://localhost:12345> and make sure the {{< param "PRODUCT_NAME" >}} [UI][] loads without error.

[Linux containers]: #run-a-linux-docker-container
[Windows containers]: #run-a-windows-docker-container
[Docker]: https://docker.io
[run]: ../../../reference/cli/run/
[UI]: ../../../tasks/debug/#grafana-alloy-ui