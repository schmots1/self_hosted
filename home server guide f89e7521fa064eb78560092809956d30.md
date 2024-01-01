# home server guide

![home%20server%20guide%20f89e7521fa064eb78560092809956d30/image1.jpeg](home%20server%20guide%20f89e7521fa064eb78560092809956d30/image1.jpeg)

# Introduction

Self-hosting an application involves running the service on a computer that you own. This computer can be either a physical machine or a virtual instance on a cloud provider like Amazon AWS or Oracle OCI. The beauty of self-hosting is that it grants you control over your applications, ranging from simple blog websites to browser-based computer desktops accessible from anywhere in the world.

One of the core benefits of self-hosting is data ownership. When using services like Dropbox, the company managing the service has full access to your files and may provide them to any party that requests them, even if the request appears semi-official. Moreover, free, and paid hosting providers, including Dropbox, collect vast amounts of information about you and sell it to third parties. In essence, your file storage is not their primary product…you are. By hosting all services, yourself, only you have access to your files, and there's no one to collect information about you.

Another advantage of self-hosting is cost efficiency. Instead of paying monthly fees for various services, which can quickly add up, you only incur the initial hardware costs and regular electricity and internet bills. Having your own server at home offers numerous perks, including the ability to tailor features to your needs, the security of knowing your files are in your possession, and the avoidance of subscription fees. Additionally, the pride of doing it yourself adds an extra sense of accomplishment.

Now, let's explore some of the applications you can run on your home server:

- Cloud storage: Set up your own file storage and syncing solution.
- Blog sites: Host your own blogs and have full control over their content.
- Media servers: Create your own internal streaming service for media consumption.
- Web-based book reading and management: Enjoy reading and organizing your eBooks via a web interface.
- Game servers: Host your own game servers, such as Minecraft, for a customized gaming experience.
- Download management and more: Take charge of downloading and managing files efficiently.

Many individuals find the idea of hosting their own applications intimidating due to a perceived lack of knowledge about the applications or server/computer management. That's precisely where this guide comes in. With step-by-step instructions and copy-and-paste examples, you'll swiftly get your self-hosted services up and running.

By the end of this guide, you'll have an impressive array of services running on your self-hosted system, including an eBook library, space usage reporting, backup services, blogging, a private git repository, media serving, graphical management, movie management, Usenet downloads, TV show management, and a private wiki.

Get ready to embark on a journey toward reclaiming control over your digital ecosystem and experiencing the true power of self-hosted applications on your very own home server. Let's dive in and make it happen!

## Virtual Machines vs Docker vs Kubernetes

When it comes to running multiple applications on a single host, there are various approaches to consider. One option is to install the applications directly and hope for the best in terms of avoiding conflicts. Another approach involves utilizing software that enables the creation of Virtual Machines (VMs), where each application resides on a separate VM. Alternatively, applications can be run as "microservices" within containers. In this guide, we will focus on the latter option and explore the utilization of Kubernetes for managing these containers. To gain a better understanding of this choice, let's delve into a comparison of VMs, Docker (containers), and Kubernetes.

### Virtual Machines: Overview and Benefits

Virtual Machines (VMs) are software that allows you to run programs and deploy applications. They are not physical hardware but rather software that provides computing resources. Multiple virtual machines can be run on a single physical machine, allowing for the simultaneous operation of different operating systems like macOS and Windows on the same computer. This eliminates the need for additional physical machines to accommodate different operating system requirements.

Virtual machines have gained wide popularity in both on-premises and cloud environments, as they offer convenience and flexibility. Various VM products have been developed and made available in the market.

### Containers: Overview and Benefits

A container is software that includes code and all its dependencies, enabling an application to run reliably across different computing environments. When you package an application into a container, you can deploy and run it on various devices, including personal computers and remote servers in the cloud. A container contains everything necessary for the application to run, making it compatible with any operating system and infrastructure.

The concept of a container can be likened to containers used in the shipping industry, where different cargoes are isolated. Similarly, each container in software contains a different application and its required dependencies. Once a container is built, it can be easily deployed to the desired environment.

### Docker: Introduction and Major Features

