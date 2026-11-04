# stable-reshade

This repository is a small GitHub Actions runner that provides stable `.dll` sources for [ReShade](https://github.com/crosire/reshade).

ReShade is BSD-3-Clause licensed. As a result, `.dll`s distributed here are also licensed under BSD-3.

## Usage

Output .dlls are available under the releases tab.

For Nix users, you'll probably want to do something like this:

```nix
reshade64 = pkgs.fetchurl {
  url = "https://github.com/NekoDrone/stable-reshade/releases/download/v6.8.0/ReShade64.dll";
  hash = "sha256-…"; # or lib.fakeHash and fail build before replacing with actual hash. Or prefetch hash, whatever works.
};
```
