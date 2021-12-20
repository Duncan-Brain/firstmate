# <img src="/assets/logo-300px.png" width='75px'></img> Firstmate - v.0.1.0
Firstmate is a boilerplate full-stack web controller that allows you to initialize and maintain a web-based project in a CI/CD style pipeline.

Boilerplate projects are available to help you get started or adapt to your own containerized project. They have

Once setup, new websites, subdomains or other projects can be added easily to the controller. Be sure to choose the appropriate server resources your cluster will need to handle your projects.

## Vision
This project is for those maybe struggling to show off their projects because backend maintenance and a simple workflow for CI/CD is cumbersome. Firstmate can also be useful for hackathons or other temporary projects. <a href="/#updating-web-projects" style="color: blue; text-decoration: underline; text-decoration-style: dotted;font-size: small">A workflow diagram</a> of the after-setup workflow is shown in the *'Updating Web Projects'* section.

The goal is to move towards a `.yaml` style setup file with options for alternate cloud providers, image stores etc. Differently similar to a Docker and Kubernetes workflow. Eventually look to have setup be less than 1 hour.

While this workflow could be adapted to be completely automated on push to `master`. Some manual control is useful.

Some extra benefits of using Firstmate could include:

- Forcing the user to have better git management practices (not working solely off of the master branch)
- Possibly an increased default level of backend security

