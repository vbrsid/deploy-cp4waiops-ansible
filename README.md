# Deploy IBM Cloud Pak for Watson AIOps using Ansible

IBM Cloud Pak® for Watson AIOps (CP4WAIOps) is an AIOps platform that deploys advanced, explainable AI across the IT Operations (ITOps) toolchain so that you can confidently assess, diagnose, and resolve incidents across mission-critical workloads. You can find more information at in [CP4WAIOps Knowledge Center](https://www.ibm.com/docs/en/cloud-paks/cloud-pak-watson-aiops/3.2.0). 

This repository provides Ansible-way to deploy CP4WAIOps on an existing OpenShift Cluster. 

### 1. Pre-requisites
Please ensure that the following pre-requisites are met before executing the ansible scripts to deploy CP4WAIOps.

1. You need an ansible-controller machine from which the scripts are executed. This could be your laptop or a dedicated linux machine. This can only be a Mac or Linux machine and NOT Windows.
2. Install Python 3.10+ on the ansible-controller. Check the version with 'python --version'.
3. Install Ansible 2.12+ on the ansible-controller.Check the version with 'ansible --version'.
4. Ensure that the Python used by Ansible matches with the Python version on the ansible-controller.
5. Check the OpenShift sizing required for CP4WAIOps in the knowledge center. Preferred configuration would be 5 nodes of 16 core, 64 GB each. Setup OpenShift and ensure that it is reachable from ansible-controller.
6. Install 'oc' (OpenShift CLI) client on ansible-controller.
7. Login into OpenShift cluster using 'oc login' from the ansible-controller.
8. Install the kubernetes core collection for Ansible by running 'ansible-galaxy collection install kubernetes.core'.

**Notes**:
1. The scripts are tested with Python 3.10.1 and Ansible 2.12.1 on MacOS.
2. The scripts are work-in-progress and updated frequently.
3. The script is meant for setup of sandbox environment only on IBM ROKS (OpenShift on IBM Cloud) and not for production.


### 2. Run the scripts to deploy CP4WAIOps

You need to clone the repository on ansible-controller machine. 

Open 'deploy-cp4wa.yml' file and enter the right value for the variable 'ENTITLED_REGISTRY_PWD' and save the file (replace the 'put-your-entitlement-key-here' string with your key). You can obtain this key from [MyIBM Container Software Library](https://myibm.ibm.com/products-services/containerlibrary).

Run the following command to run the ansible script, which deploys CP4WAIOps. 

```
ansible-playbook deploy-cp4wa.yml
```
It would take about 2 hours for the installation to complete. Once the installation is completed, the URL to access the AIOps console and the 'admin' password to login are presented on the screen. Use them to access the console and checkout the features as described in [IBM CloudPak for Watson AIOps Knowledge Center](https://www.ibm.com/docs/en/cloud-paks/cloud-pak-watson-aiops/3.2.0). 

**Note**: if the script throws errors, re-run the script.

### 3. Uninstall Watson AIOps

At this point in time, there is a good shell script provided by IBM for uninstalling the CloudPak for Watson AIOps. The shell script is available in this repository as well. 

Switch to 'uninstall-sh-scripts' and run the following:

```
./uninstall-cp4waiops.sh
```

After the shell script is executed completely, CP4WAIOps is removed from the target OpenShift Cluster. You can remove the 'cp4waiops' namespace manually. If you want to install CP4WAIOps again, run the ansible script as mentioned in step 2. 