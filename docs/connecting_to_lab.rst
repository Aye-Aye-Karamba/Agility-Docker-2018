**Last Revised on July 20\ , 2018**

**Version 1.4**

|image0|


Administrating F5 with Ansible
------------------------------

**Document Owners:**

**Mark Lowcher**

1. .. rubric:: *Connecting to your Lab environment*
      :name: connecting-to-your-lab-environment
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

Connecting to the jump server
-----------------------------

Start an RDP connection to the FQDN that I sent you in an email last
night. This will be your Jump server.

Logon is:

-  Username: user

-  Password: Agility1.

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
.. |image9| image:: media/image10.png
   :width: 6.53194in
   :height: 2.06667in
.. |image10| image:: media/image11.png
   :width: 6.53194in
   :height: 2.00417in
.. |image11| image:: media/image12.png
   :width: 6.53194in
   :height: 2.84931in
.. |image12| image:: media/image13.png
   :width: 4.60494in
   :height: 2.58887in
.. |image13| image:: media/image14.png
   :width: 6.53194in
   :height: 2.57500in
.. |image14| image:: media/image15.png
   :width: 6.53194in
   :height: 1.15069in
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
