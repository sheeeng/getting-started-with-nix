---
marp: true
lang: en-US
title: Marp CLI example
description: Hosting Marp slide deck on the web
theme: uncover
transition: fade
paginate: true
_paginate: false
---

![bg opacity](./assets/gradient.jpg)

# <!--fit--> Marp CLI example

Hosting Marp slide deck on the web

<https://github.com/yhatt/marp-cli-example>

<style scoped>a { color: #36c; }</style>

<!-- This is presenter note. You can write down notes through HTML comment. -->

---

![Marp bg 60%](https://raw.githubusercontent.com/marp-team/marp/master/marp.png)

---

<!-- _backgroundColor: "#123" -->
<!-- _color: "#fff" -->

##### <!--fit--> [Marp CLI](https://github.com/marp-team/marp-cli) + [GitHub Pages](https://github.com/pages) | [Netlify](https://www.netlify.com/) | [Vercel](https://vercel.com/)

##### <!--fit--> 👉 The easiest way to host<br />your Marp deck on the web

---

![bg right 60%](https://icongr.am/octicons/mark-github.svg)

## **[GitHub Pages](https://github.com/pages)**

#### Ready to write & host your deck

[![Use this as template h:1.5em](https://img.shields.io/badge/-Use%20this%20as%20template-brightgreen?style=for-the-badge&logo=github)](https://github.com/yhatt/marp-cli-example/generate)

---

![bg right 60%](https://icongr.am/simple/netlify.svg?colored)

## **[Netlify](https://www.netlify.com/)**

#### Ready to write & host your deck

[![Deploy to Netlify h:1.5em](./assets/netlify-deploy-button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/yhatt/marp-cli-example)

---

![bg right 60%](https://icongr.am/simple/zeit.svg)

## **[Vercel](https://vercel.com/)**

#### Ready to write & host your deck

[![Deploy to Vercel h:1.5em](https://vercel.com/button)](https://vercel.com/import/project?template=https://github.com/yhatt/marp-cli-example)

---

### <!--fit--> :ok_hand:

---

![bg 40% opacity blur](https://avatars1.githubusercontent.com/u/3993388?v=4)

### Created by Yuki Hattori ([@yhatt](https://github.com/yhatt))

<https://github.com/yhatt/marp-cli-example>

---

```nix
src = pkgs.fetchFromGitHub {
  owner = "catppuccin";
  repo = "bottom";
  rev = "eadd75acd0ecad4a58ade9a1d6daa3b97ccec07c";
  sha256 = "16ba69j4n4qca1zb2qvcggxja69jxwcjh0v08ijhvfpl9rva9yvm";
};
```

---

```shell
nix run nixpkgs#nurl -- \
  https://github.com/catppuccin/bottom \
  eadd75acd0ecad4a58ade9a1d6daa3b97ccec07c \
  2&>/dev/null
```

```nix
fetchFromGitHub {
  owner = "catppuccin";
  repo = "bottom";
  rev = "eadd75acd0ecad4a58ade9a1d6daa3b97ccec07c";
  hash = "sha256-dfukdk70ug1lRGADKBnvMhkl+3tsY7F+UAwTS2Qyapk=";
}
```

---

## Fetching GitHub hashes

### Multiple approaches available

- ✨ **nurl** (recommended)
- **nix-prefetch-github**
- **nix-prefetch-url** (with tarball)
- **nix-prefetch-git**

---

### Option 1: nurl (recommended)

Modern and convenient approach.

```shell
nix run nixpkgs#nurl -- \
  https://github.com/catppuccin/bottom \
  eadd75acd0ecad4a58ade9a1d6daa3b97ccec07c

# Output: fetchFromGitHub {
#   owner = "catppuccin";
#   repo = "bottom";
#   rev = "eadd75acd0ecad4a58ade9a1d6daa3b97ccec07c";
#   hash = "sha256-dfukdk70ug1lRGADKBnvMhkl+3tsY7F+UAwTS2Qyapk=";
# }
```

✅ Generates complete `fetchFromGitHub` expression.
✅ No installation required.

---

### Option 2: nix-prefetch-github

Specialized for GitHub repositories.

```shell
nix-prefetch-github catppuccin bottom \
  --rev eadd75acd0ecad4a58ade9a1d6daa3b97ccec07c
```

✅ Clean, simple syntax.
✅ Purpose-built for GitHub.

```json
{
    "owner": "catppuccin",
    "repo": "bottom",
    "rev": "eadd75acd0ecad4a58ade9a1d6daa3b97ccec07c",
    "hash": "sha256-dfukdk70ug1lRGADKBnvMhkl+3tsY7F+UAwTS2Qyapk="
}
```

---

### Option 3: nix-prefetch-url

Using GitHub's tarball URL.

```shell
$ nix-prefetch-url --unpack \
  https://github.com/catppuccin/bottom/archive/\
eadd75acd0ecad4a58ade9a1d6daa3b97ccec07c.tar.gz
16ba69j4n4qca1zb2qvcggxja69jxwcjh0v08ijhvfpl9rva9yvm
```

⚠️ More verbose.
⚠️ Manual tarball URL construction.

```console
$ nix hash to-sri --type sha256 16ba69j4n4qca1zb2qvcggxja69jxwcjh0v08ijhvfpl9rva9yvm
sha256-dfukdk70ug1lRGADKBnvMhkl+3tsY7F+UAwTS2Qyapk=
```

---

### Option 4: nix-prefetch-git

Direct git repository prefetch.

```shell
nix-prefetch-git \
  --url https://github.com/catppuccin/bottom \
  --rev eadd75acd0ecad4a58ade9a1d6daa3b97ccec07c
```

✅ Works with any git repository.
⚠️ Slower (full git clone).

```json
{
  "url": "https://github.com/catppuccin/bottom",
  "rev": "eadd75acd0ecad4a58ade9a1d6daa3b97ccec07c",
  "date": "2025-04-18T23:41:21+01:00",
  "path": "/nix/store/7dxd7gfjwidz92g2lasskqxj0r57csq8-bottom-eadd75a",
  "sha256": "16ba69j4n4qca1zb2qvcggxja69jxwcjh0v08ijhvfpl9rva9yvm",
  "hash": "sha256-dfukdk70ug1lRGADKBnvMhkl+3tsY7F+UAwTS2Qyapk=",
  "fetchLFS": false,
  "fetchSubmodules": false,
  "deepClone": false,
  "fetchTags": false,
  "leaveDotGit": false,
  "rootDir": ""
}
```

---

### <!--fit--> 💡 Pro tip

**nix-prefetch-url** is for direct file URLs.

For GitHub repos, use:
**nurl** or **nix-prefetch-github**.

---
