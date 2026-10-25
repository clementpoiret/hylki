# Nix packaging

- The flake checks build the package itself, including the Rust tests. Keep
  these enabled rather than adding a separate evaluation-only check.
- WebKitGTK already loads Enchant, so the subject-line checker's `dlopen`
  resolves it without a source patch or `LD_LIBRARY_PATH` override (verified
  with the pinned WebKitGTK).
- Keep `glib-networking` in the runtime inputs so `wrapGAppsHook4` exposes the
  GIO TLS modules WebKit needs for HTTPS.
- The MIME database must be on `XDG_DATA_DIRS` during both tests and runtime;
  without it, GIO misidentifies attachments as `application/octet-stream`.
