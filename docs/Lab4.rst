*Lab 4- Licensing the Bigips*
============================

1. .. rubric:: *Licensing the Bigips*
      :name: lab-4---Licensing-the-Bigips
      :class: H1

Open the “license\_F5\_pair.yml” playbook. Edit the file by replacing
the existing registration keys with the ones that were provided for you.

Notice the use of bigip[0] to address the first bigip in the
/etc/ansible/hosts file and bigip[1] to address the second bigip. This
tells the playbook to use the first registration key for the first bigip
in the /etc/ansible/hosts file and the second registration key for the
second Bigip. You could also use bigip1 and bigip2. Save and close this
file.

Access the GUI of the bigips from Chrome on the Jump server. Logon is
admin/Agility1. Verify that both your bigips are not licensed.

Both bigip screens should look like below. Notice that both devices have
a hostname of bigip1. This is the default of a fresh installation.
Verify that both show “No license exists for this device” and that the
screen is on the “Setup Utility” wizard.

Log out of the GUI but leave the tabs open.

|image10|

Now go back to your Ansible SSH session and run the
“license\_F5\_pair.yml” playbook with the following command.

*ansible-playbook license\_F5\_pair.yml*.

Below is an example of a successful run.

Notice that changes are shown in yellow and that both devices were
licensed in one pass.

Notice that what was written in the playbook under tasks and after
*-name* is echoed to the screen.

Notice that this playbook is using the Ansible “raw” module rather than
F5 written modules. It is always best to use modules written by the
vendor but in cases where there is no vendor written modules for your
desired task, you can always use Ansible written modules.

At a later time, be sure to go to https://docs.ansible.com to take a
look at all the modules that are available for use.

|image11|

Log back in to the GUI and verify that both bigips no longer show the
not licensed message and that they are both still on the “Setup Utility”
wizard. (this might take a minute as licensing causes some daemons to
restart)

If one or both are not on the setup utility screen you will need to
reset the device(s) to factory default. Use the following Ansible ad-hoc
command. For instance, if the first bigip needs to be reset issue the
following:

*ansible -a ‘tmsh load sys config default’ bigip1*

Native tmsh or bash commands can be run with the ansible -a flag and the
command wrapped in single quotes. At the end you target the systems you
want to address. If you wanted to reset both devices you would change
*bigip1* to just *bigip*. This would then target ALL devices under the
heading of [bigip] in your /etc/ansible/hosts file.

After the command has finished executing, ssh into that device and
verify that the system does not require a reboot. The command line and
the GUI will either show “Active:Standalone” or REBOOT REQUIRED. If it
reads the later, go to the Ansible ssh session and enter the following
ad-hoc command.

*ansible -a ‘reboot’ bigip1 (or bigip2 of bigip if both need it.)*

Notice the time saved and ease of using Ansible ad-hoc commands for one
off commands.

Go into each GUI and verify that both bigips are now at the “System
Utility” wizard and the no license message is gone and there are no
reboot required messages.

.. |image10| image:: media/image11.png
   :width: 6.53194in
   :height: 2.00417in
.. |image11| image:: media/image12.png
   :width: 6.53194in
   :height: 2.84931in