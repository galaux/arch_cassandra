# `arch_cassandra`

Arch Linux User Repository package for [Cassandra](https://cassandra.apache.org/).

This is **a clone** of [AUR Cassandra package](https://aur.archlinux.org/packages/cassandra/)
augmented with several patches. Commits should be self-explanatory.

## TODO

- [ ] move data dir to `/var/lib/cassandra/` (watch out for out of package
      linked dirs in `.install`!)
- [ ] remove non x86_64 sigar files
- [ ] extract sigar lib?
- [ ] investigate logs not being sent to Systemd
