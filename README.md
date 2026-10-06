Ready-to-run [whisper.cpp](https://github.com/ggml-org/whisper.cpp) builds for
GPUs that upstream doesn't ship Windows binaries for — starting with **Vulkan**
(AMD and other Vulkan-capable GPUs). Built automatically in the cloud from
official whisper.cpp sources; nothing here is hand-compiled on a random PC.

## Available builds

| Flavor | File | Size | Needs |
|---|---|---|---|
| Vulkan, Windows x64 | `whisper-vulkan-win-x64-<build>.zip` | ~18 MB | AVX2-capable CPU · Vulkan driver (AMD Adrenalin / Intel / NVIDIA all provide one) |

> **CPU note:** these builds require a CPU with AVX2 (roughly 2013+). On older
> CPUs the binary exits immediately — use a CPU-only whisper.cpp build instead.



1. Download the zip from the [Releases](../../releases) page.
2. Verify it (compare with `SHA256SUMS.txt` on the same page):
   - Windows: `Get-FileHash whisper-vulkan-win-x64-*.zip -Algorithm SHA256`
   - macOS/Linux: `shasum -a 256 whisper-vulkan-win-x64-*.zip`
3. Extract it anywhere and run `whisper-cli.exe --help` — it must exit cleanly.


## How builds are made

`.github/workflows/build-whisper-vulkan.yml` — GitHub's servers compile
pinned official sources (`-DGGML_VULKAN=ON -DGGML_NATIVE=OFF`), smoke-test
the binary, and publish the zip + checksums to a release tag named
`engine-vulkan-<whisper-build>` (e.g. `engine-vulkan-b5130`). Re-running for
a new whisper.cpp version = bump one version string, run again.

## License & trust

[whisper.cpp](https://github.com/ggml-org/whisper.cpp) is MIT-licensed;
these are unmodified builds of its released sources — no extra code, no
bundled surprises. Check the workflow file if you want to see exactly what
runs. If you'd rather build it yourself with the same flags, the recipe is
right there — that's the point of keeping it public.
