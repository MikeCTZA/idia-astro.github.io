---
layout: page
title: Access to IDIA Cloud
permalink: /access/
---

This page provides details on how to obtain access to the virtual machines in the IDIA cloud system.

Please identify the projecct team that you are a part of when you request access. This is
important, since it allows us to provide you with access to the relevant project files.

# Requesting Access to the IDIA Machines

If you are already part of an IDIA project team, you can request access as follows:

* Send an email to **support@idia.ac.za** with the following information:
    * The name of your project team.
    * Your home institution.
    * Your local phone number (so that we can call you if there's a security problem).
    * The MeerKAT science projects that you are involved in, if applicable.
    * Your preferred username, first-name and last-name.
    * Your [ssh public key][sshkey].

Your username, password and SSH public key will be added to LDAP (default username will be created
from pre-@ part of email)

This will enable you to log into all IDIA machines that connect to LDAP, allowing you to log into
VMs using ssh using their SSH key without needing to use your password.

# Access

You can access IDIA machines via a Jupyter-Hub (preferred) or SSH (traditional). 

The URL usually corresponds to the name of the VM, and is served on the IDIA domain. For example,
our **helo** node can be accessed via [https://helo.idia.ac.za][helo].

### Jupyter-Hub
A Virtual Machine (VM) can be accessed online using your browser (Chrome/Firefox preferred). Simply
type in the URL provided.

You will be presented with a login window for the Jupyter-Hub. Use your previously generated (LDAP)
username and password to access your account.

### SSH
To `SSH` into an IDIA VM, you will need your SSH key. 

This is how you would `SSH` into **helo** with X-forwarding:
````bash
$ ssh  -XY -i /path/to/your/key.pem helo.idia.ac.za -l <username>
````

# Changing your Password
You need to change your generic password as soon as possible. You can do this with the following
command (one line on the prompt):

`$ ldappasswd -H ldap://10.102.4.109 -x -D "cn=username,ou=users,dc=idia,dc=arc,dc=ac,dc=za" -W -S -A`

*Important:* In the command above, you will need to change `username` to your _username_.

You will then be prompted for passwords as follows:
* Twice for your current password (verification).
* Twice for your new password. 
* Once for your _LDAP_ password, which will be your *old* password. This is required to bind to the
  LDAP server to commit the change to your password. 

This is a little more involved then usual, because your credentials are not specific to a machine.
Access on the cloud is coordinated on using the LDAP server -- this is why you need to do the
_authenticate -> enter new password -> authorize/bind_ process to propagate your password to the
server. This allows us to provide you with access to any machine provisioned for your project
without having to remember a myriad of passwords. 

Incidentally, you can do this without ssh'ing into the machine -- simply open up a terminal using
the Jupyter-Hub and use this to change your password.

# Storage
 All virtual machines will have the IDIA storage attached. You will have access to your work and your data on any system that you're
logged into. Access to data is managed with Unix groups.

There are several storage areas available.

* `/users/<username>/`, where `/users` is a shared BeeGFS volume.
* `/data/users/<username>/`, where `/data` is a shared BeeGFS volume. This is the preferred space
  for you to store your longish term data products.
* `/data/<Project>` is a shared directory on BeeGFS for a project. You can fetch raw data from here.
  Please steer away from dumping data into this directory.
* `/scratch/users/<username>/` is the shared working directory for <username>, where `/scratch` is a
  BeeGFS volume). This is the preferred space for intermediate data products, e.g., you can use this
  space to do imaging.


# GitHub
* [IDIA Containers][idia-containers]: Provides a repository for the [Singularity][singularity] containers used at IDIA.

[idia-containers]: https://github.com/AfricanResearchCloud/idia-containers
[singularity]: http://singularity.lbl.gov/
[sshkey]: https://confluence.atlassian.com/bitbucketserver/creating-ssh-keys-776639788.html
[helo]: https://helo.idia.ac.za
[request-vm]: https://docs.google.com/forms/d/e/1FAIpQLSc6GwFfqTUcKVmkcmn1VRIBADp-_JOSVt9aW1dfNmc12kxuvg/viewform
