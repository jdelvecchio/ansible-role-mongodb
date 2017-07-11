# ansible-role-mongodb


Ansible role which installs and configure a mongodb replicaSet. [MongoDB](https://www.mongodb.com/)

* Install and configure a mongodb simple replicaset, with 1 primary and x secondaries
* All secondaries replicate the data and are eligible to become primary nodes
* Uses a keyfile for internal authentification inside the cluster
* Schema of the replicaSet created :
![Image of mongodb replicaset](https://docs.mongodb.com/manual/_images/replica-set-primary-with-two-secondaries.bakedsvg.svg "MongoDB ReplicaSet")


#### Variables

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
mongo_keyfile_content: |
  eNkRZn2fL/1ICC0EMlPpbAKmMDLSQCfSS0lSSVCcr1E6v10Ulz/mQ5Zi5DiwhWgp
  1Exj6WW5p6UuXO2Yn2CN6aibM8OBdmYfHj/YeerfraU46ORQAaA0qePEY14zSeBu
  fk73OF9Rmu9BYQ7lBklASf07530HGrOdVej6j7PzOJuU7G9johHw23A39gstRrde
  Puevtn+QBnY8jZ6S3343JAvITtoqpCDH8J6gGf4Ab70ahODNQMExvdPjBxuN8kGx
  sLnLzsi+uLu4DUpVX8wRf1lPdS60FKxjH/SCFwOvHdYkay2gtgP8YvEOla6RonOc
  g5fCxNEKtbl0rWbwVgO4K4BCqfVgh9r26/3YIAaArXa23ieIlopv24uvE8/xoN9s
  z61rPvJYGYSNsG/o+kSitO0N9lffqfvoy1v+HST01GdvnLKkns83rk6Mn0++/Gq4
  7E1rYBssEE9oUbK90c7NCtZWDN54noCkQhqlFT5Uuh0y0X+bvtx+BjcfMtzJEHXg
  W+CoTfCEqc7+7Vr4GvPTYFXhtYw6kfEKy4+VSaahUTZ8//Dl2v/0ff/chTjhqn18
  6PhnP7TG6Q+a8yZADLGJ5cmAR5DT+A+oJAz9FLfJnzXxM6YdxaJp6VStRIek7b7j
  D0OfnzDHpulgSs8twhWEnVsV9PhES7anNSmAbK8IitEqgnvJJ4IOp+hYqpqujrlj
  OK/+o/br4rc4yG7sV/5kKnCRUQ9GDyTi+JWsgF0EotK2bn6oAbGTEQpyzIooUPDH
  5dVMDmM27o2eqY7IcriDd2KTlZ+Enau0gpCiQg5DB59hSXMzZb1OqnfQlkl89iop
  ZMYiOp1ivfX6rUBasqiiuIVv/wMOdNnoS2ojKVuCfTHSSUKC3iHbm9hwPetvDtLX
  tW6lHcLf1xt4uWH2FMPJgr/EWZ4dfhWdg7Ysnm4cWi+GLOqVDJpP0jgQGPfcp1nx
  4dvnfQVmUgpQOJTJ2ybWMQTXKW0JxStwSvY2J237ubxfDiGM

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
