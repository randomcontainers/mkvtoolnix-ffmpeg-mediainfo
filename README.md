# mkvtoolnix-ffmpeg-mediainfo

MKVToolNix with FFmpeg and MediaInfo, for converting, remuxing and checking video files in one image.

This image is the default image of [mkvtoolnix](https://github.com/randomcontainers/mkvtoolnix) (`ghcr.io/randomcontainers/mkvtoolnix:latest`), published under its own name. The contents are the same; the digests differ. It contains MKVToolNix, FFmpeg and MediaInfo, on Ubuntu or Alpine, for `linux/amd64` and `linux/arm64`.

These are unofficial builds, not affiliated with or endorsed by the upstream projects. Report problems with the image in [randomcontainers/mkvtoolnix](https://github.com/randomcontainers/mkvtoolnix/issues) and problems with a tool itself in that tool's own issue tracker.

## Quick start

```sh
docker run --rm --user "$(id -u):$(id -g)" -v "$PWD:/work" ghcr.io/randomcontainers/mkvtoolnix-ffmpeg-mediainfo -o output.mkv input.mp4
```

The examples in the [mkvtoolnix README](https://github.com/randomcontainers/mkvtoolnix#readme) work with this image too.

## Tags

`<version>` is the MKVToolNix version.

| Tags | Base |
|---|---|
| `latest`, `<version>`, `ubuntu`, `<version>-ubuntu`, `<version>-ubuntu26.04` | Ubuntu 26.04 |
| `alpine`, `<version>-alpine`, `<version>-alpine3.24` | Alpine 3.24 |

`latest` and `<version>` are the Ubuntu 26.04 images. The images are currently built on Ubuntu 26.04 and Alpine 3.24. Tags without a distro version move to the next distro release when the project does; tags ending in `ubuntu26.04` or `alpine3.24` stay on that release and are no longer rebuilt once the project moves to the next one.

Only the tags of the MKVToolNix version currently in [mkvtoolnix's package.yml](https://github.com/randomcontainers/mkvtoolnix/blob/main/package.yml) are rebuilt, exact-version tags included, so pin a digest when you need the same bytes every time. Tags of older versions stay as they were last built. The published tags and their digests are listed on the [package page](https://github.com/orgs/randomcontainers/packages/container/package/mkvtoolnix-ffmpeg-mediainfo).

## Platforms

`linux/amd64` and `linux/arm64`, both built natively on GitHub-hosted runners.

## Files and permissions

The working directory is `/work`. The image runs as UID 1000, and any other UID works too: `HOME` is then `/`, and caches go to `/cache`, which anyone can write to. How to get output files owned by you depends on how you run containers:

| Runtime | Flag |
|---|---|
| Docker on Linux (rootful), GitHub Actions | `--user "$(id -u):$(id -g)"` |
| Rootless Podman | `--userns=keep-id` |
| Rootless Docker | `--user 0:0` (root in the container is your user on the host) |
| Docker Desktop on macOS or Windows | none, file ownership is mapped for you |

## Contents

| Package | License | Repository |
|---|---|---|
| [MKVToolNix](https://mkvtoolnix.download/) | `GPL-2.0-only AND GPL-2.0-or-later AND LGPL-2.1-or-later AND MIT AND BSL-1.0` | [randomcontainers/mkvtoolnix](https://github.com/randomcontainers/mkvtoolnix) |
| [FFmpeg](https://ffmpeg.org/) | `GPL-3.0-or-later` | [randomcontainers/ffmpeg](https://github.com/randomcontainers/ffmpeg) |
| [MediaInfo](https://mediaarea.net/en/MediaInfo) | `BSD-2-Clause AND Zlib AND MIT AND Brian-Gladman-2-Clause AND Brian-Gladman-3-Clause` | [randomcontainers/mediainfo](https://github.com/randomcontainers/mediainfo) |

## Verifying

Each image has a build provenance attestation from this repository's GitHub Actions run. The run uses the shared build workflow of [randomcontainers/ci](https://github.com/randomcontainers/ci), which signs the attestation, so name both repositories:

```sh
gh attestation verify oci://ghcr.io/randomcontainers/mkvtoolnix-ffmpeg-mediainfo:latest \
  --repo randomcontainers/mkvtoolnix-ffmpeg-mediainfo --signer-repo randomcontainers/ci
```

Images from `ghcr.io/randomcontainers/mkvtoolnix` are built in [randomcontainers/mkvtoolnix](https://github.com/randomcontainers/mkvtoolnix), so verify them with `--repo randomcontainers/mkvtoolnix --signer-repo randomcontainers/ci`.

## Updates

The images are rebuilt when a new image of a package above is published, for example after an upstream release. They are also rebuilt when the base image changes and at least every 7 days, so distro security fixes reach the current tags. The package repositories describe how each upstream release is picked up.

## Licenses

The image contents are licensed under `GPL-2.0-only AND GPL-2.0-or-later AND LGPL-2.1-or-later AND MIT AND BSL-1.0 AND GPL-3.0-or-later AND BSD-2-Clause AND Zlib AND Brian-Gladman-2-Clause AND Brian-Gladman-3-Clause`. The version of each package is in `/usr/local/share/randomcontainers/<package>/version` and its license files are in `/usr/local/share/randomcontainers/<package>/licenses/`.

Corresponding source:

- MKVToolNix: [randomcontainers/mkvtoolnix](https://github.com/randomcontainers/mkvtoolnix#licenses) has a `v<version>` release with the source of each MKVToolNix version it builds.
- FFmpeg: [randomcontainers/ffmpeg](https://github.com/randomcontainers/ffmpeg#licenses) has a `v<version>` release with the source of each FFmpeg version it builds.

Ubuntu and Alpine packages keep their own licenses. The SBOM of each platform image lists them with their versions:

```sh
docker buildx imagetools inspect ghcr.io/randomcontainers/mkvtoolnix-ffmpeg-mediainfo:latest --format '{{ json .SBOM }}'
```

The files in this repository are available under the MIT license, see [LICENSE](LICENSE).

## Requesting a tool

To suggest another tool, use the [Request a tool](https://github.com/randomcontainers/.github/issues/new?template=tool-request.yml) form.

## This repository

The files here are generated from the `combos` section of `package.yml` in [randomcontainers/mkvtoolnix](https://github.com/randomcontainers/mkvtoolnix). Open issues and pull requests there.
