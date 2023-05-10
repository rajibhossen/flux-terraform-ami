# Flux Terraform AMI

Terraform module to create Amazon Machine Images (AMI) for Flux Framework HashiCorp Packer and AWS CodeBuild.
We are mirroring functionality from [GoogleCloudPlatform/scientific-computing-examples](https://github.com/GoogleCloudPlatform/scientific-computing-examples/tree/openmpi/fluxfw-gcp). Thank you Google, we love you!

## Usage

### Build Images with Packer

Let's first go into [build-images](build-images) to use packer to build our images.
You'll need to export your AWS credentials in the environment:

```bash
export AWS_ACCESS_KEY_ID=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
export AWS_SECRET_ACCESS_KEY=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

You'll need to first [install packer](https://developer.hashicorp.com/packer/downloads)
You can use the Makefile there to build all (or a select set of) images.

```bash
cd ./build-images
```
```bash
$ make
# or
$ make compute
$ make login    # not done yet
$ make manager  # not done yet
```

These are under development! My plan is to finish the base images, and then
figure out bringing them all up, and likely we will need a common metadata Api
for different sets of images to see one another, from a networking standpoint.
Stay tuned!


### Develoipment

Note that I found it helpful to test commands first before actually running it
automated! To connect to a new instance:

```bash
$ ssh -o 'IdentitiesOnly yes' -i "mykey.pem" rocky@ec2-xx-xxx-xx-xxx.compute-1.amazonaws.com
```