| Table of Contents |
| --- |
| 1. [Boilerplate projects](#boilerplate-projects) |
| 2. [Deployment instructions](#instructions) |
| 3. [Custom deployment](#custom-deployment) |
| 4. [Roadmap](#roadmap) |
| 5. [Learning resources](#learning-resources) |
| 6. [References](#references) |
| 7. [License](#license) |

## Boilerplate Projects
The <a href="/#boilerplate-projects" style="color: blue; text-decoration: underline; text-decoration-style: dotted;font-size: small">firstmate-boilerplates</a> repo has a brief overview of each type of boilerplate and stores them as submodules for convenient viewing.

For boilerplate type requests please make an issue or upvote an existing request on the firstmate-boilerplates repo.

For boilerplate subtype requests, please make an issue or upvote an existing request on that specific subtype repo.

| Project Name | Repo | Status | Variations | Min Cost |
| --- | --- | --- | --- | --- |
| Basic Website | URL | Pre-Production | 1 | $43.55 CAD |
| API w Datastore | URL | Concept | 0 | N/A |
| Web App w Datastore | URL | Concept | 0 | N/A |
| Private Data Science Pipeline | URL | Concept | 0 | N/A |
| Private Git Store | URL | Concept | 0 | N/A |
| Decentralized App w Node | URL | Concept | 0 | N/A |

## Instructions
| Overview |
| --- |
| 1. [Setup](#setup) |
| >> [Web services](#web-services) |
| >> [Command line tools](#command-line-tools) |
| >> [API access tokens](#api-access-tokens) |
| 2. [Boilerplate setup](#boilerplate-setup) |
| 3. [Firstmate controller initialization](#cluster-initialization) |
| 4. [First deployment](#first-deployment) |
| 5. [CI/CD Updating a project](#update-web-projects) |
| 6. [Troubleshooting](#troubleshooting) |

### Primary Stack
| Tool | Description |
| --- | --- |
| Kubernetes | Server Microservices Architecture |
| Docker | Containerization and Image Store |
| node.js | DOM VM |
| Helm | Microservices Package Manager |
| LetsEncrypt | SSL Certication |

### Setup
The following resources may be required to continue.

#### Web Services
##### Git
Clone Firstmate (this) directory locally. Choose a boilerplate project from the list above and clone that directory locally.

##### Domain Name Service
Any DNS should work. You will need to be able to create A records.

##### Docker Hub
You will need to manually make a private image repository for each separate project you wish to have available as a unique domain. For our boilerplate check name as *'template-xxxx-image'* or *'dev-template-xxx-image'*.

***Hopefully in the future more CLI resources are available with DockerHub making this step unnecessary.***
***
#### Command Line Tools
##### doctl [optional]

Digital Ocean Control is capable of creating/editing/deleting the server resources you pay for. Use with caution.

<a href="https://docs.digitalocean.com/reference/doctl/how-to/install/" style="color: blue; text-decoration: underline;text-decoration-style: dotted;">How to Install</a> |
<a href="https://docs.digitalocean.com/reference/doctl/reference/" style="color: blue; text-decoration: underline;text-decoration-style: dotted;">Documentation</a>

##### kubectl
Kubernetes control is capable of creating/editing/deleting cluster resources on your nodes.

<a href="https://kubernetes.io/docs/tasks/tools/" style="color: blue; text-decoration: underline;text-decoration-style: dotted;">How to Install</a> |
<a href="https://kubernetes.io/docs/reference/kubectl/" style="color: blue; text-decoration: underline;text-decoration-style: dotted;">Documentation</a>

##### gpg
Gnu Privacy Guard is a tool for digital encryption and signing. In many cases pre-installed.

<a href="https://gnupg.org/download/" style="color: blue; text-decoration: underline;text-decoration-style: dotted;">Installation</a> |
<a href="https://linux.die.net/man/1/gpg" style="color: blue; text-decoration: underline;text-decoration-style: dotted;">Manual</a>
***

#### API Access Tokens
API tokens are secret and can control purchases and sensitive account info, follow best practices when using.
##### Digital Ocean API Token [optional]
Referred below as: `<do-api-token-file>`

Instructions: Navigate to *API* on your Digital Ocean Dashboard menu. Generate a new token with read and write access. Save the token as text without file extension in a private folder on your computer.  

##### Github API Token
Referred below as: `<github-api-token-value>`

Instructions: Navigate through your Github profile: *Settings* > *Developer Settings* > *Personal access tokens*. Generate a new token with repo and workflow access only, choose an expiration date you feel comfortable with (Choose *no expiration* for a less secure no maintenance option). Use as directed in the initialization steps.

##### DockerHub API Token
Referred below as: `<docker-hub-api-token-value>`

Instructions: Navigate through your DockerHub profile *Account Settings* > *Security*. Generate a new token and allow it Read, Write, Delete permissions. Use as directed in the initialization steps.
***

### Boilerplate Setup
#### Step 1: Create a private project Github repo
Create a private Github repository with a name of your choice. Preferable lowercase, and with '-' as spaces.

#### Step 2: Add secrets to your private project repo
i) Navigate through *your_project_repository* > *Settings* > *Secrets* from the menu

ii) Add repository secrets (same as Firstmate controller) with your values for the following:

**Do not change secret names**

| Name | `<Your-Value>` |
| --- | --- |
| DOCKER_HUB_USERNAME | `<docker-hub-username>` |
| DOCKER_HUB_TOKEN | `<docker-hub-api-token>` |

#### Step 3: Edit the repo name in project files
There are several mentions of 'template-xxxx' in the files and folders `k8s`, `dev-k8s`, `deploy.sh`, `dev-deploy.sh`, `.github/workflows` and also in the `firstmate-resources/k8s` and `firstmate-resources/.github/workflows`. Replace all instances including file names with the name you chose for your Github repo.

#### Step 4: Replace dummy variables in Kubernetes Project Files and Firstmate Controller resources
Two sets of Kubernetes resources are available in the template project. One with testing and deployment resources for dev.example.ca, the other for production without testing. One set is available in the Firstmate resources

i) In the `template-xxxx-deployment.yaml` in both the `k8s` `dev-k8s` folder edit the *DOCKERHUB_USERNAME* with your own Docker Hub username.

ii) In the `template-xxxx-certificate.yaml` in both the `k8s` `dev-k8s` folder edit the *example.ca* with your own domain name.

iii) In the `ingress-service.yaml` in both the `k8s` `dev-k8s` folder edit the *example.ca* with your own domain name.

#### Step 5: Add/Edit Ingress Service to Firstmate

i) A file `template-xxxx-ingress-service.yaml` is available in the `firstmate-resources/k8s` folder in the specific boilerplate project folder. Copy this ingress service file to your Firstmate controllers' `k8s` folder. This should be the only ingress service file. ***If adding to an existing controller, merge this file instead of replace***

ii) Replace any *example.com* with your domain name in the transferred file `template-xxxx-ingress-service.yaml`.

#### Step 6: Add Workflows to Firstmate

i) One or multiple files such as `template-xxxx.yml` or `dev-template-xxxx.yml` is available in the `firstmate-resources/.github/workflows` folder in the specific template project folder. Copy these workflow files to the Firstmate controllers' `.github/workflows` folder. It is possible to have many files with different names here.

#### Step 7: Push images to docker hub
i) Push all files to `master` on your new repository. Once the Github Actions workflow is present in master branch it will attempt to push the main project image to Docker Hub.

ii) Create a branch called `dev` and the Github Actions workflow will attempt to push the dev image to Docker Hub.
***

### Cluster Initialization

#### Step 1: Create a Kubernetes cluster on Digital Ocean
***Notice: Digital Ocean will begin to charge by the hour upon completion of this step***

 i) In your Digital Ocean dashboard click [Create] and choose the *Kubernetes* option.

 ii) Configure as desired and click [Create Cluster].

Example basic configuration:

|Configuration| Value |
| --- | --- |
| Kubernetes Version | Recommended \| Latest |
| Datacentre Region | Location served \| Your location |
| Node Pool Name | Default |
| Machine Type (droplet) | Basic nodes |
| Node Plan | Basic plan (cheapest) |
| Node Count | 2 |
| Name | Identifying name + default |
| Project | Default |
| Tags | None |

#### Step 2: Retrieve the admin kubeconfig file from your Digital Ocean cluster
***Similar instructions are provided on the cluster overview page on Digital Ocean after cluster creation***

**Method A:** Using [doctl](#doctl-optional)

Retrieve your `<cluster-id>` from your newly created cluster by navigating to the cluster overview page on Digital Ocean.
```
# Edit the commands below with your values
$ doctl auth init --access-token=$(cat /path/to/<do-api-token-file>)
$ doctl kubernetes cluster kubeconfig save <cluster-id>
```
This will typically save the config file to the config path `$HOME/.kube` .

**Method B:** Manually

i) Click the download config file from the cluster overview page.

ii) Merge with or replace the config file in your `$HOME/.kube` directory.

iii) Retrieve the `<cluster-name>` for your cluster from the config file.

iv) Set your local config context with:

```$ kubectl config set-context --current <cluster-name>```

#### Step 3. Create a service account and cluster role binding for Github Actions

Creating the user ```github-actions``` as good practice to limit scope or track behavior.
```
$ kubectl create sa --namespace kube-system github-actions
$ kubectl create clusterrolebinding github-actions-admin --clusterrole=cluster-admin --serviceaccount=kube-system:github-actions
```

#### Step 4. Retrieve the secret service account token for the github-actions user.
**Method A:** Using kubectl ( 2021 Oracle[^1] )

```
$ TOKENNAME=`kubectl -n kube-system get serviceaccount/github-actions -o jsonpath='{.secrets[0].name}'`
$ TOKEN=`kubectl -n kube-system get secret $TOKENNAME -o jsonpath='{.data.token}'| base64 --decode`
$ kubectl config set-credentials github-actions --token=$TOKEN
```

The token should now be visible in your `/.kube/config` file

**Method B:** Manually

i) In your Digital Ocean Dashboard, navigate to your Kubernetes cluster overview page

