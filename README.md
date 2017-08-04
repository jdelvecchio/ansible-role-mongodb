# ansible-role-mongodb

## test
Ansible role which installs and configure a mongodb replicaSet. [MongoDB](https://www.mongodb.com/)

* Install and configure a mongodb simple replicaset, with 1 primary and x secondaries
* All secondaries replicate the data and are eligible to become primary nodes
* Uses a keyfile for internal authentification inside the cluster
* Schema of the replicaSet created :
![Image of mongodb replicaset](https://docs.mongodb.com/manual/_images/replica-set-primary-with-two-secondaries.bakedsvg.svg "MongoDB ReplicaSet")


### Variables

Here is the list of all variables and their default values:

```yaml

# Paths
mongo_path: /data/mongodb					# Parent dir for data,logs and keyfile
mongo_data_path: "{{ mongo_path }}/data"			# Where to store the data
mongo_log_path: "{{ mongo_path }}/log"				# Where to store the logs
mongo_keyfile_path: "{{ mongo_path }}/keyfile"			# Where to store the keyfile (used for internal authentification)

# ReplicaSet
mongo_replset_name: jim						# Name of the replicaset
mongo_replset_init: false					# Initialize the replicaset, set to true on first run only
mongo_replset_members: ['hostname1', 'hostname2', 'hostname3']	# Hostnames of your servers, where to deploy the replicaset
mongo_replset_primary: "hostname1"				# Hostname of the primary, which server will be the primary

# Content of the keyfile, must generate it with openssl rand -base64 756
mongo_keyfile_content: ''

# Tuning
mongo_transparent_hugepage_disable: true			# Disables transparent_hugepages and transparent_hugepages_defrag

# Admin User
mongo_admin_user: 'admin'					# Admin username
mongo_admin_password: 'passwd'					# Admin password

# Logrotate
mongo_logrotate: yes
mongo_logrotate_options:
  - compress
  - copytruncate
  - daily
  - dateext
  - rotate 7
  - size 10M
```

### Usage


Clone the repo.
```bash
$ git clone https://github.com/jdelvecchio/ansible-role-mongodb
```
Then set vars in your playbook file.

Example with minimum required variables :

```yaml

- hosts: all
  gather_facts: yes
  become: yes
  roles:
    - role: ansible-role-mongodb
      mongo_replset_init: true
      mongo_replset_members: ['hostname1', 'hostname2', 'hostname3']
      mongo_replset_primary: "hostname1"
      mongo_keyfile_content: |
        sbOJJ2eEY4mUg24KUkkQgdYy+EOzNXKRCqiFhhK2a8Zv5h9SqfR7vySGSaBLMMZW
        Sk3K5ZHh++PVKyTJrnuvVsNT/oRku7ji+YeSKNqAKtWgm+ktci3/PzNk3gP9SzZC
        5KjQF/ClnwWpeZ76NIIB8te9izBDdQ/eOorYFNfmtS2PSuR2LcRvK77jUn5qkNFW
        9aqxUTjvCJxfOwVXpE9fHkhgbF0qlOhI+hDmMfKR60fqIWV98WSFdIRoFh4D2fSw
        VWTZVIxbHA/OrK5Rb5O+HHjhtDRhl9VqjJsViQ1QLusN/UBPFCMP+SiSipumwC4s
        mbIkPKQxmZQxsW9LTUmaVRdEw3pN/V94MyZD/kadMxsf0rqAYYrMjqFk/SGDn2oO
        16+xuYuXbbFJ5C1+SDpz/tgHgpu+p7U94C+lLv+fsX7ZgaEcstkGDYKAhqHy58en
        cxr6iTh0HkXe6sH2/JxmLZT+Kj003eUr5X0/KeL3DM+nVU1QVpem0gmddc8i2Mz9
        uwCYoqUCLmcrYK3JVrwi0oeWhtTGyABTGAYNjQmKT9FYw0IVMnfw2onN9Ia6wVtH
        Ve3KKKhxeOgOcN98yhXbg8yOLWShs9rR3G4bgj2sciJn5obZ9+HNui9pxsoJit8x
        2+k0ZyizNBIFQeNvuUoX215VWy2t0j4lVvFW8AhKlakhAFejrpC4xr3NZ/y0pXfU
        TAp1OKdoVveDf+GeugfwLECP/AvfKmgrxDoKE2YFyhnZZzASTpOSECyHOu+YiBDv
        esh4QQ6v7KufVhTfzUlCSLKNB56onq1SQo4nRor2/RA33yj9FuNVnrDCds+c50vD
        Ahj8v/JSKyFKAslJicFCMme/3bLycvzMzVZvHM2wWtDOmusUUvMEy2e2E2dYK1i2
        R6aTEx/EhVFa0ToVpTrwk4zNYJFgYjNZviSbeMiTSCQwmrAPNu5eicpPC6rQUp/y
        3L2lbVcR1fTqlG6SoV/EBwRkN/9RLBvb9XcXIXzNBOxqMFND
      
