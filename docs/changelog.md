# Changelog

## 0.11.0

### Fixes

- Fix not being able to parse ssh config if match keyword found [35](https://github.com/alajmo/sake/pull/35)

### Features

- Support Bastion/jump host [32](https://github.com/alajmo/sake/pull/32)

## 0.10.3

### Fixes

- Previously known_hosts didn't work correctly when specifying port other than 22
- Fix authentication failures [32](https://github.com/alajmo/sake/pull/30)

### Features

- Resolve hosts from ssh_config
- Support hashing known_host entries

## 0.10.2

### Fixes

- Allow duplicate hosts
- Fix correct exit code on remote/local task errors (#27)
- Fix local WorkDir when it's not explicitly set

## 0.10.1

### Fixes

- Small fix for WorkDir being related to calling file when server is local

## 0.10.0

### Fixes

- Fix issue where ipv6 was not added correctly to known_hosts (brackets without ip)
- Fix TTY in sub-tasks
- Only task or cmd allowed in inline `tasks` definition

### Changes

- [BREAKING CHANGE]: Updated prefix handling in text output, now supports golang templating
  - Old config:
  ```yaml
  themes:
    default:
      text:
        header: true
        header_prefix: "TASK"
        header_char: "*"
  ```

  - New config:
  ```yaml
  themes:
    default:
      text:
        header: '{{ .Style "TASK" "bold" }} {{ .Name }}'
        header_filler: "*"
  ```
- WorkDir is now relative to the calling task for local commands, previously it was to the users `cwd`
- Remove debug flag

### Features

- Add sub-command `check` to check for configuration errors
- Add `shell` property to override the default shell

## 0.1.8

### Fixes

- Support ipv6 hosts (#13)
- Fix identity_file when set via config (#7)
- Don't apply work_dir when running local tasks

## 0.1.7

### Fixes

- Use uint16 for port (#4)

## 0.1.6

This is the initial release. Basic functionality is supported: running tasks over multiple remote servers and localhost.

- Add `known_hosts_file` flag/env/config setting and `disable_verify_host` config setting
- Add `identity`/`password` pair flag/config setting
- Add sub-command ssh to easily ssh into servers
- Add `tty`/`local`/`attach` config settings
- Support nested tasks and pass down environment variables
- Add flag/config setting `ignore-unreachable` flag for ignoring unreachable servers
- Add flag/config setting `any-errors-fatal` for stopping all tasks for all servers when error is encountered
- Add `work_dir` config setting for servers and tasks
