# CREATE VM AND PORT FORWARDING
## 1. Create VM
### 1.1. Download an OS Image(Ubuntu,centos,..)
You can download an Ubuntu image [here](https://ubuntu.com/download/desktop). Make sure to save it to a memorable location on your PC! For this tutorial, we will use the latest Ubuntu 22.10 release.
### 1.2. Download and install VirtualBox
You can download VirtualBox from the downloads page [here](https://www.virtualbox.org/wiki/Downloads). This page includes instructions on how to install VirtualBox for your specific OS so we won’t repeat those here.

Once you have completed the installation, go ahead and run VirtualBox.
![1](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/e75262a2-608c-49a8-9a1c-d9ba9e27c447)

### 1.3. Create a new virtual machine
Click New to create a new virtual machine. Fill in the appropriate details:
- Name: If you include the word Ubuntu in your name the Type and Version will auto-update.
- Machine Folder: This is where your virtual machines will be stored so you can resume working on them whenever you like.
- ISO Image: Here you need to add a link to the ISO you downloaded from the Ubuntu website.

We want to install Ubuntu unattendedly so we can leave the checkbox to skip unchecked.
![2](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/1e8506b6-3b5a-4546-ad1f-0a219205fbee)

#### Create a user profile

To enable the automatic install we need to prepopulate our username and password here in addition to our machine name so that it can be configured automatically during first boot.

The default credentials are:
- Username: vboxuser
- Password: changeme
It is important to change these values since the defaults will create a user without sudo access.

Ensure your Hostname has no spaces to proceed!

![3](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/c52d9f44-2d50-4580-ab3f-7e153c1f6ef1)

#### Define the Virtual Machine’s resources

In the next section we can specifiy how much of our host machine’s memory and processors the virtual machine can use. For good performance it’s recommended to provide your VM with around 8GB of RAM (althought 4GB will still be usable) and 4 CPUs. Try to remain in the green areas of each slider to prevent issues with your machine running both the VM and the host OS.
![4](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/24824283-76c2-416d-a035-a0912a9bd88e)

Then we need to specify the size of the hard disc for the virtual machine. For Ubuntu we recommend around 25 GB as a minimum. By default the hard disk will scale dynamically as more memory is required up to the defined limit. If you want to pre-allocate the full amount, check the ‘Pre-allocate Full Size’ check box. This will improve performance but may take up unnecessary space.
![5](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/381b933f-7ed2-4e68-8406-eb7f1f4a249c)

Click Next to continue and view a summary of your machine setting.
![6](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/09c841a1-2b97-4db9-a07e-f6ebe413309a)

After this click Finish to initialize the machine!

### 1.4. Change network to Bridged Adapter
Select **your VM** --> select **Settings**
![7](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/3df18a3f-0c57-44e0-bc26-2cbadf6c362e)

Select **Network** --> select **Bridged Adapter** --> **OK**
![8](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/4a3de6f5-5863-4f02-8728-9cea68b3700d)

**Don't forget reboot your VM**

## 2. Port forwarding (Router mikrotik)
### 2.1. Install Winbox 
You can install Winbox follow [here](https://help.mikrotik.com/docs/display/RKB/How+to+install+WinBox)
### 2.2. Configure port forwarding
Open Winbox --> type ip's router(192.168.1.1), your user, your password
![9](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/2070471e-9c60-43d6-a3a2-a3c1d20e9942)

  1. Go to IP, Firewall section;

  ![10](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/d54e0068-0d6f-4f4a-924e-714f60c83411)
  
  2. Open the NAT tab;
  3. Create a new record by pressing Add New;

  ![11](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/7c8bc782-0b1a-4b5f-abee-aa46cf827eca)

  4. A new window will open and fill in the following fields:
  
  ![12](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/b49cf5b7-2a7e-48d1-80f6-fcc4b8da04a9)
  
  5. Chain, choose dstnat because the IP address of the recipient will be changed;
  6. Dst. Address, indicate the incoming interface to which the specific rule will apply, in this case it is WAN have public ip(27.74.244.188);
  7. Select a protocol such as TCP;
  8. Dst. Port, specify the port that will be forwarded, for example port 5555;
  9. Go to the bottom of the page, to the Action section;
  
  ![13](https://github.com/go-julian/crate-vm-port-forwarding/assets/130023825/3fe39a77-64bc-4960-8609-139e9f33eabe)
  
  10. Action, select dst-nat;
  11. Enter the desired address to which you want to forward the data;
  12. Enter the required port.
This established rule can be translated as follows: When an incoming connection with the TCP protocol requests port 5555, translate the recipient's address and redirect it to the local address 192.168.1.58 and port 5000.
# REFERENCE
[Create VM by virtuabox](https://ubuntu.com/tutorials/how-to-run-ubuntu-desktop-on-a-virtual-machine-using-virtualbox#1-overview)

[Port forwarding (Router mikrotik)](https://help.mikrotik.com/docs/display/RKB/Port+forwarding)

    

    



    
    












