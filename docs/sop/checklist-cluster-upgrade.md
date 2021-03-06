- [ ] If the minor version of openshift has not been used in an upgrade before
  - [ ] Vendor the required version of openshift ansible version of openshift-ansible
  - [ ] Setup tech profile: https://github.com/openshift/openshift-ansible-ops/pull/2431/files
- [ ] If the cluster has not been upgraded before
  - [ ] Ensure that there is an ssh key for the cluster in Jenkins
  - [ ] Setup tower authorized_keys for the ssh key
  - [ ] Create the template directory for the cluster (including upgrading the private AWS information for the cluster)
  - [ ] If the job is an upgrade, log into the cluster and remove any legacy yum repos
- [ ] Re-vendor appropriate openshift-ansible if it is still not dynamic  (origin/openshift-ansible:stage? release-1.5?)
- [ ] Modify cluster template with target OpenShift version: openshift-ansible-private/private_roles/aos-cicd/files/CLUSTER/CLUSTER_aws_cluster_setup.yml
- [ ] Check that the yum repo for the cluster's target version is accurate: openshift-ansible-private/private_vars/global/aws/dev-preview-int/int/dev-preview-int/yum_extra_repos.yml
  - e.g. Set to https://mirror.openshift.com/enterprise/enterprise-3.4/latest/x86_64/os/ if back leveling to 3.4
- [ ] Ensure that firewall settings are correct for the cluster (e.g. disable firewalld in config loop if the cluster is using iptables): openshift-ansible-private/private_vars/global/aws/CLUSTER/ENVIRONMENT/CLUSTER/main.yml  (os_firewall_use_firewalld: false)
- [ ] Change g_play_openshift_version for the cluster if appropriate: openshift-ansible-ops/playbooks/site/CLUSTER/openshift_master.yml
- [ ] Make sure, within the logging namespace, that the logging pvcs are labeled logging-infra=support  (e.g. oc label pvc logging-es- logging-infra=support). https://github.com/openshift/openshift-ansible/issues/3896
- [ ] Make sure that metrics pvcs are labeled in the openshift-infra namespace with metrics-infra: hawkular-cassandra 
- [ ] Make sure that the cluster does not contain any openshift, openshift-, kube, kube- namespaces which have a requester annotation.
