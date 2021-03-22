
# drone-exec-runner
<!-- markdownlint-disable MD033 -->

[![Build Status](https://drone.osshelp.ru/api/badges/ansible/drone-exec-runner/status.svg)](https://drone.osshelp.ru/ansible/drone-exec-runner)

Role installs and configures drone-exec-runner.

## Usage (example)

### Minimal

``` yaml
roles:
  - role: drone-exec-runner
    drone_rpc_host: 'drone-ci.servername.tld'
    drone_rpc_secret: 123123123123123123123123123123213
```

### With web-interface enabled

``` yaml
  roles:
    - role: drone-exec-runner
      drone_rpc_host: 'drone-ci.servername.tld'
      drone_rpc_secret: '123123123123123123123123123123213'
      drone_ui_username: 'http-auth-user'
      drone_ui_password: 'http-auth-pass'
```

### With existed user usage and without sudo commands

``` yaml
  roles:
    - role: drone-exec-runner
      drone_rpc_host: 'drone-ci.servername.tld'
      drone_rpc_secret: '123123123123123123123123123123213'
      user: {name: root}
      sudo_commands: []
```

or with unprivileged user:

``` yaml
  roles:
    - role: drone-exec-runner
      drone_rpc_host: 'drone-ci.servername.tld'
      drone_rpc_secret: '123123123123123123123123123123213'
      user: {name: someuser}
      sudo_commands: []
```

### With custom sudo commands

``` yaml
  roles:
    - role: drone-exec-runner
      drone_rpc_host: 'drone-ci.servername.tld'
      drone_rpc_secret: '123123123123123123123123123123213'
      sudo_commands:
        - /usr/local/sbin/custom.script1
        - /usr/local/sbin/custom.script2
```

## Available parameters

### Main

| Param | Default | Description |
| -------- | -------- | -------- |
| `type` | `osshelp` | **depricated.** Installation type: osshelp build or github release |
| `user.name` | `drone` | Username for runnig drone-exec-runner |
| `drone_rpc_host` | - | **required.** Credentials to DroneCI host |
| `drone_rpc_secret` | - | **required.** Credentials to DroneCI host |
| `drone_secret_endpoint` | - | required for access to vault (e.g. `https://project-vault-endpoint.servername.tld`) |
| `drone_secret_token` | - | required for access to vault (e.g. `bea26a2221fd8090ea38720fc445eca6`) |
| `drone_ui_username` | - | required for web dashboard. Sets the basic authentication username used to authenticate and access the web dashboard |
| `drone_ui_password` | - | required for web dashboard. Sets the basic authentication password used to authenticate and access the web dashboard |
| sudo_commands | see full list [here](defaults/main.yml#L23-L35) | Commands which will run by runner with root privileges via sudo |

### Misc

| Param | Default | Description |
| -------- | -------- | -------- |
| `drone_rpc_proto` | `https` | DroneCI proto - http or https |
| `drone_http_bind` | `:19300` | Optional string value configures the http listener port |
| `drone_runner_name` | `inventory_hostname` | Runner name |
| `drone_runner_max_procs` | `4` | Limits the number of concurrent steps that a runner can execute for a single pipeline |
| `drone_runner_capacity` | `4` | Limits the number of concurrent pipelines that a runner can execute |
| `drone_runner_labels` | `"instance:" ~ inventory_hostname` | Sets labels for runner. Labels used for pipeline setting `node: { instance: hostname }` |
| `drone_runner_envirion` | `env:production` | Provides a set of global environment variables that are injected into every pipeline step |
| `drone_runner_path` | `/usr/local/bin:/usr/local/sbin:/usr/bin:/usr/sbin:/sbin:/bin` |  Sets the PATH variable for all pipeline steps |
| `drone_limit_repos` | any repo | Configures the runner to only process matching repositories |
| `drone_limit_events` | `push,tag,promote,rollback` | Provides a white list of build events that can be processed by this runner |
| `drone_log_file_max_size` | `50` | Maximum log file size in megabytes |
| `drone_log_file_max_age` | `30` | Number of days to retain |
| `drone_log_file_max_backups` | `7` | Number of files to retain |

See all avalibale parameters [here](defaults/main.yml).

## FAQ

...

## Useful links

- [Exec runner documentation](https://readme.drone.io/runner/exec/overview/)
- [Drone CI documentation](https://readme.drone.io/)
- [Drone CI plugins](https://github.com/search?q=topic%3Adrone-plugin+org%3AOSSHelp+fork%3Atrue)

## TODO

- Add setup mode. See [OSSHelp KB article](https://oss.help/kb4895)
- Fix drone_runner_envirion usage. Variable doesn't use for target option
- Fix variables names (prefix `drone_`)
- sudo_commands. Add user for commands. Default (root). If needed
- Remove installation type. Install our build only
- debug settings

## License

GPL3

## Author

OSSHelp Team, see <https://oss.help>
