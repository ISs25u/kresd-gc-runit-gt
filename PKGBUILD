
_sed_args=(-e 's|/var/run|/run|g' -e 's|/usr/sbin|/usr/bin|g' -e 's|/opt/bin|/usr/bin|g' -e 's|/var/service|/run/runit/service|g' -e 's|/usr/libexec|/usr/lib|g')

pkgname=kres-cache-gc-runit-gt
pkgver=20201210
pkgrel=1
pkgdesc="Runit service script for knot resolver cache garbage collector"
arch=('any')
url="https://github.com/ISs25u"
license=('GPL3')
depends=('knot-resolver')
conflicts=('systemd-sysvcompat')
source=("kres-cache-gc.run")
sha256sums=("52cbeb0c97e26256d2684fb4edec2b6a8ba8524bc38aee9041d6ad5a2f4353a0")

_inst_logsv() {
    for file in run finish check; do
        if test -f "$srcdir/log$1.$file"; then
            install -Dm755 "$srcdir/log$1.$file" "$pkgdir/etc/runit/sv/$1/log/$file"
            sed "${_sed_args[@]}" -i "$pkgdir/etc/runit/sv/$1/log/$file"
        fi
    done
}

_inst_sv() {
    if test -f "$srcdir/$1.conf"; then
        install -Dm644 "$srcdir/$1.conf" "$pkgdir/etc/runit/sv/$1/conf"
    fi

    for file in run finish check; do
        if test -f "$srcdir/$1.$file"; then
            install -Dm755 "$srcdir/$1.$file" "$pkgdir/etc/runit/sv/$1/$file"
            sed "${_sed_args[@]}" -i "$pkgdir/etc/runit/sv/$1/$file"
        fi
    done
}

package() {
    _inst_sv 'kres-cache-gc'
}

