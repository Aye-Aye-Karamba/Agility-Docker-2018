*Lab 7 – Provision the ASM Module*
==================================

1. .. rubric:: *Provision the ASM Module*
      :name: lab-7---provision-the-asm-module
      :class: H1

The bigip is currently only provisioned for LTM. We will be using a WAF
(Web Application Firewall) policy in a later lab which requires the
provisioning of the ASM module (Application Security Module)

 Review the provision Playbook
------------------------------

Go into the GUI of bigip1 and go to System -> Resource Provisioning.
Notice that only LTM is provisioned.

Open the provision.yml playbook. Notice that it contains one play that
will provision ASM onto bigip1.

It uses the F5 bigip\_provision module. This module will not let the
play finish until the bigip is ready to accept another API call. This is
important. If there were other plays in this book we would not want them
to execute until the bigip was ready for the next command. That is the
power of using a specific module rather than a generic module such as
“bigip\_command”. Only use generic modules when the exact one for your
task is not available.

Close the playbook and run it. Notice that it appears to hang . It will
not relinquish to a next task until the F5 is ready to accept it.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This will take a couple of minutes. Time to get some more coffee!

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once the play finishes and you see the PLAY RECAP, go back to the GUI of
bigip1.

Go to System -> Resource Provisioning and notice that the ASM module is
now provisioned.

Provisioning a new module re-distributes the memory, CPU and storage, it
also causes the system to restart daemons. You never want to provision
modules during production as this would cause a 1 to 2-minute outage.

You may now move on to the next lab.