# Enceladus

[![enceladus build badge](https://github.com/daudix/enceladus/actions/workflows/build.yml/badge.svg)](https://github.com/daudix/enceladus/actions/workflows/build.yml)

My personal flavor of [Fedora Silverblue](https://fedoraproject.org/atomic-desktops/silverblue/). It includes a small amount of chnages that I always do on my own system:

- Adds all neccesary media codecs and thumbnailers
- Installs [fish shell](https://fishshell.com)
- Installs additional GNOME wallpapers
- Removes additional Fedora wallpapers
- Removes Firefox RPM and installs Vivaldi RPM (and not Flatpak because of compatibility with KeePassXC)
- Removes GNOME Classic session
- Replaces Fedora Flatpaks with Flathub

As this image is for personal use, I can't guarantee that its scope won't change, in fact it will quite often, as I change my own scope just as often.

## Installation

> [!WARNING]  
> [This is an experimental feature](https://www.fedoraproject.org/wiki/Changes/OstreeNativeContainerStable), try at your own discretion.

To rebase an existing atomic Fedora installation to the latest build:

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/daudix/enceladus:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Then rebase to the signed image, like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/daudix/enceladus:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

The `latest` tag will automatically point to the latest build. That build will still always use the Fedora version specified in `recipe.yml`, so you won't get accidentally updated to the next major version.

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/daudix/enceladus
```
