# Augustinian Sermon Parallelism (ASP) Dataset
**Authors**: 
* Stephen Bothwell, Theresa Crnkovich, Hildegund Müller, and David Chiang (University of Notre Dame)
* Justin DeBenedetto (Villanova University)

**Maintainer**: Stephen Bothwell

## Summary

This repository contains the Augustine Sermon Parallelism (ASP) dataset--a collection of sermons from Augustine's *Sermones* annotated for rhetorical parallelism. 
It is intended to be used to study the phenomenon of rhetorical parallelism both in the application of language broadly and in the specific context of Augustine of Hippo.

### Statistics

The table below summarizes its base statistics. For exact definitions of *parallelism* and *branch*, please see our paper. 
For a basic understanding, consider a *branch* to be a continuous span of annotated text; 
then, consider a *parallelism* to be a group of said spans.

| Quantity       | Total (Nested) |
|----------------|----------------|
| Documents      | 80             |
| Sections       | 477            |
| Parallelisms   | 2,062 (14)     |
| Branches       | 4,651 (39)     |
| Branched Words | 19,701         |
| Words          | 134,956        |

Note that the word-based quantities are applied post-tokenization, 
with tokenization being done via the `LatinWordTokenizer` from the Classical Language Toolkit (Johnson *et al.* 2021).

### Use

The annotations in this dataset are licensed under a Creative Commons Attribution 4.0 International (CC-BY) license. 
For more information, please see https://creativecommons.org/licenses/by/4.0/.

## Background

This section is a work in progress.

## Contents

This repository contains three versions of our dataset. Each version of the dataset progressively imposes greater constraints on the way in which the data is presented. 
These three versions are as follows:
* **Raw**: In our `data/original` directory, we provide the version of the dataset collected from the `brat` annotation tool (Stenetorp *et al.* 2012). This format consists of two types of files:
  1. Input text (`.txt`) files extracted of Augustine's *Sermones* from the InteLex database.
  2. Annotation files (`.ann`) generated by `brat` in that program's annotation encoding format.

  Each `.txt` file is paired with a `.ann` file of the same name. The `.ann` file in a given pair labels our annotator's decisions concerning parallel structure. We provide a description of our annotation scheme in our paper as well as in the `procedures` folder.
* **Untokenized XML**: In our `xml/untokenized` directory, we provide XML files which combine the `.txt` files and `.ann` files in a nested format. These files (sans the pretty-printed formatting imposed by `xml.dom.minidom`) were provided as input to the system in our paper. 
Annotations were organized in order to represent their nested structure. Each XML file contains up to three types of tags:
  * The `<sermon>` tag wraps around the entire text to indicate it as one unit. It has an `id` attribute which indicates that text's numerical indicator within Augustine's *Sermones*.
  * The `<section>` tag denotes a *section* of text--a subdivision of the sermon imposed by editors. Each section has an `id` attribute which indicates what index editors applied to each section; such indices start at 1 and increase sequentially.
  * The `<parallelism>` tag designates a branch of some parallelism in the text. Being presented in this format, `<parallelism>` tags can nest indefinitely; however, in this dataset, parallelisms nest at most once. Each branch has an `id` attribute which notes to what parallelism it belongs.
  It also has a `part` attribute that shows the numerical ordering of individual branches. Both `id` and `part` start from 1 and increase sequentially. 
  When nested branches start at the same point, the parallelism that *ends* first has a smaller `id`. In other words, nested parallelisms tend to come before nesting parallelisms.
* **Tokenized XML**: In our `xml/tokenized` directory, we provide XML files which combine the `.txt` files and `.ann` files in a nested format. Like the untokenized variant, this version also contains up to three types of tags. 
The `<sermon>` and `<section>` tags reprise their roles above. However, the third tag, `<token>`, designates a tokenization applied through the [Classical Language Toolkit](http://cltk.org/) (Johnson _et al._ 2021). 
Each `<token>` has an `id` attribute indicating its position within a given section, starting from 1. 
The actual token is given in the `cont` attribute, following the convention of the [PSE](https://github.com/Mythologos/Paibi-Student-Essays) dataset.
Finally, a `parallelism_id` and `branch_id` are given for each applicable stratum (or level of nesting).
These values start from 1 and increase sequentially, following the same rules as the untokenized XML's `id` attributes.

We also provide information about our process for developing the dataset. To this end, please see the PDF file available in the `procedure` directory. 
We give a sketch of our initial guidelines used to produce this data in the `"RPD - Original Annotation Guidelines"` PDF. 
We further present a revised version of the guidelines engendered through a critical evaluation of our annotations in the `"RPD - Revised Annotation Guidelines"` PDF.

## Contributing

This repository is intended to provide a single, definitive version of this dataset for future work and research. 
However, if there are issues or mistakes with the data, we would be glad to investigate them. 
Please open an issue to start a conversation on the subject. 

Any future updates of the dataset will be tagged with a version number so as to make it easy to designate and compare results. 
The current version is `v1.0`.

## Citations

### Our Work

To cite this dataset, please use the following paper:

```
...
```

... as well as the following source text:

```
@book{augustineofhippoSermonesPart2000,
  title = {{Sermones: Part 1}},
  author = {{Augustine of Hippo}},
  editor = {Mayer, Cornelius},
  year = {2000},
  series = {{Saint Augustine: Opera Omnia - Corpus Augustinianum Gissense. Electronic Edition}},
  volume = {12},
  publisher = {{InteLex Corp.}},
  address = {{Charlottesville, Virginia, U.S.A.}},
  urldate = {2020-10-19},
  langid = {latin}
}
```

### Others' Work

We also provide citations of relevant scholarly works mentioned above. These are as follows:

```
@inproceedings{johnsonClassicalLanguageToolkit2021,
  title = {The {{Classical Language Toolkit}}: {{An NLP}} Framework for Pre-Modern Languages},
  booktitle = {Proceedings of the 59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint Conference on Natural Language Processing: {{System}} Demonstrations},
  author = {Johnson, Kyle P. and Burns, Patrick J. and Stewart, John and Cook, Todd and Besnier, Cl{\'e}ment and Mattingly, William J. B.},
  year = {2021},
  month = aug,
  pages = {20--29},
  publisher = {{Association for Computational Linguistics}},
  address = {{Online}},
  doi = {10.18653/v1/2021.acl-demo.3},
  abstract = {This paper announces version 1.0 of the Classical Language Toolkit (CLTK), an NLP framework for pre-modern languages. The vast majority of NLP, its algorithms and software, is created with assumptions particular to living languages, thus neglecting certain important characteristics of largely non-spoken historical languages. Further, scholars of pre-modern languages often have different goals than those of living-language researchers. To fill this void, the CLTK adapts ideas from several leading NLP frameworks to create a novel software architecture that satisfies the unique needs of pre-modern languages and their researchers. Its centerpiece is a modular processing pipeline that balances the competing demands of algorithmic diversity with pre-configured defaults. The CLTK currently provides pipelines, including models, for almost 20 languages.}
}

@inproceedings{stenetorpBratWebbasedTool2012,
  title = {{{brat}}: A Web-Based Tool for {{NLP-assisted}} Text Annotation},
  booktitle = {Proceedings of the Demonstrations Session at {{EACL}} 2012},
  author = {Stenetorp, Pontus and Pyysalo, Sampo and Topi{\'c}, Goran and Ohta, Tomoko and Ananiadou, Sophia and Tsujii, Jun'ichi},
  year = {2012},
  month = apr,
  publisher = {{Association for Computational Linguistics}},
  address = {{Avignon, France}}
}
```