# Maintainer: David Ostrovsky <david@ostrovsky.org>

pkgname=bazel
pkgver=0.16.1
pkgrel=0
pkgdesc='Correct, reproducible, and fast builds for everyone'
arch="all"
license="ASL-2.0"
url='https://bazel.io/'
depends="bash openjdk8 libarchive zip unzip"
# coreutils can be removed as a make dependency once expr in busybox is compatible with the BSD version, see following bug reports:
# Patch bazel: https://github.com/bazelbuild/bazel/issues/4055
# https://bugs.alpinelinux.org/issues/8121
makedepends="coreutils git linux-headers protobuf python"
options="!distcc !strip"
source="https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip
        https://github.com/bazelbuild/bazel/releases/download/${pkgver}/bazel-${pkgver}-dist.zip.sig"

sha512sums="89cefed69df1cae7076673900546199427fab3508aad1f0347b9da38153b6b1566b19a4c205055f41ca431fd9444ec772c86bc32fbff0da0485a5e5f11728932  bazel-0.16.1-dist.zip
0efadd70c6b671ab64ac742c46c15e45bee9a412c6d67d4941fc9657747eed4b29c643477475fa59b699c481b46c217fed9fc1892d42a93ef1f0d7259209dc6f  bazel-0.16.1-dist.zip.sig"

build() {
  ./compile.sh
  ./output/bazel build -s --verbose_failures scripts:bazel-complete.bash
  cd output
  ./bazel shutdown
}

package() {
  install -Dm755 ${srcdir}/scripts/packages/bazel.sh ${pkgdir}/usr/bin/bazel
  install -Dm755 ${srcdir}/output/bazel ${pkgdir}/usr/bin/bazel-real
  install -Dm644 ${srcdir}/bazel-bin/scripts/bazel-complete.bash ${pkgdir}/usr/share/bash-completion/completions/bazel
  install -Dm644 ${srcdir}/scripts/zsh_completion/_bazel ${pkgdir}/usr/share/zsh/site-functions/_bazel
}
# vim:set ts=2 sw=2 et:

