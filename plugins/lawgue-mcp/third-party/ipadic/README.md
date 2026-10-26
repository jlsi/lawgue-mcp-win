# Source-pinned MeCab IPADIC

The embedded dictionary is built only from the source archive recorded in
[PROVENANCE.json](PROVENANCE.json). No BCCWJ, Vibrato binary, customer text or
D1-Law data is an input. delarocha orders connection ids using the lexicon's
prior weights (`DictionaryPrior`), not corpus statistics.

`COPYING` preserves the source license bytes, including its Latin-1 final
characters. [COPYING.UTF-8](COPYING.UTF-8) changes only its character encoding.
Retain the complete license when redistributing this dictionary or a binary
that embeds it. [NOTICE](NOTICE) records the transformations.

From the repository root:

```sh
python3 scripts/rebuild-mecab-dict.py --verify
python3 scripts/rebuild-mecab-dict.py
```

Regeneration requires Python 3, the workspace Rust toolchain, zstd 1.5.7 and
access to the source archive and private workspace dependencies. delarocha
includes prebuilt native compiler libraries for supported host targets;
regeneration does not require a local Zig installation on those targets. It verifies the source archive, raw dictionary,
compressed dictionary and upstream license. CSV filenames are sorted in byte
order; dictionary inputs are converted from EUC-JP to UTF-8. The compiler is
pinned to delarocha 0.1.1 and the output format is DLRDIC04.

The old blob had 392127 lexicon entries. This pinned source has 392126 entries;
we do not claim the two dictionaries have identical output. Both Elsa server
and MCP use this shared dictionary, so their Japanese lint tests must pass
before release. The cache key changes automatically with the compressed blob.
