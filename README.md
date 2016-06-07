ngrok
=====

This role will download and install ngrok binary and add a custom tunnel configuration. 

Requirements
------------

None

Role Variables
--------------

| Name                     | Default                                                            | Description                                                                 |
|:-------------------------|:-------------------------------------------------------------------|:----------------------------------------------------------------------------|
| ngrok_download           | https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip  |                                                                             |
| ngrok_path_download_tmp  | /tmp                                                               |                                                                             |
| ngrok_path_install       | /opt/ngrok                                                         |                                                                             |
| ngrok_path_bin           | /usr/bin/ngrok                                                     |                                                                             |
| ngrok_path_init          | /etc/init.d                                                        |                                                                             |
| ngrok_auth_token         |                                                                    | **required**, to be set in playbook vars                                    |
| ngrok_console_ui         | false                                                              |                                                                             |
| ngrok_region             | eu                                                                 |                                                                             |
| ngrok_tunnels            | []                                                                 |                                                                             |
| ngrok_user               |                                                                    | optional, default if not set: ansible_ssh_user                              |
| ngrok_start_tunnel       | --all                                                              | tunnel to run in service (optional), by default all tunnels will be started |
| ngrok_install_as_service | false                                                              | creates init script                                                         |
| ngrok_service_name       | ngrok                                                              |                                                                             |
| ngrok_daemon             | {{ ngrok_path_bin }}                                               |                                                                             |
| ngrok_daemon_opts        | start {{ ngrok_start_tunnel }} --config /home/{{ ngrok_user }}/.ngrok2/ngrok.yml |                                                               |
| ngrok_pidfile            | /var/run/ngrok.pid                                                 |                                                                             |

**Example for a tunnel configuration:**

```
ngrok_tunnels:
  - name:       "custom-name-for-tunnel"
    hostname:   "my-custom-host.ngrok.io"    # optional
    subdomain:  "my-custom-subdomain"        # subdomain for ngrok.io (optional), only used if hostname is not defined.
                                             # if subdomain is also not defined, ngrok uses tunnel name as subdomain
    address:    "my.local.address:80"
    proto:      "http"                       # optional, default: http
    bind_tls:   both                         # optional, default: both (false: only http, true: only https, both: http & https)
    auth:
      username: "ngrokuser"
      password: "secretpassword"
```

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: "votum.ngrok" }

License
-------

This project is under the MIT License. See the [LICENSE](LICENSE) file for the full license text.

Author Information
------------------

[Bernd Alter](https://github.com/bazoo0815) / [VOTUM GmbH](https://votum.de)
