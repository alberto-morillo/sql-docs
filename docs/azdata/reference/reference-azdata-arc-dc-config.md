---
title: azdata arc dc config reference
titleSuffix: SQL Server big data clusters
description: Reference article for azdata arc dc config commands.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 04/06/2021
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
---

# azdata arc dc config

Applies to [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

The following article provides reference for the **sql** commands in the **azdata** tool. For more information about other **azdata** commands, see [azdata reference](reference-azdata.md)

## Commands

|Command|Description|
| --- | --- |
[azdata arc dc config init](#azdata-arc-dc-config-init) | Initializes a data controller configuration profile that can be used with control create.
[azdata arc dc config list](#azdata-arc-dc-config-list) | Lists available configuration profile choices.
[azdata arc dc config add](#azdata-arc-dc-config-add) | Add a value for a json path in a config file.
[azdata arc dc config remove](#azdata-arc-dc-config-remove) | Remove a value for a json path in a config file.
[azdata arc dc config replace](#azdata-arc-dc-config-replace) | Replace a value for a json path in a config file.
[azdata arc dc config patch](#azdata-arc-dc-config-patch) | Patches a config file based on a json patch file.
## azdata arc dc config init
Initializes a data controller configuration  profile that can be used with control create. The specific source of the configuration profile can be specified in the arguments.
```bash
azdata arc dc config init 
```
### Examples
Guided data controller config init experience - you will receive prompts for needed values.
```bash
azdata arc dc config init
```
arc dc config init with arguments, creates a configuration profile of aks-dev-test in ./custom.
```bash
azdata arc dc config init --source azure-arc-kubeadm --path custom
```
### Global Arguments
#### `--debug`
Increase logging verbosity to show all debug logs.
#### `--help -h`
Show this help message and exit.
#### `--output -o`
Output format.  Allowed values: json, jsonc, table, tsv.  Default: json.
#### `--query -q`
JMESPath query string. See [http://jmespath.org/](http://jmespath.org) for more information and examples.
#### `--verbose`
Increase logging verbosity. Use --debug for full debug logs.
## azdata arc dc config list
Lists available configuration profile choices for use in `arc dc config init`
```bash
azdata arc dc config list 
```
### Examples
Shows all available configuration profile names.
```bash
azdata arc dc config list
```
Shows json of a specific configuration profile.
```bash
azdata arc dc config list --config-profile aks-dev-test
```
### Global Arguments
#### `--debug`
Increase logging verbosity to show all debug logs.
#### `--help -h`
Show this help message and exit.
#### `--output -o`
Output format.  Allowed values: json, jsonc, table, tsv.  Default: json.
#### `--query -q`
JMESPath query string. See [http://jmespath.org/](http://jmespath.org) for more information and examples.
#### `--verbose`
Increase logging verbosity. Use --debug for full debug logs.
## azdata arc dc config add
Adds the value at the json path in the config file.  All examples below are given in Bash.  If using another command line, please be aware that you may need to escape quotations appropriately.  Alternatively, you may use the patch file functionality.
```bash
azdata arc dc config add 
```
### Examples
Ex 1 - Add data controller storage.
```bash
azdata arc dc config add --path custom/control.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### Global Arguments
#### `--debug`
Increase logging verbosity to show all debug logs.
#### `--help -h`
Show this help message and exit.
#### `--output -o`
Output format.  Allowed values: json, jsonc, table, tsv.  Default: json.
#### `--query -q`
JMESPath query string. See [http://jmespath.org/](http://jmespath.org) for more information and examples.
#### `--verbose`
Increase logging verbosity. Use --debug for full debug logs.
## azdata arc dc config remove
Removes the value at the json path in the config file.  All examples below are given in Bash.  If using another command line, please be aware that you may need to escape quotations appropriately.  Alternatively, you may use the patch file functionality.
```bash
azdata arc dc config remove 
```
### Examples
Ex 1 - Remove data controller storage.
```bash
azdata arc dc config remove --path custom/control.json --json-path ".spec.storage"
```
### Global Arguments
#### `--debug`
Increase logging verbosity to show all debug logs.
#### `--help -h`
Show this help message and exit.
#### `--output -o`
Output format.  Allowed values: json, jsonc, table, tsv.  Default: json.
#### `--query -q`
JMESPath query string. See [http://jmespath.org/](http://jmespath.org) for more information and examples.
#### `--verbose`
Increase logging verbosity. Use --debug for full debug logs.
## azdata arc dc config replace
Replaces the value at the json path in the config file.  All examples below are given in Bash.  If using another command line, please be aware that you may need to escape quotations appropriately.  Alternatively, you may use the patch file functionality.
```bash
azdata arc dc config replace 
```
### Examples
Ex 1 - Replace the port of a single endpoint (Data Controller Endpoint).
```bash
azdata arc dc config replace --path custom/control.json --json-values "$.spec.endpoints[?(@.name=="Controller")].port=30080"
```
Ex 2 - Replace data controller storage.
```bash
azdata arc dc config replace --path custom/control.json --json-values "spec.storage={"accessMode":"ReadWriteOnce","className":"managed-premium","size":"10Gi"}"
```
### Global Arguments
#### `--debug`
Increase logging verbosity to show all debug logs.
#### `--help -h`
Show this help message and exit.
#### `--output -o`
Output format.  Allowed values: json, jsonc, table, tsv.  Default: json.
#### `--query -q`
JMESPath query string. See [http://jmespath.org/](http://jmespath.org) for more information and examples.
#### `--verbose`
Increase logging verbosity. Use --debug for full debug logs.
## azdata arc dc config patch
Patches the config file according to the given patch file. Please consult http://jsonpatch.com/ for a better understanding of how the paths should be composed. The replace operation can use conditionals in its path due to the jsonpath library https://jsonpath.com/. All patch json files must start with a key of "patch" that has an array of patches with their corresponding op (add, replace, remove), path, and value. The "remove" op does not require a value, just a path. Please see the examples below.
```bash
azdata arc dc config patch 
```
### Examples
Ex 1 - Replace the port of a single endpoint (Data Controller Endpoint) with patch file.
```bash
azdata arc dc config patch --path custom/control.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":"$.spec.endpoints[?(@.name=="Controller")].port","value":30080}]}
```
Ex 2 - Replace data controller storage with patch file.
```bash
azdata arc dc config patch --path custom/control.json --patch ./patch.json

    Patch File Example (patch.json):
        {"patch":[{"op":"replace","path":".spec.storage","value":{"accessMode":"ReadWriteMany","className":"managed-premium","size":"10Gi"}}]}
```
### Global Arguments
#### `--debug`
Increase logging verbosity to show all debug logs.
#### `--help -h`
Show this help message and exit.
#### `--output -o`
Output format.  Allowed values: json, jsonc, table, tsv.  Default: json.
#### `--query -q`
JMESPath query string. See [http://jmespath.org/](http://jmespath.org) for more information and examples.
#### `--verbose`
Increase logging verbosity. Use --debug for full debug logs.

## Next steps

For more information about other **azdata** commands, see [azdata reference](reference-azdata.md). 

For more information about how to install the **azdata** tool, see [Install azdata](..\install\deploy-install-azdata.md).

