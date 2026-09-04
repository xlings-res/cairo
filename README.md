# cairo

xlings-res payload for **cairo 1.18.4**.

- **Upstream:** https://gitlab.freedesktop.org/cairo/cairo
- **Platform:** linux x86_64
- **Built by:** [`.agents/tools/graphics/build-gtk4-stack.sh`](https://github.com/openxlings/xim-pkgindex/blob/main/.agents/tools/graphics/build-gtk4-stack.sh)
  in [openxlings/xim-pkgindex](https://github.com/openxlings/xim-pkgindex)

## How these bytes were produced

meson, `-Dglib=enabled -Dxlib=enabled -Dxcb=enabled -Dfreetype=enabled -Dfontconfig=enabled`.
Ships `libcairo-gobject.so.2` and `cairo-gobject.pc`, which GTK 4 hard-requires and the
previous 1.18.0 payload did not contain.

Every payload here is produced inside an xlings subos by
[`build-in-subos.sh`](https://github.com/openxlings/xim-pkgindex/blob/main/.agents/tools/graphics/build-in-subos.sh),
which refuses to package a result that fails either of two checks:

- **inputs** — every include/library path the build actually resolved must come
  from the subos, not the host;
- **payload** — no RPATH outside the payload, and no absolute host path baked
  into a `.pc`, `.la` or `*-config` file.

The tarball is then stripped (`--strip-unneeded`, after the checks, so the
debug info is still there when they run) and packaged reproducibly —
`--sort=name`, `--owner=0 --group=0 --numeric-owner`, a fixed `--mtime`, and
`gzip -n` — so the same inputs give the same bytes.

## Mirrors

| region | url |
|---|---|
| GLOBAL | `https://github.com/xlings-res/cairo/releases/download/1.18.4/cairo-1.18.4-linux-x86_64.tar.gz` |
| CN | `https://gitcode.com/xlings-res/cairo/releases/download/1.18.4/cairo-1.18.4-linux-x86_64.tar.gz` |

Both regions are published from the same local file and then re-downloaded and
compared byte for byte before the recipe's `sha256` is written.
