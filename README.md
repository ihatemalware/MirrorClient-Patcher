# MirrorClient-Patcher

A Proof of Concept (PoC) demonstrating a client-side in-app purchase (IAP) validation flaw in KeloCube MirrorClient (SuperDisplay).

**DISCLAIMER: For Educational and Security Research Purposes ONLY.**
I do not provide any APK files. This repository contains a bash script that demonstrates how client-side validation can be bypassed by modifying Smali opcodes. Please support the original developers and buy the app if you use it.

## The Vulnerability
The application relies solely on local boolean checks to verify Google Play Billing state:
`com.kelocube.mirrorclient.Billing -> isPurchased()Z`

By modifying a single conditional jump (`if-eqz` to `goto`) in the Dalvik bytecode, the application can be tricked into granting Premium access without server-side verification.

## Requirements
- `apktool` (v2.10.0+ recommended)
- `zipalign` & `apksigner`
- Java / JRE

## How to use (PoC)
1. Extract the `base.apk` from the original `.apkm` bundle.
2. Patch the apk.
3. Zipalign and sign the output `patched_unsigned.apk` with your own keystore.
