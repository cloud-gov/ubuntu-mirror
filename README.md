# Ubuntu Mirror

Mirror a subset of Ubuntu images to our private registry.

The container build jobs in [common-pipelines/container](https://github.com/cloud-gov/common-pipelines/tree/main/container) are all configured to pull their base image from ECR. This is fine for almost all pipelines because they are based on a hardened base image that we push to ECR. The sole exception is [ubuntu-hardened](https://github.com/cloud-gov/ubuntu-hardened), which is based on the public `ubuntu` image made available in Docker Hub.

The base image resource in the common container pipeline cannot be made configurable without every user of the pipeline providing configuration for their base image registry. This would require more work by every pipeline user, when in practice they will all be based on the same base image, with the exception of the base image itself. To work around this, the `ubuntu-mirror` repository and the corresponding pipeline pull `ubuntu` from Docker Hub and push it to ECR, where it can later be used by `ubuntu-hardened`. Because of this, `ubuntu-hardened` can use the same common pipeline as every other repository.
