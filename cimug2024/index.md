---
marp: true
theme: rose-pine-dawn
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
    color: rgb(87, 82, 121);
    margin-top: 1.5rem;
  }
  table th:empty {
    display: none;
  }
  table tr, table tr:nth-child(2n) {
    background-color: unset;
  }
  table tr > td {
    border-left: 0;
    border-right: 0;
  }
  table tr:not(:last-child) > td {
    border-bottom: 0;
  }
---

# Building CIM-based Data Products with LinkML: the Linked Data Modeling Language
<!-- _backgroundImage: unset -->

###### Bart Kleijngeld | May 16th, 2024

![bg opacity:0.3](Attachments/scott-webb-mV9-1XjnM4Y-unsplash.jpg)

---

## Hello :wave:
<!-- _class: align-left -->

![bg cover right:50%](Attachments/me-coffee.jpg)
* My name is Bart Kleijngeld
	* :triangular_ruler: Data Architect
	* :man_technologist: Software Developer
    * :walking_man: :musical_note: :film_strip: :books: :seedling: :coffee: :beer: 

---

- Enough chit-chat...
    * Let's get started! :muscle:

<!-- Outline.

1. What is a Data Product?
2. How to Model a Data Product?
3. Modeling Data Products with Sparx EA
4. Linked Data and The Semantic Web
5. LinkML

-->

---

## What is a Data Product?

---
<!-- header: "What is a Data Product?" -->

To understand data products we first have to talk about decentralized architecture

---

### Data Mesh

![Data Mesh Core Principles.excalidraw.light](Attachments/Data%20Mesh%20Core%20Principles.excalidraw.light.svg)

---

### Data Mesh

![Data Mesh Core Principles DP highlighted.excalidraw.light](Attachments/Data%20Mesh%20Core%20Principles%20DP%20highlighted.excalidraw.light.svg)

---

Let's visualize that mesh

---


![Data products.excalidraw.light](Attachments/Data%20products.excalidraw.light.svg)

---

So, what is a data product?

---
<!--
- Data outlives technology and organisation, and therefore
* Data products are abstract
	* Decoupled from technology/implementation
	* Metadata driven
-->

![What are Data Products.excalidraw.light](Attachments/What%20are%20Data%20Products.excalidraw.light.svg)
<!-- TODO: Improve drawing. -->

---

We will focus on the information modeling which is crucial when decentralizing
* but it's also harder

---
<!-- header: "" -->

## Modeling Data Products

---
<!-- header: "Modeling Data Products" -->

### What modeling requirements are set by Data Mesh?

---

Recall we're working bottom up, empowering autonomous teams

---

The information models are maintained by these teams themselves

---

They have their own tools and way of working
* and they should be met where they're at

---

However...

* We *do* still need to be able to manage and govern the data

---

You may not be able to force them to use tools
* but you can enforce the use of a contract

---

Remember data products?

---

We need information models to be machine-readable
* as way of a contract
* exchangeable as part of data products

---
<!-- _class: with-bullets -->

Moreover, this enables teams to do lots of clever - and familiar - automations

* Version control
* (Automatic) Generation of code and documentation
* Data product deployment (CI/CD)

---
<!-- _class: with-bullets -->





- Move quickly
- Version easily
- Accessible to maintain
    - comfortable and easy to learn tech stack
    - no academic degree in modeling required

|                                                 |                    |
| ----------------------------------------------- | ------------------ |
| Accessible to be maintained by teams themselves | :white_check_mark: |
| CI/CD                                           | :x:                |





---

* Machine readable
    * CI/CD
    * catalog
    * federated computational governance




---

<!--
* Machine readable is nice:
	* generation
	* interaction
	* maintenance
-->

#### NORA &mdash; MIM Conceptual Framework
<style scoped>
ul { padding-inline-start: 0 }
</style>
  ![width:700px](Attachments/MIM%20Conceptual%20Framework.excalidraw.light.svg)
<!-- Mention RFC3444-->
* #### The CIM
   ![width:700px](Attachments/RFC3444%20Variant.excalidraw.light.svg)

<!--
* reusable definitions
* proper model serialization for code generation and CI/CD solutions
* accessible and easy to maintain documentation of definitions and models
* expressive modeling languages to cover all needs
-->

### How Do We Model Data Products?

## Sparx EA

![bg 50% opacity:1.0](Attachments/Sparx%20EA%20Header%20BG.excalidraw.light.svg)

### Modeling workflow

---

![bg 70%](Attachments/Sparx%20EA.excalidraw.light.svg)

---

![bg 70%](Attachments/Sparx%20EA%200.excalidraw.light.svg)

---

![bg 70%](Attachments/Sparx%20EA%201.excalidraw.light.svg)

<!--
#### Models are not textual

* Making changes is tedious
* No access to many tools to help
	* text editors
	* search and manipulation tools
	* language servers
* Version control and collaboration are non-trivial

#### Model serialization is complex

* Native formats couple you tightly to EA
	* but standardized formats (like XMI) have limitations and issues
* We practically have vendor lock-in

#### The metamodel is UML and only UML

* No
	* top-level slots and individuals, preventing re-use of definitions of attributes and relations
	* multiple inheritance or mixins
	* support for global identifiers
	* support for other metamodels than UML

- Because of the lack of slots, one cannot simply re-use a `name`, but must use complicated inheritance structures to obtain it, or rely on stereotypes. Compare this to how simple RDFS and LinkML make this
-->

---

Sparx EA and UML offer no support for Linked Data in models
no support for slots


### Why Use Sparx EA?

* Normative model of the CIM
* Accessible and feature rich

---

But that shouldn't suffice

### Further shortcomings

* No global, namespaced identifiers

----

#### Schema and documentation generation

* Need to start expensive and heavy application to do generation
	* so it cannot be run from a CI/CD pipeline for instance
* No freedom of choice in what programming language you use
	* and limited choice in development tools

### How do we overcome these challenges?

## The Semantic Web

![bg 30%](Attachments/Semantic%20Web%20Header%20BG.excalidraw.light.svg)

<!-- NOTE:
- Mention the fear of text, and how developers are working with gigantic models. It's actually better for overview, since it's not a mess with more than a few classes, and you can search and filter and transform text easily.
-->

### Modeling overview

---

![bg 70%](Attachments/Semantic%20Web%20flowchart.excalidraw.light.svg)

---

![bg 70%](Attachments/Semantic%20Web%20flowchart%202.excalidraw.light.svg)

### Why use Semantic Web technology?

---

It solves many of the issues with Sparx EA
* but introduces new ones

---

#### Everything is plain text

---

* Self-documenting
* Global identifiers using URIs
	* enabling Linked Data
* Graph
* Language tagged literals (langstrings)



## LinkML: The Actual Savior

## Roadmap
* LinkML Profiler
* LinkML Language Server
* The entire CIM in LinkML schemas

## Demo (5 min)
* Showcase: EN-TSO-E CGMES profiles in LinkML
	* Generated documentation
	* Live generation of Pydantic, JSON Schema and SQL DDL


----

![ik 1](Attachments/ik%201.png)
