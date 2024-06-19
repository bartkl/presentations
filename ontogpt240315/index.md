---
marp: true
headingDivider: 2
theme: minimal
title: "Building CIM-based Data Products with LinkML: the Linked Data Modeling Language"
size: 16:9
footer: "![w:100px h:60px](Attachments/alliander_logo.png)"
style: |-
  section {
    font-family: "Fira Sans";
    font-size: 1.8rem;
    text-align: left;
  }
  h1 { font-size: 3.0rem; }
  h2 { font-size: 2.8rem; }
  h3 { font-size: 2.3rem; }
  h4 { font-size: 1.8rem; }
  p {
    font-weight: normal;
    font-size: 1.8rem;
  }
  footer img {
    background-color: unset;  /* Fixes transparancy. */ 
  }
  section.align-center {
    text-align: center;
  }
  section.align-left {
    text-align: left;
  }
  section.with-bullets ol, section.with-bullets ul {
    list-style: disc;
    margin-bottom: 0;
  }
  ol, ul {
    list-style: none;  /* No bullet points for fragments. */
    margin-bottom: 0;
  }
  ul > li,
  ol > li {
    /* color: rgb(87, 82, 121); */
    color: rgb(31, 35, 40);
    margin-top: 1.5rem;
  }
---
<!-- class: with-bullets -->

# Entity and Relation Extraction using OntoGPT and SPIRES

###### Bart Kleijngeld | March 3rd, 2024

## Goal
Populate a knowledge graph from unstructured text with as much structure as we can

* *Entity and relation extraction* from unstructured text
* *Grounding* these terms on ontologies (aka *entity linking*)

---

## SPIRES
[Structured Prompt Interrogation And Recursive Extraction Of Semantics (SPIRES): A Method For Populating Knowledge Bases Using Zero-Shot Learning](https://arxiv.org/abs/2304.02711)

> Given a detailed, user-defined knowledge schema and an input text, SPIRES recursively performs prompt interrogation against an LLM to obtain a set of responses matching the provided schema. SPIRES uses existing ontologies and vocabularies to provide identifiers for matched elements.

Developed by the Monarch Initiative
* Field of Bio Informatics
* Involvement of Berkeley Lab

## How it Works

---

### Overview

![bg w:400px](Attachments/Pasted%20image%2020240311133543.png)

---

- Recursive prompting
	* For each attribute
* Entity grounding
	* Services that provide LD URIs from ontologies

## OntoGPT

- Implementation of SPIRES
* Model-agnostic, but easiest is to use OpenAI GPT
	* we use OpenAI GPT3.5 Turbo

## Demo

Extraction of music artist information from Miles Davis Wikipedia page excerpt
<!--
1. SSH into `bart-k-semantics`
2. ~/ontogpt-kg $ poetry shell
3. ~/ontogpt-kg $ ontogpt extract -i m.txt -t person

`person` is the schema for music artist extraction which I've added. Make sure to generate a new Pydantic schema whenever you change the person schema:

	gen-pydantic ~/.cache/pypoetry/virtualenvs/ontogpt-kg-ipkDGH2g-py3.10/lib/python3.10/site-packages/ontogpt/templates/person.yaml

-->

## Notes

* Scalable method
* High-level
	* Abstracts away the prompting
* Relatively cumbersome schema due to how SPIRES works
* Great grounding performance
	* let's have a look...

## Performance

 > Current SPIRES accuracy is comparable to the mid-range of existing Relation Extraction (RE) methods, but greatly surpasses an LLM’s native capability of grounding entities with unique identifiers

>  This grounding method offers far more consistent mapping to unique identifiers than hallucination-prone LLM querying alone

---

### Benchmarks: Entity Grounding
Precision of grounding 100 randomly selected entities

|       | GPT3.5T (SPIRES) | GPT4T (SPIRES) | GPT3.5T        | GPT4T  |
| :---- | :--------------- | :------------- | :------------- | :----- |
| GO    | 0.98             | 0.97           | 0.03           | -      |
| MUNDO | 0.97             | 0.18           | ≤ 0.01         | ≤ 0.01 |
| EMADA | 1.00             | 1.00           | wrong ontology | -      |

<!--
* With large general purpose LLMs such as these I can imagine a large probability for finding false positives (such as the EMADA wrong ontology choice by GPT3.5T)
	* Grounding with dedicated annotator services provides the precise scope/context to do it right, as in: if recall succeeds it's likely accurate.
-->

---

### Benchmarks: NER
Precision/recall for NER including grounding

---

![bg 80%](Attachments/Pasted%20image%2020240311141253.png)

## Challenges and questions
* Token limit exceeded very quickly with OpenAI
	* How many requests will this take?
* Flaky: very different outcomes and performance with different models
* How well does it perform, offset against impact on resources?
* Very promising results
* How to determine what to do next?
