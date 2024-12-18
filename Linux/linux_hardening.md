# Learning Dependecies

## 13th December 2024
I learned about **Linux Navigation**, ****, and **Virtual Private Server**. How to install them and make basic configurations. 


### Key Takeaways
- **User Management**: 
- **Package Management**: 
- **Service and Process Management**:
- **Task Scheduling**:
- **File Descriptions and Redirections**:
- **Filter Contents**:
- **Regular Expressions**:
- **Permission Managment**:

### Reflections
## Hardening

Several mechanisms are highly effective in securing Linux systems in keeping our and other companies' data safe. Three such mechanisms are SELinux, AppArmor, and TCP wrappers. These tools are designed to safeguard Linux systems against various security threats, from unauthorized access to malicious attacks, especially while conducting a penetration test. 

SELinux is a MAC system that is built into the Linux kernel. It is designed to provide fine-grained access control over system resources and applications. SELinux works by enforcing a policy that defines the access controls for each process and file on the system. It provides a higher level of security by limiting the damage that a compromised process can do.

AppArmor is also a MAC system that provides a similar level of control over system resources and applications, but it works slightly differently. AppArmor is implemented as a Linux Security Module (LSM) and uses application profiles to define the resources that an application can access. AppArmor is typically easier to use and configure than SELinux but may not provide the same level of fine-grained control.

TCP wrappers are a host-based network access control mechanism that can be used to restrict access to network services based on the IP address of the client system. It works by intercepting incoming network requests and comparing the IP address of the client system to the access control rules. These are useful for limiting access to network services from unauthorized systems.

## Exercises done:

 

## **SELinux**

1. Install SELinux on your VM.
2. Configure SELinux to prevent a user from accessing a specific file.
3. Configure SELinux to allow a single user to access a specific network service but deny access to all others.
4. Configure SELinux to deny access to a specific user or group for a specific network service.

## **AppArmor**

1. Configure AppArmor to prevent a user from accessing a specific file.
2. Configure AppArmor to allow a single user to access a specific network service but deny access to all others.
3. Configure AppArmor to deny access to a specific user or group for a specific network service.

## **TCP Wrappers**

1. Configure TCP wrappers to allow access to a specific network service from a specific IP address.
2. Configure TCP wrappers to deny access to a specific network service from a specific IP address.
3. Configure TCP wrappers to allow access to a specific network service from a range of IP addresses.

## **Firewall Setup**
