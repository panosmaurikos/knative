### Knative

**What is Knative?**
Knative is an open source platform that aims to simplify the deployment and management of serverless workloads on Kubernetes. It provides a set of building blocks that remove the complexity of managing the underlying infrastructure, allowing developers to focus on writing and developing code. It was developed in 2018 and is supported by a group of companies that have collaborated (Google, IBM, Pivotal, Red Hat and SAP) to help Kubernetes run microservices and efficiently handle serverless applications.

**Installing Knative using quickstart**

**Installation prerequisites**
• kind or minikube to be able to run a local Kubernetes cluster.
• Kubectl is a Kubernetes command line tool that allows running commands on Kubernetes clusters.
• Knative CLI provides a quick and easy interface to create Knative resources, such as Knative Services and Event Sources, without the need to create or modify YAML files directly.
• At least 3 CPUs and 3 GB of RAM available to be able to create the cluster.
• Docker

**Install kind**

With the curl command we download Kind.
curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.19.0/kind-linux-amd64

Change the permissions to make it executable.
chmod +x ./kind

Move kind to an application directory such as bin.
sudo mv ./kind /bin/kind

![image](https://github.com/nubificus/roadmap/assets/72733593/f1a2ed9b-9f47-4220-990f-90ffdb99c7d7)


**Install kubectl**

Download the latest version with the command:
curl -LO https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl

Validate correct file download:
curl -LO https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256

echo "$(cat kubectl.sha256) kubectl" | sha256sum --check

Install kubectl:
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

Test version
kubectl version –client

![image](https://github.com/nubificus/roadmap/assets/72733593/f8320e90-5228-4171-a7d2-be0348679366)


**Install Docker**

1. sudo apt-get install -y docker.io
 
 ![image](https://github.com/nubificus/roadmap/assets/72733593/c82a1a6b-ce58-4280-9746-de8b97686e50)
  
2. sudo systemctl enable docker
3. sudo apt-get install -y apt-transport-https ca-certificates curl
 
 ![image](https://github.com/nubificus/roadmap/assets/72733593/20d8be95-3926-4ac6-ad11-7d866022ae94)
 
4. sudo systemctl status docker
 ![image](https://github.com/nubificus/roadmap/assets/72733593/a115e6d4-833c-4672-ba15-6d874be6084c)


**Brew installation**

1. sudo apt-get install build-essential

2. Install Git

sudo apt install git -y

3. Run Homebrew installation script

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

4. Add Homebrew to your PATH

(echo; echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"') >> /home/$USER/.bashrc
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

5. Check Brew is working fine

brew doctor


![image](https://github.com/nubificus/roadmap/assets/72733593/ede56c42-2c2b-4efb-a562-e0745c0eafd1)
![image](https://github.com/nubificus/roadmap/assets/72733593/c4026169-ce75-42fd-9ed2-22ff0e58e5f1)
![image](https://github.com/nubificus/roadmap/assets/72733593/bbae60e6-863c-4fee-b85e-24575d93d1bc)
![image](https://github.com/nubificus/roadmap/assets/72733593/5ce69ccd-e7bd-4c10-9076-d027e63632af)


**Install Knative**

To install kn using Homebrew, we run the command:
brew install knative/client/kn

![image](https://github.com/nubificus/roadmap/assets/72733593/7ef08006-c41e-4429-a62b-3812cf88b72d)


**Install the Knative plugin**
brew install knative-sandbox/kn-plugins/quickstart

To get a local deployment of Knative, we run the command:
kn quickstart kind

```diff
- In case we encounter the following error, we execute the command
```
```diff
- sudo usermod -aG docker $USER
```
```diff
- sudo systemctl restart docker
```
```diff
- and restart our system.
```
![image](https://github.com/nubificus/roadmap/assets/72733593/1bd9a8d1-3c23-4af2-bfe9-d89d1393b9c3)

If everything works normally, we should see the image below

![image](https://github.com/nubificus/roadmap/assets/72733593/daa3035b-e256-4ed0-a16f-1bb684db8d84)

After the plugin installation is complete we make sure we have a cluster called knative with the command:
kind get clusters

![image](https://github.com/nubificus/roadmap/assets/72733593/471c9aef-b6b2-4d4f-9ae1-2994838014ad)


### **Knative Functions**
Knative Functions provides a simple programming model for using functions in Knative, without requiring in-depth knowledge of Knative, Kubernetes, containers, or docker files.


**Installing Native Functions**
To install Knative Functions we execute the following commands:

brew tap knative-sandbox/kn-plugins

brew install func

![image](https://github.com/nubificus/roadmap/assets/72733593/68074e3f-5f40-4263-b432-04e43385f1f1)


**Create Function**
func create -l <language> <function-name> …….… format

func create -l go hello


### **Knative Function example**

We run func create -l go Knative-function-demo to create a function with the go language


![image](https://github.com/nubificus/roadmap/assets/72733593/64b179cf-1189-419f-bd48-98f432528e11)

Then we enter the directory where the function is stored to see that the files have been created.

![image](https://github.com/nubificus/roadmap/assets/72733593/0699b3f7-5895-4050-bebd-fa2051db1379)

With the help of vim or nano we edit the handle.go file

![image](https://github.com/nubificus/roadmap/assets/72733593/6da66480-6e5c-48fa-9f19-89b8f304bed5)


And we modify it to have the following form:

![image](https://github.com/nubificus/roadmap/assets/72733593/add0c3c5-9f24-4543-a918-1918f88721fd)

To run the function (local) we created, execute the command:
   func run –build –registry {registry}


![image](https://github.com/nubificus/roadmap/assets/72733593/8dda2055-a4eb-4d48-90f2-91464cae7908)

Now if in a browser at http://localhost:8080 we will see our function running.

![image](https://github.com/nubificus/roadmap/assets/72733593/72beaec7-e223-4502-956a-b7e519667231)


In case we want a production solution, we have to build a Container
image and use it to run our function. To build the container image I run the following command:
func build –image {registry}

![image](https://github.com/nubificus/roadmap/assets/72733593/70a7a0b7-1fa6-4078-9aba-2391922b6fad)
![image](https://github.com/nubificus/roadmap/assets/72733593/1a6c501f-f397-425d-901d-50ad24e617d9)


To deploy our function in a production environment, I execute the command:

func –namespace default deploy

![image](https://github.com/nubificus/roadmap/assets/72733593/34cf9ac8-3c7a-4b45-8ecd-57b1491e4e9a)

The last line gives us , from where we will access.

![image](https://github.com/nubificus/roadmap/assets/72733593/7b8b27dd-72b1-49e5-b23b-1c8cd6983c94)


With the commands:
  func –namespace default invoke …. that I was seeing in the browser but from a terminal
func –namespace default list … list of all functions within the namespace
func –namespace default info …. information
func –namespace default delete … delete


![image](https://github.com/nubificus/roadmap/assets/72733593/608bbe90-9500-4d41-914c-f9c82997d8cd)


**### Knative Service(example)**

we will develop a Knative Service "Hello world" that accepts the environment variable TARGET and will print Hello ${TARGET}!.
We deploy the Service with the command:

kn service create hello \
--image ghcr.io/knative/helloworld-go:latest \
--port 8080 \
--env TARGET=World

![image](https://github.com/nubificus/roadmap/assets/72733593/ad64e422-0416-4568-83f3-8bc9e553d769)

Knative Serving provides auto-scaling. This means that a Knative service defaults to zero pods when not in use.
We use the Knative (kn) CLI to find the URL where our Knative service is hosted. This is done with the command:
kn service list

![image](https://github.com/nubificus/roadmap/assets/72733593/be7946f6-96de-441e-bfc2-dcd56a4bc746)
![image](https://github.com/nubificus/roadmap/assets/72733593/41d67de0-5a53-495a-95db-8cbddd2eddfb)


In addition to opening the service in the browser, we can also open it from the terminal with the command:
echo "Accessing URL $(kn service describe hello -o url)"
curl "$(kn service describe hello -o url)"

Knative also allows us to track pods and see how they scale.
kubectl get pod -l serving.knative.dev/service=hello -w

![image](https://github.com/nubificus/roadmap/assets/72733593/0bcfd502-2187-4d37-bfb8-eaf64c0cd728)

**Create a new Revision**
Every time we make changes to the configuration of a Knative service, a new revision is created. When splitting traffic, Knative splits traffic between different revisions of the Knative service.
Updated version of Knative service

kn service update hello \
--env TARGET=Knative
We created hello-00002.

![image](https://github.com/nubificus/roadmap/assets/72733593/4507e06b-759e-492e-8987-841fe16ffe2d)

Also with the command kn revisions list we can see a list of revisions
When we create a new revision of a Knative service, Knative by default directs 100% of the traffic to that latest revision. We can change this default behavior by specifying how much traffic we want each revision to receive.
This is done with the following command:

kn service update hello \
--traffic hello-00001=50 \
--traffic @latest=50

![image](https://github.com/nubificus/roadmap/assets/72733593/5639d404-de1f-4e7a-8973-1e38c6d379e0)
