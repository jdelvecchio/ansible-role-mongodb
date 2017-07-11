# ansible-role-mongodb


Ansible role which installs and configure a mongodb replicaSet with internal authentification using a keyfile.[MongoDB](http://http://www.mongodb.com/)

* Install and configure mongodb replicaSet


#### Variables

Here is the list of all variables and their default values:

```yaml


# Paths
mongo_path: /data/mongodb				# Parent dir for data,logs and keyfile
mongo_data_path: "{{ mongo_path }}/data"		# Where to store the data
mongo_log_path: "{{ mongo_path }}/log"			# Where to store the logs
mongo_keyfile_path: "{{ mongo_path }}/keyfile"		# Where to store the keyfile (used for internal authentification)

# Cluster

