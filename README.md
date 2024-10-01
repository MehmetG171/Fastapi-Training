# Jenkins-Fastapi-Compose-Deployments

## Prerequisite: an Ubuntu VM w/ SSH access

### VM on Vagrant (the better way)

- [ ] Create a `Vagrantfile` and provision a Ubuntu VM with docker and docker-compose installed
  - expose port 8000, 9000, 10000, 11000, 12000
- [ ] setup ssh access for Jenkins to the VM

### VM on Cloud (not recommended, easy way)

- [ ] you know what to do, right?
- [ ] Install docker and docker-compose
- [ ] setup ssh access for Jenkins to the cloud VM

## Task: Part 1

You can find the [fastapi app](fastapi/) in this directory.

Create a Jenkins pipeline that will deploy the fastapi app to the VM.

Do the following steps in a jenkins pipeline:

- [ ] Connect to VM via SSH
- [ ] Clone this repo (or your fork)
- [ ] Create a separate folder named `jenkinsapp` in the VM in your $HOME directory if it doesn't exists (this will be the workspace for our application)
- [ ] Stop the docker-compose service if it is running
- [ ] Create a backup of the current `jenkinsapp` folder and zip it.
- [ ] move fastapi app file in this repo to `$HOME/jenkinsapp`
- [ ] Build the application docker image with `docker-compose build` command
- [ ] Start the docker-compose service with `docker-compose up -d` command
- [ ] Show the output of `curl --include http://localhost:8000` x 10 times.

**Bonus Tasks**

- [ ] Create a separate Jenkinsfile for docker image build and push to dockerhub, and use it in the main Jenkinsfile instead of building the image in the VM.

---

## Task: Part 2

> You must complete `Task: Part 1` before starting this task.

- We have a VM with a fastapi app running in docker-compose.
- But this app only consumes a small amount of resources in the VM.
- We want to deploy envs. for the same app.

- [ ] Create a separate repo for the fastapi app
- [ ] Create 3 branches in the repo named `dev`, `test`, `prod`
- [ ] Use ports as `dev`, `test`, `prod`: `9000`, `10000`, `11000`
- [ ] In each branch, randomize the chance of getting errors in the app (So the code differs in each branch)
  ```python
  should_fail_500 = percentile_true(10) # make it 20, or smt.
  should_fail_400 = percentile_true(10) # make it 30, or smt.
  should_fail_404 = percentile_true(10) # make it 5, or smt.
  ```
- [ ] Transform your Jenkins pipeline you made in Task: Part 1
- [ ] Your pipeline should have a parameter named `Environment` with `dev`, `test`, `prod` options

---
