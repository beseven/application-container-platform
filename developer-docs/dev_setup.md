# Developer Getting Started

## Pre-requisites
You should already have access to:

* Github, with membership of the UKHomeOffice org. This also grants access to:
* ukhomeofficedigital quay (login with your github account)
* Artifactory (login with Office 365)

## Introduction
This guide is aimed at developers that want to start using the platform to host their application.
You will need to:

1. [Request Access to the VPN and kubernetes](#requesting-access)
2. [Install the kubectl client](http://kubernetes.io/docs/user-guide/prereqs/)
3. [Configure your kubectl client](#configure-the-kubectl-client)
4. [Test your setup](#testing-the-setup)

## Requesting Access
To connect to the platform you will need 2 accounts:

1. VPN access via Office 365
2. Kubernetes access token

Please request access by adding an issue to the Platform Access column [here](https://github.com/UKHomeOffice/hosting-platform-bau/projects/1).

Please use the below template for your request

```
Please can I have VPN access for DSP Platform Dev, CI, Ops, and a kubernetes token with access to my teams namespaces.  
Email: xxx.xxx@digital.homeoffice.gov.uk  
Name: xxx xxx  
Team: My Project Team  
Public GPG Key: xxxxxxxxx
Namespace: dev-induction
```
You need to provide your public gpg key as the kube token you receive back will be encrypted using it. If you need to, you can [generate a gpg key](https://help.github.com/articles/generating-a-new-gpg-key/)

## Configure the kubectl client
You will need to configure the kubectl client with the appropriate details.
We recommend copying the [example kubectl config](resources/kubeconfig) to ~/.kube/config. Note that you may need to create this directory and file.

The only change you will need to make is to replace "XXXXXXXXXX" with your kubernetes token.

## Connect to the VPN
Once you've been given access to the DSP Platform VPN you can now navigate to https://authd.digital.homeoffice.gov.uk and login with your Office 365 account by clicking on the 365 link on the right.

Once you're logged in please download the VPN profile called 'DSP Platform Dev, CI, Ops' from under VPN Profiles.

If you're using a Mac you can download and install [Tunnelblick](https://tunnelblick.net/) and you should be able to double click the VPN profile you've downloaded and it will automatically be added to Tunnelblick, and you should then be able to connect to the VPN using the UI.
If you're not on a Mac you can use the command
```bash
sudo openvpn <vpn_profile_file>
```
You'll need to download and connect to a new VPN Profile every 12 hours.

## Testing the setup
Run:
```bash
kubectl get pods
```
You should get an empty reply with just some column headers. The config file by default looks only at the *dev-induction* namespace. 
To look at other namespace you can, for example do:
```bash
kubectl --namespace=my-namespace get pods 
```
You can also edit your kubernetes config, either by editing the file directly or by running:
```
kubectl config
```