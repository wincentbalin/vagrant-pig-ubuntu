This is a Vagrant file that creates an [Apache Pig](http://pig.apache.org) installation. You can run `pig -x local` just fine. Additionally, `vim` and `htop` are installed.

If you want to work with data from your host machine, just place it into this `Vagrantfile`'s directory. You will find it in the `/data` directory on the guest machine then.
