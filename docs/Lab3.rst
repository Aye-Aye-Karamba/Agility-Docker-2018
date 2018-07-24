*Lab 3 - Changing the default passwords*
=======================================

1. .. rubric:: *Changing the default passwords*
      :name: lab-3---changing-the-default-passwords
      :class: H1

Since our lab is open to the internet we will want to change the default
passwords before we license the devices. A brand new bigip will have the
following default users and credentials.

-  Https GUI access

   -  Username: admin

   -  Password: admin

-  SSH CLI access

   -  Username: root

   -  Password: default

From the Ansible CLI, cd into the ansible/playbooks/Agility2018 directory.
This is where all the playbooks are. Open the change\_password playbook.

You will remember that we set the credentials for Ansible to use in the
/etc/ansible/hosts file. Ansible uses SSH to connect to the bigips so we
used the CLI credentials of root/default. 

The F5 modules use the GUI credentials when they access the bigip which
by default is admin/admin.

Notice under the line “vars” We are setting variables for our playbook.
The F5 module requires the GUI credentials to be set within the module.
The username and password variables are using our current GUI
credentials of admin/admin. Since we will be using both the root and
admin accounts in our plays we will want to change the passwords for
both accounts.

The first play in the change\_password playbook is going to change the
password for the admin account. It will replace it with our variable
“newpass”. That variable is set to make the new password “Agility1”.

The second play is going to change the root password. Notice that the
“password” in our module changed from the variable “{{password}}” to
“{{newpass}}” We changed the password in the previous play, so we had to
change it in this play or the playbook would not successfully complete
the second task.

Ansible playbooks are run from the CLI using the "ansible-playbook" command.
From the CLI run the following command:

*ansible-playbook change\_passwords.yml*

Your play recap should look like the following.

|image9|

Keep in mind that Ansible has tab completion. So you don't have to
type the entire command. For example, ans <hit tab> -pl <hit tab> etc...

Now that the passwords for both accounts have been changed on both
devices we need to update our /etc/ansible/hosts file and change the
password for root from default to Agility1.

Open the /etc/ansible/hosts file and notice at the end of the last two
lines that the password is set to default. Close this file. 

Open the "ansible_hostsfile_newpass.yml" playbook. Notice that these plays
are addressing the Ansible host itself rather than the bigips. Thats why
we see the username as "f5". We are using the Ansible module "lineinfile"
to change the last word in the line from default to Agility1.

Now run the playbook named ansible\_hostsfile\_newpass.yml with the following
command.

*ansible-playbook ansible\_hostsfile\_newpass.yml*

Re-open the /etc/ansible/hosts file. The password has been changed to
Agility1. Close the file and test the connectivity to the bigips.

*ansible -m ping bigip*

You should have two green successful pings.

.. |image9| image:: media/image10.png
   :width: 6.53194in
   :height: 2.06667in
