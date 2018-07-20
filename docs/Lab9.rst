*Lab 9 – Opening a support case with F5*
=========================================

1. .. rubric:: *Adding an Application using an iApp Template*
      :name: lab-9---open-support-case-with-f5
      :class: H1

Opening a support case always involves creating and downloading a qkview
file. And it often involves running a tcpdump and downloading the pcap
file off of the bigip. In this lab we will learn how to do both
programmatically using Ansible.

– Programmatically collecting a qkview for bigip
------------------------------------------------

Review the “fetch\_qkview” playbook. This playbook will create a qkview
.ucs file and place it in the /var/tmp directory on the F5 and then move
it to the Ansible machines /tmp directory.

Check the Ansible /tmp directory and verify that there is no qkview file
name agility\_bkup.ucs.

Run the fetch\_qkview playbook.

Verify that the file now exists in the Ansible /tmp directory.

– Programmatically running and downloading a tcpdump
----------------------------------------------------

Review the “tcpdump\_from\_F5” playbook. This playbook will start a
tcpdump that will run for 60 seconds or until the user hits Ctrl + c
then c to continue. Under vars you define which vlan or interface to
capture on and what capture filter to apply as well as the desired name
for the capture file.

The playbook is currently setup to capture on the ha\_vlan with a filter
to only capture icmp packets.

Start an SSH session to bigip1. Now start a ping to 10.1.30.2. This is
the ha\_selfip on bigip2. You should see successful pings.

Go back to Ansible and run the “tcpdump\_from\_F5” playbook. Once the
screen shows the message, “Pausing for 60 seconds”, wait about 10
seconds and then stop the capture with the Ctrl +c then c to continue
command.

The playbook will stop the capture and move it to the Ansible machine
into the /tmp directory.

Verify that the “packet\_capture\_date\_icmp.pcap” file is in the /tmp
directory.

Read the capture file from the Ansible machine with the following
command:

*tcpdump -r /tmp/ packet\_capture\_date\_icmp.pcap *

You can see the icmp packets in the capture file.