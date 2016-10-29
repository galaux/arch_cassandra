# Arch Linux User Repository package for Cassandra

## TODO

- [x] use proper PGP signatures check
- [x] remove `.install` file from `source` array
- [x] links created in install scripts are not tracked by pacman and should
       thus be avoided
- [x] groups should not be removed when package is uninstalled because
       left-over files in `/var/lib/cassandra` would thus be left without owner
       and group
  - remove `post_remove` function from install scripts
- [x] use Systemd's `ProtectSystem` and `ProtectHome` in service file
- [ ] extract and create dependency `sigar` (will require
      `aur/apache-ant-cpptasks`)
- [x] remove PowerShell scripts from package
- [x] get rid of patch `fix_cassandra_home_path` and use a `sed … > …`
- [ ] use Systemd logging?
- [x] when stopped, `systemd status cassandra` says `failed`: fix that
- [ ] check limits set in service file (specifically `infinity` values)
- [x] remove `JAVA_HOME` from Systemd service file? (no need to set it)
- [x] remove execute rights to `bin/stop-server`
- [x] remove script `cqlsh` as it just tries to figure out whether Python2 is
      installed and afterwards just run `cqlsh.py` which actually itself is a
      shell script (and not a python one). In `/usr/bin`, create link `cqlsh`
      that points to `cqlsh.py`
- [x] fix dependency on Python: requires `python2` and not `python`
- [x] either make the package depend on `python2` or package all Python CLI
      on their own
