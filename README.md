## OBJECTIVE: 
Deploy a web server on a set of Virtual Machines (VMs) and load balance the traffic  going to it. Also, to configure health probes to switch between the VMs to avoid downtimes. 

## PROCEDURE AND CONFIGURATION: 
• Created a new resource group (CS4037D-Assignment-1) that is used to hold all  resources for the assignment 

• Created a new virtual network (Virtual-Network-1) to host the VMs required, the IP  range for this Virtual Network is 10.1.0.0/16. Also, a default subnet was created – 10.1.0.0/24.

• Created a new a Virtual Machine (VM-1) and attach it to the above subnet. The  following is the VM configuration. 

    o OS image: Ubuntu Server 18.04 LTS – Gen1 
    o Size: Standard_B1ls – 1vCPU, 0.5GiB Memory 
    o Allowed public inbound ports: 22(SSH), 80(HTTP), 443(HTTPS) 
    o Availability: Zone 
    o Disk: Standard HDD 
    o Network: Virtual-Network-1 
    o Public IP: VM-1-ip (52.146.16.33) 
    o Private IP: 10.1.0.4 
    
• Now to configure the VM-1 to host the web server. SSH into the VM and perform the  following steps. 

    o Install apache2 web server: sudo apt-get install apache2 
    o Update the index.html file at /var/www/html to reflect the VM-1’s name. • Create another Virtual Machine (VM-2) by following the same steps as VM-1 but replacing VM-1 to VM-2 as required. 
    o Public IP: VM-2-ip (52.146.16.69) 
    o Private IP: 10.1.0.5 
    
• Now the webpages are accessible through their public IPs. 

• Create a load balancer (Load-Balancer) with the following configuration o SKU: Standard 

    o Type: Public 
    o Public-IP: Load-Balancer-IP (52.146.16.20) 
    
• Attach a backend pool (Backend-Pool) to above created load balancer with VM1 and  VM2.  

• Add a health probe (Health-Probe) with the following configurations

    o Protocol: HTTP 
    o Port: 80 
    o Path: / 
    o Interval: 5 
    o Unhealthy threshold: 2 
    
• Add a load balancing rule (Load-Balancing-Rule) with the following configurations 

    o Port: 80/80 
    o Backend pool: Backend-pool (2-virtual-machines) 
    o Health probe: Health-probe (HTTP:80) 
    o Session Persistence: None 
    
## NOTE
The given configuration and naming is only for reference.

## ARCHITECTURE

![Screenshot from 2021-07-27 14-36-16](https://user-images.githubusercontent.com/63281605/127127895-f717b612-cf93-460e-b273-803781647563.png)
