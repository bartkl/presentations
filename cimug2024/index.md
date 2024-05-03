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
    text-align: center;
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
---

# Building CIM-based Data Products with LinkML: the Linked Data Modeling Language
<!-- _class: align-left -->
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

---
<!-- _class: align-left -->
## Managing Data in a Decentralized World

---
<!-- header: "Managing Data in a Decentralized World" -->

In many ways, the world of IT has been decentralizing

---
<!-- _class: align-left with-bullets -->

Agile flipped our way of working from top down to **bottom up** so we
* can move faster
* improve team autonomy
* have less waste

<!-- I won't be going into too much detail: this is not a talk about Agile.-->

---

This comes with challenges
* integrating components
* governing a maintainable landschape
* standardization and conventions

In short: managing and governing products



<!-- Not least for data -->

---


How do you govern and manage data in a decentralized architecture?

---

Information modeling becomes more important but also harder to do

---
<!-- _class: align-left with-bullets -->

Decentralization makes you **move faster** but have **less control**

---

Luckily people have come up with smart ideas to tackle these challenges

---
<!-- _class: align-left -->
#### Data Mesh

![Data Mesh Core Principles.excalidraw.light](Attachments/Data%20Mesh%20Core%20Principles.excalidraw.light.svg)
<!--
Mentioned only for reference; we will be looking only at "data as a product"

* Mention the link between Agile and Data Mesh
-->

---
<!-- _class: align-left -->

#### Data Mesh

![Data Mesh Core Principles DP highlighted.excalidraw.light](Attachments/Data%20Mesh%20Core%20Principles%20DP%20highlighted.excalidraw.light.svg)

---
<!-- _class: align-left with-bullets -->

Data Mesh 
* centralize 
* govern using metadata
* platform or catalog
* kko


---

## Modeling Data Products


---

<!--

1. Agile and Decentralized Architecture
    1. Moving faster with bottom up, iterative way of working
    2. Developer autonomy to facilitate this WoW
    3. Challenges of decentralization
        1. Loss of control and overview
        2. No central point of maintenance
2. Code-Based Model Benefits
3. Linked Data
4. Modeling LinkML
5. 

-->

0) Data Challenges at Alliander
    1) Shift to Agile Way of Working and Data Mesh
    2) FAIR
    3) Governance
    4) Everlasting Debates
    5) Interoperability
2) Data Mesh and Data Products
3) Building Data Products with Sparx EA
    1) 
4) Linked Data
5) Settling for Pragmatism with LinkML
6) Demo

---

## Data Products and Modeling Challenges
<!-- _class: lead -->

---
### Data Mesh

* Decentralized architecture which empowers teams
* ![Data Mesh Core Principles.excalidraw.light](Attachments/Data%20Mesh%20Core%20Principles.excalidraw.light.svg)
<!-- Mentioned only for reference; we will be looking only at "data as a product" -->

---

#### A Mesh of Data Products

![Data products.excalidraw.light](Attachments/Data%20products.excalidraw.light.svg)

### What is a Data Product?

---

![bg 80%](Attachments/What%20are%20Data%20Products.excalidraw.light.svg)

<!--
- Data outlives technology and organisation, and therefore
* Data products are abstract
	* Decoupled from technology/implementation
	* Metadata driven
* Machine readable is nice:
	* generation
	* interaction
	* maintenance
-->

---

A bit of clarification...

---

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
