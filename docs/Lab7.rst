*Lab 7 – Creating a clientssl Profile*
====================================

1. .. rubric:: *Create a clientssl profile*
      :name: lab-6---creating-the-default-passwords
      :class: H1

A clientssl profile consists of a digital certificate and a private key.
Adding a clientssl profile to a virtual server will cause the bigip to
decrypt client connections as they come into the VIP.

Now that we have a certificate and key pushed up to the bigip, we can
create a clientssl profile.

Review the create\_clientssl\_profile Playbook
----------------------------------------------

Open the create\_clientssl\_profile playbook. Verify that all the
variables are correct for your environment.

Notice that the variable “cert\_chain” has a placeholder of “xxxxxx” and
that the “chain” under cert\_key\_chain” has been commented out with a
hashtag. That is because we will not be using a chain certificate. If in
the future, you needed to add one you would simply upload it to the
bigip and then enter the correct variable name and uncomment the chain:
"{{cert\_chain}}" line.

Notice the ciphers line. ciphers:
"!SSLv3:!SSLv2:ECDHE+AES-GCM+SHA256:ECDHE-RSA-AES128-CBC-SHA"

We are setting the desired ciphers within the playbook. We are turning
off unsecure ciphers such as SSLv2 and SSLv3 and we are specifying the
list of ciphers that we want to support. This is a secure set of ciphers
that would get your website an A+ rating by SSLlabs.

Go into the GUI under Local Traffic -> Profiles -> SSL -> Client and
look at the existing clientssl profiles. There should be 5 default
clientssl profiles.

Run the create\_clientssl\_profile Playbook
-------------------------------------------

Run the create\_clientssl\_profile playbook. 

*ansible-playbook create_clientssl_profile.yml*

Go back into the GUI of bigip1 and verify that there is now a new 
clientssl profile named “agility2018\_clientssl”.

Click the profile to open it up.

Notice next to “Certificate Key Chain” that the f5agility2018
certificate and key were used for this profile.

Click the “custom” check box on the right to ungray the “Configuration”
section. Now change this section from “basic” to “advanced”.

Notice that a new section popped up under the “Certificate Key Chain”
named “ciphers”.

Notice that instead of the ciphers being “DEFAULT” that they contain the
strong ciphers we specified in the playbook.
