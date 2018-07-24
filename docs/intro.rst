**Last Revised on July 20\ , 2018**

**Version 1.4**

|image0|


*Lab 1 - Connecting to your Lab Environment*
============================================

**Document Owners:**

**Mark Lowcher**

1. .. rubric:: *Connecting to your Lab environment*
      :name: lab1---connecting-to-your-lab-environment
      :class: H1

  1.  .. rubric:: Lab Topology
         :name: lab-topology
         :class: H2

There are 4 virtual machines in your cloud lab. Every student will have
their own lab environment with the same ip addressing. 

.. NOTE::
    Connection to the Lab environment will be to a Windows Jump server. Access to the other
    virtual machines will be from the jump server. The screenshot below
    shows the layout of the lab.

The ip addressing for all the virtual machines is shown on the diagram.

|image1|

**Connecting to the jump server**

Start an RDP connection to the FQDN that I sent you in an email last
night. This will be your Jump server.

Logon is:

-  Username: user

-  Password: Agility1.

As you attempt to login, your RDP client will have the username last used. 
You may need to click on "More choices" and then "Use a different account"
to enter the correct username and password.

Once your Remote Desktop session has started. You may access both Bigips
GUI using the shortcuts seen in the Chrome browser on your Windows
desktop.

|image2|

You can also access the Ansible machine and both Bigips through the
Putty on the desktop.

|image3|

.. |image0| image:: media/image1.jpeg
   :width: 2.72923in
   :height: 2.39167in
.. |image1| image:: media/image2.png
   :width: 6.53194in
   :height: 3.79653in
.. |image2| image:: media/image3.png
   :width: 4.58333in
   :height: 0.97917in
.. |image3| image:: media/image4.png
   :width: 3.90000in
   :height: 3.73856in
