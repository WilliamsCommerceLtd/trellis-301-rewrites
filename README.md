Trellis 301 rewrites
====================

This role is designed to work with [Trellis](https://github.com/roots/trellis). It will allow you to add a 301 rewrites file to nginx.

Requirements
------------

This role is made for Trellis (previously known as Bedrock-Ansible), so it depends on it.

Role Variables
--------------

The role will read from the `wordpress_sites` dict set in environments files of Trellis. It will check if the `nginxrewrites` key is defined.

Example:
--------
<pre>
wordpress_sites:
  example.com:
    site_hosts:
      - canonical: example.dev
    local_path: '../site' # path targeting local Bedrock site directory (relative to Ansible root)
    admin_email: admin@example.dev
    multisite:
      enabled: false
    ssl:
      enabled: false
    cache:
      enabled: false
    <b>nginxrewrites:</b>
</pre>

Adding rewrites
---------------
You will need to create a directory within yor trellis root called 'rewrites' witing there create a file called 'nginxrewrites', you will need to put yor rewrites in this file.
An example rewrite will look like:
<pre>
rewrite ^/some/url$ /some/other/url permanent;
</pre>

Dependencies
------------

[Trellis](https://github.com/roots/trellis).

Example Playbook
----------------

To get started, add this role (`WilliamsCommerceLtd.trellis-301-rewrites`) to the `requirements.yml` file in your Trellis installation like so:

```
- name: trellis-301-rewrites
  src: WilliamsCommerceLtd.trellis-301-rewrites
  version: 1.0.0
```

Then re-run the `ansible-galaxy install -r requirements.yml` to install the new role. You might need to add the `-f` option to force install of previously downloaded roles.

You will also need to add the role to the `server.yml` like so:

```
roles:
  ... other Trellis roles ...
  - { role: trellis-301-rewrites, tags: [rewrites] }
```


Adding / Removing nginxrewrites
--------------------------------------
**To Add**: Run the Trellis command to set up your previously configured remote server: `ansible-playbook server.yml -e env=<environment>`
**To Remove**: Remove the `nginxrewrites` key from `wordpress_sites` and reconfigure via: `ansible-playbook server.yml -e env=<environment>`
