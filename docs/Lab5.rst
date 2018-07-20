*Lab 5 - Push a Certificate and Key to the F5*
==============================================
1. .. rubric:: *Push a Certificate and Key to the Bigip*
      :name: lab-5-push-a-certificate-and-key-to-the-bigip
      :class: H1

   1. .. rubric:: Review the push\_cert\_and\_key\_to\_bigip Playbook
         :name: review-the-push_cert_and_key_to_bigip-playbook
         :class: H2

Open the “push\_cert\_and\_key\_to\_bigip” playbook. Notice that we are
only addressing one bigip in this playbook. The reason is we already
have an active/standby configuration. This means we can now perform all
none network configuration changes on one device and sync that
configuration to the other device.

Notice that there are two tasks or “plays” in this playbook. The first
will be pushing a certificate to the bigip to be used in creating a
clientssl profile so that the application VIP can perform SSL offload.
This play is using the F5 “bigip\_ssl\_certificate” module.

Notice that all the variables are defined under “vars” and that these
variables are called out in the module using the name of the variable in
between quotes and curly braces. “{{ }}” This is a better practice than
hard coding all the variables within the plays themselves. By doing
this, you know you only have to change what is under the “vars” section.

Notice the “content” line in both plays. The certificate and key we will
be using is located under /var/tmp on the Ansible host. Verify that the
certificate and key are in /var/tmp and that the names match the names
defined under the vars section of the playbook.

Once you have confirmed that the variables are correct for your
environment and that the files are located in the proper directory with
the correct spelling, close the playbook.

Now log into the GUI of the both bigips. Go to System -> File Management
-> SSL Certificate List.

Notice that there are 3 default entries but no “RSA Certificate & Key”
named “f5agility2018”

|image14|

Run the push\_cert\_and\_key\_to\_bigip Playbook
------------------------------------------------

Go back to SSH session on the Ansible machine and run the playbook.

*ansible-playbook push\_cert\_and\_key\_to\_bigip.yml*

Did your playbook finish successfully? If so go back to the GUI. Is
there a new entry under SSL Certificate List for f5agility2018?

Re-open the playbook and change the “state” under vars from “present” to
“absent”. Rerun the playbook and check the GUI. Is the f5agility2018
certificate and key gone?

Re-open the playbook and change the state back to present and re-run the
playbook. Verify that the f5agility2018 certificate and key bundle are
back.

Notice in the top left of the GUI that the sync status is “changes
pending”. Log into the second bigip GUI and look at System -> File
Management -> SSL Certificate List. The agility2018 RSA cert/key bundle
is not there.

Run the config-sync playbook.

*ansible-playbook config-sync.yml*

Go back and look at both GUIs. The state has changed to “in sync” and
both devices have the cert/key bundle.


.. |image14| image:: media/image15.png
   :width: 6.53194in
   :height: 1.15069in