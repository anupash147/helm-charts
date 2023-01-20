# Service Helm Chart
Deploys a headless service


## Installing
First add Helm repo to Helm
```console
$ helm repo add custom https://anupash147.github.io/helm-charts/
$ helm repo update
```

Create values.yaml file with the parameters specified  

Run Helm command:  
```console
$ helm install nginx-headless custom/ingress-headless-service -f myValues.yaml --version 0.1.0
```
## Configuration
The following table, lists the configurable parameters.

Parameter | Description                                                                                                                                                                                                                                                                                    | Example
--- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| ---
**[Service](#adding-service)** |
`namespace` | Set Namespace                                                                                                                                                                                                                                                                 | `kube-system`
`selectorApp` | App that will reference this headless service                                                                                                                                                                                                                               | `ingress-controller-nginx`

## Releases

0.1.0 - Initial Release
