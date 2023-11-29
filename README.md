# Augustinian Sermon Parallelism (ASP) Dataset
**Authors**: 
* Stephen Bothwell, Theresa Crnkovich, Hildegund Müller, and David Chiang (University of Notre Dame)
* Justin DeBenedetto (Villanova University)

**Maintainer**: Stephen Bothwell

## Summary

This repository contains the Augustine Sermon Parallelism (ASP) dataset--a collection of Latin sermons from Augustine's *Sermones* annotated for rhetorical parallelism. 
It is intended to be used to study the phenomenon of rhetorical parallelism both in the application of language broadly and in the specific context of Augustine of Hippo.

### Statistics

The table below summarizes its base statistics. For exact definitions of *parallelism* and *branch*, please see our paper. 
For a high-level understanding, consider a *branch* to be a continuous span of annotated text; 
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

The annotations in this dataset are licensed under a Creative Commons Attribution-Sharealike 4.0 International (CC-BY-SA) license. 
For more information, please see https://creativecommons.org/licenses/by-sa/4.0/.

## Background

Among the Latin Church Fathers of late antiquity, Augustine of Hippo (354-430) stands out through the amount of his writings, the theological depth of his major treatises, and the vast influence he exerted on the Western Church in the Middle Ages and beyond. 
In his own time, Augustine was known as a prolific and fascinating preacher, having been invited to preach in numerous North African cities in addition to his own church, Hippo Regius (now Annaba, Algeria). 
Many of his sermons were delivered in the provincial capital of Carthage. 
In spite of the conquest of Roman North Africa by the Vandals and the widespread destruction that followed, the majority of Augustine’s works were preserved and copied throughout the Middle Ages. 
This includes a large number of sermons. 
Altogether, the extant sermons number about 800, and hitherto unknown sermons are still being identified in medieval manuscripts.

Augustine improvised his sermons and never used a written draft. 
During the delivery in church, his words were taken down in shorthand by scribes present in the audience and later transcribed in longhand and preserved in his library. 
Most of his sermons were apparently not edited or redacted for publication, which makes them precious documents of the spoken rhetoric of late antiquity. 
In some cases, Augustine (or his secretaries) later collected his sermons on a book of the Bible and supplied dictated passages to form a complete commentary (*On the Psalms*, *Tractates on the Gospel of John*, *Tractates on the Epistle of John*). 

The vast majority of Augustine’s preaching is scriptural and exegetical. 
Augustine uses various exegetical strategies, but he prefers allegorical readings. 
The additional depths of meaning found in scripture through allegory provide the main structure and content of the sermons and eclipse other typical subjects of late ancient sermons, such as moral education or discussion of contemporary political and cultural issues. 
This approach also allowed Augustine to touch upon complicated theological matters that other preachers avoided; 
his sermons include discussions of his teachings on all major subjects of Christian doctrine, such as trinity, the nature of good and evil, justice and mercy, predestination and free will, and others. 
In his reading, the Bible provides images and examples to clarify complex subjects to an unlearned audience, and the shared history of the chosen people establishes the unity of the Church from its beginnings to Augustine’s listeners. 
In fourth and fifth-century North Africa, where this unity was imperiled by internal schisms and external threats, the sermons thus provided an appeal to agreement among the listeners and strengthened their continued identification as members of the church itself, the body of Christ.

Augustine had been educated in classical rhetoric, and before his conversion to Christianity, he had been a renowned teacher of rhetoric himself. 
For his preaching, he chose to reinvent his rhetoric in a style better adapted to the understanding of a socially mixed audience and the simple truths underlying the message of the Gospel. 
He eschewed the wide variety of rhetorical embellishments taught by late ancient rhetoricians and instead relied on a small number of simple rhetorical figures that not only were recognizable by his listeners but also allowed him to put the logical structure of his teachings into sharper focus. 
Such devices included parallelism, rhyming, and alliteration. 
While influenced by the language of Latin Scripture, he never attempted to imitate it; 
instead, the omnipresence of Scripture serves as an additional embellishment and constant subtext to the words of the preacher.

## Contents

