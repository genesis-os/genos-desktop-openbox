# Maintainer: Aditya Shakya <@adi1090x>

pkgname=genos-desktop-openbox
pkgver=1.0
pkgrel=1
pkgdesc="GenOS OpenBox desktop dotfiles and configs"
arch=('any')
license=('GPL3')
makedepends=('git')
# depends=('openbox' 'obconf' 'adapta-gtk-theme' 'rofi' 'dunst' 'zsh' 'terminator' 'alacritty' 'thunar' 'thunar-archive-plugin' 'thunar-media-tags-plugin' 'thunar-volman' 'ranger' 'flameshot')
conflicts=()
provides=("${pkgname}")
options=(!strip !emptydirs)
url="https://github.com/genesis-os"
source=(${pkgname}::"git+${url}/${pkgname}")
sha256sums=('SKIP')

pkgver() {
  cd $pkgname

  echo $(git rev-list --count HEAD).$(git rev-parse --short HEAD)
}

package() {
	cd $pkgname

	# Install configs
	mkdir -p $pkgdir/etc/skel/.config
	cp -r config $pkgdir/etc/skel/.config

	# Copy dotfiles
	dotfiles=(`ls -p dotfiles`)
	for file in "${dotfiles[@]}"; do
		cp -r dotfiles/"$file" "$pkgdir/etc/skel/.$file"
	done

	# Install nessary scripts for genos-openbox desktop
	install -Dm755 scripts/* -t $pkgdir/usr/local/bin/

	# Install genos fonts
	find fonts/ -type f -exec install -Dm 644 "{}" "$pkgdir/usr/share/fonts/{}" \;

	# Install icons
	mkdir -p "$pkgdir/usr/share/icons"
	cp -r icons/* "$pkgdir/usr/share/icons/"
}
