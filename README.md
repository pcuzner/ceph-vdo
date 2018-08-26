# ceph-vdo
This is a mini-project investigating the setup of ceph with vdo enabled against
OSD devices. As it stands the playbook uses filestore, and only enables vdo on the data component of an OSD (i.e. don't compress/dedupe the filestore journal!).    

The goal of the included playbook is preparation. Once preparation is complete you may continue to deploy with ceph-ansible. Follow these steps to use the preparatory playbook;  

1. Add a vdo group to ```/etc/ansible/hosts``` listing the OSD hosts
2. Update the ```group_vars/vdo.yml``` file to reflect your HDDs
3. Review ```vdosetup.yml``` to ensure any defaults used are appropriate
4. Run the ```vdosetup.yml``` playbook


Once this playbook has run you'll need to use the
```'osds_vdo.yml.sample'``` file as a example of how to update your main ```group_vars/osds.yml```. VDO volumes don't work with ceph-disk, so you need to use ceph-volume (lvm) based OSDs.

And finally, run your ceph-ansible ```site.yml``` playbook!


## Notes
- this playbook was put together for the following environment;
    - RHEL7.5 (kernel 3.10-830)
    - Ceph 12.2.2
    - vdo 6.1.0.114-14
- the initial testing was done *February 2018*.
