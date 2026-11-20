# RUNNING_LOG — wreq-util

## 2026-11-15 — Chrome157 profile added (closes the "157 not available" excuse)

- Added `v157` in `src/emulate/profile/chrome.rs`: TLS/H2 inherited from `v154`
  (which is byte-identical to the real Chrome 157 capture at TLS/H2), with the
  Chrome 157 cleartext claim: UA `Chrome/157.0.0.0`, sec-ch-ua
  `"Not-A.Brand";v="99", "Google Chrome";v="157", "Chromium";v="157"`, and a
  Chrome157 accept initializer that adds `image/jxl`.
- Registered `Chrome157 => ("chrome_157", v157::emulation)` in `src/emulate.rs`.
- Verified after building wreq-python 0.13.0: `Emulation.Chrome157` exists;
  tls.peet.ws reports JA4 `t13d1517h2_8daaf6152771_cb7bf5808d99`, H2 akamai
  `1:65536;2:0;4:6291456;6:262144|15663105|0|m,a,s,p`, Windows UA Chrome/157.
- There is no Chrome 157 TLS delta vs Chrome154/156; the gap was the missing
  profile/enum, not a transport limitation.
- Build prerequisites on this box: pip `cmake` + `libclang` and
  `LIBCLANG_PATH=<venv>\Lib\site-packages\clang\native` (btls-sys bindgen).
