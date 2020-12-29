# iot-plugandplay-models

## `dmr-client` Tool

The tools used to validate the models during the PR checks can also be used to add and validate the DTDL interfaces locally.

> Note: These tools require the [.NET SDK](https://dotnet.microsoft.com/download) (3.1 or greater)

### Install `dmr-client`

#### Linux/Bash

```bash
curl -L https://aka.ms/install-dmr-client-linux | bash
```

#### Windows/Powershell

```powershell
iwr https://aka.ms/install-dmr-client-windows -UseBasicParsing | iex
```

### Import a Model to the `dtmi/` folder

If you have your model already stored in json files, you can use the `dmr-client import` command to add those to the `dtmi/` folder with the right file name.

```bash
# from the local repo root folder
dmr-client import --model-file "MyThermostat.json"
```

>Note: You can use the `--local-repo` argument to specify the local repo root folder

### Validate Models

You can validate your models with the `dmr-client validate` command.

```bash
dmr-client validate --model-file ./my/model/file.json
```

>Note: The validation uses the latest DTDL parser version to ensure all the interfaces are compatible with the DTDL language spec

To validate external dependencies, those must exist in the local repo. To validate those you can specify a `local` or `remote` folder to validate against.

```bash
# from the repo root folder
dmr-client validate --model-file ./my/model/file.json --repo .
```

#### Strict validation

The Device Model Repo includes additional [requirements](pr-reqs.md), these can be validated with the `strict` flag.

```bash
dmr-client validate --model-file ./my/model/file.json --repo . --strict true
```

#### Export models

Models can be exported from a given repo (local or remote) to a single file using a JSON Array. 

```bash
dmr-client export --dtmi "dtmi:com:example:TemperatureController;1" -o TemperatureController.expanded.json
```

## Consuming

Any HTTP client can consume the models by just applying the [convention](https://github.com/Azure/iot-plugandplay-models-tools/wiki/Resolution-Convention) to translate *DTMI ids* to relative paths:

Eg, the interface:

```cmd
dtmi:azure:DeviceManagement:DeviceInformation;1
```

can be retrieved from [here](https://devicemodels.azure.com/dtmi/azure/devicemanagement/deviceinformation-1.json):

```cmd
https://devicemodels.azure.com/dtmi/azure/devicemanagement/deviceinformation-1.json
```