Docker, established in 2013, has become a prominent software and trademark for containerization. It provides OS-level virtualization to package applications and their dependencies into containers. Docker works on Linux, Windows, and Mac computers, allowing for the creation of virtual containers for different platforms.

Major Features of Docker

Docker's popularity as a Platform-as-a-Service (PaaS) software stems from its wide range of features, which include:

- Easy configuration of application environments, freeing users from infrastructure requirements.
- Isolated containers that do not interfere with each other.
- Complete independence of containers.
- User-friendly graphical interface (GUI) and command-line interface (CLI) support for container management.
- Overcoming hardware limitations and reducing the cost of physical infrastructure needed for running diverse applications.
- Lightweight and portable software suitable for microservices development.
- Creation of local microservice environments, such as coding for AWS Lambda functions.

### Kubernetes: Introduction and Major Features

Kubernetes is an open-source platform specifically designed for managing containers. By combining Kubernetes with Docker, developers and organizations can enhance the efficiency of application development and deployment.

Major Benefits of Kubernetes

Kubernetes has gained widespread adoption for managing infrastructures both on-premises and in the cloud. Some key benefits of using Kubernetes include:

- Increased productivity in managing applications across different environments, including AWS, Google Cloud Platform, and Microsoft Azure.
- Ability to apply updates to containers without downtime, ensuring application reliability and availability.
- Scalability of infrastructure without significant cost implications.
- Strong community support due to its widespread use.
- High flexibility and compatibility, enabling usage in private or public clouds.
- Support for multiple operating systems, such as Windows and Linux.

### Virtualization vs. Containerization: Understanding the Difference

Virtualization involves running an entire operating system and multiple applications within a virtual environment. In contrast, containerization, using tools like Docker, allows multiple containerized applications to share the same operating system of a server. Containers are more lightweight and consume fewer resources compared to virtual machines.

When considering the choice between virtualization and containerization, it's important to factor in the lifecycle of the application. Containers excel in scenarios where applications have shorter lifecycles due to their swift configuration and lightweight characteristics. They offer quick deployment, scalability, and efficient resource utilization. On the other hand, virtual machines are better suited for applications with longer lifecycles, even though they require more setup time and resources. In the context of self-hosted applications, containers prove advantageous due to their agility, ease of deployment, and ability to effectively manage resources, making them a favorable choice for hosting and running applications on your own infrastructure.

# Host Considerations for Kubernetes Installation

To start your journey of setting up a self-hosted home server, the first crucial decision is determining the platform on which you'll host your applications. While it is recommended to have a dedicated system for this purpose, separate from your everyday desktop, you can still run these solutions on the same computer. However, be aware that this approach may not work as effectively and can lead to some issues.

When planning to have an always-on system, there are several factors to consider even before exploring computer options or components. You should consider fan noise, power consumption (higher power usage means increased electricity bills), and heat generation.

