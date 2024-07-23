<!--
Copyright (C) Jacob Hummer

SPDX-License-Identifier: curl
-->

# cURL prebuilt

📦 Prebuilt `libcurl.a`, `curl.exe`, `libcurl.so`, etc. \
🔀 Forked from [curl/curl](https://github.com/curl/curl)

<table align=center><td>

TODO: Add screenshot of "Assets" dropdown in releases tab once I make the first release

</table>

<p align=center>
  <a href="https://github.com/jcbhmr/curl/releases">GitHub releases (this project)</a>
  | <a href="https://curl.se/">Official cURL website</a>
  | <a href="https://github.com/curl/curl">Official cURL GitHub</a>
</p>

🏭 Builds everything using GitHub Actions \
🚚 Nicely distributed in prebuilt `.tar.gz` or `.zip` bundles \
📄 No source code patches; it's all CI

## Installation

**🛑 Use the [official cURL download page](https://curl.se/download.html)** to find, download, and install cURL for your platform.

<dl>
<dt>Windows
<dd>

Windows already provides a `curl.exe`. You can download libcurl using [Vcpkg](https://vcpkg.io/) or another C/C++ dependency manager.

```cmd
vcpkg install curl
```

<dt>Ubuntu
<dd>

`curl` is already installed. You can install libcurl using apt:

```sh
sudo apt install libcurl4
```

<dt>macOS
<dd>

Both `curl` and libcurl are already installed.

</dl>

You can get cURL (library and binary) builds built by this project from [the GitHub releases tab](https://github.com/jcbhmr/curl/releases). **These are unofficial.**

## Usage

![Windows](https://img.shields.io/static/v1?style=for-the-badge&message=Windows&color=0078D4&logo=Windows&logoColor=FFFFFF&label=)
![Linux](https://img.shields.io/static/v1?style=for-the-badge&message=Linux&color=222222&logo=Linux&logoColor=FCC624&label=)
![macOS](https://img.shields.io/static/v1?style=for-the-badge&message=macOS&color=000000&logo=macOS&logoColor=FFFFFF&label=)
![C](https://img.shields.io/static/v1?style=for-the-badge&message=C&color=222222&logo=C&logoColor=A8B9CC&label=)

This project intends to provide binaries that can be used and integrated with other software **where you don't want to have to compile cURL on a user's computer**. Bindings to high-level scripting-like languages are a good example where a user _doesn't want to wait_ for cURL to configure & build.

Here's some relevant URLs that you might use in your code to fetch (or store) the build artifacts:

```
https://github.com/jcbhmr/curl/releases/download/curl-8_8_0/curl-aarch64-apple-darwin.tar.gz
https://github.com/jcbhmr/curl/releases/download/curl-8_8_0/curl-x86_64-apple-darwin.tar.gz
https://github.com/jcbhmr/curl/releases/download/curl-8_8_0/curl-aarch64-unknown-linux-gnu.tar.gz
https://github.com/jcbhmr/curl/releases/download/curl-8_8_0/curl-aarch64-unknown-linux-musl.tar.gz
https://github.com/jcbhmr/curl/releases/download/curl-8_8_0/curl-x86_64-unknown-linux-gnu.tar.gz
https://github.com/jcbhmr/curl/releases/download/curl-8_8_0/curl-x86_64-unknown-linux-musl.tar.gz
https://github.com/jcbhmr/curl/releases/download/curl-8_8_0/curl-x86_64-pc-windows-msvc.zip
https://github.com/jcbhmr/curl/releases/download/curl-8_8_0/curl-x86_64-pc-windows-gnu.zip
https://github.com/jcbhmr/curl/releases/download/curl-8_8_0/curl-unknown-unknown-cosmo.zip
https://github.com/jcbhmr/curl/releases/download/curl-8_8_0/curl-wasm32-wasmer-wasi.zip
```

ℹ This project tries to stay up-to-date with [the latest curl/curl release](https://github.com/curl/curl/releases/latest) and also mirrors the release tag convention of `curl-X_Y_Z` tags.

You are encouraged to pin to a particular version and then update periodically.

There's also nightly builds if you're interested. I don't recommend using them but I wanted to highlight how cool😎 the [nightly.link](https://nightly.link/) service is for this kind of thing! 🤩

```
https://nightly.link/jcbhmr/curl/workflows/cmake-build/master/curl-x86_64-unknown-linux-gnu.zip
https://nightly.link/jcbhmr/curl/workflows/cmake-build/master/curl-aarch64-apple-darwin.zip
https://nightly.link/jcbhmr/curl/workflows/cmake-build/master/curl-x86_64-apple-darwin.zip
https://nightly.link/jcbhmr/curl/workflows/cmake-build/master/curl-x86_64-pc-windows-msvc.zip
```

The `.zip` and `.tar.gz` archives are what was `cmake --install`-ed. The layout is mostly the same across platforms.

```
.
├── bin/
│   ├── curl
│   ├── curl-config
│   ├── mk-ca-bundle.pl
├── include/
│   └── curl/
│       ├── curl.h
│       ├── curlver.h
│       ├── easy.h
│       ├── header.h
│       └── ...
├── lib/
│   ├── cmake/
│   │   └── CURL/
│   │       ├── CURLConfig.cmake
│   │       ├── CURLConfigVersion.cmake
│   │       ├── CURLTargets.cmake
│   │       └── CURLTargets-relwithdebinfo.cmake
│   ├── pkgconfig/
│   │   └── libcurl.pc
│   ├── libcurl.a
│   ├── libcurl.so
│   ├── libcurl.so.4
│   └── libcurl.so.4.8.0
└── share/
    └── man/
        ├── man1/
        │   ├── curl.1
        │   ├── curl-config.1
        │   └── mk-ca-bundle.1
        └── man3/
            ├── curl_easy_cleanup.3
            ├── curl_easy_dubhandle.3
            ├── curl_easy_escape.3
            ├── curl_easy_getinfo.3
            └── ...
```

Note that everything **is in the root folder** of the archive! That means if you do `unzip` it will extract _to `.`_. There's not an extra inner folder. TODO: Is this the right way? What's the prevailing convention?

## Development

![LLVM](https://img.shields.io/static/v1?style=for-the-badge&message=LLVM&color=262D3A&logo=LLVM&logoColor=FFFFFF&label=)
![Wasmer](https://img.shields.io/static/v1?style=for-the-badge&message=Wasmer&color=4946DD&logo=Wasmer&logoColor=FFFFFF&label=)
![CMake](https://img.shields.io/static/v1?style=for-the-badge&message=CMake&color=064F8C&logo=CMake&logoColor=FFFFFF&label=)
![Zig](https://img.shields.io/static/v1?style=for-the-badge&message=Zig&color=222222&logo=Zig&logoColor=F7A41D&label=)

This is a 🔀fork of the [curl/curl](https://github.com/curl/curl) project. I don't know if the cURL project wants to host prebuilt binaries. 🤷‍♀️ The goal is to have a small patch of (hopefully) just `.github/workflows/*.yml` files to build each new cURL version and publish some sweet precompiled binaries and libraries for any platform that is in demand. Want to add another OS/arch combo? [Open an issue](https://github.com/jcbhmr/curl/issues/new) or [a Pull Request](https://github.com/jcbhmr/curl/pulls)! ❤️

Todos:

- Try to cross-compile everything using `zig cc`
- Use `zig cc` or a native ARM runner to compile an AArch64 Linux version of cURL
- Obtain precompiled (or compile them ourselves) versions of OpenSSL and others for `cosmocc` builds
- Obtain precompiled versions of OpenSSL and zlib for WASIX builds

The best way to test changes right now is to open a Pull Request and see if the build workflow succeeds.

Make sure **not** to use the GitHub web UI to perform a <kbd>Merge</kbd> (merge commit) from the upstream curl/curl project. We want to _rebase_ and put this repo's changes/patchset on top of any updates.

To perform a rebase merge using the GitHub web UI:

1. Create a new Pull Request from curl/curl `master` ➡ jcbhmr/curl `master`.
2. **Make sure things still build and work** even with the new upstream changes.
3. Click the <kbd>🔽</kbd> extra options dropdown on the Merge button. Choose the Rebase option.

To create a release:

1. Rebase against the upstream release tag that corresponds to the release you want to make. Each release of this repository should correspond with a release from curl/curl. curl/curl already nicely configures and sets all the version magic everywhere so we can just take advantage of that.
2. Manually update the few spots where jcbhmr/curl versions are hardcoded. These are: the readme list of release URLs, the readme zip/tarball folder structure.
3. Manually run the `gh release create` workflow in the Actions tab. Choose `draft: true` first.
4. Wait and make sure that CI creates the draft release.
5. Manually check that things look good and work with all the draft release artifacts.
6. Publish the release! 🚀

---

<!--
Copyright (C) Daniel Stenberg, <daniel@haxx.se>, et al.

SPDX-License-Identifier: curl
-->

# [![curl logo](https://curl.se/logo/curl-logo.svg)](https://curl.se/)

Curl is a command-line tool for transferring data specified with URL
syntax. Find out how to use curl by reading [the curl.1 man
page](https://curl.se/docs/manpage.html) or [the MANUAL
document](https://curl.se/docs/manual.html). Find out how to install Curl
by reading [the INSTALL document](https://curl.se/docs/install.html).

libcurl is the library curl is using to do its job. It is readily available to
be used by your software. Read [the libcurl.3 man
page](https://curl.se/libcurl/c/libcurl.html) to learn how.

You can find answers to the most frequent questions we get in [the FAQ
document](https://curl.se/docs/faq.html).

Study [the COPYING file](https://curl.se/docs/copyright.html) for
distribution terms.

## Contact

If you have problems, questions, ideas or suggestions, please contact us by
posting to a suitable [mailing list](https://curl.se/mail/).

All contributors to the project are listed in [the THANKS
document](https://curl.se/docs/thanks.html).

## Commercial support

For commercial support, maybe private and dedicated help with your problems or
applications using (lib)curl visit [the support page](https://curl.se/support.html).

## Website

Visit the [curl website](https://curl.se/) for the latest news and
downloads.

## Git

To download the latest source from the Git server, do this:

    git clone https://github.com/curl/curl.git

(you will get a directory named curl created, filled with the source code)

## Security problems

Report suspected security problems via [our HackerOne
page](https://hackerone.com/curl) and not in public.

## Notice

Curl contains pieces of source code that is Copyright (c) 1998, 1999 Kungliga
Tekniska Högskolan. This notice is included here to comply with the
distribution terms.

## Backers

Thank you to all our backers! 🙏 [Become a backer](https://opencollective.com/curl#section-contribute).

## Sponsors

Support this project by becoming a [sponsor](https://curl.se/sponsors.html).