ii) Open the [Kubernetes Dashboard] for this cluster

iii) In the Kubernetes dashboard, navigate to *Secrets* under *Config and Storage* section of the menu

iv) Look through the paginated tabs and select the secret similar to *github-actions-token-xxxxx*

v) Under the *Data* heading there should be: *token* :eye: :pencil2: . Reveal the token using the eye.

#### Step 5. Clone this Firstmate 'controller' git repo
To a private Github repository of your own and locally.

#### Step 6. Move and rename the dummy templated kubeconfig file
i) Copy the file `.DELETEME.github-actions-kubeconfig` to your `/.kube` folder

ii) Rename the `.DELETEME.github-actions-kubeconfig` file in your `/.kube` folder to simply `github-actions-kubeconfig`

iii) Delete the `.DELETEME.github-actions-kubeconfig` file from your private repo. ***Moving forward only encrypted versions of this file should ever be added to your Github repo.***

#### Step 7. Fill out the dummy variables in the `github-actions-kubeconfig` file
i) Copy the secret token for the github-actions user into the `github-actions-kubeconfig` file.

ii) Fill in the other missing elements from the admin kubeconfig retrieved from your Digital Ocean cluster.

***The main difference between these two files is the users section at the end of the text.***

#### Step 8. Encrypt the `github-actions-kubeconfig` file