This repository contains three versions of our dataset. Each version of the dataset progressively imposes greater constraints on the way in which the data is presented. 
These three versions are as follows:
* **Raw**: In our `data/original` directory, we provide the version of the dataset collected from the `brat` annotation tool (Stenetorp *et al.* 2012). This format consists of two types of files:
  1. Input text (`.txt`) files extracted of Augustine's *Sermones* from the InteLex database.
  2. Annotation files (`.ann`) generated by `brat` in that program's annotation encoding format.

  Each `.txt` file is paired with a `.ann` file of the same name. The `.ann` file in a given pair labels our annotator's decisions concerning parallel structure. We provide a description of our annotation scheme in our paper as well as in the `procedures` folder.
* **Untokenized XML**: In our `xml/untokenized` directory, we provide XML files which combine the `.txt` files and `.ann` files in a nested format. These files (sans the pretty-printed formatting imposed by Python's `xml.dom.minidom`) were provided as input to the system in our paper. 
Annotations were organized in order to represent their nested structure. Each XML file contains up to three types of tags:
  * The `<sermon>` tag wraps around the entire text to indicate it as one unit. It has an `id` attribute which indicates that text's numerical indicator within Augustine's *Sermones*.
  * The `<section>` tag denotes a *section* of text--a subdivision of the sermon imposed by editors. Each section has an `id` attribute which indicates what index editors applied to each section. Such indices start at 1 and increase sequentially.
  * The `<parallelism>` tag designates a branch of some parallelism in the text. Being presented in this format, `<parallelism>` tags can nest indefinitely; however, in this dataset, parallelisms nest at most once. Each branch has an `id` attribute which notes to what parallelism it belongs.
  It also has a `part` attribute that shows the numerical ordering of individual branches. Both `id` and `part` start from 1 and increase sequentially. 
  When nested branches start at the same point, the parallelism with the branch that *ends* first has a smaller `id`. In other words, nested parallelisms tend to come before nesting parallelisms.
* **Tokenized XML**: In our `xml/tokenized` directory, we provide XML files which combine the `.txt` files and `.ann` files in a nested format. Like the untokenized variant, this version also contains up to three types of tags. 
The `<sermon>` and `<section>` tags reprise their roles above. However, the third tag, `<word>`, designates a tokenization applied through the [Classical Language Toolkit](http://cltk.org/) (Johnson _et al._ 2021). 
Each `<word>` has an `id` attribute indicating its position within a given section, starting from 1. 
The actual token is given in the `cont` attribute, following the convention of the [PSE](https://github.com/Mythologos/Paibi-Student-Essays) dataset.
Finally, a `parallelism_id` and `branch_id` are given for each applicable stratum (or level of nesting).
These values start from 1 and increase sequentially, following the same rules as the untokenized XML's `id` attributes.

We also provide information about our process for developing the dataset. To this end, please see the PDF file available in the `procedure` directory. 
We give a sketch of our initial guidelines used to produce this data in the `"RPD - Original Annotation Guidelines"` PDF. 
We further present a revised version of the guidelines engendered through a critical evaluation of our annotations in the `"RPD - Revised Annotation Guidelines"` PDF.

To further show the validity of our data, we provide a portion of the data annotated both by the single annotator of the dataset at large, Hildegund Müller, and by Theresa Crnkovich. 
Eight sermons were annotated by each of them, and the results of their annotation are presented in the `data/agreement-study` subdirectory. (The data presented here includes no pretty-printing and is exactly as it was originally used.) 
Hildegund Müller and Theresa Crnkovich are annotators A and B, respectively. We discuss in our paper the results of an inter-annotator agreement study across each of our proposed metrics, 
and we provide the code with which this study was performed in the [Intro-RPD](https://github.com/Mythologos/Intro-RPD) repository.

## Contributing

This repository is intended to provide a single, definitive version of this dataset for future work and research. 
However, if there are issues or mistakes with the data, we would be glad to investigate them. 
Please open an issue to start a conversation on the subject. 

Any future updates of the dataset will be tagged with a version number so as to make it easy to designate and compare results. 
The current version is `v1.0`.

## Citations

### Our Work

To cite this dataset, please use the following paper citation:

```
@inproceedings{bothwellIntroducingRPD2023,
    author = {Bothwell, Stephen and DeBenedetto, Justin and Crnkovich, Theresa and M{\"u}ller, Hildegund and Chiang, David},
    title = "Introducing Rhetorical Parallelism Detection: {A} New Task with Datasets, Metrics, and Baselines",
    booktitle = "Proc. EMNLP",
    year = "2023",
    note = "To appear"
}
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