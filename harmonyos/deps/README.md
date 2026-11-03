# Vendored dependencies

These are source snapshots pinned by the HarmonyOS port. The previous
`celestia-ohos` repository recorded them as gitlinks (mode `160000`) but shipped
no `.gitmodules`, so a fresh clone produced empty directories. They are vendored
here instead, so a clone is directly buildable.

| Directory | Upstream commit | Upstream project |
|---|---|---|
| `fast_float-src/` | `a8a02f77480d10c5dc90d39f7b890bc1dff9c1b9` | https://github.com/fastfloat/fast_float |
| `fmt-src/` | `e27cc20bd93a4e280fb9268d41cd131069a9c73f` | not recorded in the previous repository |
| `libepoxy-src/` | `d1f952c4565c389d82fd1657153e84e050f35b27` | not recorded in the previous repository |

`libintl/`, `locale/` and `pc/` are first-party: a small gettext implementation
written for this port, the compiled `.mo` catalogues, and pkg-config stubs.

`prefix/` is a build output (installed headers and libraries) and is ignored by
git.

## Why the gettext API is renamed

HarmonyOS links against musl, whose dynamic linker exports a `gettext()` stub
that returns the msgid unchanged and wins symbol resolution over any bundled
libintl. `libintl/` therefore exports `cel_gettext()` and friends, and
`src/celutil/gettext.h` maps the standard names onto them.
