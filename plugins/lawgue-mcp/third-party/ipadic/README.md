# Source-pinned MeCab IPADIC

The embedded dictionary is built only from the source archive recorded in
[PROVENANCE.json](PROVENANCE.json). No BCCWJ, Vibrato binary, customer text or
D1-Law data is an input. delarocha orders connection ids using the lexicon's
prior weights (`DictionaryPrior`), not corpus statistics.

`COPYING` preserves the source license bytes, including its Latin-1 final
characters. [COPYING.UTF-8](COPYING.UTF-8) changes only its character encoding.
Retain the complete license when redistributing this dictionary or a binary
that embeds it. [NOTICE](NOTICE) records the transformations.

From the [Elsa 2.53.9 source repository](https://github.com/jlsi/elsa/tree/2.53.9) root
(the following script is maintained upstream, not in this distribution repository):

```sh
python3 scripts/rebuild-mecab-dict.py --verify
python3 scripts/rebuild-mecab-dict.py
```

The verification script checks the source archive, raw dictionary,
compressed dictionary and upstream license. CSV filenames are sorted in byte
order; dictionary inputs are converted from EUC-JP to UTF-8. The compiler is
pinned to delarocha 0.1.1 and the output format is DLRDIC04.
