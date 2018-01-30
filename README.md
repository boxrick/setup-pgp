setup-pgp
=========

This module installs and sets up gnupg (PGP) on Ubuntu and OSX systems. The intent here is to simplify the management of GPG to allow easy use on multiple systems.

Requirements
------------

This module requires Ansible 2.4

Role Variables
--------------

See defaults for variables and descriptions

## Usage

This role works best when a private key is generated as follows:

#gpg(2) --gen-key

Then export it and place it in the files directory of this role, this will prompt for a passphrase.

#gpg --export-secret-key -a > private.key

If no private key is provided one will be generated based on variables passed into this role ( A mininum of real_name and email_address and optional passphrase) GPG1 is used for generating the keys since it doesn't rely on a passphrase. If any private keys are present under the user then nothing will be changed.

Secondly this role takes a list of GPG keyids and pulls them down from the key server and generates implicit trust for all. This is to ease some of the manual setup required around GPG.

Finally this role will push your public key upstream, this behaviour can be overidden and it only happens if the key does not already exist in keyserver

Dependencies
------------

This role

Example Playbook
----------------

Example to call:

    - hosts: all
      roles:
         - { role: setup-pgp }
