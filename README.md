# ansible-role-devtools
![Build Test](https://github.com/williamsmt/ansible-role-devtools/workflows/Build%20Test/badge.svg)

An application role to configure a linux host with a configurable selection of developer tools and SDKs (e.g. Hashicorp, Google Cloud SDK, etc). Generally, this role installs Terraform, Packer, Ansible, and any corresponding test harnesses.

Requirements
------------

N/A

Role Variables
--------------

| Variable | Required | Default | Choices | Comments |
|----------|----------|---------|---------|----------|
| hashi_packages | no | null | any available Hashicorp package from the vendor repo |      |
| hashi_debian_channel | yes | main | main | Controls APT mirror used |
| hashi_rhel_channel | yes | stable | stable,test | Controls Yum mirror used |
| ansible_packages | no | null | any available python package via pip | |
| gcloud_download_root | yes | https://packages.cloud.google.com | Any public repo URL | |
| gcloud_packages | no | null | Google package name for gcloud SDK | |
| gcloud_debian_channel | yes | main | main | Controls APT mirror used |

Dependencies
------------

No dependent roles required. Many of the tasks are currently conditioned for Debian and RHEL flavor support, but can be easily modified to support other linux distributions. Please submit a PR for any enhancements you choose to include in the role.

Sample requirements.yml file for custom playbook:

    roles:
      - src: https://github.com/williamsmt/ansible-role-devtools.git
        version: 21.2.1
        name: ansible-role-devtools

To install this role using a requirements.yml file in the playbook directory:

`ansible-galaxy role install -r requirements.yml -p ./roles`

Example Playbook
----------------

Sample playbook passing mix of latest packages and specific point release versions:

    - name: Install developer tools
        hosts: all
        vars:
          hashi_packages:
            - terraform=0.13.6
            - packer
          ansible_packages:
            - ansible==2.9.18
            - ansible-lint
            - yamllint
            - molecule[docker]

        roles:
          - ./roles/ansible-role-devtools

Run the playbook as:

`ansible-playbook -i {ip_address_of_host_or_inventory_file}, playbook.yml`

License
-------

Released under the [Apache-2.0 license](LICENSE)

Author Information
------------------

https://github.com/williamsmt

This is not an officially supported Google product