Many individuals prefer small form-factor systems due to their low power draw, relatively quiet operation, and often affordable price range. For example, a quick search on Amazon yielded the GEEKOM MINI IT8 TECH system (link: [https://tinyurl.com/yh6ptams](https://tinyurl.com/yh6ptams)), which features an Intel Coffee Lake i5 8259U processor, Intel Iris Plus Graphics 655, 8/16GB dual-channel DDR4-3200 memory (expandable to 32GB), and storage options of 256GB/512GB SSD (with support for a 2.5" SATA HDD up to 2TB). It comes with Windows 11 Pro pre-installed and includes features like Bluetooth, dual-band Wi-Fi, HDMI2.0 and DisplayPort video outputs, Ethernet LAN, USB ports, and more. This system can serve as a suitable starting point for your self-hosted applications. However, feel free to explore other options that meet the following key criteria:

- Intel/AMD-based x86_64 processors: These processors offer greater compatibility with various services compared to ARM processors found in devices like Raspberry Pi.
- 16GB or more of RAM: This should be sufficient for most use cases unless you plan to host resource-intensive applications like multiple Minecraft game servers. You can go as low as 8GB of RAM, but it will limit how many services you can run and the performance of those you select.
- Hard drive: Aim for at least 256GB of storage, preferably in the form of an SSD for faster performance. External drives can be of any type.
- Wired network connection: While Wi-Fi can work, this guide doesn't cover its setup.
- USB thumb drive: You'll need a minimum of 4GB for the operating system installation.

If you're well-versed in system building, you can find an excellent hardware analysis and suggestions for speed and power draw considerations in this repository: [https://github.com/zilexa/Homeserver/blob/master/Recommendations.md](https://github.com/zilexa/Homeserver/blob/master/Recommendations.md).

Lastly, consider whether you want to access your services from outside your home network. If so, you'll need a few additional things:

- Access to your home router and the ability to edit port forwarding rules: Since router configurations vary, you may need to search online for instructions specific to your router model. For example, search for "Linksys 54GT port forwarding" if you own a Linksys 54GT router.
- Know your public IP address: You can easily find this by visiting a website like [https://showmyip.com](https://showmyip.com/). It will display your public IP address.
- Domain name: To access your services using a memorable address, you can purchase a domain name from a domain registrar like Cloudflare.com or set up a free subdomain using a service like Dynu.com. Keep in mind that free subdomains may reveal some information about your usage and traffic.

<aside>
💡 **For further instructions on accessing services outside your home network, refer to the Appendix in this guide.**

</aside>

Now that you have a clear understanding of the hardware considerations and external access requirements, let's move forward and setup the Operating System on your computer.

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

[data:image/png;base64,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YDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAADg/7d3JuDeVuPifv05OFGGlBSlWYNKpUgqyVihQQOaqGRoVigapGhUEYk0a0AqkYpCGlU0DxoIlZnq4Dgc/3Ovvmdb3/re9zfvvd+9931f17r2/r3jetd61rOe9axJREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdbwxAUXXPCAP/7xj9Xf/va36glPeMKswyIiIiLt4V//+tes/0RkFGj3i4iISJt5wqqrrvqve++9t8JpqeEiIiIibQNn5TLLLFMdcMAB1d///vdZR0VkEJ761KdWRxxxRHXttddq+4uIiEhr0WEpIiIirQaH5f/ZK9Xpp59e/fd///esoyIyCE972tOq973vfdXFF1+s7S8iIiKtRYeliIiItBoclqusskp18skn67AUGZK55pqr2nXXXatLL71U219ERERai5vuiIiIiIiIiIiISGvQYSkiIiIiIiIiIiKtQYeliIiITFn+8z//szr66KOrjTfeuNpwww1T2GCDDaqrr766espTnjLrqv5hquyTn/zkjqGt02mf9KQnVffcc09Kk4suuihtsjIqePZEpMP/+3//b7Z39Ap5fvnll6dvv+WWW/q6d6ryH//xH9Udd9yR5D7KAN/PJlXDlAERERGRyUSHpYiIiExZcJb95je/qR544IHqGc94RjXvvPOmgKOKtS8HgWf+7W9/q370ox9V119/fWPgmjY6LYkTa32SJn/+859HFkeciD/96U9nSxf+f+yxx0aaDrznkUceSc8m3HDDDdU//vGPWWc7QzyID9/+17/+tZX5Mx7gtAzZf9aznpW+/8EHH5wx3y8iIiLTDx2WIiIiMqXBwfXEJz6xOuGEE6qzzjqrOvPMM6uXvvSl1d///vdZV/QHz8LZ8653vat65zvf2RhwBj796U+fdVe7CEcVaTMKGFmJI+yQQw6ZLV34/7bbbksOs1GBs5nRkTybsMMOO1SPPvpoz9/yz3/+M/393//93/R3uvM///M/1ZJLLpnknsBu+uSVzkoRERGZyuiwFBERkWkBjhuclIRhnVXh7HnZy15WHXjggdW+++47R/jSl75UfeYzn0nOvBLurwudqLue0Il+rx8EHIg33XRTtddee1VrrbVWtf/++8+WDosttljPIyB7gXxcYoklUrqvsMIKs472BvFYeeWVU7wWX3zxxnjl6VSmX36ujrrrCZ2ou54wKhhNHLI/qKNeREREpE3osBQRERFpYJlllqm23nrr6m1ve9tsYcstt6y++93vpjUiy5F/OI+Ykp07kAgc6+RIjWvKe2LEYB049/J7+H/QqfBN8P777ruv+upXv5rSY6uttpotLeaff/6Rjmbkfc997nNTui+66KJ9OUP/8pe/VM9//vOrTTfdNMWrLu0if+JcP2k4kXkrIiIiMpPRYSkiIiLSAM4y1kKsC2xoUm5qMvfcc6cp0q973etqA5sBzTPPPLOufhyewfPe/OY3197z2c9+Nk3xzR2jTFt/2tOeVr3//e+f4/pf//rXaTOiYeF9TMV+wxveUP34xz+uvv/976cRj0yFz9NhPKZe80ye3atDj7j+6U9/Smn42te+tnrNa16T4lxuusNo2Iceeqh605veVJ188snVc57znMY0nGuuuWbd9ThM/7/zzjvnuDbCFVdckdZRzUdOkrc4JjfaaKPae4499tg58lZEREREdFiKiIiIjARG3+G0uvvuu6sXv/jF1bLLLjtb4NgvfvGLtIs1jjgcWzgemW595ZVXVksttVS13HLLzXEPzjtGc+IoxLHFPb/85S+ryy67LI0iXH755ceu5/4bb7wxbYgzCnj3ww8/nJxuCyywQHLAjXoE5yggTjgj+f5nP/vZ1e9+97s0irFu2jVpz/nbb7+9+s53vtOYhtddd93Y/Tz/hz/8YXJYNuXtr371q5RPjNiMvL355pvTfawxWZe3wD04W3VaioiIiPybJ6y66qr/uvfee6s//vGPtUadiIiIyGSCs2iVVVZJI+JwnOUwCm6PPfaoLr300uqSSy5Jo9WGHfGH4+uee+5J04rZWIY1G//rv/5r1tnHIU5rrrlmco59/etfT04qwqte9arkeDz33HPTLuI5xJXn4bAkMBrvqU99appejtOSHbEZNZk7BBkpeeKJJ1YHH3xw9cUvfrFabbXVUvw+//nPV8ccc0x1zjnnVCuttFJ6N2DLEa8//OEP6ffee+9dbbPNNmm0Yr/gQMM+ZMQioyyPO+64OdIB+M7xGGVJehH/Cy+8MOUvO2B3eg/f/sxnPjNtvMQalp/73OdSWuQyQ9rdf//91SabbDL2LK5n3cs8DddZZ530/vPPPz8d59p11123WnjhhasLLrigVg533HHHFE+coMgFebv99ttXV111VXJ+MkKzKW9JW9YHLZ/bL8Sd+JJfrC16yimn1MrhrrvumuKq7S8iIiJtxa5cERERkQYYxbjTTjslBw9h9913r3bbbbcU3vve91Yf+MAHZltjEScVTjEcT3WBc+yoHY4ijjEl+bDDDku/cS6V94STKx+Bx3MA51Q+PZs1HA866KAUt1FBfBmxmadDhF122SWtbznKXcIHhXQiDcLx2AmufcUrXlEdccQRab3Mxx57bLZ0ZCp5Od2fvOU7y/yJQJ4wqjJ3AnJ9TAuPEO9gxCwOaHZex8ndS7xFREREZgo6LEVEREQaYAo3I+a+973vJeflxRdfnEZy/uAHP0ij99Zee+05Rv0x5Rhn1COPPDJb4FjplOLa1VdfPY2Iw9lYd085Qq4br371q9NovVGBE441HSMdyvDggw+muE8lcFiyizgjLRnp2usI0X7ylncwipKRlThE41qeAfxlxCbraXYbPSoiIiIy09BhKSIiItLAW9/61rQGIY45phjDzjvvnKZvs2FL6ahjNB3Tu3EYsvFLHl75ylem55QwcpI1DDfYYINqvfXWm+Mepn73A6P4WL9xVOAwxQlKOjCNOA84bk877bRqiy22mHIOt9hQqdd4k7dsqISTOs+jyCccuhAjYkm3/fbbrzrppJOqzTffPKUh+Yt8xHIA5D3X6awUERERmR0dliIiIiINMDUY5xKj5BZccMHqjW98Y3Iu4ZzC2VWuAcg51lHEOcU6iHnA0cV6kDyD6cM4thi9eM011yTnH1OUWQMzv4fnMF14smFqM+nADud54BgOUkYQTnfIW763W94iM+QtAack61niwI78ZFOm8847L62F+ZOf/GRser+IiIiI/BsdliIiIiIN4HTCUcV0XxyWjLJkQxs2+mGnaRyOOVzHjtCf/exn08jIMhx99NFpzUKmCvNsnFtsoPPxj388bb5y7LHHznY979tss81mPX3yiHSoCzhtZ8LmLeTtoosumjbIyfMoAnl76KGHzrZxEulDXrNGKXl7/PHHJ+f0XnvtVe2zzz7VmWeemTaKcodwERERkdnROhIRERHpAZxP+S7ZOCvrHE2sTchU8brA9F+ma4dDC5hqjFOLEZvl9YxezDf16QXipANsfEAGyjyKQN6SX3neRl7ENey6vueee445L1/0ohdV73jHO9KoS0daioiIiPwbrVkRERGRHsEZxfRw1q/E+fT73/++59GFXMdalWxgkzu1msA59vDDD6eNWvqBkZ+MApWJg7xl4x3ylnyLY2V+c27FFVdMU/9Zz5Ip5ldccUW6TieziIiIyL/RMhIRERHpEUZBbr/99mn9wY985CPVbrvtltZ3DDjPiEhGTJaBtQw/8YlPpB3BGakZDipGXDI6j/UO41qcoo8++mi17rrrVp/+9KfTdTkx6pJ35++Ya665qm233bbaZZdd0vlhwdHGiFFC/p48MFWa+I+KPB1iyn3dsRym1sd5/ocYuUrI82hQ+Ea+NZ6ZB/KWad+vf/3rU76Rtxw/4IADqg033DClI3nDMUZSxshLEREREanniQsuuOABjBDACJsJ6w+JiIjI1IP1I9/ylrckx1kOjqiLL764uu+++6qtttoqOYR6Gb3YCRxJjFA855xz0mg4doDGURVwHqcZu2PjFNt0003HRtXhiJxvvvmqX/ziF2k36FtuuWUs3HrrrcnRuPTSS1drrLHG2BRgHFzc89vf/jZdE9czTZjv5hsZafnmN785/eZdOEZx4vG+O++8s7r55pvH7pt77rnT8+6///60kc9KK63U97TygLTkHfPOO2/1wAMPpE1i4j0E4ouD8MUvfnG12mqrDW1L8m3f/OY3qx//+Mfp2VdddVUaochGRnwn78SZy7qPkc+kI7uVX3311eme6667LqUd1/3yl79M+cB07Oc///npekYznn322SnObIaT5y3wDWeddVb6LnaJL/M2nlmmA47nyFvyLEZY4sxk1Guet3EPx1kXc/XVV0/fGO8aFN7JM84444yURhtttNEceU/cvv3tb6cyo+0vIiIibeUJq6666r/uvffeNK1Jo0VERETaBo6pVVZZpTr55JPTGoE5jFpjAxw2Mrn88suTcwiHDU6aQZ0/OMB++tOfJmfV2972tjSSEodXDnFiNB2OvK9+9avJWQU4iS677LJqhx12SL9LGIXHc3GIhsONb+D3mmuumX4HbN6CY+zUU0+tPvaxj1Unnnhi9dKXvjSlAc407mMEJs7RHJxRxHfjjTdO6yW+853vTA7OQcA2JE2//OUvV/vuu++so7PzpS99KTn+cM4NA+/Cech06U7xJS022WSTsWtIB9aBvPHGG9PvOti9+6ijjkod9DjqSJvNN9+82n///efIW+LB9aT/17/+9TGHJg5FHKOkZx1smoS8RN4SiBtTxXFi1sF7WMuSpQVKZ3w/EOdwkhJfdiNfbLHFqlNOOWWO0a/Eadddd01lhutFRERE2ogOSxEREWk13RyWTMu+5JJL0gYmOBu5ninRL3/5y8ccif2APYSThxF9888/f7XQQgvVOj/vuOOO9L6lllpqzPnI6EvWnMS2Ku0qrllkkUXGnKo5OFh5Hse5j2txSi677LJpFB6j+th9PN+BmusYSYjDLd7FuWWWWSY5vzhH3PmGQZ23ECNOf/7zn9d+0xJLLJFGM0a8hoFnkO7kW/ku4HyZhsQPJySOwaZ7WHN04YUXTvdE3jJaklGX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](data:image/png;base64,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YDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAAAAABgMAUsAAAAAYDAELAEAAACAwRCwBAAAAAAGQ8ASAADg/7d3JuDeVuPifv05OFGGlBSlWYNKpUgqyVihQQOaqGRoVigapGhUEYk0a0AqkYpCGlU0DxoIlZnq4Dgc/3Ovvmdb3/re9zfvvd+9931f17r2/r3jetd61rOe9axJREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdagw1JERERERERERERagw5LERERERERERERaQ06LEVERERERERERKQ16LAUERERERERERGR1qDDUkRERERERERERFqDDksRERERERERERFpDTosRUREREREREREpDXosBQREREREREREZHWoMNSREREREREREREWoMOSxEREREREREREWkNOixFRERERERERESkNeiwFBERERERERERkdbwxAUXXPCAP/7xj9Xf/va36glPeMKswyIiIiLt4V//+tes/0RkFGj3i4iISJt5wqqrrvqve++9t8JpqeEiIiIibQNn5TLLLFMdcMAB1d///vdZR0VkEJ761KdWRxxxRHXttddq+4uIiEhr0WEpIiIirQaH5f/ZK9Xpp59e/fd///esoyIyCE972tOq973vfdXFF1+s7S8iIiKtRYeliIiItBoclqusskp18skn67AUGZK55pqr2nXXXatLL71U219ERERai5vuiIiIiIiIiIiISGvQYSkiIiIiIiIiIiKtQYeliIiITFn+8z//szr66KOrjTfeuNpwww1T2GCDDaqrr766espTnjLrqv5hquyTn/zkjqGt02mf9KQnVffcc09Kk4suuihtsjIqePZEpMP/+3//b7Z39Ap5fvnll6dvv+WWW/q6d6ryH//xH9Udd9yR5D7KAN/PJlXDlAERERGRyUSHpYiIiExZcJb95je/qR544IHqGc94RjXvvPOmgKOKtS8HgWf+7W9/q370ox9V119/fWPgmjY6LYkTa32SJn/+859HFkeciD/96U9nSxf+f+yxx0aaDrznkUceSc8m3HDDDdU//vGPWWc7QzyID9/+17/+tZX5Mx7gtAzZf9aznpW+/8EHH5wx3y8iIiLTDx2WIiIiMqXBwfXEJz6xOuGEE6qzzjqrOvPMM6uXvvSl1d///vdZV/QHz8LZ8653vat65zvf2RhwBj796U+fdVe7CEcVaTMKGFmJI+yQQw6ZLV34/7bbbksOs1GBs5nRkTybsMMOO1SPPvpoz9/yz3/+M/393//93/R3uvM///M/1ZJLLpnknsBu+uSVzkoRERGZyuiwFBERkWkBjhuclIRhnVXh7HnZy15WHXjggdW+++47R/jSl75UfeYzn0nOvBLurwudqLue0Il+rx8EHIg33XRTtddee1VrrbVWtf/++8+WDosttljPIyB7gXxcYoklUrqvsMIKs472BvFYeeWVU7wWX3zxxnjl6VSmX36ujrrrCZ2ou54wKhhNHLI/qKNeREREpE3osBQRERFpYJlllqm23nrr6m1ve9tsYcstt6y++93vpjUiy5F/OI+Ykp07kAgc6+RIjWvKe2LEYB049/J7+H/QqfBN8P777ruv+upXv5rSY6uttpotLeaff/6Rjmbkfc997nNTui+66KJ9OUP/8pe/VM9//vOrTTfdNMWrLu0if+JcP2k4kXkrIiIiMpPRYSkiIiLSAM4y1kKsC2xoUm5qMvfcc6cp0q973etqA5sBzTPPPLOufhyewfPe/OY3197z2c9+Nk3xzR2jTFt/2tOeVr3//e+f4/pf//rXaTOiYeF9TMV+wxveUP34xz+uvv/976cRj0yFz9NhPKZe80ye3atDj7j+6U9/Smn42te+tnrNa16T4lxuusNo2Iceeqh605veVJ188snVc57znMY0nGuuuWbd9ThM/7/zzjvnuDbCFVdckdZRzUdOkrc4JjfaaKPae4499tg58lZEREREdFiKiIiIjARG3+G0uvvuu6sXv/jF1bLLLjtb4NgvfvGLtIs1jjgcWzgemW595ZVXVksttVS13HLLzXEPzjtGc+IoxLHFPb/85S+ryy67LI0iXH755ceu5/4bb7wxbYgzCnj3ww8/nJxuCyywQHLAjXoE5yggTjgj+f5nP/vZ1e9+97s0irFu2jVpz/nbb7+9+s53vtOYhtddd93Y/Tz/hz/8YXJYNuXtr371q5RPjNiMvL355pvTfawxWZe3wD04W3VaioiIiPybJ6y66qr/uvfee6s//vGPtUadiIiIyGSCs2iVVVZJI+JwnOUwCm6PPfaoLr300uqSSy5Jo9WGHfGH4+uee+5J04rZWIY1G//rv/5r1tnHIU5rrrlmco59/etfT04qwqte9arkeDz33HPTLuI5xJXn4bAkMBrvqU99appejtOSHbEZNZk7BBkpeeKJJ1YHH3xw9cUvfrFabbXVUvw+//nPV8ccc0x1zjnnVCuttFJ6N2DLEa8//OEP6ffee+9dbbPNNmm0Yr/gQMM+ZMQioyyPO+64OdIB+M7xGGVJehH/Cy+8MOUvO2B3eg/f/sxnPjNtvMQalp/73OdSWuQyQ9rdf//91SabbDL2LK5n3cs8DddZZ530/vPPPz8d59p11123WnjhhasLLrigVg533HHHFE+coMgFebv99ttXV111VXJ+MkKzKW9JW9YHLZ/bL8Sd+JJfrC16yimn1MrhrrvumuKq7S8iIiJtxa5cERERkQYYxbjTTjslBw9h9913r3bbbbcU3vve91Yf+MAHZltjEScVTjEcT3WBc+yoHY4ijjEl+bDDDku/cS6V94STKx+Bx3MA51Q+PZs1HA866KAUt1FBfBmxmadDhF122SWtbznKXcIHhXQiDcLx2AmufcUrXlEdccQRab3Mxx57bLZ0ZCp5Od2fvOU7y/yJQJ4wqjJ3AnJ9TAuPEO9gxCwOaHZex8ndS7xFREREZgo6LEVEREQaYAo3I+a+973vJeflxRdfnEZy/uAHP0ij99Zee+05Rv0x5Rhn1COPPDJb4FjplOLa1VdfPY2Iw9lYd085Qq4br371q9NovVGBE441HSMdyvDggw+muE8lcFiyizgjLRnp2usI0X7ylncwipKRlThE41qeAfxlxCbraXYbPSoiIiIy09BhKSIiItLAW9/61rQGIY45phjDzjvvnKZvs2FL6ahjNB3Tu3EYsvFLHl75ylem55QwcpI1DDfYYINqvfXWm+Mepn73A6P4WL9xVOAwxQlKOjCNOA84bk877bRqiy22mHIOt9hQqdd4k7dsqISTOs+jyCccuhAjYkm3/fbbrzrppJOqzTffPKUh+Yt8xHIA5D3X6awUERERmR0dliIiIiINMDUY5xKj5BZccMHqjW98Y3Iu4ZzC2VWuAcg51lHEOcU6iHnA0cV6kDyD6cM4thi9eM011yTnH1OUWQMzv4fnMF14smFqM+nADud54BgOUkYQTnfIW763W94iM+QtAack61niwI78ZFOm8847L62F+ZOf/GRser+IiIiI/BsdliIiIiIN4HTCUcV0XxyWjLJkQxs2+mGnaRyOOVzHjtCf/exn08jIMhx99NFpzUKmCvNsnFtsoPPxj388bb5y7LHHznY979tss81mPX3yiHSoCzhtZ8LmLeTtoosumjbIyfMoAnl76KGHzrZxEulDXrNGKXl7/PHHJ+f0XnvtVe2zzz7VmWeemTaKcodwERERkdnROhIRERHpAZxP+S7ZOCvrHE2sTchU8brA9F+ma4dDC5hqjFOLEZvl9YxezDf16QXipANsfEAGyjyKQN6SX3neRl7ENey6vueee445L1/0ohdV73jHO9KoS0daioiIiPwbrVkRERGRHsEZxfRw1q/E+fT73/++59GFXMdalWxgkzu1msA59vDDD6eNWvqBkZ+MApWJg7xl4x3ylnyLY2V+c27FFVdMU/9Zz5Ip5ldccUW6TieziIiIyL/RMhIRERHpEUZBbr/99mn9wY985CPVbrvtltZ3DDjPiEhGTJaBtQw/8YlPpB3BGakZDipGXDI6j/UO41qcoo8++mi17rrrVp/+9KfTdTkx6pJ35++Ya665qm233bbaZZdd0vlhwdHGiFFC/p48MFWa+I+KPB1iyn3dsRym1sd5/ocYuUrI82hQ+Ea+NZ6ZB/KWad+vf/3rU76Rtxw/4IADqg033DClI3nDMUZSxshLEREREanniQsuuOABjBDACJsJ6w+JiIjI1IP1I9/ylrckx1kOjqiLL764uu+++6qtttoqOYR6Gb3YCRxJjFA855xz0mg4doDGURVwHqcZu2PjFNt0003HRtXhiJxvvvmqX/ziF2k36FtuuWUs3HrrrcnRuPTSS1drrLHG2BRgHFzc89vf/jZdE9czTZjv5hsZafnmN785/eZdOEZx4vG+O++8s7r55pvH7pt77rnT8+6///60kc9KK63U97TygLTkHfPOO2/1wAMPpE1i4j0E4ouD8MUvfnG12mqrDW1L8m3f/OY3qx//+Mfp2VdddVUaochGRnwn78SZy7qPkc+kI7uVX3311eme6667LqUd1/3yl79M+cB07Oc///npekYznn322SnObIaT5y3wDWeddVb6LnaJL/M2nlmmA47nyFvyLEZY4sxk1Guet3EPx1kXc/XVV0/fGO8aFN7JM84444yURhtttNEceU/cvv3tb6cyo+0vIiIibeUJq6666r/uvffeNK1Jo0VERETaBo6pVVZZpTr55JPTGoE5jFpjAxw2Mrn88suTcwiHDU6aQZ0/OMB++tOfJmfV2972tjSSEodXDnFiNB2OvK9+9avJWQU4iS677LJqhx12SL9LGIXHc3GIhsONb+D3mmuumX4HbN6CY+zUU0+tPvaxj1Unnnhi9dKXvjSlAc407mMEJs7RHJxRxHfjjTdO6yW+853vTA7OQcA2JE2//OUvV/vuu++so7PzpS99KTn+cM4NA+/Cech06U7xJS022WSTsWtIB9aBvPHGG9PvOti9+6ijjkod9DjqSJvNN9+82n///efIW+LB9aT/17/+9TGHJg5FHKOkZx1smoS8RN4SiBtTxXFi1sF7WMuSpQVKZ3w/EOdwkhJfdiNfbLHFqlNOOWWO0a/Eadddd01lhutFRERE2ogOSxEREWk13RyWTMu+5JJL0gYmOBu5ninRL3/5y8ccif2APYSThxF9888/f7XQQgvVOj/vuOOO9L6lllpqzPnI6EvWnMS2Ku0qrllkkUXGnKo5OFh5Hse5j2txSi677LJpFB6j+th9PN+BmusYSYjDLd7FuWWWWSY5vzhH3PmGQZ23ECNOf/7zn9d+0xJLLJFGM0a8hoFnkO7kW/ku4HyZhsQPJySOwaZ7WHN04YUXTvdE3jJaklGX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)

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

Now, open a browser and navigate to ‘

**http://<your host IP>:8080**

’. You should receive a response like the example provided.

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