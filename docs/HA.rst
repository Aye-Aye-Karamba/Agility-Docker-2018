
*Lab 5 – Creating a High Availability Configuration*
====================================================

There are over 70 steps to configuring bigips into an active/standby
pair. Network configuration is unique to each device and must be
addressed independently. Once an HA configuration has been completed all
other configurations can be made on one device and “config synced” to
the other device. (Except for any changes made to the network portion of
the configuration.)

Review the Variables in the f5\_active-standby.yml Playbook
-----------------------------------------------------------

The f5\_active-standby.yml playbook will perform all the tasks to bring
a newly licensed pair of bigips to an active/standby state. This
playbook is already properly configured for your environment. You should
however open it up and go through the file from top to bottom to
understand what is going on.

Notice at the top under “vars” all the variables that will be used in
this playbook. Variables can be in the playbook itself as in this case.
Or it can be a separate file that is referenced under “vars”

You could also change “vars” to “vars\_prompt” and the user executing
the playbook would be prompted for an answer to each variable before the
playbook is run.

Notice that under “tasks” are each of the “plays” in the playbook. A
description of the play is written after *-name*. This portion will be
echoed to the screen during runtime to help you follow what is going on
during runtime.

Notice that this playbook is using all F5 written modules rather than
native Ansible modules.

Most F5 modules are “idempotent” except for the ones that are used to
issue native tmsh or bash commands. So the “bigip\_command” or
“bigip\_raw” F5 modules would be idempotent for read command but not for
write commands.

Review the Modules used in the f5\_active-standby Playbook
----------------------------------------------------------

Some of the F5 modules used in these labs are still “experimental”. You
can go to https://docs.ansible.com to see all the F5 modules that are
GA. For the ones that are still “experimental”, you can go to the F5
github repository to see them.

Go to https://github.com/F5Networks/f5-ansible and go into the Library
directory and then the modules directory.

Open the bigip\_device\_connectivity.py python file. Looking through
this you can see all the options for this module as well as an example.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

NOTE: Not all examples are 100%. If you use this example, it will throw
an error stating that maybe you did not turn off certificate checking.
This example should also have a statement at the same indent as password
with “validate\_certs: no”

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Watch the TASK messages as the playbook runs to see the configuration
attributes that are occurring. Your play recap should look like below.

|image13|

Log into the GUI of both bigips. You now have an active/standby
configuration with one device as active and the other in standby and
both show “in sync”.

.. |image13| image:: media/image14.png
   :width: 6.53194in
   :height: 2.57500in
