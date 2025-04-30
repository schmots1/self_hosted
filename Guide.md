# home server guide

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image1.jpeg](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image1.jpeg)


# Introduction

Self-hosting an application means running the service on a computer that you own and control. This could be a physical machine in your home or a virtual server hosted on a cloud provider like Amazon AWS or Oracle OCI. The appeal of self-hosting lies in the control it gives you—whether you're running a simple blog or a full browser-based desktop environment accessible from anywhere in the world.

## Data Ownership

One of the biggest advantages of self-hosting is **data ownership**. When you use services like Dropbox, the company hosting your files has full access to them and may share them with third parties—even in response to vague or unofficial requests. Worse, many free and paid providers collect extensive data about you and sell it to advertisers. In these cases, your files aren’t the product—**you are**. By hosting services yourself, **only you** have access to your data, and there’s no third party collecting or monetizing your personal information.

## Cost Efficiency

Another major benefit is **cost efficiency**. Instead of paying monthly subscription fees for multiple services, you make a one-time investment in hardware and cover ongoing electricity and internet costs. Hosting a server at home gives you the ability to:

- Customize everything to your exact needs  
- Maintain full control over your files  
- Eliminate recurring costs  

Plus, there’s a real sense of satisfaction that comes from building and managing something yourself.


## What Can You Run?

Now, let's explore just a few of the applications you can run on your home server:

- **Cloud storage** – Set up your own file storage and syncing solution.
- **Blog sites** – Host your own blogs and have full control over the content.
- **Media servers** – Stream your own music, TV shows, and movies from anywhere.
- **Web-based book libraries** – Read and organize your eBooks through a web interface.
- **Game servers** – Run custom game servers, like Minecraft, for a tailored experience.
- **Download management** – Automate and manage your downloads efficiently.

## Why This Guide?

Many people find the idea of self-hosting intimidating, often due to a lack of familiarity with servers, Linux, or the applications themselves. That’s exactly what this guide is here to address. With clear, step-by-step instructions and copy-and-paste examples, you’ll be able to get your self-hosted services up and running with confidence.

By the end of this guide, you'll have an impressive set of services running on your home server, including:

- An eBook library
- Cloud file hosting
- Space usage reporting  
- Backup solutions  
- A personal blog  
- A private Git repository  
- Media streaming  
- A graphical dashboard  
- A private wiki  

## Ready to Begin?

Get ready to take back control of your digital life and experience the full power of self-hosted applications—all on hardware you own. Let’s dive in and make it happen!


# Virtual Machines vs Docker vs Kubernetes

When it comes to running multiple applications on a single host, there are several approaches to consider. One option is to install all applications directly on the host and hope for the best in terms of avoiding conflicts. A more reliable approach is to use **Virtual Machines (VMs)**, where each application runs in its own isolated environment. Alternatively, you can use **containers** to run applications as microservices. In this guide, we focus on the latter—specifically using **Docker** and **Kubernetes** to manage containers.

To help you understand why, let’s break down the differences between VMs, containers, and Kubernetes.

---

## Virtual Machines

**Virtual Machines** simulate an entire operating system on your hardware. They allow you to run multiple operating systems—like Windows and Linux—on a single physical machine. This is made possible by virtualization software such as VirtualBox, VMware, or KVM.

### Benefits of VMs:
- Full isolation between applications  
- Ability to run multiple operating systems on the same hardware  
- Widely supported across on-prem and cloud infrastructure  
- Mature tooling and ecosystem  

However, VMs are resource-intensive since each VM runs a full OS instance, making them less efficient for lightweight or short-lived applications.

---

## Containers

**Containers** package an application and all its dependencies into a single, portable unit that runs reliably in different environments. Unlike VMs, containers share the host operating system, which makes them faster and more lightweight.

Think of containers like shipping containers: each one is isolated, yet they can all travel on the same ship.

### Benefits of Containers:
- Lightweight and fast startup  
- Portable across environments (PCs, servers, cloud)  
- Isolated but share the same OS kernel  
- Ideal for microservices  
- Easier to manage and update than VMs  

---

## Docker

**Docker** is the most popular tool for creating, running, and managing containers. Introduced in 2013, Docker revolutionized containerization with simple tools and strong ecosystem support.

### Key Features of Docker:
- Easy application packaging and deployment  
- Strong isolation between containers  
- Works on Linux, Windows, and macOS  
- CLI and GUI tools for managing containers  
- Reduces infrastructure overhead  
- Enables microservice development  
- Great for local development (e.g., AWS Lambda emulation)

---

## Kubernetes

**Kubernetes** is an open-source platform designed to manage containerized applications at scale. While Docker helps you run a single container or small group, Kubernetes helps you coordinate, scale, and maintain hundreds (or thousands) of containers.

### Key Benefits of Kubernetes:
- Automated container deployment, scaling, and management  
- Zero-downtime rolling updates  
- Works across clouds (AWS, Azure, GCP) and on-premises  
- Strong community and ecosystem  
- Highly flexible and cloud-native  
- Supports both Linux and Windows containers  

---

## Virtualization vs. Containerization

