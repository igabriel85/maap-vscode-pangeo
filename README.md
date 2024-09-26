# MAAP VSCode Pangeo

This repository contains the Dockerfile and associated files for building a Docker container for the MAAP Pangeo Eclipse Che workspace.
It is based on the [Pangeo Docker image](https://github.com/pangeo-data/pangeo-docker-images) used in [Pangeo Cloud](https://pangeo.io/cloud.html).

# Adding workspace to Eclipse Che

## Manual
Eclipse Che only requires a valid devfile to create a workspace. The devfile for the MAAP Eclipse Che workspace is located in this repository. Thus, we can just specify
the URL of this repository in  Eclipse Che workspace creation textbox.

## Kubernetes ConfigMap
Alternatively, if we have administrator access to Eclipse Che, we can add the workspace to the list of available workspaces in the `getting-started-sample` Kubernetes configmap. We can use `kubectl` as follows:

```bash
kubectl create configmap getting-started-samples --from-file=full_test.json -n eclipse-che
```

```bash
kubectl label configmap getting-started-samples app.kubernetes.io/part-of=che.eclipse.org app.kubernetes.io/component=getting-started-samples -n eclipse-che
```

Please note that some of the commands above may require administrator access to the Kubernetes cluster and the Eclipse Che namespace.

An example of the `maap_sample.json` file is provided in this repository. The file contains the following information:
```json
[
  {
    "displayName": "MAAP Pangeo Notebook",
    "description": "MAAP Pangeo based workspace",
    "tags": "maap, pangeo, python 3.12.5",
    "url": "https://gitlab.dev.info.uvt.ro/sage/maap/maap-vscode-pangeo",
    "icon": {
      "base64data": "<base64_encoded_data>",
      "mediatype": "image/png"
    }
  }
]
```
For custom icons, we must convert the image data into base64 encoding. We can use online tools such as [base64-image.de](https://www.base64-image.de/) to convert the image data to base64 encoding.


