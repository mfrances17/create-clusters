# create-clusters

The first time installing a cluster with this script, you need to create an install-config file. Download the installer from [here](https://mirror.openshift.com/pub/openshift-v4/clients/ocp-dev-preview/latest-4.10/) and run the command:

```
$ openshift-install create install-config
```

## Creating a cluster

You can create a cluster by running `./create-cluster`. The cluster created lasts about 10 hours. It is
named based on the user creating the cluster, version, options, and the time of creation. The script will
scale up the machine sets for the cluster to 2 each. Upon cluster creation, the server information will be shown.
This information includes the server version, URL to the cluster console, username and password, and command line
login command. 

The install files and eventually the `kubeconfig` and `kubeadmin-password` files will be created/copied to `~/clusters/<...>`
based on the options supplied (`cluster-manual` if none, `cluster-manual-<version>`, etc).

There are a variety of options you can apply:

#### -v | --version < version number >
creates the latest nightly update for the given version number

ex. `-v 4.9`

#### -n | --name < string >
names the cluster as specified. Be sure not to use URL reserved characters such as `/`

ex. `-n my-new-cluster`

#### -s | --save
Does not remove the previous cluster created (based on version or `special`). Use only if you need to prevent the previous from being destroyed (ie. still in use).

ex. `-s`

#### -l | --late
Create another version of a cluster that may already be created, just named differently. Useful when you want a duplicate cluster of one that is already running and still in use.

ex. `-l`

#### --special
Create a cluster with a specified version. That version is specified in the script. Someday it should be a parameter ;)

ex. `--special`


## For ease of login:

Run the `update-kubeconfig` script with the same arguments used for `create-cluster` to copy the `kubeconfig` and `kubeadmin-password` files to a `KUBECONFIG_DIR`

Run the `login-kubeadmin` script to login to the cluster whose credentials are in the `KUBECONFIG_DIR`
