*Lab 8 – Adding an Application using an iApp Template*
======================================================

1. .. rubric:: *Adding an Application using an iApp Template*
      :name: lab-8---add-app-using-iapp-template
      :class: H1

IApp templates are the best practice for configuring application
deployment when using automation. When you deploy with an iApp template,
you define the desired end state and all objects configured for that
application are managed as a “service”. Should you decide to remove the
“service” you can re-run the Ansible playbook that utilized an iApp with
the “state: absent” option. This will remove ALL objects associated with
that “service”. It will not affect the objects that are “network based”
In other words, it your service used vlan 10, it will not remove that
vlan or it’s self ip addresses.

 Review the deploy\_app\_svcs\_waf Playbook
-------------------------------------------

F5 maintains iApp templates and updates them. Your software version will
not have the latest version of an iApp. You should always make sure you
have the latest version of the iApp you will be using.

Most iApps are for deploying a specific application. The iApp we will be
using is maintained and available at F5’s Github repository. It is
called the “F5-application-services-integration-iApp” and can be found
at:

https://github.com/F5Networks/f5-application-services-integration-iApp

This iApp is specifically meant for http/https applications that will
attach layer 4-7 services to the application “service”.

The following link will lead to F5’s Devcentral to download the
documentation of how you can modify the app-svcs iApp to bundle in
various security and authentication policies as well as iRules into your
iApp.

You can then use the modified iApp to deploy a service with the exact
layer 4-7 services you wish to use.

https://devcentral.f5.com/wiki/iApp.AppSvcsiApp_userguide_userguide.ashx

For this lab the app-svcs iApp we will use is already on the Ansible
control machine. It has already been bundled with 3 different “Web
Application Firewall” policies named:

-  Linux-low

-  Linux-medium

-  Linux-high

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

NOTE: Currently the app-svcs-iapp does not create the clientssl profile
for you. That is why we did so in the previous lab. At a later date the
app-svcs-iapp may be updated to create the clientssl profile for you. If
that happens you would no longer use the “create\_clientssl\_profile”
playbook but you would still use the “push\_cert\_and\_key\_to\_bigip”
playbook to stage the files for the iApp to use.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Now open and review the “deploy\_app\_svcs\_waf” playbook.

Under “vars” you will notice that we will only be addressing one bigip
for reasons described above.

You will need to change the server var to point to one of your bigips.
Lets pick bigip1. Replace the current ip address with 10.1.0.20 or
bigip1 or bigip[0]. Change the policy name to any name you wish.

Notice under the first TASK we will be pushing our iApp to the bigip.
Verify that the iApp we will be pushing out is currently in the correct
directory on the Ansible machine and that the iApp name is correct.

See screenshot below. Also notice that the “state is “present”. If we
wanted to remove the iApp from the bigip we could change “present” to
“absent”.

|image15|

Now look at the second task in the playbook.

|image16|

An iApp template is a list of questions that you answer, and responses
are the variables used to create the service. For automation purposes we
fill out the iApp template in the GUI with our desired options and
deploy the iApp. We can then follow the documentation above from the
app-svcs guide to extract the variables into a json file. This has
already been done and is in the file named waf\_final.json under
/var/tmp in the Ansible virtual machine.

In the

 Review the waf\_final.json File
--------------------------------

Open the waf\_final.json file and review it.

-  Which ASM policy is currently defined to be attached the application?
   Low, medium or high?

-  Are there any pool members defined? How many?

-  Look for clientssl within the file by typing */clientssl* and hitting
   Enter. We want to use the clientssl profile we created earlier named
   “agility2018\_clientssl” Is that the clientssl currently entered to
   be used?

-  Type */.crt* and hit Enter. Is the file configured to use the correct
   certificate?

-  Type */.key* and hit Enter. Is the file configured to use the correct
   key?

-  Go through the rest of the file and notice how all our profiles are
   already defined. For TCP profile we have tcp-lan-optimized, for SNAT
   we have “automap” defined.

-  Go back to the top of the file and type */vs\_Name* and hit Enter.
   The current name of the VIP is “cust7\_waf” Change the vip name to
   one of your choosing. Save and close the file.

   1. .. rubric::  Run the deploy\_app\_svcs\_waf Playbook
         :name: run-the-deploy_app_svcs_waf-playbook
         :class: H2

Go into the GUI of bigip1. Go to iApps -> Application Services. Notice
that the Application Services currently has no applications.

|image17|

Run the deploy\_app\_svcs\_waf playbook.

-  Go back into the GUI of the bigip1 and into iApps -> Application
   Services. You should now see one application that used the
   appsvcs\_integration\_v2.0.004\_test iapp.

-  Click on the application name. You can see all the components that
   were created when the playbook was run.

-  Click on the “reconfigure” tab up top. You now see the iApp template
   with all the variables populated from the waf\_final.json file.

-  Go to Local Traffic -> Network Map. Notice that two vips were
   created. One is a port 80 vip with an irule that does a redirect to
   the port 443 vip. This is to catch users that may enter HTTP into
   their browsers rather than HTTPS.

-  Open the https vip and notice all the profiles associated with the
   vip. Remember the SNAT automap in the json file? Notice that SNAT
   automap has been applied.

-  Go to Security -> Application Security -> Security Policies. Notice
   that there are three ASM policies. These are the 3 policies that were
   bundled into the iApp. Notice that the *linux-high* policy is
   currently applied to our application.

-  Go to iApps -> Application Services and re-open the application. You
   are now in the components view we saw earlier. Switch to the
   “Reconfigure” tab. Now you see the iApp populated with all the
   variables from the json file.

-  Scroll down to near the bottom to L7 Policy Rules Action. Change the
   “bundled:linux-high” to “bundled:linux-medium”. Just edit the current
   field by replacing *high* with *medium* then go to the bottom and
   click finish.

    |image18|

-  Once the component view is display again go back to Security ->
   Application Security -> Security Policies. Notice that the *medium*
   policy is now applied to the vip.

-  Go back to the deploy\_app\_svcs\_waf playbook and change the “state”
   under “vars” to “absent”. Notice that the second task uses a variable
   for the state while the pushing of the iApp has the state hardcoded
   to present. By changing the state under vars we will be removing the
   application but we will leave the iApp on the bigip as its state is
   hardcoded

-  Re-run the deploy\_app\_svcs\_waf playbook.

-  Notice the PLAY RECAP is yellow showing that there has been a change.

-  Go back to the iApps applications. Notice that the application
   service is gone.

-  Click on the “Create” button. From the template drop down look for
   the appsvcs\_integration\_v2.0.004\_test iApp. It is still there.

   1. .. rubric:: – Using include to build a workflow
         :name: using-include-to-build-a-workflow
         :class: H2

Open and look at the “include” playbook. Notice that you can “stitch”
your playbooks together to create a workflow. You could also add
individual plays between playbooks.

.. |image15| image:: media/image16.png
   :width: 6.53194in
   :height: 1.69931in
.. |image16| image:: media/image17.png
   :width: 6.53194in
   :height: 1.90972in
.. |image17| image:: media/image18.png
   :width: 6.53194in
   :height: 1.33125in
.. |image18| image:: media/image19.png
   :width: 6.53194in
   :height: 0.75208in
