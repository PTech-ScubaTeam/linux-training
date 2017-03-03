## Up and Running

We are going to use Vagrant to create a ubuntu VM image that we can play with in our examples.  With VirtualBox installed Vagrant will, in the background, create and configure a virtual machine (vm) and allow us to SSH (Secure Shell) into the VM to play around.

### Steps
1. Download or git clone the [Vagrantfile](Vagrantfile)
2. While in the terminal / command window type:
```
vagrant up
```
This will take a few minutes the first time you do this.
3. Once the VM is created you can SSH into the VM by typing:
```
vagrant ssh
```
If you've got everything set up correctly you should see the hashtag (#) prompt
