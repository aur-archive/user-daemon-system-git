# Maintainer: Guten Ye

pkgname="user-daemon-system-git"
pkgver=20120911  
pkgrel=3
pkgdesc="A User based Daemon System for ZSH. READ https://github.com/GutenYe/user-daemon-system FIRST." 
arch=("i686" "x86_64")
url="https://github.com/GutenYe/user-daemon-system"
license=("MIT")
depends=("zsh")
makedepends=("git")
provides=("user-daemon-system")
conflicts=("user-daemon-system")
backup=("home/$USER/etc/rc.conf")

_gitroot="git://github.com/GutenYe/user-daemon-system"
_gitname="user-daemon-system"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"
}

package() {
  cd "$srcdir/$_gitname-build"

  mkdir -p $pkgdir/home/$USER/var/{run/daemons,cache,log}
  mkdir -p $pkgdir/home/$USER/etc/{conf.d,rc.d/functions.d}
  mkdir -p $pkgdir/home/$USER/usr/bin

  cp -rT etc $pkgdir/home/$USER/etc
  install -Dm755 bin/user-daemon-system $pkgdir/usr/bin/user-daemon-system

  chown $USER:$USER -R $pkgdir/home/$USER
}

# vim:set ts=2 sw=2 et:
md5sums=()
