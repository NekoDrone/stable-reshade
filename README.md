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

## Caveats (FAQ)

**Q. Do your hashes match?**
A. No. MSVC embeds timestamps and other build-specific data, so even within repeated runs of the build using this repository's workflow will result in two differing hashes. This is not to mention the additional version metadata attached in the workflow build. Additionally, this project was built with `RESHADE_ADDON=2`, in order to support ongoing development of [`xiv-flake`](https://github.com/NekoDrone/xiv-flake), which requires addon support when providing ReShade.

**Q. Are your builds reproducible?**
A. No. See above.

**Q. So how can I trust you?**
A. You can't. The best you can do is look at `.github/workflows/build-reshade.yaml` to see that all this repository is doing is taking already available code, building it, and providing it in a stable manner to be reused elsewhere, such as in Nix flakes, or anywhere else that demands stability.

**Q. Can I have the official ReShade .dlls?**
A. Yes. You can download the official .exe installer [here](https://reshade.me), extract it yourself (`unzip -c unzip -j ReShade_Setup_6.8.0_Addon.exe ReShade64.dll`), and use that .dll wherever you want. The reason this repository exists is so that you can pin specific versions of the `ReShade64.dll` for stable builds with a stable hash.
