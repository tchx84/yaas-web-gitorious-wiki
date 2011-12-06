Upgrading yaas can be done with "yum update" like any other package. This page lists any special considerations that must be kept in mind.

# Upgrading from yaas-web-0.3 to yaas-web-0.4

yaas-web-0.3 requires Rails 2 (e.g. Fedora 11 - Fedora 14), yaas-web-0.4 requires Rails 3 (Fedora 15+). You are advised to combine a system upgrade to a newer Fedora with the upgrade to yaas-web-0.4.

In yaas-web-0.4, the application root path changed from `/var/yaas-web/application` to `/var/yaas-web`. After upgrading, you will have to manually move your config file (`/var/yaas-web/application/etc/yaas.yml`) to the new location (`/var/yaas-web/etc/yaas.yml`).