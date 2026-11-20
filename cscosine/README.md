# fmt: the cscosine fork

fmt, as built and released by [third_party_base_libs](https://github.com/cscosine/third_party_base_libs) for the
cscosine projects: the upstream release plus a few commits of ours on top. This folder is ours; the rest of the
repository is upstream.

| | |
|---|---|
| Upstream | <https://github.com/fmtlib/fmt> |
| Base | upstream tag `12.2.1` (also in this repository) |
| Our changes | `git log 12.2.1..dev` |
| Our releases | tags `v<upstream>-cs.<n>`, see [CHANGELOG.md](CHANGELOG.md) |
| License | upstream's (`LICENSE`, MIT) |

## Our changes

| Commit | What | Why |
|---|---|---|
| csCMake presets | `CMakePresets.json`, `csCMakeProjectSetup.json` (csCMake presets, level 3): macOS deployment target 13.3, recorded in the installed package | Built with the csCMake presets on every platform of the matrix; 13.3: the floating-point `std::to_chars` of Apple's libc++ |
| Tests: format-impl-test not with Xcode | `test/CMakeLists.txt` | `FMT_ASSERT` is defined twice in that test executable; Xcode's linker keeps the aborting one (details in the commit). A candidate for upstream |
| this folder | `cscosine/README.md`, `CHANGELOG.md` | Where the fork comes from, what we change, why |

Upstream's `.github/` stays as it is: GitHub Actions is disabled on this repository.

## Syncing with a new upstream release

Fetch the new upstream tag (`git fetch https://github.com/fmtlib/fmt.git refs/tags/<new>:refs/tags/<new>`), rebase our
commits on it (`git rebase --onto <new> <old> dev`), drop those upstream has absorbed, build through
third_party_base_libs, then tag `v<new>-cs.1`.
