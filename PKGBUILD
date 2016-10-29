# Maintainer: Carsten Feuls <archlinux@carstenfeuls.de>
# Contributor: Guillaume ALAUX <guillaume at alaux dot net>
# Contributor: Thomas Dziedzic < gostrc at gmail >
# Contributor: Konstantin Nikiforov <helllamer@gmail.com> 
# Contributor: Alper Kanat <alperkanat@raptiye.org>
# Contributor: adam2fours <adam@2fours.com>

# check() function is used to verify GPG signature. check() imports 3 keys into your GPG keyring at first build.
# See http://scarybeastsecurity.blogspot.com/2011/07/alert-vsftpd-download-backdoored.html for reason of this step.
# If you have problems with gpg, you can remove check() function, and all will be ok.

pkgname=cassandra
pkgver=3.9
pkgrel=1
pkgdesc='Apache Cassandra NoSQL database'
arch=('any')
url='http://cassandra.apache.org/'
license=('APACHE')
depends=('java-runtime' 'python2')
backup=(etc/cassandra/cassandra-env.sh
        etc/cassandra/cassandra-rackdc.properties
        etc/cassandra/cassandra-topology.properties
        etc/cassandra/cassandra.yaml
        etc/cassandra/commitlog_archiving.properties
        etc/cassandra/logback.xml
        etc/cassandra/logback-tools.xml)
install=cassandra.install
source=(http://www.apache.org/dist/${pkgname}/${pkgver}/apache-${pkgname}-${pkgver}-bin.tar.gz{,.asc}
        'cassandra.service'
        'cassandra-tmpfile.conf'
        'cassandra-user.conf')
validpgpkeys=('A26E528B271F19B9E5D8E19EA278B781FE4B2BDA') # Michael Shuler

sha256sums=('27cf88a6bce1ee2fb1a1c936094b9200ad844414c2b5b1491ba4991fcc0fd693'
            'SKIP'
            '6a15c8e12c55e1f84a99a0065a255b319bc781c2dbed45ee9f1a94e55aaab925'
            '7ea0024331734b9755b6fa2ed1881f9bc608b551990b96f14e80406cb6b05eb8'
            '7a87a4369ca2c13558fa8733f6abdcf548c63dda8a16790b5bcc20bae597ee91')

package() {
  cd ${srcdir}/apache-cassandra-${pkgver}

  mkdir -p ${pkgdir}/{etc/cassandra,var/log/cassandra}
  mkdir -p ${pkgdir}/{usr/bin,usr/share/cassandra,usr/share/java/cassandra}

  cp -a bin interface pylib tools ${pkgdir}/usr/share/cassandra

  # `cqlsh` just checks Python 2.7 is available then calls `cqlsh.py`
  # which actully is a shell script, not a Python one
  rm ${pkgdir}/usr/share/cassandra/bin/{cqlsh,cassandra.in.sh,*.bat,*.ps1}
  chmod -x ${pkgdir}/usr/share/cassandra/bin/stop-server
  pushd ${pkgdir}
  find usr/share/cassandra/bin -type f -executable \
    -exec ln -s /{} ${pkgdir}/usr/bin \;
  mv usr/bin/cqlsh.py usr/bin/cqlsh
  popd

  sed 's|"`dirname "$0"`/.."|"/usr/share/cassandra"|' bin/cassandra.in.sh \
    > ${pkgdir}/usr/share/cassandra/cassandra.in.sh

  cp -a lib/* ${pkgdir}/usr/share/java/cassandra/
  ln -s ../java/cassandra ${pkgdir}/usr/share/cassandra/lib

  cp -a conf/* ${pkgdir}/etc/cassandra/
  ln -s /etc/cassandra ${pkgdir}/usr/share/cassandra/conf

  ln -s /var/lib/cassandra ${pkgdir}/usr/share/cassandra/data
  ln -s /var/log/cassandra ${pkgdir}/usr/share/cassandra/logs

  install -Dm644 ${srcdir}/cassandra.service ${pkgdir}/usr/lib/systemd/system/cassandra.service
  install -Dm644 ${srcdir}/cassandra-tmpfile.conf ${pkgdir}/usr/lib/tmpfiles.d/cassandra.conf
  install -Dm644 ${srcdir}/cassandra-user.conf ${pkgdir}/usr/lib/sysusers.d/cassandra.conf
}

# vim:set ts=2 sw=2 et:
