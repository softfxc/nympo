# Security Policy

## Supported Versions

If you believe you have found a security vulnerability in this project, please do not open a public issue. 
And when reporting a vulnerability, please include:
- a clear description of the issue
- steps to reproduce it
- affected version
- proof of concept, logs, screenshots, or sample files if relevant
- your assessment of impact

## Tools Notice

This project may embed helper binaries from `resources/` into the final executable and materialize them at runtime. Because of that, every bundled third-party binary should be treated as a supply-chain surface and should have, ideally:

- a documented upstream source
- a documented version
- a documented license

## Third-Party Components Referenced in the README

The following notes are intended as a practical compliance and transparency summary for tools mentioned in the Nympo README and resource list.

| Component | Typical files | License
|---|---|---|---|
| 7-Zip | `7z.exe`, `7z.dll` | Mostly GNU LGPL
| Zstandard | `zstd.exe` | BSD OR GPLv2
| bzip3 | `bzip3.exe` | LGPLv3 only
| cmix | `cmix.exe` | GPL-3.0
| paq8px | `paq8px.exe` | GPL-2.0-or-later
| lrzip | `lrzip.exe` | GPL-2.0-or-later
| FreeArc | `Arc.exe` | GPLv2
| XTool | `xtool.exe` | License not fully verified from the referenced archive page
| NNCP | `nncp.exe` | Version-specific / mixed / verify exact upstream bundle
| LibNC | `libnc.dll`, `libnc_cuda.dll` | Free to use as a binary shared library
| zlib | `zlib1.dll` | zlib license
| mingw-w64 / winpthreads | `libwinpthread-1.dll` | Project-level licensing is mixed
| Cygwin runtime | `cygwin1.dll`, `cygbz2-1.dll`, `cyglzo2-2.dll`, `cygz.dll`, `cyggcc_s-seh-1.dll`, `cygstdc++-6.dll`, `cygiconv-2.dll`, `cygintl-8.dll` | Mixed


## Additional Notes

### cmix

Downloaded from:
https://www.byronknoll.com/cmix.html

Official upstream repository:
https://github.com/byronknoll/cmix

### NNCP

Official page:
https://bellard.org/nncp/

VirusTotal reference:
https://www.virustotal.com/gui/file/8c18fdf3ac334f7257fc44b53c1b31f1da935f3752d0eff0697305b1c3b9128f

### bzip2

GnuWin32 package page:
https://gnuwin32.sourceforge.net/packages/bzip2.htm

Original upstream homepage:
http://www.bzip.org/

Original upstream source referenced by GnuWin32:
http://www.bzip.org/1.0.5/bzip2-1.0.5.tar.gz

Additional official documentation:
https://sourceware.org/bzip2/
https://sourceware.org/bzip2/manual/manual.html

VirusTotal reference:
https://www.virustotal.com/gui/file/40fc2876f9673f9de95f6ef18422d8de15a0b510701cdc187d516518482127ee/summary

## Important Notice About Antivirus Detections

Some third-party binaries, packers, compressors, or low-level utilities may trigger detections in multi-engine antivirus services.
These detections do not automatically prove that a file is malicious, but they also should not be ignored.

## Licensing

If this repository ships, embeds, extracts, or redistributes third-party binaries, the maintainer should preserve all required upstream notices and comply with the corresponding license obligations.
