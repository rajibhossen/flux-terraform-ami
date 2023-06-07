# Currently Under Construction

# Instructions
Assumes you already have the image from the main instructions [../../README.md](README.md) 
And then init and build:

```bash
$ make init
$ make fmt
$ make validate
$ make build
```

Or they all can be run with `make`:

```bash
$ make
```

You can then shell into any node, and check the status of K3S.

```bash
$ ssh -o 'IdentitiesOnly yes' -i "mykey.pem" rocky@ec2-xx-xxx-xx-xxx.compute-1.amazonaws.com
```

Check the cluster status, the overlay status, and try running a job:

```bash
$ kubectl get nodes
```

You can look at the startup script logs like this if you need to debug.
```bash
$ cat /var/log/cloud-init-output.log
```

That's it. Enjoy!

## Developer

### AMIs

The following AMIs have been used at some point in this project:

  - `ami-0ff535566e7c13e8c`: current AMI, modified to have cgroups version 2 
  - `ami-02eac56446a475861`: original AMI, early 2023 (March-May) without cgroups 2

### Credentials

The best practice approach for giving the instances ability to list images (and get the hostnames)
is with an IAM role. However, we used a previous approach to add credentials (scoped) directly to
the environment in the startscript. That looked like this:

```
Since we want to get hosts on the instance using the aws client, export your credentials to the environment
for the instances:

```bash
export TF_VAR_aws_secret=$AWS_SECRET_ACCESS_KEY 
export TF_VAR_aws_key=$AWS_ACCESS_KEY_ID 
export TF_VAR_aws_session=$AWS_SESSION_TOKEN 
```

Thanks [Vsoch](https://github.com/vsoch)