Navigate to your `/.kube` folder and encrypt your `github-actions-kubeconfig` file. Use a secure `<decrypt-passphrase>` of your choice and remember it for future steps.
```
cd path/to/.kube
gpg --symmetric --cipher-algo AES256 github-actions-kubeconfig
```

#### Step 9. Add the .gpg encrypted file back into to your private Firstmate repository
Again, only encrypted versions of this file should ever be added to your repo.

#### Step 10. Add secrets to your controller repository on Github.
i) Navigate through *your_controller_repository* > *Settings* > *Secrets* from the menu

ii) Add new repository secrets with your values for the following

| Name | `<Your-Value>` |
| --- | --- |
| DECRYPT_PASSPHRASE | `<decrypt-passphrase>` |
| DOCKER_HUB_USERNAME | `<docker-hub-username>` |
| DOCKER_HUB_TOKEN | `<docker-hub-api-token>` |
| DOCKER_HUB_EMAIL | `<docker-hub-email>` |
| TOKEN_GITHUB | `<github-api-token>` |

#### Step 11. Replace the dummy domain name Kubernetes setup files
i) Purchase a domain with your chosen DNS

ii) Replace *example.com* with your domain name in `issuer.yaml`.

iii) If using the boilerplates, a file `template-xxxx-ingress-service.yaml` is available in the `firstmate-resources/k8s` folder in the specific template project folder. Copy this ingress service file to merge/replace in the Firstmate controller `k8s` folder.

iv) Replace any *example.com* with your domain name in the transferred file `template-xxxx-ingress-service.yaml`.

#### Step 12. Run the Github Actions `cluster_init.yml` workflow
i) Navigate to the repository *Actions* tab for the `cluster_init.yml` workflow. Click *Run workflow* and enter 'true' in the input box to run. The status of the workflow progress will appear.

#### Step 13. If needed, troubleshoot workflow failures
i) If the workflow in your *Actions* tab in your Github repository fails. Click through and expand log snippets to see the point of failure.

ii) If no simple typos or syntax errors seeem to be the cause try clicking the [Re-run all jobs] button on the failed attempt.

iii) Create an issue on the repo if more challenging problems occur and I will try to help out as soon as I can.

#### Step 14. Retrieve the server endpoint IP address
**Method A:** Digital Ocean Load Balancer

i) Navigate through *Networking* > *Load Balancers* on your Digital Ocean Dashboard.

ii) A load balancer with IP address (same as Method B) should now be visible.

iii) Referred to as `<ip_address>` moving forward.

**Method B:** Kubernetes Ingress Service

i) Navigate through the Digital Ocean Dashboard to your Kubernetes cluster overview page and click through to your [Kubernetes Dashboard]

ii) Navigate through to *Ingresses* under *Service* on your Kubernetes Dashboard

iii) A service named *ingress-service* should now be visible with an endpoint IP address (same as Method A)

iv) Referred to as `<ip_address>` moving forward.

#### Step 15. Add *A Records* to your DNS
Using the `<ip_address>` as the endpoint create seperate A records for the main domain 'www' as *Host*, and for the subdomain with 'dev' as *Host*.
***

### First Deployment
#### Step 1: Push images to docker hub (completed in boilerplate setup)
The first push to `master` and `dev` in the project repository with the Github Actions workflow present will attempt to push images to Docker Hub.

#### Step 2: Create deployment branches in Firstmate repo
i) In the Firstmate repo create a branch for each project template. The name for the branch to create would be found in the `boilerplate-xxxx/firstmate-resources/.github/workflows` files transferred to the Firstmate controller, now found in your `firstmate/.github/workflows` these should be called something like `update-template-xxxx` or `update-dev-template-xxxx`. ***This should initiate the deployment workflow to your server***

ii) Should the workflow not run automatically ensure the branch name matches the `on:` setup in the workflow. And try a manual update as part of regular CI/CD flow (below).
***

### Updating Web Projects
i) To push the new project image to your website simply add an arbitrary change to the comments in the project specific workflow on the `update-template-xxxx` or `update-dev-template-xxxx` branch. I typically do this manually in the Github UI.

ii) Commit and push the arbitrary change to the update branch. This is done so that a useful message is shown for the workflow 'run'.

The reason we do it this way is due to a missing feature on workflows (https://github.community/t/github-actions-dynamic-name-of-the-workflow-with-workflow-dispatch/150327). This method will hopefully change in the future.

<img src="/assets/workflow-diagram-841px.png" width='1100px'></img>
***

### Troubleshooting
| Overview |
| --- |
| [Cluster initialization fail](#cluster-initialization-fail) |
| [Website not viewable](#website-not-viewable) |

#### Cluster Initialization Fail
The workflow has failed during initialization. Try re-running initialization. If problem persists review naming then check issues.

#### Website Not Viewable
i) Wait up to an hour or so for LetsEncrypt to process the certificate request.

ii) Wait 24-48 hours for your DNS A-Record to be disseminated.
***

## Custom Deployments
Please choose a template project most similar to your needs. Suggestions for customizing the stack will try to be addressed within the specific boilerplate projects.

Generally speaking I see a few things to keep in mind when building out a custom project using this template:
- One time initializations (Workflow)
    - Ex. Setting up a datastore or
- How you serve or your project (Dockerfiles)
    - static
    - Node.js
    - Next.js
- Other resources (Kubernetes reseources)
    - data store
    - worker server
    - computation
    - ingress

Then of course different image stores or cloud services which will hopefully be addressed in a future, simpler, rollout of Firstmate.
***

## Roadmap
- Convert roadmap to issue, add link to README
- Yaml style file setup (bash?)
- Consider an option for fully automatic deployment on push to master
- Refine RBAC
- Release and update watcher
***

## Learning Resources
Docker & Kubernetes: The Complete Guide by Stephen Grider - [https://www.udemy.com/share/101WjM3@5Giyf_mjbu3rRKfp8Zw-L5GLUKBHLGx7u4OUK4RpOxcd72CrdrTgJI6y4kx60BZh/](https://www.udemy.com/share/101WjM3@5Giyf_mjbu3rRKfp8Zw-L5GLUKBHLGx7u4OUK4RpOxcd72CrdrTgJI6y4kx60BZh/)
***

## References
[^1]: Oracle - Step 4, Setting up a Service Account [https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengaddingserviceaccttoken.htm](https://docs.oracle.com/en-us/iaas/Content/ContEng/Tasks/contengaddingserviceaccttoken.htm)
***

## License
Right now I am thinking [GPLv3](https://www.gnu.org/licenses/gpl-3.0.html) if I am able.

My understanding of this would be (among other things):
i) You can use this project to make a profit or start a business. But specifically when it comes to the code/software is that any upgrades you make you must share as open source code if you wish to sell the upgraded software.

ii) I will try to make push good software but I make no claims about it's security, and am not responsible if something bad happens from you implementing this code.
