# [Nginx Configuration Boilerplate](https://github.com/kwelong/nginx-configs)

**Nginx Configuration Boilerplate** is a collection of snippets to ease the
management of configuration. I have incorporated performance and security
related configuration  as much as possible.

## Getting Started

### Prerequisites

* [Nginx Beginners Guide](https://nginx.org/en/docs/beginners_guide.html)
* [Nginx Request Processing](https://nginx.org/en/docs/http/request_processing.html)


### Check distro-specific settings

Most specific variables are:

* `user`
* `group`
* `pid`
* `socket`
* `web root`
* `error_log`
* `access_log`

### Nginx test and restart

* To verify Nginx config

  ```shell
  nginx -t
  ```

* To verify Nginx config with a custom file

  ```shell
  nginx -t -c nginx.conf
  ```

* To reload Nginx and apply the new config

  ```shell
  nginx -s reload
  systemctl reload nginx
  ```

## Configuration structure

The configuration has the following structure:

```text
/etc/nginx
├── conf-available/
│   ├── 0-general.conf
│   └── ...
├── conf-enabled/
│   ├── 0-general.conf
│   └── ...
├── sites-available/
│   ├── 99-example.com.conf
│   └── ...
├── sites-enabled/
│   ├── 99-example.com.conf
│   └── ...
├── templates/
│   ├── ssl.tmpl
│   └── ...
├── ssl/
│   ├── example.com
│   │   └── ...
│   └── ...
├── mime.types
├── nginx.conf
└── ...
```

* **`conf-available/`**

  This directory contains config snippets (mixins) to be included as desired.
  The files **are not** loaded automatically. If you want to enable a configuration,
  please soft link it into `conf-enabled` directory.

* **`conf-enabled/`**

  Except if they are dot prefixed or non `.conf` extension, all files in this
  directory **are** loaded automatically. You should soft link the enabled
  configuration file from `conf-available` directory into this directory.

* **`sites-available/`**

  This directory contains all the `server` (site specific) definitions.
  The files in this directory **are not** loaded automatically.
  If you want to enable a specific configuration file, create a soft link
  in the `sites-enabled` directory.

* **`sites-enabled/`**

  Except if they are dot prefixed or non `.conf` extension, all files in this
  directory **are** loaded automatically. You should soft link the enabled site
  configuration file from `sites-available` directory into this directory.
  The files are loaded in alphabetical order.

* **`templates/`**

  Files in this directory contain a `server` template for secure and non-secure
  hosts. They are intended to be included in the site-specific configuration
  files in `sites-available`.

## Acknowledgements

[Nginx Configuration Boilerplate](https://github.com/kwelong/nginx-configs) borrows
the idea from the awesome [Nginx Server Configs](https://github.com/h5bp/server-configs-nginx)
and unknown contributors on the Internet.

