Upgrading yaas can be done with "yum update" like any other package. This page lists any special considerations that must be kept in mind.

# Upgrading v0.3 to v0.4

yaas-web-0.3 requires Rails 2 (e.g. Fedora 11 - Fedora 14), yaas-web-0.4 requires Rails 3 (Fedora 15+). You are advised to combine a system upgrade to a newer Fedora with the upgrade to yaas-web-0.4.

In yaas-web-0.4, the application root path changed from `/var/yaas-web/application` to `/var/yaas-web`. After upgrading, you will have to manually move your config file (`/var/yaas-web/application/etc/yaas.yml`) to the new location (`/var/yaas-web/etc/yaas.yml`).

# Upgrading v0.4 to v0.5

When upgrading from v0.4 to v0.5 (e.g. updating to Ruby-1.9), we had to make some changes (improvements) to work with Ruby's improved unicode support. This exposed the fact that we were previously storing UTF-8 data in latin1 columns in the MySQL database. As this raw UTF8 data will now be encoded as latin1 under the new setup, you need to perform a one-off conversion to UTF-8 with:

 rake utf8_migration:run
