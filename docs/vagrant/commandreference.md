# Vagrant Command Reference
Some basic vagrant commands

<br/>

**vagrant init [boxname]** - creates a vagrant file in the working directory and initializes a box based on the boxname. This box name corresponds to the boxes found in the directory linked on the [Vagrant](/vagrant) page.

**vagrant up** - starts the box based on the vagrantfile. If running the first time, it may take a while for the downloads and provisioning. Any subsequent runs of this command will not re-download or provision the machine again.

**vagrant halt** - stops the virtual machine

**vagrant destroy** - deletes the virtual machine entirely

**vagrant reload** - reboots the machine and takes in any changes to the vagrant files

**vagrant status** - gives a status of the current machine

**vagrant ssh** - ssh into the virtual machine. Typing "exit" will take you back out to our own command prompt
