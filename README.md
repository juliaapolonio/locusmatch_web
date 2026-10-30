# locusmatch web

The browser version of **locusmatch**: compare the fine-mapped signals of a GWAS with every
earlier study of the trait and see which are novel loci, new signals in known loci or known
signals, on a genome-wide signal map.

**Open the app: <https://juliaapolonio.github.io/locusmatch_web/>**

## How it works

The app is the locusmatch Shiny application compiled with
[Shinylive](https://posit-dev.github.io/r-shinylive/): R runs inside your browser through
WebAssembly ([webR](https://docs.r-wasm.org/webr/)). There is no server.

* The first visit downloads the R runtime and packages (about 100 MB, then cached by the
  browser); the app is ready after roughly 15–30 seconds.
* Files you upload are read by R in your own browser and are not sent anywhere.
* Earlier studies are fetched directly from the
  [Open Targets Platform](https://platform.opentargets.org) API; those requests contain only
  trait names, study accessions and credible-set identifiers.
* Analyses run more slowly than in R on your computer: comparing a GWAS with the 35 earlier
  primary GWAS of schizophrenia (about 1,200 credible sets) takes around a minute and a half.

## Using it

1. **Earlier studies**: search a trait (or paste GWAS Catalog / FinnGen / UK Biobank
   accessions), filter by year, ancestry, study kind and number of cases, untick studies you
   do not want, and press *Use selected studies*. You can also upload your own credible sets.
2. **Your GWAS**: upload its credible sets, or pick one of the loaded studies.
3. **Signal map**: explore the interactive figure and download it (PNG, PDF) together with
   the classification tables (TSV).

The app opens with simulated data, so the signal map tab works immediately.

File formats: a table of credible sets with columns `cs_id`, `study_id`, `chrom`, `pos`
(GRCh38), `variant_id` (`chrom:pos:allele1:allele2`) and `pip`, optionally `lbf`
(natural-log Bayes factor), `in_cs`, `p` and `gene`; a study table with `study_id` and
`pub_date`; optionally thinned summary statistics (`chrom`, `pos`, `p`) and LD blocks (BED).

## Contents of this repository

This repository only holds the built site; it is generated from the locusmatch R package
with

```sh
Rscript web/build.R <path-to-this-repository>
```

run from the package repository. Do not edit the files here by hand. For large analyses, the
full documentation and fine-mapping functions, use the R package.
