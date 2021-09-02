# Getting Started with MongoDB Atlas and Terraform

This repository contains the source code and the instructions that are required to successfully deploy a basic [Replica Set Cluster](https://docs.atlas.mongodb.com/view-replica-set-metrics/) in [MongoDB](https://www.mongodb.com/what-is-mongodb) using [Terraform](https://www.terraform.io/).

The purpose of this guide is to serve as a template for developers who would like to develop and deploy their own Atlas Clusters.

> Note: This guide is for Windows users **only**.

## **Step 1: Preparing the Development Environment**
- Install [VS Code](https://code.visualstudio.com/download).
- Install [MongoDB extension for VS Code](https://marketplace.visualstudio.com/items?itemName=mongodb.mongodb-vscode).
- Install [Terraform extension for VS Code](https://marketplace.visualstudio.com/items?itemName=HashiCorp.terraform). 

Although not strictly necessary, the Terraform extension for VS Code greatly enhances the user experience by adding syntax highlighting and autocompletion.

## **Step 2: Installing Terraform**
The most straightforward way to install Terraform is by using [Chocolatey](https://chocolatey.org/), the free and open-source package management system.

Firstly, make sure that you are using an *administrative shell*. With PowerShell, you must ensure that [Get-ExecutionPolicy](https://docs.microsoft.com/en-gb/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.1) is not restricted. 

Run `Get-ExecutionPolicy`. If it returns `Restricted`, then run `Set-ExecutionPolicy AllSigned`.

Now you can install Chocolatey by running the following:
```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

After completion, verify the installation by running `choco`.

With that done simply run `choco install terraform` and verify the installation afterwards, by typing `terraform --help`.

## **Step 3: Creating an Atlas Account and Generating API Keys**

Firstly create [Atlas account](https://account.mongodb.com/account/register?tck=docs_atlas), then create an **Atlas Organisation** within it. Once that is done navigate into the **Access Manager** bar in the **Organizations Menu** and click **Generate API Key**. Enter a description and ensure that the the *Organization Owner* or *Organization Project Creator* role is selected.

After that copy and save your **Public** and **Private API Key**, paying extra attention to the **Private Key** which will only be shown **once**.

Finally click **Add Access List Entry**. Enter an IP address from which you want Atlas to accept API requests for the API Key that you have just generated.
It is also possible to click **Use Current IP Address** if the host you are using to access Atlas also will make API requests using this API Key.



## **Step 4: Adding Configuration Data to Terraform**
After opening the project folder in VS Code, create a new file within that folder named `terraform.tfvars` and paste the following configuration data in it:

```
org_id = "value"
project_name = "value"
cluster_name = "value"
cloud_provider = "value"
region = "value"
mongodbversion = "value"
dbuser = "value"
dbuser_password = "value"
database_name = "value"
ip_address = "value"
```
Fill in your data according to the table below:

| Attribure            | Description              |
| ---------            | -----                    |
| `org_id`             | MongoDB Organization ID. |
| `project_name`       | The MongoDB Atlas Project Name. |
| `cluster_name`       | The MongoDB Atlas Cluster Name. |
| `cloud_provider`     | The cloud provider to use, must be either [AWS](https://aws.amazon.com/), [GCP](https://cloud.google.com/gcp?utm_source=google&utm_medium=cpc&utm_campaign=emea-gr-all-en-bkws-all-all-trial-e-gcp-1010042&utm_content=text-ad-none-any-DEV_c-CRE_501834844532-ADGP_Hybrid%20%7C%20BKWS%20-%20EXA%20%7C%20Txt%20~%20GCP%20~%20General%23v2-KWID_43700061559683581-aud-606988878174%3Akwd-26415313501-userloc_9067712&utm_term=KW_google%20cloud%20platform-NET_g-PLAC_&gclid=CjwKCAjw95yJBhAgEiwAmRrutHnCPQ6lMfRLvEI2oD8uu7rT8xwiiPtyMpJrBszsWJnDT4_rn64D6RoCdt8QAvD_BwE&gclsrc=aw.ds) or [AZURE](https://azure.microsoft.com/en-us/). |   
| `region`             | MongoDB Atlas Cluster Region, must be a region that is supported by the chosen cloud provider. | 
| `mongodbversion`     | The Major MongoDB Version. |
| `dbuser`             | MongoDB Atlas Database User Name. |
| `dbuser_password`    | MongoDB Atlas Database User Password. |
| `database_name`      | The database in the cluster to limit the database user to, the database does not have to exist yet. |
| `ip_address`         | The IP address that the cluster will be accessed from. |

## **Step 5: Deployment**
Initialise Terraform by opening  a terminal in VS Code and running `terraform init`.

Run `terraform plan` and type in the **Public** and **Private API Key** that you have saved earlier to see a summary of all the configuration settings.

Check if everything is good, then run `terraform apply`, enter your API keys and type **yes** when prompted. Once it's done loading it should display a **Connection String** that you will need in order to connect to your cluster, so hang onto it. And that's it! 

All you need to do in order to connect to your cluster now is paste the **Connection String** that you have saved, into the terminal and enter your user credentials that were defined earlier when prompted to do so.

## **Resources & Going Further**
- The [MongoDB University](https://university.mongodb.com/) is an excellent platform to learn about pretty much everything there is to know about MongoDB and it is completely free.

- There's plenty of information on the [MongoDB Atlas Documentation Page](https://docs.atlas.mongodb.com/) about how to use, monitor and manage your database.

- You can also check out their [Github Page](https://github.com/mongodb) for source codes, drivers and examples.


Shield: [![CC BY-NC-SA 4.0][cc-by-nc-sa-shield]][cc-by-nc-sa]

This work is licensed under a
[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[![CC BY-NC-SA 4.0][cc-by-nc-sa-image]][cc-by-nc-sa]

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
[cc-by-nc-sa-image]: https://licensebuttons.net/l/by-nc-sa/4.0/88x31.png
[cc-by-nc-sa-shield]: https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg
