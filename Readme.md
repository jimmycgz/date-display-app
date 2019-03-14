# Summary

I joined this Dojo as a key player building CI/CD pipeline.

In this challenge, we built an elaborated Continuous Integration / Continuous Deployment pipeline using Jenkins, one of the most popular CI/CD tools. 

In summary, this pipeline will do the following actions:

* Checkout a GitHub repository containing a simple Node.js application
* Run a few tests
* Build a Docker image and push it to Dockerhub
* Deploy the application to Kubernetes using Helm (Kubernetes' package manager)

To simplify the process, you will follow a number of steps. Each step will help you build a tiny bit of the final solution.

## Jenkins on Kubernetes
We usually run Jenkins on virtual machines and provide it with a script which is going to run on the host. However, for this challenge, Jenkins will be running on a Kubernetes cluster, which means that all scripts will have to run in containers. This is a bit of a shift of paradigm, but there are good reasons for that approach. Read them below if you have the time, otherwise, proceed to the Getting started section.

## Why run Jenkins on a container orchestration platform? (Optional section - read at your own free time)
There are a couple of reasons why running pipelines in containers is a better approach. Let's suppose that Jenkins is running on a single virtual machine, and is being managed by an operations team. The developers have just started developing a new Node.js application and ask the operations team to install NPM on the Jenkins host. The operations team install it. A month later, they start developing a microservice written in Python and therefore need Pip. Developers ask the operations team to install pip on Jenkins for their new python application. A month later, they start developing a Java application. You know what's going to happen, right? There's just too much unnecessary work for the operations team.

Things can get much worse if the operations team decide to run Jenkins in a Master-Worker fashion (one Master node and multiple worker nodes). If before it was challenging to manage one host (Jenkins Master), imagine multiple hosts.

How can this dev and ops relationship be improved? By introducing containers. In this new scenario, whenever developers start developing some new application or decide to improve existing applications, they should provide the CI/CD pipeline with a Dockerfile which builds a Docker image and run everything that needs to be run. This means that if there is a Node.js application with dependencies, all the tools necessary to test and build the application will be installed in the container. This means that developers do not need to come to the operations team anymore and ask them to install tools in the virtual machines. Developers only need to provide the ops team with a Dockerfile. The ops team does not need to worry about which tools and commands are needed to build the application.
