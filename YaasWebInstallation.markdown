Create `/etc/yum.repos.d/yaas.repo` with the following contents:

    [inventario]
    name=Inventario
    baseurl=http://dev.laptop.org/~dsd/inventario-repo/f$releasever
    enabled=1
    gpgcheck=0

The basic setup corresponds to a typical Ruby on Rails application.

Install and enable mysql
    # yum install mysql-server
    # chkconfig mysqld on
    # service mysqld start

The yaas-web installation expects the `root` mysql user to have no password (you can add one after), and requires mysqld to be running (as above). Install it now:

    # yum install yaas-web

Install Passenger:

    # yum install mod_passenger

If using SELinux, enable apache to run in permissive mode

    # yum install selinux-policy-devel policycoreutils-python
    # semanage permissive -a httpd_t
    # semanage permissive -a passenger_t

>This command enables apache to run in "permissive" mode, meaning that your whole apache installation ignores all policies normally enforced by SELinux. I tried, and ran out of patience before being able to produce a leaner way to get passenger and SELinux working together without error.

Copy the inventario apache config into place, and customise the file to change the ServerName to one that is appropriate for the system
    # cp /usr/share/doc/inventario-*/yaas-web.conf /etc/httpd/conf.d
    # $EDITOR /etc/httpd/conf.d/yaas-web.conf

Modify the yaas-web communication configuration file:

    # vim /var/yaas-web/config/yaas.yml

Finally, (re)start apache

    # service httpd restart