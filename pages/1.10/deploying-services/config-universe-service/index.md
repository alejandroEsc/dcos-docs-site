---
layout: layout.pug
navigationTitle:  Configuring Universe Services
title: Configuring Universe Services
menuWeight: 2
excerpt:

enterprise: false
---

<!-- This source repo for this topic is https://github.com/dcos/dcos-docs -->


Each Universe service installs with a set of default parameters. You can discover the default parameters and change them as desired.

This topic describes how to use the DC/OS CLI to configure services. You can also customize services by using the [**Services**](/1.10/gui/services/) tab in the DC/OS UI. 

1. View the available configuration options for the service with the `dcos package describe --config <package-name>` command.

    ```bash
    dcos package describe --config marathon
    ```

    The output should be something like:
    
    ```json
    {
    ...
      "service": {
        "additionalProperties": false,
        "description": "Marathon app configuration properties.",
        "properties": {
          "cpus": {
            "default": 2,
            "description": "CPU shares to allocate to each Marathon instance.",
            "minimum": 0,
            "type": "number"
          },
          ...
          "instances": {
            "default": 1,
            "description": "Number of Marathon instances to run.",
            "minimum": 0,
            "type": "integer"
          },
          "mem": {
            "default": 1536,
            "description": "Memory (MB) to allocate to each Marathon instance.",
            "minimum": 512,
            "type": "number"
          }
        },
        ...
      }
    }
    ```

2.  Create a JSON configuration file. You can choose an arbitrary name, but you might want to choose a pattern like `<package-name>-config.json`. For example, `marathon-config.json`.

    ```bash
    nano marathon-config.json
    ```

3.  Use the `properties` objects to build your JSON options file. For example, to change the number of Marathon CPU shares to 3 and memory allocation to 2048:

    ```json
    {
      "application": {
        "cpus": 3.0, "mem": 2048.0
       }
    }
    ```

4.  From the DC/OS CLI, install the DC/OS service with the custom options file specified:

    ```bash
    dcos package install --options=marathon-config.json marathon
    ```

For more information, see the [dcos package](/1.10/cli/command-reference/dcos-package) documentation.
