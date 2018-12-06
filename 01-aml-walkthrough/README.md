# Introduction to Azure Machine Learning service
The goal of this series of labs is to introduce core features of Azure Machine Learning service and demonstrate how AML service can be used to orchestrate machine learning workflows. The labs  walk you through the key phases of a machine learning workflow: from data preparation, through model training, to model operationalization.


## Lab environment set up

You can use your workstation or Azure Data Science Virtual Machine as your lab environment.

### To set up Azure Data Science Virtual Machine

1. Open Azure Cloud Shell (Bash)

2. Create `Resource Group` to host your virtual machine
```
az group create --name <YOUR-RESOURCE-GROUP-NAME> --location <YOUR-REGION>
```

3. Create Azure Ubuntu Data Science VM
```
# create a Ubuntu DSVM in your resource group
# note you need to be at least a contributor to the resource group in order to execute this command successfully
# If you need to create a new resource group use: "az group create --name YOUR-RESOURCE-GROUP-NAME --location YOUR-REGION (For example: westus2)"
az vm create --resource-group <YOUR-RESOURCE-GROUP-NAME> --name <YOUR-VM-NAME> --image microsoft-dsvm:linux-data-science-vm-ubuntu:linuxdsvmubuntu:latest --admin-username <YOUR-USERNAME> --admin-password <YOUR-PASSWORD>
```

3. Open Jupyter port on DSVM
```
az network nsg rule create \
--resource-group <YOUR-RESOURCE-GROUP-NAME> \
--nsg-name <YOUR-VM-NAME>NSG \
--name Jupyter \
--protocol tcp \
--priority 1010 \
--destination-port-range 8000

```

5. When your VM is ready log into it an update AML SDK. This step is a temporary workaround.
The next release of DSVM will include updated SDK.

```
# Logon to your VM
ssh <your username>@<vm ip address>

# Update SDK and install AML Widgets
sudo -i
conda activate py36 

# Update AML Python SDK
pip install --upgrade azureml-sdk[notebooks,automl,contrib]


```
6. Install the workshop's dependencies and clone the labs.
```
# Install h5py
conda install h5py

# Install tensorflow 1.10
# Azure DSVM has TensorFlow 1.12 pre-installed. AzureML Brainwave components which are used in the labs
# require 1.10 so we need to downgrade the default installation
pip install --upgrade tensorflow==1.10

# Clone the labs under the notebooks folder
cd notebooks
git clone https://github.com/jakazmie/AMLsLabs.git
exit
```

7. Use Chrome browser to connect to Jupyter Hub at `http://<your machine's IP address>:8000`. 
You may receive a warning that `Your connection is not private`. Ignore it and press on **ADVANCED** to proceed.

8. Use your username and password to log in to Jupyter and navigate to the lab's folder. You are ready to start the labs


**Important**. Make sure to set the kernel of each notebook in the lab to *Python 3.6 - AzureML*.




### To set up your workstation

1. Follow instructions below to install Anaconda for Python 3

https://www.anaconda.com/

2. Create a new conda environment

```
conda create -n <your env name> Python=3.6 anaconda

# On Linux or MacOs
source activate <your env name>

# On Windows 
activate <your env name>
```

3. Install Azure ML Python SDK
```
pip install --upgrade azureml-sdk[notebooks,automl,contrib]
```


4. Install TensorFlow. The labs require 1.10 version
```
pip install --upgrade tensorflow==1.10
# pip install --upgrade tensorflow-gpu==1.10
```

6. Clone this repo
```
git clone <repo URL>
```

7. Start Jupyter and enjoy
```
jupyter notebook
```










