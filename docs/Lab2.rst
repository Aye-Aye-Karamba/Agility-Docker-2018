*Lab 2 - Setting up the Connectivity between Ansible and the F5s*
=================================================================

1. .. rubric:: *Ansible Setup*
      :name: lab-2---ansible-setup
      :class: H1

   1. .. rubric:: Setting up the Connectivity between Ansible and the
         F5s.
         :name: setting-up-the-connectivity-between-ansible-and-the-f5s.
         :class: H2

Using putty on your Windows desktop, start an SSH session to the Ansible
machine.

We will configure Ansible for use with our bigips.

Use your favorite linux editor to open the /etc/ansible/hosts file.
There is a top section named [bigip] underneath this heading are
connection parameters for Ansible to use to connect to managed devices.

Ansible can be used to configure almost any device you want. In a
production network you might have other headings in this file such as
[database], [webservers] [cisco\_switches] etc…

You will notice that the first entry is commented out with a hashtag.
This is just an example to show you how to set up connectivity to a
managed device using public/private key pairs. For this lab we will be
connecting using a username and password. The username and password
currently configured is for the default credentials of a bigip.

Notice that we have two bigips defined, bigip1 and bigip2. We also have
“ansible\_host=” twice, once for each device. This will allow us to
target a specific bigip by using bigip1 or bigip2 in our playbooks. Or
for plays that will address both systems at the same time we can target
“ansible\_host”. The other parameters tell Ansible how to connect to
these devices. In this case SSH. Ansible supports other protocols such
as netconf and https but for the scope of this lab we will stick with
ssh. Close this file.

|image4|

Now open and inspect the /etc/hosts file.

The /etc/ansible/hosts and /etc/hosts files work together to let us use
names when addressing the F5s with Ansible. Close this file.

|image5|

Now test connectivity to the F5s using the following command.

*ansible -m ping bigip*

Ansible “ping” does not do an ICMP ping but rather looks at the
/etc/ansible/hosts file for connectivity information. In this case it
will create an SSH connection to both F5s using the username and
password specified and verify that Ansible can successfully interact
with the F5s.

|image6|

Since the Ansible workstation has never connected to the F5s, this will
fail.

From Ansible, ssh as root to each of your bigips with password “default”
and type yes to accept the RSA fingerprint.

Example: *ssh root@bigip1*

|image7|

Now retry the *ansible -m ping bigip command*.

|image8|

Now Ansible can communicate with the F5s.

Review the ansible.cfg Config File
----------------------------------

Open the ansible.cfg file:

*sudo vi /etc/ansible/ansible.cfg*

Certain settings in Ansible are adjustable via a configuration file
(ansible.cfg). The stock configuration should be sufficient for most
users, but there may be reasons you would want to change them. Take a
quick look through the file to familiarize yourself with it. We will
make a change to it in a later lab.

.. |image4| image:: media/image5.png
   :width: 6.53194in
   :height: 1.15347in
.. |image5| image:: media/image6.png
   :width: 6.53194in
   :height: 0.55417in
.. |image6| image:: media/image7.png
   :width: 6.53194in
   :height: 1.66458in
.. |image7| image:: media/image8.png
   :width: 6.53194in
   :height: 0.90278in
.. |image8| image:: media/image9.png
   :width: 6.53194in
   :height: 1.49722in