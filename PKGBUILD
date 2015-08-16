## Maintainer: shyokou <shyokou at gmail dot com>
##
pkgname=meek-client
_pkgname=${pkgname%-*}
pkgver=0.17.20150412
pkgrel=1
pkgdesc='A pluggable transport proxy written in Go'
arch=('i686' 'x86_64')
url='https://trac.torproject.org/projects/tor/wiki/doc/'${_pkgname}
license=('CC0')
conflicts=('meek-client')
provides=('meek-client')
makedepends=('git' 'go')
optdepends=(
	'tor: you need tor to use this package'
)
source=(
	'git+https://git.torproject.org/pluggable-transports/'${_pkgname}'.git'
)
sha256sums=(
	'SKIP'
)

pkgver()	{
  cd "$srcdir/${_pkgname}"

  ##	tag & date from the last commit
  echo $(git describe --always | sed 's:^'${pkgname}-'::; s:-.*::').$(git log -1 --pretty='%cd' --date=short | tr --delete '-')
}

build()	{
  cd "${srcdir}/${_pkgname}/${pkgname}"

  export GOPATH=~/go
  export GOBIN="."
  go get
  go build
}

package()	{
  cd "${srcdir}/${_pkgname}/${pkgname}"

  #export GOPATH=~/go
  #go install
  install -D -m 0755		"${pkgname}"		"${pkgdir}/usr/bin/${pkgname}"
  install -D -m 0644		"../doc/${pkgname}.1"	"${pkgdir}/usr/share/man/man1/${pkgname}.1"
  install -D -m 0644		"../README"		"${pkgdir}/usr/share/doc/${pkgname}/README"
  install -D -m 0644		torrc			"${pkgdir}/etc/tor/torrc.${_pkgname}"
}

## vim:set ts=2 sw=2 et:
