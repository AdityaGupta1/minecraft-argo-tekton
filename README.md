# Minecraft with Argo CD and Tekton CD

This repository shows how to use [Tekton CD](https://tekton.dev/) to change and sync an (Argo CD)[https://argoproj.github.io/argo-cd/] application running a Minecraft server from a Helm chart.

## Setup

1. Fork or copy this repository.
  - Argo CD applications use Git repositories as sources of truth, as per the GitOps model. Therefore, you'll need your own copy of this repository so you can use that as the underlying repository for the application you will create.
1. Install Argo CD by following the instructions [here](https://argoproj.github.io/argo-cd/getting_started/).
1. Create an Argo CD application with your forked/copied repository. 
1. Install Tekton CD by following the instructions [here](https://github.com/tektoncd/pipeline/blob/master/docs/install.md).
1. Edit the [example pipline](pipeline.yaml), replacing everything in angle brackets (`< >`) with the proper data. Make sure to also replace the repository URL with your own and the command/commit message with whatever you want to run.
  - The example command given simply replaces the motd (message of the day) in `values.yaml` with "hello from tekton".
1. Apply the pipeline by running `kubectl apply pipeline.yaml`.
1. Once the pipeline completes, the motd of your server should be updated. Log in to the server with the external IP of the Minecraft service and check that the message has changed.

## Known issues

Currently, logging in with an authentication token does not seem to work. It gives an error similar to the following:

```
rpc error: code = Internal desc = stream terminated by RST_STREAM with error code: PROTOCOL_ERROR
```

Until this issue is resolved, login using a username and password.