| Feature               | Virtual Machines                  | Containers                        |
|----------------------|-----------------------------------|-----------------------------------|
| OS Overhead          | High (each VM has its own OS that the user must manage)     | Low (containers are built on stub OS setups that the user doesn't have to manage host OS)    |
| Resource Usage       | More CPU and memory               | More lightweight                  |
| Startup Time         | Slower (full OS boot)             | Faster (just the app starts)      |
| Portability          | Less portable                     | Highly portable                   |
| Ideal Use Case       | Long-lived, full-featured systems | Short-lived or scalable services  |

---

## Which Should You Use?

For self-hosted applications, **containers are often the better choice**. They’re quick to deploy, use fewer resources, and are easy to manage with tools like Docker and Kubernetes. While VMs still have their place, particularly for running full OS environments or legacy software, containers are ideal for the kind of lightweight, flexible services you'll be running on your home server.

# Host Considerations for Kubernetes Installation

Before diving into setting up self-hosted services, the first crucial step is choosing where your applications will run. While it's best to use a **dedicated system** separate from your everyday desktop, you can technically use the same computer. Just note that this may introduce stability and performance issues.

If you're planning to run an always-on server, consider the following **key factors**:

- **Fan noise** – A loud machine can quickly become annoying, especially in shared spaces.  
- **Power consumption** – Higher power usage means higher electricity bills.  
- **Heat generation** – More powerful hardware often generates more heat, which may require additional cooling.  

---

## Recommended Hardware: Small Form-Factor Systems

Many people opt for **small form-factor systems** thanks to their:

- Low power draw  
- Quiet operation  
- Compact size  
- Budget-friendly options  

For example, one popular choice is the [GEEKOM MINI IT8 TECH](https://tinyurl.com/yh6ptams), which offers:

- Intel Coffee Lake i5-8259U processor  
- Intel Iris Plus Graphics 655  
- 8GB/16GB DDR4-3200 RAM (expandable to 32GB)  
- 256GB/512GB SSD (plus optional 2.5" HDD up to 2TB)  
- Windows 11 Pro pre-installed  
- Bluetooth, Wi-Fi, Ethernet, HDMI, DisplayPort, and USB ports  

While this is a solid option, feel free to explore alternatives that meet the following **minimum system requirements**:

### ✅ Minimum Recommended Specs

- **CPU**: Intel or AMD x86_64 processor  
  - (Avoid ARM-based CPUs like those in Raspberry Pi for broader compatibility)
- **RAM**: At least **16GB**  
  - 8GB is workable for basic setups, but it limits how many services you can run
- **Storage**: At least **256GB SSD**  
  - SSDs are faster; external drives are fine for media and backups
- **Network**: Wired **Ethernet** connection  
  - Wi-Fi is possible, but this guide doesn't cover setup
- **Bootable USB**: At least **4GB**  
  - For installing the operating system

For DIY builders, this hardware guide is worth checking out:  
👉 [zilexa/Homeserver Recommendations](https://github.com/zilexa/Homeserver/blob/master/Recommendations.md)

---

## External Access (Optional)

If you want to access your self-hosted services from outside your home network, you’ll need to set up a few additional components:

- **Router access**: You must be able to configure **port forwarding** on your home router.  
  - Search for your model's guide (e.g., _"Linksys 54GT port forwarding"_)
- **Public IP address**: Visit [https://showmyip.com](https://showmyip.com/) to find yours.
- **Domain name**:  
  - Purchase one from a registrar like [Cloudflare](https://cloudflare.com)  
  - Or get a free subdomain from [Dynu](https://www.dynu.com)  
  - _Note: Free options may share some traffic/usage metadata publicly_

> 💡 **See the Appendix of this guide for full instructions on external access setup.**

---

Now that you have a solid understanding of the hardware and networking requirements, let’s move on to installing the operating system.


# Operating System Installation

To ensure optimal functionality of the services discussed in this guide, Linux will be used as the operating system. Specifically, we will cover the installation process using the Ubuntu distribution.

If you are not familiar or comfortable with Linux do not worry. This guide will include all the commands needed to accomplish these tasks and most commands and files can be copy and pasted right from the guide.

## Creating the Bootable USB Thumb Drive

1. Download the Ubuntu Server 22.04 LTS ISO from [https://releases.ubuntu.com/22.04.2/ubuntu-22.04.2-live-server-amd64.iso](https://releases.ubuntu.com/22.04.2/ubuntu-22.04.2-live-server-amd64.iso)
2. Download 'unetbootin' from [ [https://unetbootin.github.io/](https://unetbootin.github.io/)]. You can find versions for Windows, Linux, and macOS.
3. Run unetbootin and select the ISO file downloaded in step 1.

<aside>
🔥 Important: This process will erase all data on the USB drive, so make sure to backup any important files.

</aside>

<aside>
💡 The duration of this step depends on various factors, such as your computer's speed, the USB drive's speed, and the current workload on your computer. It may take a few seconds or up to 10-15 minutes or more. If the process is running and your USB drive's LED is blinking, it is progressing correctly.

</aside>

## Ubuntu Server Installation

These instructions will guide you through the successful installation of the Ubuntu operating system, enabling you to proceed with the setup of your server.

1. Connect the USB drive to the system that will become your server. Ensure that the host is already connected to your router via an Ethernet cable.
2. Power on or reboot the server system. As soon as it boots, press the key that allows you to access the boot options (usually F2 or F10 key). Select the USB drive as the boot device.
3. Choose "Try or Install Ubuntu."
4. Follow these selection steps:
    1. Select your preferred language and press 'Return.'
    2. Choose "Continue without updating" and press 'Return.'
    3. Select your keyboard type and press 'Return.'
    4. Select "Ubuntu Server minimized."
    5. Accept the DHCP-pulled IP address (note it down). Use the 'Tab' key to select the 'Done' option at the bottom of the screen and press 'Return.'
    6. Press 'Return' to leave the proxy field blank.
    7. Press 'Return' to accept the default repository URL.
    8. Ensure that "Use entire disk" is selected, then choose "Done" and press 'Return.'
    9. Press 'Return' to accept the drive layout proposed by Ubuntu, then select "Continue" and press 'Return.'
    10. Fill out your name, username, password, and choose a server name. For example, you can use "server" for the server’s name and "user" for the username. Use the 'Tab' key to move between fields.
    11. Do not enable Ubuntu Pro.
    12. Press the 'Space Bar' to select "Install OpenSSH server." Unless you have an identity to import, leave the option as "No." Use 'Tab' to select "Done" and press 'Return.'
    13. Press 'Tab' to select "Done" and press 'Return.' Do not select any additional packages.
5. While the operating system installs, take a break, and enjoy a coffee or soda.
6. Once the option reads "Reboot Now," select it and press 'Return.'
7. When you see the message "Please remove the installation medium, then press ENTER," press 'Return' and remove the USB drive.
8. After rebooting, you may need to press 'Return' once. Then, log in using the username and password specified in step 4j.
9. Lastly, make a note of the IP address assigned to the server. The IP address acts as the computer's home address on the network and will be used to remotely connect to the server for further setup. You can use the command "ip address" to find this information.

Important: It is necessary to have previously noted the name of your Ethernet port. For example, in this example, the 'inet' or internet address for 'enp0s3' is '172.31.199.126'.

```bash
ip address
```

![image2.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image2.png)

Your server currently has an automatically assigned IP address that may change upon reboot or after a certain period of time, depending on your router's settings. However, for a server, it is essential to have a "static" IP address that doesn't change. To set a static IP address, you need to note three things:

1. The IP address you will use as your static address.
2. The default gateway, which is the IP address of your router and is used to reach the internet (I'll show you how to find this).
3. The default DNS system, which is usually your router as well (I'll guide you on how to find this).

## Selecting an IP Address for Kubernetes

To begin, you need to choose an IP address that is not already in use by any other device. In most home networks, a class C network is used. You don't need to understand the technical details but remember that only the last number in the IP address sequence changes. For example, if you have an IP address like 192.168.0.100, the 192.168.0. part remains the same. The last number can range from 1 to 255, excluding 255 which is reserved for special purposes. Since routers often assign IP addresses starting from 100, let's consider numbers below that range. For instance, in my network with an IP address of 172.31.199, I will try using 90.

Checking for IP Address Availability

To ensure your server has a consistent IP address that doesn't change, follow these steps:

1. Choose a unique IP address: Select an IP address that is not already in use by any other device on your network. In most home networks, the IP address format is like this: 192.168.0.X, where X can range from 1 to 255 (excluding 255). Since routers often assign IP addresses starting from 100, it's safer to choose a number below that range. For example, if your network IP address is 172.31.199, you can try using 90.
2. Check IP address availability: To confirm if the chosen IP address is available, we'll use a program called 'ping'. However, 'ping' is not installed by default on Ubuntu Server 22.04. You can install it using the following command:

```bash
sudo apt install iputils-ping -y
```

After installation, you can test the address availability by running the ping command:

```bash
ping -c 4 172.31.199.90
```

This command sends four test pings to the address. If there is no response, it means the IP address is available.

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image3.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image3.png)

<aside>
💡 **This is a ping failing.**

</aside>

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image4.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image4.png)

<aside>
🔥 **This is a ping succeeding.**

</aside>

1. Install a text editor: We'll use the 'nano' text editor to modify a configuration file. Install it with the command:

```bash
sudo apt install nano -y
```

1. Edit the network configuration file: Open the configuration file with the nano editor:

sudo nano /etc/netplan/00-installer-config.yaml

**Edit the file from looking like this…**

![VirtualBox_homeserver_24_12_2023_15_01_26.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/VirtualBox_homeserver_24_12_2023_15_01_26.png)


**To looking like this.**

![VirtualBox_homeserver_24_12_2023_15_03_46.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/VirtualBox_homeserver_24_12_2023_15_03_46.png)

In this file, update the interface name from 'enp0s3' to match your host, and replace the IP addresses with your chosen static IP address. Also, update the IP address in the 'gateway4' field to match the first three sections of your IP address. For example, if you chose '192.168.0.90' as your IP address, use '192.168.0.1' as the gateway IP. Save the changes by pressing Ctrl+X, then 'y', and finally Enter.

1. Apply the network configuration changes: Make the new network configuration take effect by using the netplan application:

```bash
sudo netplan apply
```

1. Verify the updated IP address: Confirm that the IP address has been updated by running the command ‘ip address’ again.

```bash
ip address
```

This simplified explanation aims to help you select and verify an available IP address for your server. Now that you have that address you can remotely connect to the host. For this you will use a protocol called SSH, which is a Secure SHell connection. If you use windows, you can download the application Putty from [https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html). If you are on a Mac or Linux, you can use the terminal. From the terminal the command you will use is.

```bash
ssh -l user 172.31.199.90
```

<aside>
⛔ Update the username 'user' and the IP address '172.31.199.90' to your username and host IP address.

</aside>

The first time you connect you will be asked to accept the identity of the host to which you can just type 'yes' and hit enter. Then you will be asked for your user accounts password. Now you are remotely connected to the Host.

# Installing Kubernetes

Installing Kubernetes can be a complex process with various options available. Some installations are simple but lack scalability, while others offer extensive customization but are challenging to set up. To provide a balance between simplicity and flexibility, this guide focuses on the K3S Kubernetes distribution and installer.

K3S was initially developed by the Rancher team at [www.rancher.com](http://www.rancher.com/). It serves as both an installation method and a specialized Linux distribution called K3OS. Not only does K3S have low resource requirements, but it is also now owned and maintained by the Cloud Native Computing Foundation (CNCF), the authority on Kubernetes specifications. This ensures its compliance with industry standards and best practices.

These steps will install K3S and configure the Kubernetes cluster on your server, as well as set up the necessary environment variables for using kubectl commands.

1. Set an environment variable with the IP address of the server:

```bash
export SERVER_IP=172.31.199.90
```

<aside>
⛔ Replace 172.31.199.90 with the IP address of your server.

</aside>

This is done so that the large install command for K3S can be copied and pasted without having to edit it.

1. Install K3S using the following command:

```bash
curl -sfL https://get.k3s.io | \
INSTALL_K3S_VERSION=v1.24.13+k3s1 \
INSTALL_K3S_EXEC="server --advertise-address $SERVER_IP --disable traefik --disable servicelb" sh -
```

Enter your user password when prompted

This will go through and fully setup a Kubernetes deployment on your host and set your “SERVER_IP” address as the address it listens for incoming network connections on for management.

1. Create a directory for the Kubernetes config file and copy created config file then set it to be owned by your user:

```bash
mkdir ~/.kube
sudo cat /etc/rancher/k3s/k3s.yaml > ~/.kube/config
sudo chown **user**: ~/.kube/config
```

<aside>
⛔ Replace **user** with your username.

</aside>

The utility ‘kubectl’, which is used to manage Kubernetes from the command line, needs to be authenticated for each run. It does this by reading from a configuration file that contains the proper access token for the server for a specific user. This configuration file has the token and authentication for the Kubernetes cluster admin.

1. Set an environment variable for the KUBECONFIG. This informs kubectl where to find the configuration file:

```bash
export KUBECONFIG=~/.kube/config
```

This export is created so that when kubectl is run, it knows where to find the configuration file for authentication based on the value of KUBECONFIG.

1. Optionally, add the environment variable to the bashrc file so that it is set automatically every time you log in:

```bash
echo 'export KUBECONFIG=~/.kube/config' >> ~/.bashrc
```

This step will make it so that the variable KUBECONFIG is set every time you log in and not require you to set it manually again like in step 4.

## Testing Your Kubernetes Installation

To ensure that all components of Kubernetes are functioning correctly, follow these simple steps to test your setup.

1. Test authentication and node information retrieval by using the ‘**kubectl**’ command to get information about the nodes:

```bash
kubectl get nodes
```

You should see an output like the following, with the NAME replaced by the name you assigned to your host:

```bash
NAME     STATUS   ROLES                  AGE   VERSION
server   Ready    control-plane,master   19m   v1.24.13+k3s1
```

1. Verify the ability to deploy containers to the host by running the following command to create an Nginx pod:

```bash
kubectl run nginx --image=nginx
```

1. Check the status of the deployed pod using the command:

```bash
kubectl get pods
```

This will list all pods deployed in the default namespace. You should see an output like the following, indicating that the Nginx pod is running:

```bash
NAME    READY   STATUS    RESTARTS   AGE
nginx   1/1     Running   0          10s
```

1. Validate networking to pods by creating a service that forwards a port to the test pod:

```bash
kubectl port-forward pod/nginx 8080:80 --address=0.0.0.0
```

Now, open a browser and navigate to ‘**http://<your host IP>:8080**’. 

You should receive a response like the example provided.

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image7.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image7.png)

To end the port-forwarding, use the ‘**ctrl+c**’ key combination.

1. You can delete the Nginx pod that was set up for this test using the following command:

```bash
kubectl delete pod nginx
```

Congratulations! If all the above steps worked successfully, you now have a functional Kubernetes system ready to add services.

<aside>
💡 **See Appendix for adding additional worker nodes to the Kubernetes cluster.**

</aside>

## Adding Certificate Manager and Helm Installation

To ensure HTTPS certification for Rancher and any exposed applications, a certificate manager needs to be installed on your Kubernetes system. The Kubernetes certificate manager can be easily installed using an online manifest directly from the internet.

1. Install the Certificate Manager by applying the following command:

```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.11.0/cert-manager.yaml
```

This will install the Certificate Manager onto your Kubernetes cluster.

1. Install Helm, which is required for using Helm Charts for Kubernetes deployments. Helm is a tool that helps in configuring and distributing applications in Kubernetes.

> a. Download the Helm installation script using the following command:
> 

```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
```

> b. Make the script executable and run it by running:
> 

```bash
chmod 700 get_helm.sh
sudo ./get_helm.sh
```

<aside>
💡 *Enter your user password if prompted.*

</aside>

This script will download and install Helm on your system.

After completing these steps, you will have the Certificate Manager and Helm installed on your Kubernetes system, allowing you to manage certificates and utilize Helm Charts for deployments.

In the next sections, we will cover adding some quality-of-life services before proceeding to application services typically associated with self-hosted setups.

## Installing Metal Load Balancer

To simplify networking in Kubernetes, we will install MetalLB ([https://metallb.universe.tf/](https://metallb.universe.tf/)), a Load Balancer that can assign IP addresses to services. While cloud providers can automatically assign IP addresses, for a home server setup, MetalLB provides an easier solution. This guide will use a range of 10 IP addresses, specifically 172.31.199.91-172.31.199.99, based on the example IP used (172.31.199.90). Even though the range covers 10 addresses only 4 will be assigned during this guide.

1. Install the MetalLB manifest from the internet using the following command:

```bash
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.13.9/config/manifests/metallb-native.yaml
```

1. Define the range of IP addresses to be used by MetalLB by creating a file called ippool.yaml with the following contents. *Make sure to update the address range to match your network:*

```json
apiVersion: metallb.io/v1beta1
kind: IPAddressPool
metadata:
  name: first-pool
  namespace: metallb-system
spec:
  addresses:
  - 172.31.199.91-172.31.199.99
```

Use the nano text editor to create and save the file:

```bash
nano ippool.yaml
```

1. Create a file named advert.yaml with the following content to assign the IP address pool to be advertised by MetalLB:

```json
apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: example
  namespace: metallb-system
spec:
  ipAddressPools:
  - first-pool
```

Use the nano text editor to create and save the file:

```bash
nano advert.yaml
```

1. Apply the configuration files to Kubernetes using the following command:

```bash
kubectl apply -f ippool.yaml -f advert.yaml
```

1. Test and verify the MetalLB setup by creating a temporary pod and setting up a Load Balancer service:

```bash
kubectl create deploy nginx --image nginx
kubectl expose deploy nginx --port 80 --type LoadBalancer
kubectl get all
```

1. Verify that the EXTERNAL-IP field for the service/nginx shows an IP address from the specified range.

```bash
deployment.apps/nginx created
service/nginx exposed
NAME                        READY   STATUS              RESTARTS   AGE
pod/nginx-8f458dc5b-gs9nf   0/1     ContainerCreating   0          0s

NAME                 TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)        AGE
service/kubernetes   ClusterIP      10.43.0.1       <none>          443/TCP        20m
service/nginx        LoadBalancer   10.43.174.187   1**72.31.199.91**   80:30533/TCP   0s

NAME                    READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/nginx   0/1     1            0           0s

NAME                              DESIRED   CURRENT   READY   AGE
replicaset.apps/nginx-8f458dc5b   1         1         0       0s
```

1. Access the assigned IP address in your web browser to see the Nginx screen.

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image8.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image8.png)

1. Clean up the temporary deployment with the following commands:

```bash
kubectl delete service nginx
kubectl delete deploy nginx
```

<aside>
⛔ Note: Please make sure to replace the IP address range and adjust the commands accordingly based on your specific setup.

</aside>

## Traefik and the Need for Reverse Proxy

In a Kubernetes environment, managing incoming network traffic and directing it to the correct destinations is crucial. Traefik simplifies this process by acting as a traffic manager.

Traefik is a powerful tool that efficiently manages the flow of incoming network traffic in a Kubernetes cluster. It serves as an intermediary between users accessing the cluster from the internet and the internal services running within it. Traefik handles the distribution of incoming requests, ensures secure connections, and facilitates advanced routing and traffic management.

In summary, Traefik allows you to direct all traffic to a single IP address on specific HTTP/HTTPS ports and redirect it to various applications, regardless of the ports on which those services are running.

### Key Features of Traefik in Kubernetes:

1. Ingress Controller: Traefik functions as a traffic controller, determining where incoming requests should be directed based on predefined rules and configurations. It identifies which services should handle specific requests, such as serving web pages or processing API calls.
2. Load Balancing: Traefik evenly distributes incoming traffic across multiple instances of an application or service. This ensures that no single instance becomes overwhelmed with requests, maintaining overall performance and service availability.
3. SSL/TLS Termination: Traefik manages the encryption and decryption of secure connections (HTTPS) on behalf of your services. It simplifies the process of securing your applications with SSL/TLS certificates, enabling access through secure connections.
4. Dynamic Configuration: With Traefik, you can dynamically modify routing and load balancing configurations as services and endpoints change within the Kubernetes cluster. This adaptability ensures that traffic is always directed correctly without requiring manual updates.
5. Service Discovery: Traefik automatically discovers newly added services in the Kubernetes cluster. It keeps track of these services and their locations, eliminating the need for manual configuration whenever a new service is deployed.

By utilizing Traefik as a reverse proxy in your Kubernetes environment, you can benefit from its advanced routing, load balancing, and secure connection capabilities. Traefik simplifies the management of incoming network traffic, enhances application security, and ensures efficient distribution of requests to the appropriate services.

### Install Traefik

Traefik also has a helm chart, so its installation is very simple. It’s just three commands.

1. Add the Traefik Helm repository:

```bash
helm repo add traefik https://helm.traefik.io/traefik
```

1. Create a namespace for Traefik:

```bash
kubectl create ns traefik
```

1. Install Traefik using Helm:

```bash
helm install -n traefik traefik traefik/traefik
```

These commands will add the Traefik Helm repository, create a namespace called "traefik", and install Traefik into that namespace using Helm.

Traefik will take an IP address from MetalLB. To see what address it has you need to look at the service for Traefik. This command will do that:

```bash
kubectl get svc -A
```

That command lists ALL the services currently on the Kubernetes system.

```bash
NAMESPACE        NAME                   TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)                      AGE
default          kubernetes             ClusterIP      10.43.0.1       <none>          443/TCP                      21m
kube-system      kube-dns               ClusterIP      10.43.0.10      <none>          53/UDP,53/TCP,9153/TCP       21m
kube-system      metrics-server         ClusterIP      10.43.21.76     <none>          443/TCP                      21m
cert-manager     cert-manager           ClusterIP      10.43.146.40    <none>          9402/TCP                     16m
cert-manager     cert-manager-webhook   ClusterIP      10.43.36.197    <none>          443/TCP                      16m
metallb-system   webhook-service        ClusterIP      10.43.43.88     <none>          443/TCP                      15m
traefik          traefik                LoadBalancer   10.43.122.214   172.31.199.91   80:31086/TCP,443:32088/TCP   9s
```

# Setting up Services

## Prep

After going through the necessary preparation steps, it's finally time to install some services that you can use on your self-hosted setup. However, before diving into the service installations, there are two more initial steps to complete.

### Create a Namespace

Namespaces in Kubernetes are used for organizing and managing services in a group. The Kubernetes system already has several namespaces. There is kube-system, which is the namespace all the core Kubernetes elements are in, Cert-manager which is where the certification manger elements are, metallb-system and traefik for the MetalLB and Traefik elements respectively. To manage all the services effectively, it's recommended to create a dedicated namespace. This allows you to look up information about all the elements you are self-hosting in a single namespace. In this guide, we will use the namespace 'homeserver', but feel free to choose a different name if you prefer. Just keep in mind that the examples provided will use 'homeserver' as the namespace.

You can create the namespace using either of the following methods:

Method 1: Command Line Execute the following command to create the 'homeserver' namespace:

```bash
kubectl create ns homeserver
```

Method 2: Manifest File Alternatively, you can create a manifest file called 'namespace.yaml' using a text editor like nano. Add the following content to the file:

```json
apiVersion: v1
kind: Namespace
metadata:
  name: homeserver
```

Save the file and apply the manifest using the following command:

```bash
kubectl apply -f namespace.yaml
```

### Create a Certificate Issuer

Now that you have a namespace in place, you need to define the Let's Encrypt issuer certificate that will be used for any services accessed from outside your private network (i.e., over the internet). This is required for secure access of services over the internet.

This can be achieved by creating another manifest file, named 'issuer.yaml'. Use nano or any text editor to create the file and add the following content:

```json
apiVersion: cert-manager.io/v1
kind: Issuer
metadata:
  name: le-http
  namespace: homeserver
spec:
  acme:
    email: $EMAIL_ADDRESS
    server: https://acme-v02.api.letsencrypt.org/directory
    privateKeySecretRef:
      name: issuer-account-key
    solvers:
    - http01:
      ingress:
        class: traefik
```

**Make sure to replace $EMAIL_ADDRESS with your actual email address. If you skip this set you will not be able to issue SSL certs for https traffic**

Save the file and apply the manifest using the following command:

```bash
kubectl apply -f issuer.yaml
```

### Create Directories for file and data storage

Before proceeding, it's important to create two directories: one for storing Kubernetes manifest files which will allow you to keep all your configurations in one place, and another for saving data from deployed services so you have a single directory of data to back up to backup your services data.

1. Create a directory to store Kubernetes manifest files. In this guide, we will use the **~/kubernetes** directory as an example. Execute the following command to create the directory:

```bash
mkdir ~/kubernetes
```

1. Create a directory to store service data. For instance, we will use **/server** as the directory path. Use the following commands to create the directory and change its ownership:

```bash
sudo mkdir /server
sudo chown **user**: /server
```

**Replace user with your actual username.**

Note that you have the flexibility to use an external drive mounted at **/server** to expand your storage capacity or relocate your data to another location. Alternative methods of data access exist, but they are beyond the scope of this guide.

With these steps completed, you're now ready to proceed with installing the desired services on your self-hosted Kubernetes cluster

## Setting Up Services – Manifests

This section will contain manifests for services. Unless a manifest has something unique to it verses other manifests, that section will only contain the manifest.

In this section, you will find manifests for various services that can be deployed on your self-hosted Kubernetes cluster. Each manifest represents a specific service and provides the necessary configurations to deploy and manage that service within your cluster.

For manifests that share similar structures and settings, only the specific details and unique aspects will be highlighted in each section. This approach aims to provide a concise and focused view of each service, making it easier for you to understand and implement the desired services.

Simply locate the manifest for the service you wish to deploy and follow the instructions provided. If there are any specific considerations or additional steps required for a particular service, they will be clearly outlined within the respective manifest section.

Feel free to explore the various manifests and select the services that best suit your needs. As you go through each manifest, you'll gain a deeper understanding of the configurations and components required for deploying and managing services in your self-hosted Kubernetes environment.

### DNS – CoreDNS

CoreDNS is a versatile and lightweight DNS server that is commonly used in Kubernetes clusters to provide DNS-based service discovery and name resolution. As an integral part of the Kubernetes networking stack, CoreDNS offers a flexible and extensible DNS infrastructure for resolving domain names within the cluster. It replaces the traditional kube-dns component and offers enhanced functionality, including support for custom DNS configurations, plugin-based architecture, and seamless integration with other Kubernetes components. With CoreDNS, Kubernetes clusters can efficiently resolve DNS queries, facilitate communication between services, and enable seamless discovery of resources within the cluster environment.

In addition to the default instance of CoreDNS running within the Kubernetes system for internal networking, this guide will help you set up another instance of CoreDNS specifically for your private network. This customized CoreDNS instance will enable you to use DNS names for your home services, with the chosen DNS name being "server.home" throughout the examples. However, you have the flexibility to choose any DNS name with a ".home" suffix that suits your preference. By configuring CoreDNS in this manner, you can easily access and manage your home services using familiar DNS names within your private network environment.

CoreDNS needs a directory where it will store local configuration files for the application and for DNS entries. Create that directory.

```bash
mkdir -p /server/coredns/root
```

Next, use your preferred text editor, such as nano, to create and edit the Corefile file within the newly created directory:

```bash
nano /server/coredns/root/Corefile
```

The Corefile contains the configuration for CoreDNS. Here is an example configuration that you can customize:

```json
.:53 {
        forward . 8.8.8.8 1.1.1.1
        log
        errors
}

server.home:53 {
        file /root/dns.db
        log
        errors
}
```

In the above configuration:

- Lines 1-5 set up DNS forwarding to Google's 8.8.8.8 DNS server and the anonymous DNS 1.1.1.1 for any requests that CoreDNS cannot resolve internally.
- Lines 7-11 define the DNS for the home network with the domain name "server.home". If you choose a different domain name, make sure to update line 7 accordingly.

To create the DNS database file, execute the following command:

```bash
nano /server/coredns/root/dns.db
```

In the dns.db file, start with the following line, adjusting the server.home parts if you are using an alternative name:

```bash
server.home. IN SOA dns.server.home. user.server.home 2023122908 7200 3600 120966 3600
```

Then, on the subsequent lines, add the DNS entries for the services you are setting up or will set up. Here's an example for Rancher, a wiki service, and a dashboard service:

```bash
wiki.server.home. IN A 172.31.199.91
dashboard.server.home. IN A 172.31.199.91
```

Replace "172.31.199.91" with the IP address that Traefik is using from MetalLB. Save the file.

Together that would make the file look like this.

```bash
server.home. IN SOA dns.server.home. user.server.home 2023122908 7200 3600 120966 3600

wiki.server.home. IN A 172.31.199.91
dashboard.server.home. IN A 172.31.199.91
```

Whenever you add a new service, you can add a new entry line for it in the dns.db file and redeploy CoreDNS.

To properly organize the CoreDNS configuration, create a directory specifically for the CoreDNS manifest file. Execute the following command to create the directory:

```bash
mkdir ~/kubernetes/coredns
```

To create the manifest file for CoreDNS, execute the following command:

```bash
nano ~/kubernetes/coredns/manifest.yaml
```

Paste the following contents into the manifest file:

```json
apiVersion: v1
kind: Service
metadata:
  name: coredns-udp
  namespace: homeserver
spec:
  ports:
  - name: web
    port: 53
    targetPort: web
    protocol: UDP
  selector:
    app: coredns
  type: LoadBalancer
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: coredns
  namespace: homeserver
  labels:
    app: coredns
spec:
  replicas: 1
  selector:
    matchLabels:
      app: coredns
  template:
    metadata:
      labels:
        app: coredns
    spec:
      hostname: coredns
      containers:
      - name: coredns
        ports:
        - name: web
          containerPort: 53
          protocol: UDP
        image: coredns/coredns
        args:
        - -conf
        - /root/Corefile
        volumeMounts:
        - name: coredns-root
          mountPath: '/root'
    volumes:
    - name: coredns-root
      hostPath:
        path: '/server/coredns/root'
        type: Directory
```

This manifest file consists of two sections: Service and Deployment.

The Service section creates a LoadBalancer-backed port entry for UDP traffic on port 53, which is used for DNS communication. It assigns one of the MetalLB IPs to this service based on the selector information.

The Deployment section ensures that there is always one instance of CoreDNS running. It uses the coredns/coredns container image and adds the arguments **-conf /root/Corefile** to the CoreDNS executable. It also specifies a volume at **/server/coredns/root** that should be mounted at the path **/root** in the container.

To apply this manifest to Kubernetes, use the following command:

```bash
kubectl apply -f ~/kubernetes/coredns/manifest.yaml
```

After setting up the services, you need to update the DNS of any system you want to use these addresses on your network. You can refer to the provided link for instructions on how to change the DNS server on Windows and Mac systems. You can check the all services command to see what IP address MetalLB gave CoreDNS:

```bash
kubectl get svc -A
```

```bash
NAMESPACE        NAME                   TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)                      AGE
default          kubernetes             ClusterIP      10.43.0.1       <none>          443/TCP                      197d
kube-system      kube-dns               ClusterIP      10.43.0.10      <none>          53/UDP,53/TCP,9153/TCP       197d
kube-system      metrics-server         ClusterIP      10.43.29.172    <none>          443/TCP                      197d
cert-manager     cert-manager           ClusterIP      10.43.247.5     <none>          9402/TCP                     197d
cert-manager     cert-manager-webhook   ClusterIP      10.43.73.34     <none>          443/TCP                      197d
metallb-system   webhook-service        ClusterIP      10.43.232.252   <none>          443/TCP                      197d
traefik          traefik                LoadBalancer   10.43.30.25     172.31.199.91   80:32611/TCP,443:30861/TCP   197d
homeserver       **coredns**-udp            LoadBalancer   10.43.167.38    **172.31.199.92**   53:30085/UDP                 197d
```

How to update your DNS

[[https://www.hellotech.com/guide/for/how-to-change-dns-server-windows-mac](https://www.hellotech.com/guide/for/how-to-change-dns-server-windows-mac)]

(Windows and Mac instructions)

Once the services are set up in the following sections, you can access them using the following URLs:

- [http://wiki.server.home](http://wiki.network.home/)
- [http://dashboard.server.home](http://dashboard.network.home/)

To refresh the CoreDNS service you will need to scale down and backup its replica sets. Replica sets are how many copies of a pod should be running at one time. For anything with a database of any type, unless the application is designed for it, the replica count should be 1. All deployments in this guide use a replica count of 1. You can redeploy a service by scaling the replica count down to 0, and then back up to 1.

```bash
kubectl scale -n homeserver deploy/coredns --replicas=0
```

```bash
kubectl scale -n homeserver deploy/coredns --replicas=1
```

*See the ‘Adding Rancher: Simplifying Kubernetes Management’ for how to redeploy with the Rancher GUI.*

### Wiki – WikiJS

Wiki.js is an open-source application for creating collaborative documentation websites, knowledge bases, and wikis. It offers a user-friendly interface, Markdown-based editing, and support for rich media embedding and version control. Wiki.js is highly customizable with plugins and responsive across devices. It provides powerful search capabilities and supports multiple languages. In this section, you will learn how to install and set up Wiki.js in your self-hosted Kubernetes environment.

Wiki.js will require two directories for storing permeant data. Create those directories.

```bash
mkdir -p /server/wiki/config
mkdir -p /server/wiki/data
```

To store the Wiki.js manifest, create a directory named "wiki" within your "~/kubernetes" directory:

```bash
mkdir ~/kubernetes/wiki
```

Next, use an editor like nano to create a "manifest.yaml" file in the "wikijs" directory:

```bash
nano ~/kubernetes/wiki/manifest.yaml
```

Paste the following contents into the "manifest.yaml" file:

```bash
apiVersion: v1 
kind: Service 
metadata: 
 name: wikijs 
 namespace: homeserver 
spec: 
 ports: 
   - name: web 
     port: 3000 
     targetPort: web 
 selector: 
   app: wikijs 
--- 
apiVersion: apps/v1 
kind: Deployment 
metadata: 
  name: wikijs 
  namespace: homeserver 
  labels: 
    app: wikijs 
spec: 
  replicas: 1 
  selector: 
    matchLabels: 
      app: wikijs 
  template: 
    metadata: 
      labels: 
        app: wikijs 
    spec: 
      containers: 
        - name: wikijs 
          ports: 
           - name: web 
             containerPort: 3000 
          image: lscr.io/linuxserver/wikijs 
          volumeMounts: 
            - name: wikijs-config 
              mountPath: "/config" 
            - name: wikijs-data 
              mountPath: "/data" 
      volumes: 
        - name: wikijs-config 
          hostPath: 
            path: "/server/wiki/config/" 
            type: Directory 
        - name: wikijs-data 
          hostPath: 
            path: "/server/wiki/data/" 
            type: Directory 
--- 
apiVersion: networking.k8s.io/v1 
kind: Ingress 
metadata: 
 name: wikijs 
 namespace: homeserver 
 annotations: 
   cert-manager.io/issuer: "le-http" 
spec: 
 rules: 
   - host: wiki.server.home 
     http: 
       paths: 
         - path: / 
           pathType: Prefix 
           backend: 
             service: 
               name: wikijs 
               port: 
                 name: web
```

This manifest file consists of three sections: Service, Ingress, and Deployment.

The Service section defines the service for Wiki.js, specifying the port and targetPort for web traffic. Note that this isn’t using a LoadBalancer type, so an IP address will not be assigned for this service.

The Deployment section ensures that there is always one instance of Wiki.js running, using the lscr.io/linuxserver/wikijs container image. It also includes volume mounts for configuration and data directories.

The Ingress section defines how Traefik will handle incoming requests to the Wiki.js system, specifically mapping the host "wiki.server.home" to the Wiki.js service. This is actually how the service will be accessed.

Once the manifest file is created, you can apply it to Kubernetes to deploy Wiki.js:

```bash
kubectl apply -f ~/kubernetes/wiki/manifest.yaml
```

Make sure to update the DNS settings of your system to resolve the "http://wiki.server.home" address to the IP address of your server.

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image9.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image9.png)

Enter your email address and set a password. For site URL use [http://wiki.server.home*](http://wiki.server.home*/). Click ‘INSTALL’ at the bottom.

- If you are using something other than server.home for your private domain update.

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image10.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image10.png)

Wiki will create its database and redirect to the login page. This is where your email address and password from the previous step is your login.

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image11.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image11.png)

From here you can proceed to create your wiki homepage or enter the administration menu. Wiki.js is a very straight forward wiki app to use. If you need more documentation it can be found at [https://docs.requarks.io/](https://docs.requarks.io/).

### Dashboard – Homer

Homer is a versatile and user-friendly web-based dashboard application designed to help you organize and access your favorite websites, services, and tools from a centralized location. With Homer, you can create custom tiles and categories to represent each resource, allowing for a personalized and visually appealing dashboard. Whether you want quick access to social media platforms, productivity tools, news websites, or any other online destinations, Homer makes it convenient to navigate through your digital world with ease. By providing a unified interface for all your frequently used resources, Homer simplifies your online experience and enhances productivity.

To set up Homer, you need to create a directory to store its data. You can do this by running the following command:

```bash
mkdir -p /server/homer/
```

To store the Homer manifest, create a directory named "homer" within your "~/kubernetes" directory:

```bash
mkdir ~/kubernetes/homer
```

Next, you'll create a manifest file for Homer in the "~/kubernetes/homer" directory using an editor like nano:

```bash
nano ~/kubernetes/homer/manifest.yaml
```

Paste the provided manifest contents into the "manifest.yaml" file. This manifest file includes configurations for the Service, Deployment, and Ingress sections, defining the deployment of Homer in your Kubernetes cluster.

```bash
apiVersion: v1 
kind: Service 
metadata: 
 name: homer 
 namespace: homeserver 
spec: 
 ports: 
   - name: web 
     port: 8080 
     targetPort: web 
 selector: 
   app: homer 
--- 
apiVersion: apps/v1 
kind: Deployment 
metadata: 
  name: homer 
  namespace: homeserver 
  labels: 
    app: homer 
spec: 
  replicas: 1 
  selector: 
    matchLabels: 
      app: homer 
  template: 
    metadata: 
      labels: 
        app: homer 
    spec: 
      containers: 
        - name: homer 
          ports: 
           - name: web 
             containerPort: 8080 
          image: b4bz/homer 
          volumeMounts: 
            - name: homer-config 
              mountPath: "/www/assets" 
      volumes: 
        - name: homer-config 
          hostPath: 
            path: "/server/homer" 
            type: Directory 
--- 
apiVersion: networking.k8s.io/v1 
kind: Ingress 
metadata: 
 name: homer 
 namespace: homeserver 
 annotations: 
   cert-manager.io/issuer: "le-http" 
spec: 
 rules: 
   - host: dashboard.server.home 
     http: 
       paths: 
         - path: / 
           pathType: Prefix 
           backend: 
             service: 
               name: homer 
               port: 
                 name: web
```

Once the manifest file is created, you can apply it to your Kubernetes cluster using the following command:

```bash
kubectl apply -f ~/kubernetes/homer/manifest.yaml
```

Homer is configured via a static yaml file in its data directory.

You can create or edit the file /server/home/config.yml to configure what Homer looks like.

```bash
nano /server/homer/config.yml
```

You can copy and paste the provided configuration and adjust the title, subtitle, logo, colors, and services based on your needs.

```toml
--- 
# Homepage configuration 
# See https://fontawesome.com/icons for icons options 
 
title: "Self-Hosted Services" 
subtitle: "Services" 
logo: "logo.png" 
# icon: "fas fa-skull-crossbones" # Optional icon 
 
header: false 
footer: false 
columns: 3 
 
# Optional theme customization 
theme: default 
colors: 
  light: 
    highlight-primary: "#3367d6" 
    highlight-secondary: "#4285f4" 
    highlight-hover: "#5a95f5" 
    background: "#f5f5f5" 
    card-background: "#ffffff" 
    text: "#363636" 
    text-header: "#ffffff" 
    text-title: "#303030" 
    text-subtitle: "#424242" 
    card-shadow: rgba(0, 0, 0, 0.1) 
    link: "#3273dc" 
    link-hover: "#363636" 
  dark: 
    highlight-primary: "#3367d6" 
    highlight-secondary: "#4285f4" 
    highlight-hover: "#5a95f5" 
    background: "#131313" 
    card-background: "#2b2b2b" 
    text: "#eaeaea" 
    text-header: "#ffffff" 
    text-title: "#fafafa" 
    text-subtitle: "#f5f5f5" 
    card-shadow: rgba(0, 0, 0, 0.4) 
    link: "#3273dc" 
    link-hover: "#ffdd57" 
 
links: [] 
# Services 
# First level array represent a group. 
# Leave only an "items" key if not using group (group name, icon & tagstyle are optional, section separation will not be displayed). 
services: 
  - name: "Monitoring" 
    icon: "fas fa-signal" 
    items: 
      - name: "Tautulli" 
        logo: "assets/icons/tautulli.png" 
        subtitle: "Plex monitoring" 
        url: "http://plex.server.home" 
        target: "_blank" 
      - name: "Diskover" 
        logo: "assets/icons/diskover.png" 
        subtitle: "Space use monitoring" 
        url: "http://disk.server.home" 
        target: "_blank" 
  - name: "Services" 
    icon: "fas fa-cloud" 
    items: 
      - name: "NextCloud" 
        logo: "assets/icons/nextcloud.png" 
        subtitle: "File storage" 
        url: "http://nextcloud.server.home" 
        target: "_blank" 
      - name: "Duplicati" 
        logo: "assets/icons/duplicati.png" 
        subtitle: "Backup service" 
        url: "http://backup.server.home" 
        target: "_blank" 
      - name: "Ghost" 
        logo: "assets/icons/ghost.png" 
        subtitle: "Blog" 
        url: "https://blog.server.home/ghost" 
        target: "_blank" 
      - name: "Wikijs" 
        logo: "assets/icons/wikijs.png" 
        subtitle: "Wiki" 
        url: "http://wiki.server.home" 
        target: "_blank" 
      - name: "Sabnzbd" 
        logo: "assets/icons/sabnzbd.png" 
        subtitle: "Usenet downloads" 
        url: "http://sabnzbd.server.home" 
        target: "_blank" 
  - name: "Management" 
    icon: "fas fa-desktop" 
    items: 
      - name: "Rancher" 
        logo: "assets/icons/rancher.png" 
        subtitle: "Docker management" 
        url: "https://rancher.server.home" 
        target: "_blank" 
      - name: "Plex" 
        logo: "assets/icons/plex.png" 
        subtitle: "Plex manager" 
        url: "http://172.31.199.93:32400" 
        target: "_blank" 
  - name: "DevOps" 
    icon: "fas fa-code-branch" 
    items: 
      - name: "Gitea" 
        logo: "assets/icons/gitea.png" 
        subtitle: "Git repo" 
        url: "http://git.server.home" 
        target: "_blank" 
  - name: "Reading" 
    icon: "fas fa-book" 
    items: 
      - name: "Calibre-Web" 
        logo: "assets/icons/calibre-web.png" 
        subtitle: "Books" 
        url: "http://books.server.home" 
        target: "_blank" 
      - name: "Ubooquity" 
        logo: "assets/icons/ubooquity.png" 
        subtitle: "Comics" 
        url: "http://comics.server.home" 
        target: "_blank" 
  - name: "Media Acquisition" 
    icon: "fas fa-search" 
    items: 
      - name: "Sonarr" 
        logo: "assets/icons/sonarr.png" 
        subtitle: "TV search" 
        url: "http://sonarr.server.home" 
        target: "_blank" 
      - name: "Radarr" 
        logo: "assets/icons/radarr.png" 
        subtitle: "Movie search" 
        url: http://radarr.server.home 
        target: "_blank"
```

This configuration also should show how you can edit the page to your liking. All existing entries will be covered by this guide and will have their DNS added to CoreDNS. If you are not using ‘server.home’ update that for all links. You will also need to update the IP addresses that Rancher and Plex are assigned by MetalLB

Once you've made the desired changes to the config.yml file, save the file and Homer will reflect the updated configuration.

With Homer set up and configured, you can access your personalized dashboard by visiting the specified hostname ([http://dashboard.server.home](http://dashboard.server.home/)) in your browser. It provides a convenient way to access and manage your frequently used services and resources from a single location.

You will see that there are no icons showing. Homer does not ship with any icons. However, adding them is easy and will only take three commands.

```bash
sudo apt install git -y
git clone https://github.com/walkxcode/dashboard-icons
mv dashboard-icons/png/* /server/homer/icons/
```

### Cloud file storage – NextCloud

NextCloud is a robust cloud file management system that enables you to store, synchronize, and share files across multiple devices and users. With NextCloud, you can create your own private cloud storage solution, providing a secure and efficient way to manage your files and collaborate with others. Whether you need to store personal documents, share files with colleagues, or collaborate on projects, NextCloud offers the features and flexibility to meet your file management needs.

To set up NextCloud in your Kubernetes environment, you can follow the steps outlined below:

1. Create a directory to store NextCloud data and another directory to create the database files. You can use the following commands to create the directories:

```bash
mkdir -p /server/nextcloud/data
mkdir -p /server/nextcloud/db
```

1. Create a directory for the NextCloud manifest file, then create the manifest file for NextCloud in that directory using an editor like nano:

```bash
mkdir ~/kubernetes/nextcloud
```

```bash
nano ~/kubernetes/nextcloud/manifest.yaml
```

1. Paste the NextCloud manifest contents into the "manifest.yaml" file. The manifest includes configurations for the Service, Deployment, and Ingress sections, defining the deployment of NextCloud in your Kubernetes cluster. The Deployment section, which defines what a NextCloud pod will look like, has two containers defined, instead of one. The two containers are the NextCloud application container and a database application container.

```json
apiVersion: v1 
kind: Service 
metadata: 
 name: nextcloud 
 namespace: homeserver 
spec: 
 ports: 
   - name: web 
     port: 80 
     targetPort: web 
   - name: db 
     port: 3306 
     targetPort: db 
 selector: 
   app: nextcloud 
--- 
apiVersion: apps/v1 
kind: Deployment 
metadata: 
 name: nextcloud 
 namespace: homeserver 
spec: 
 selector: 
   matchLabels: 
     app: nextcloud 
 template: 
   metadata: 
     labels: 
       app: nextcloud 
   spec: 
     containers: 
       - name: web 
         image: nextcloud 
         volumeMounts: 
          - name: nextcloud-data 
            mountPath: "/var/www/html" 
         ports: 
           - name: web 
             containerPort: 80 
         env: 
           - name: MYSQL_PASSWORD 
             value: '$MYSQL_PASSWORD' 
           - name: MYSQL_DATABASE 
             value: nextcloud 
           - name: MYSQL_USER 
             value: nextcloud 
           - name: MYSQL_HOST 
             value: '127.0.0.1' 
       - name: db 
         #image: mariadb:10.1 
         image: mariadb 
         ports: 
           - name: db 
             containerPort: 3306 
         env: 
           - name: MYSQL_ROOT_PASSWORD 
             value: '$MYSQL_PASSWORD' 
           - name: MYSQL_USER 
             value: nextcloud 
           - name: MYSQL_PASSWORD 
             value: '$MYSQL_PASSWORD' 
           - name: MYSQL_DATABASE 
             value: nextcloud 
         volumeMounts: 
          - name: mariadb-db 
            mountPath: "/var/lib/mysql/" 
     volumes: 
      - name: nextcloud-data 
        hostPath: 
          path: "/server/nextcloud/data/" 
          type: Directory 
      - name: mariadb-db 
        hostPath: 
          path: "/server/nextcloud/db/" 
          type: Directory 
--- 
apiVersion: networking.k8s.io/v1 
kind: Ingress 
metadata: 
 name: nextcloud 
 namespace: homeserver 
 annotations: 
   cert-manager.io/issuer: "le-http" 
spec: 
 rules: 
   - host: nextcloud.server.home 
     http: 
       paths: 
         - path: / 
           pathType: Prefix 
           backend: 
             service: 
               name: nextcloud 
               port: 
                 name: web
```

<aside>
⛔ **update** '$MYSQL_PASSWORD' **To a password of your choosing**

</aside>

1. Apply the manifest to your Kubernetes cluster using the following command:

```bash
kubectl apply -f ~/kubernetes/nextcloud/manifest.yaml
```

1. In the manifest, ‘nextcloud.server.home’ is specified as the URL for the web access to NextCloud, so that needs to be added to your CoreDNS configuration. You can use the echo command to insert information into the file.

```bash
echo 'nextcloud.server.home. IN A 172.31.199.91' >> /server/coredns/root/dns.db
```

1. Be sure to scale the CoreDNS deployment down and back up to have it re-read the dns.db file.

```bash
kubectl scale -n homeserver deploy/coredns --replicas=0
kubectl scale -n homeserver deploy/coredns --replicas=1
```

1. When first starting NextCloud will take a few minutes for the database application to complete its startup, but after that time you can access NextCloud with its URL [http://nextcloud.sever.home](http://nextcloud.sever.home/)

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image12.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image12.png)

1. Create a username and password for your account. This account will also be the admin for NextCloud. After entering a username and password click Install to allow NextCloud to create the necessary database components.
    
    ![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image13.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image13.png)
    
2. For now, click the ‘Skip’ option for Recommended apps. They can be installed later if you want them.
    
    ![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image14.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image14.png)
    
3. Once logged in as an admin account, you can create user accounts, set up libraries, and define access permissions for users and groups. NextCloud provides a user-friendly interface with features such as file versioning, file locking, collaboration tools, and integration with desktop and mobile clients.

NextCloud also offers advanced features like file syncing, sharing links, online document editing, and encrypted libraries for enhanced security. You can explore these features and configure NextCloud according to your specific requirements.

By deploying NextCloud in your Kubernetes environment, you can have full control over your cloud file management solution, ensuring data privacy, security, and seamless collaboration among users. Whether you need personal file storage, team collaboration, or a central repository for your organization, NextCloud provides a reliable and scalable solution for effective file management.

### Backups – Duplicati

Before delving deeper, it is essential to discuss the importance of backing up your information. When you manage a self-hosted server, the responsibility for data protection falls on your shoulders, and the loss of that data can have severe consequences. To address this crucial need, utilizing a backup application is highly recommended. In this context, Duplicati emerges as the ideal choice.

Duplicati is an open-source backup solution that offers robust and efficient data protection for your files and folders. With its intuitive user interface, it provides a seamless experience for users. The versatility of Duplicati is evident through its support for a wide range of storage destinations, including local drives, network shares, and popular cloud storage services like Amazon S3 and Google Drive, among others. This flexibility allows users to choose the most convenient and secure storage option for their backups.

One of Duplicati's notable features is its ability to create automated backup schedules, ensuring that your data is consistently protected without requiring manual intervention. Additionally, it supports incremental and differential backups, which intelligently save storage space by only backing up changes since the last backup. The option to encrypt your data adds an extra layer of security, ensuring that your sensitive information remains confidential.

Duplicati goes beyond the basics and offers advanced options such as backup versioning, deduplication, and compression. These features optimize storage utilization, minimize backup time, and provide additional reliability to your backup strategy.

To set up Duplicati in your Kubernetes environment, you can follow the steps outlined below:

1. Create a directory to store Duplicati configuration data. You can use the following command to create the directory:

```bash
mkdir -p /server/duplicati/config
```

1. Create a directory and manifest file for Duplicati in the "~/kubernetes/duplicati" directory using an editor like nano:

```bash
mkdir ~/kubernetes/duplicati
```

```bash
nano ~/kubernetes/duplicati/manifest.yaml
```

1. Paste the Duplicati manifest contents into the "manifest.yaml" file. The manifest includes configurations for the Service, Deployment, and Ingress sections, defining the deployment of Duplicati in your Kubernetes cluster.

```json
apiVersion: v1 
kind: Service 
metadata: 
 name: duplicati 
 namespace: homeserver 
spec: 
 ports: 
   - name: web 
     port: 8200 
     targetPort: web 
 selector: 
   app: duplicati 
--- 
apiVersion: apps/v1 
kind: Deployment 
metadata: 
 name: duplicati 
 namespace: homeserver 
spec: 
 selector: 
   matchLabels: 
     app: duplicati 
 template: 
   metadata: 
     labels: 
       app: duplicati 
   spec: 
     containers: 
       - name: backup 
         image: linuxserver/duplicati 
         volumeMounts: 
          - name: duplicati-config 
            mountPath: "/config" 
          - name: duplicati-source 
            mountPath: "/source" 
         ports: 
           - name: web 
             containerPort: 8200 
         env: 
           - name: PUID 
             value: '1000' 
           - name: PGID 
             value: '1000' 
           - name: TZ 
             value: EST5EDT 
     volumes: 
        - name: duplicati-source 
          hostPath: 
            path: "/server/" 
            type: Directory 
        - name: duplicati-config 
          hostPath: 
            path: "/server/duplicati/config" 
            type: Directory 
--- 
apiVersion: networking.k8s.io/v1 
kind: Ingress 
metadata: 
 name: duplicati 
 namespace: homeserver 
 annotations: 
   cert-manager.io/issuer: "le-http" 
spec: 
 rules: 
   - host: backup.server.home 
     http: 
       paths: 
         - path: / 
           pathType: Prefix 
           backend: 
             service: 
               name: duplicati 
               port: 
                 name: web
```

1. Apply the manifest to your Kubernetes cluster using the following command:

```toml
kubectl apply -f ~/kubernetes/duplicati/manifest.yaml
```

1. In the manifest, ‘backup.server.home’ is specified as the URL for the web access to Duplicati, so that needs to be added to your CoreDNS configuration. You can use the echo command to insert information into the file.

```bash
echo 'backup.server.home. IN A 172.31.199.91' >> /server/coredns/root/dns.db
```

1. Be sure to scale the CoreDNS deployment down and back up to have it re-read the dns.db file.

```bash
kubectl scale -n homeserver deploy/coredns --replicas=0
kubectl scale -n homeserver deploy/coredns --replicas=1
```

1. Now you can access the Duplicati interface in a browser at [http://backup.server.home](http://backup.server.home/).

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image15.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image15.png)

1. If you select “No, my machine has only a single account” then no password security will be added to Duplicati. You should instead select “Yes”.
    
    ![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image16.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image16.png)
    
2. Check the box for “Password” and enter a password to be used twice then scroll to the bottom of the page and click “OK”. If you did this right you will get a “Not logged in” error and you will have to enter the password you just set.
3. Click “+ Add backup” from the menu on the left-hand side and with “Configure a new backup” selected click “Next >”
4. Give the backup a Name and Description if you want. Also set a Passphrase. This is the password for this backup’s encryption. You can randomly generate the Passphrase but if you do, write it down.

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image17.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image17.png)

1. From here you will need to select where you want to backup to. That could be a local directory, or it could be a paid for cloud service. If looking to have an off site backup, [https://backblaze.com](https://backblaze.com/) has a B2 object service that is very cheap. The first 10 gigs are free and then it costs around 1 dollar per month per 100 gigs you backup. Because there are so many options for setting up backups the rest of the setup will need to be handled on your own. Documentation for Duplicati is at [https://duplicati.readthedocs.io/en/latest/](https://duplicati.readthedocs.io/en/latest/)
2. No matter the backup destination, the “Source Data” in Duplicati will be under ‘Computer -> source’. This will point to your /server directory where your services data and user files are stored.

### File Use Reporting – Diskover

### Private Git Hub – Gitea

### Media Streaming – PLEX

Plex is a powerful media server platform that allows you to organize, stream, and enjoy your personal media collection across various devices. With Plex, you can easily manage your movies, TV shows, music, photos, and more, making it a central hub for all your entertainment needs. Plex provides a user-friendly interface, extensive media library management features, and support for streaming to different devices, including smartphones, tablets, smart TVs, and streaming devices.

To set up Plex in your Kubernetes environment, you can follow the steps outlined below:

Plex requires a persistent storage volume to store media files and metadata. You can configure a persistent volume and persistent volume claim to ensure data persistence across container restarts.

1. Create directories to store Plex configuration data, transcodes, and media. You can use the following command to create the directory:

```bash
mkdir -p /server/plex/config
mkdir -p /server/plex/transcode
mkdir -p /server/media/tv
mkdir -p /server/media/movies
```

1. Create a manifest file for Plex in the "~/kubernetes/plex" directory using an editor like nano:

```bash
nano ~/kubernetes/plex/manifest.yaml
```

1. Paste the Plex manifest contents into the "manifest.yaml" file. The manifest includes configurations for the Service, Deployment, and Ingress sections, defining the deployment of Plex in your Kubernetes cluster.

```bash
--- 
apiVersion: apps/v1 
kind: Deployment 
metadata: 
  labels: 
    app: plexserver                
  name: plexserver                 
  namespace: homeserver            
spec: 
  replicas: 1                      
  revisionHistoryLimit: 0 
  selector: 
    matchLabels: 
      app: plexserver 
  strategy: 
    rollingUpdate: 
      maxSurge: 0                  
      maxUnavailable: 1            
    type: RollingUpdate            
  template: 
    metadata: 
      labels: 
        app: plexserver 
    spec: 
      volumes: 
      - name: plex-config 
        hostPath: 
          path: "/plex/config/" 
          type: Directory      
      - name: plex-media 
        hostPath: 
          path: "/docker/media/" 
          type: Directory 
      - name: plex-transcode 
        hostPath: 
          path: "/plex/transcode/" 
          type: Directory 
      containers: 
      - env:                        
        - name: PLEX_CLAIM 
          value: $CLAIM 
        - name: PGID 
          value: '1000' 
        - name: PUID 
          value: '1000' 
        - name: VERSION 
          value: latest 
        - name: TZ 
          value: EST5EDT 
        image: plexinc/pms-docker    
        imagePullPolicy: Always     
        name: plexserver            
        ports: 
        - containerPort: 32400      
          name: pms-web             
          protocol: TCP 
        - containerPort: 32469 
          name: dlna-tcp 
          protocol: TCP 
        - containerPort: 1900 
          name: dlna-udp 
          protocol: UDP 
        - containerPort: 3005 
          name: plex-companion 
          protocol: TCP 
        - containerPort: 5353 
          name: discovery-udp 
          protocol: UDP 
        - containerPort: 8324 
          name: plex-roku 
          protocol: TCP 
        - containerPort: 32410 
          name: gdm-32410 
          protocol: UDP 
        - containerPort: 32412 
          name: gdm-32412 
          protocol: UDP 
        - containerPort: 32413 
          name: gdm-32413 
          protocol: UDP 
        - containerPort: 32414 
          name: gdm-32414 
          protocol: UDP 
        resources: {} 
        stdin: true 
        tty: true 
        volumeMounts:             
        - mountPath: /config      
          name: plex-config 
        - mountPath: /data 
          name: plex-media 
        - mountPath: /transcode 
          name: plex-transcode 
      restartPolicy: Always 
--- 
kind: Service 
apiVersion: v1 
metadata: 
  name: plex-udp       
  namespace: homeserver 
  annotations: 
    metallb.universe.tf/allow-shared-ip: plexserver  
spec: 
  selector: 
    app: plexserver 
  ports: 
  - port: 1900       
    targetPort: 1900 
    name: dlna-udp  
    protocol: UDP 
  - port: 5353 
    targetPort: 5353 
    name: discovery-udp 
    protocol: UDP 
  - port: 32410 
    targetPort: 32410 
    name: gdm-32410 
    protocol: UDP 
  - port: 32412 
    targetPort: 32412 
    name: gdm-32412 
    protocol: UDP 
  - port: 32413 
    targetPort: 32413 
    name: gdm-32413 
    protocol: UDP 
  - port: 32414 
    targetPort: 32414 
    name: gdm-32414 
    protocol: UDP 
  type: LoadBalancer 
--- 
kind: Service 
apiVersion: v1 
metadata: 
  name: plex-tcp               
  namespace: homeserver        
  annotations: 
    metallb.universe.tf/allow-shared-ip: plexserver   
spec: 
  selector: 
    app: plexserver            
  ports: 
  - port: 32400                
    targetPort: 32400          
    name: pms-web              
    protocol: TCP 
  - port: 3005 
    targetPort: 3005 
    name: plex-companion 
  - port: 8324 
    name: plex-roku 
    targetPort: 8324 
    protocol: TCP 
  - port: 32469 
    targetPort: 32469 
    name: dlna-tcp 
    protocol: TCP 
  type: LoadBalancer 
--- 
apiVersion: networking.k8s.io/v1 
kind: Ingress 
metadata: 
 name: plexserver 
 namespace: homeserver 
 annotations: 
   cert-manager.io/issuer: "le-http" 
spec: 
 tls: 
   - hosts: 
       - plex-server.network.home 
     secretName: tls-plex-ingress-http 
 rules: 
   - host: plex-server.network.home 
     http: 
       paths: 
         - path: /web 
           pathType: Prefix 
           backend: 
             service: 
               name: plex-tcp 
               port: 
                 name: pms-web
```

<aside>
⛔ **You will need to replace the $CLAIM with a plex claim token.**

</aside>

Plex claim tokens allow you to associate a server with your account on first deployment. Claim tokens are only valid for around 5 minutes so get your claim and update the manifest right before you deploy it. On future work with the manifest, you do not need a new manifest unless you also delete the /server/plex directory. To get your claim token go to [https://www.plex.tv/claim](https://www.plex.tv/claim). After loging in you can copy the claim token to your manifest. A claim token will look like this ‘**claim-NLJSYEmsiFF67MWQgLtC**’

This manifest is longer than others because Plex needs so many ports directed to it for all of its networking features. There are also two services created for this deployment. One for the UDP network traffic and one for the TCP traffic. Don’t worry if you don’t know enough networking to know what those are, just be aware that two services, that share one IP from MetalLB are deployed.

1. Apply the manifest to your Kubernetes cluster using the following command:

```bash
kubectl apply -f ~/kubernetes/plex/manifest.yaml
```

1. After applying the manifest, Plex will be deployed and assigned an IP by MetalLB.
2. To access the Plex web interface, open a browser and visit the specified hostname or IP address. From there, you can sign in with your Plex account or create a new one if you don't have an existing account.
3. Once logged in, you can configure and manage your media library by adding your media files, organizing them into libraries, and customizing various settings according to your preferences.

Plex provides a rich set of features, including support for transcoding, remote access, parental controls, synchronization with mobile devices, and integration with third-party plugins. You can explore these features and customize Plex to suit your media streaming and management needs.

By deploying Plex in your Kubernetes environment, you can enjoy a seamless and efficient media server solution that offers flexibility, scalability, and centralized control over your media collection.

### Media Streaming Monitor – Tautulli

Tautulli serves as a monitoring and analytics platform tailored for Plex Media Server users. It's an invaluable companion offering extensive insights and detailed statistics regarding your Plex server's activity. Through its intuitive dashboard, Tautulli tracks user behavior, including what media content has been accessed, who accessed it, and when. It goes beyond just logging plays; it captures comprehensive information about streaming quality, playback device details, and historical trends.

This tool empowers users by providing a wealth of data on media consumption patterns, allowing them to make informed decisions to enhance their Plex server's performance. Tautulli's notifications feature keeps users updated about newly added media, watched content, or specific user activities, ensuring an interactive and engaging Plex experience. Its customization options enable users to set specific triggers for notifications, ensuring a personalized and streamlined monitoring process.

Overall, Tautulli acts as a vital resource for Plex server owners, enabling them to optimize their media libraries, understand user preferences, and ensure a seamless streaming experience for themselves and their users.

To set up Tatulli, you need to create a directory to store its data. You can do this by running the following command:

```bash
mkdir -p /server/tautulli/config
```

To store the tautulli manifest, create a directory named "tautulli" within your "~/kubernetes" directory:

```bash
mkdir ~/kubernetes/tautulli
```

Next, you'll create a manifest file for Tautulli in the "~/kubernetes/tautulli" directory using an editor like nano:

```bash
nano ~/kubernetes/tautulli/manifest.yaml
```

Paste the provided manifest contents into the "manifest.yaml" file. This manifest file includes configurations for the Service, Deployment, and Ingress sections, defining the deployment of Homer in your Kubernetes cluster.

```bash
apiVersion: v1
kind: Service
metadata:
 name: tautulli
 namespace: homeserver
spec:
 ports:
   - name: web
     port: 8181
     targetPort: web
 selector:
   app: tautulli
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tautulli
  namespace: homeserver
  labels:
    app: tautulli
spec:
  replicas: 1
  selector:
    matchLabels:
      app: tautulli
  template:
    metadata:
      labels:
        app: tautulli
    spec:
      containers:
        - name: tautulli
          ports:
           - name: web
             containerPort: 8181
          image: linuxserver/tautulli
          volumeMounts:
            - name: tautulli-config
              mountPath: "/config"
      volumes:
        - name: tautulli-config
          hostPath:
            path: "/server/tautulli/config/"
            type: Directory
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
 name: tautulli
 namespace: homeserver
 annotations:
   cert-manager.io/issuer: "le-http"
spec:
 rules:
   - host: plex.server.home
     http:
       paths:
         - path: /
           pathType: Prefix
           backend:
             service:
               name: tautulli
               port:
                 name: web
```

Once the manifest file is created, you can apply it to your Kubernetes cluster using the following command:

```bash
kubectl apply -f ~/kubernetes/plex/manifest.yaml
```

1. In the manifest, ‘plex.server.home’ is specified as the URL for the web access to Tautulli, so that needs to be added to your CoreDNS configuration. You can use the echo command to insert information into the file.

```bash
echo 'plex.server.home. IN A 172.31.199.91' >> /server/coredns/root/dns.db
```

<aside>
⛔ Update the IP address 172.31.199.91 to your Traefik IP address

</aside>

1. Be sure to scale the CoreDNS deployment down and back up to have it re-read the dns.db file.

```bash
kubectl scale -n homeserver deploy/coredns --replicas=0
kubectl scale -n homeserver deploy/coredns --replicas=1
```

### Download Manager – Sabnzbd

### TV Show Manager – Sonarr

### Movie Manager – Radarr

### Ebook Manager/Reader – Calibre-Web

### Comic Book Reader – Ubooquity

### Blog – Ghost

### Gaming – Minecraft

# Adding Rancher: Simplifying Kubernetes Management

Kubernetes provides a powerful command-line interface for managing clusters, but many users prefer a Graphical User Interface (GUI) for a more intuitive and visual experience. While Kubernetes has its own dashboard application, this guide takes it a step further by recommending the community edition of Rancher ([www.rancher.com/community](http://www.rancher.com/community)).

The key feature Rancher is selected for is its user-friendly interface. Rancher's user interface simplifies the management and operation of Kubernetes clusters. It abstracts complex Kubernetes concepts and configurations, making it easier for both newcomers and experienced users to interact with the cluster.

To install Rancher using Helm, you first need to add the Rancher repository to Helm using the following command:

helm repo add rancher-latest https://releases.rancher.com/server-charts/latest

1. Namespace Organization: In Kubernetes, namespaces provide a way to divide and organize resources within a cluster. Rancher leverages namespaces to create separate scopes and environments within a single Kubernetes cluster. Each namespace has its own set of resources and policies that can be managed independently.

To create a namespace for Rancher, use the following command:

```bash
kubectl create ns cattle-system
```

1. Installation and Configuration: Once the namespace is created, Rancher can be installed using a Helm chart. Before installing, define a password for the chart to use. Set the password using the following command:

```bash
export RANCHER_PASSWORD=mypassword
```

<aside>
⛔ Replace 'mypassword' with the desired password.

</aside>

To install the Rancher deployment stack in the cattle-system namespace, use Helm:

```bash
helm install rancher rancher-latest/rancher --namespace cattle-system --set hostname=rancher.server.home --set bootstrapPassword=$RANCHER_PASSWORD
```

1. Load Balancer Configuration: Rancher automatically creates a service to expose itself to the network. However, for Kubernetes systems with MetalLB as the load balancer, it's recommended to use the LoadBalancer service type instead. Delete the old service and create a new one with the following commands:

```bash
kubectl -n cattle-system delete service rancher
kubectl -n cattle-system expose deploy rancher --port 443 --type LoadBalancer
```

To view the IP address assigned by the load balancer, use the following command within the cattle-system namespace:

```bash
kubectl -n cattle-system get service
```

```bash
NAME      TYPE           CLUSTER-IP    EXTERNAL-IP     PORT(S)         AGE 
rancher   LoadBalancer   10.43.26.25   172.31.199.91   443:30877/TCP   9s
```

## Using Rancher

Point your browser to the External-IP address that the rancher service is using. [https://172.31.199.91](https://172.31.199.91/)

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image18.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image18.png)

The password is the password you set RANCHER_PASSWORD to. On future logins you will be asked for a username as well, the default is ‘admin’.

For now, you can leave the Server URL as the IP address. You can change it later when DNS is setup for your services.

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image19.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image19.png)

Click on ‘local’ to select the Kubernetes system.

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image20.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image20.png)

Here you have some view into how much CPU and memory is being used, as well as how many total Pods are running.

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image21.png](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image21.png)

# Appendix

## External Web Access

###
