Create `/etc/yum.repos.d/yaas.repo` with the following contents:

    [yaas]
    name=Inventario
    baseurl=http://dev.laptop.org/~dsd/inventario-repo/f16
    enabled=1
    gpgcheck=0

Install the package:

    # yum install yaas-server

Generate a key pair for the SSL security:

    # openssl req -new -x509 -days 9999 -nodes -out pkey-cert.pem -keyout pkey-key.pem

Put the keys somewhere safe, and change and restrict access to the user running the yaas-server, which has to match the user executing bios-crypto script:

    # chown OWNER pkey-*.pem
    # chmod go-rwx pkey-*.pem

Install bios-crypto (e.g. in the home directory of the user that will run yaas-server)
    # yum install git make gcc zlib-devel
    # git clone git://dev.laptop.org/bios-crypto
    # cd bios-crypto/build
    # make cli

Place your private master keys developer keys and leases at

* `bios-crypto/build/developer.public`
* `bios-crypto/build/developer.private`
* `bios-crypto/build/lease.public`
* `bios-crypto/build/lease.private`

Modify the yaas-server configuration file with your favorite text editor:

    # cp /opt/yaas-server/etc/yaas.config.example /opt/yaas-server/etc/yaas.config
    # vim /opt/yaas-server/etc/yaas.config

Start the server:

    # chkconfig yaas on
    # service yaas-server start
