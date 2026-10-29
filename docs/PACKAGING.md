# Julian Calendar packaging

Version: `VERSION`. Package: `infiltrator-calendar-julian`.

`make release` creates exactly three user assets: a generic amd64 `.deb` using `-O2 -march=x86-64 -mtune=generic -flto`, a self-extracting source `.run`, and a full source ZIP including this provider, private helpers, public ABI headers, tests, licenses and build tools. No Common checkout or download is used. The `.run` verifies its embedded source checksum before extraction.

The aggressive installer compiles twice with GCC: instrumentation and actual provider-ABI training, then `-O3`, the compiler's local CPU target, LTO and measured PGO. Missing profile data is a build failure. Copy-regression and model-accuracy checks run during training, on the final build and after stripping. Floating-point semantics are preserved; no fast-math flag is used. Calendar authority comparison remains a separate forensic audit because some published authorities intentionally disagree.

The native package has version `VERSION+native1`; the generic release uses `VERSION`. The package installs exactly two files: the Julian calendar `.so` and a plain-language illustrated PDF. No source archives, technical documentation, build records or separate translation files are installed. Debian control `X-Infiltrator-*` fields preserve native build provenance and module SHA-256. Runtime dependencies include the actual minimum GLIBC symbol version, GLib where needed, and an ICU 72–81 alternative for ICU-backed formatting.

`Replaces: infiltrator-calendar-resources` permits dpkg to transfer this provider's existing path from the old combined package without deleting the other providers. Removing this package removes its own module; removing a consumer does not. Reinstalling the legacy combined package is not the independent upgrade path; InfiltratorOS now installs the independent providers. Common's source implementation is preserved.

The release workflow installs and tests the exact native `.run` on Ubuntu 24.04, seals the three qualified artifacts, stages a draft release, verifies every remotely uploaded byte, and publishes that draft. Published releases are immutable; product changes require advancing `VERSION`. A rerun for a superseded main commit does not publish.

Translations use the provider-owned gettext domain `infiltrator-calendar-julian`. The package ships only its own messages in `/usr/share/locale/<language>/LC_MESSAGES/infiltrator-calendar-julian.mo`; Common’s combined translation package is not required. The exact compiled catalogues are checked through the provider ABI before packaging.

## Two-file content and embedded translations

User-visible documentation is just `Julian Calendar.pdf`. The existing locale catalogues are compiled into `Julian Calendar.so` rather than installed as sidecar `.mo` files. CI enforces the exact two-file package layout.
