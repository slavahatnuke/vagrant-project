# Vagrant Project Skeleton

---

1. setup your server configuration
 * edit `Vagrantfile.install.sh`
2. `vagrant up` [docs](http://www.vagrantup.com/)
3. speedup network
 * install nfsd [ubuntu](https://help.ubuntu.com/community/SettingUpNFSHowTo)
 * edit `Vagrantfile.project.json`
 * set `"nfs": true`
 * `vagrant reload`
