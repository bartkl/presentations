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
---

# Building CIM-based Data Products with LinkML: the Linked Data Modeling Language

###### Bart Kleijngeld | May 16th, 2024

---

## Hello :wave:

* My name is Bart Kleijngeld
	* :triangular_ruler: Data Architect
	* :man_technologist: Software Developer

---

## Managing Data in the Face of Decentralization

---

Alliander has been decentralizing
* The Agile way of working is more bottom-up

---

Autonomous BizDevOps teams can move faster
* but there is (some) loss of control

---

To manage and govern our data, architectural changes are needed

---

Data Mesh

<!-- IMG: Four core principles -->

---

To give an idea of the mesh...

---

<!-- IMG: Mesh -->

---

Let's zoom in on an exchange of data between producer and consumer
* and see what a data product is

---

<!-- IMG: Producer -> dataset -> consumer -->

---

Note that teams are now responsible for describing what their data means

---

The CIM could be of great help here
* How can we help teams use it?

---

## Modeling Data Products

---

### Sparx EA

---

EA is a dedicated tool for information modeling
* and the CIM is maintained in it

---

To model a data product, we could simply create a profile based on the CIM

---

Teams can also generate code and other artifacts
* aiding them in their other work

---

That's not too bad, right?

---

Well...
* There are challenges

---

#### Challenges with Sparx EA

---
<!-- _class: with-bullets -->

Those BizDevOps teams that are expected to do the modeling?
* Well, turns out they have tools they prefer
* ... and this should be respected

---

And EA is not the kind of application they want to use

---

EA is heavy and has a complex UI
* Steep learning curve
* Slow to get things done in compared to textual editing

---

Moreover, models in EA are hard to use outside of the application
* so it's hard to work on these models with other tools

<!--
* Vendor specific implementations of UML
* Complex serialization with XMI
* QEA/EAP files are binary database files
-->

---

This makes it hard for those teams to put their preferred tooling to use

---

But it also makes managing versions in a VCS tedious
* making it hard to collaborate

---

Automating tasks based on models in CI/CD pipelines is difficult too
* generating documentation for example

---

<!-- TODO: This seems abrupt -->

Inversely, it is also hard to use models or standards that are not modeled in EA
* which is very constraining

---
<!-- _class: with-bullets -->

And then there's:
* Licensing costs
* Non-Windows users for whom only the SaaS would work

---

#### Challenges with UML

---

Besides EA we are confined to UML

---

Firstly, UML is not trivial to learn and complex
* neither very thrilling to most

---

Vendor implementations of UML differ
* further inhibiting interoperability

---

UML was never intended for expressive information models
* fine for data models
* ...but limiting for information models

---

One such limitation is the exclusive class-based OOP model
* one example is not being able to model properties as first-class citizens

---
<!-- _class: with-bullets -->

Identifiers are also not sophisticated enough for a decentralized architecture
* Local names don't suffice of course
* Opaque IDs such as GUIDs are hard to work with
* Meaningful global identifiers like URIs aren't part of UML

---

#### What is necessary for improvement?

---

The primary representation of models should be text
* both machine and human readable

---

This way interoperability with a myriad of tools is ensured
* for both modeling and automated tasks

---

Furthermore, we need a global identification mechanism
* with the option of human understandable IDs

---

Flexibility to use standards and models with differing metamodels
* with minimal effort

---

## The Semantic Web and Linked Data

---

The Semantic Web is the machine readable counterpart to the World Wide Web envisioned by Tim Berners-Lee

---

Its design revolves around:
* A decentralized architecture
* Modeling of information in a human and machine readable way
* Comfortably linking data around the world
    * which involves URIs as global identifiers

---

As you may have noticed this is a pretty perfect match

---

### What's great about it

---

Models and modeling languages are all code

---

It's as straightforward to add modeling languages as it is to add data
* i.e. it's extremely flexible

---

Everything is identified by a URI
* which allows encoding human readable names that are globally unique

---

Integrating data from various sources is straight-forward
* just merge the graphs
* URIs tell you what things are

---

Choosing URIs that resolve to URLs allows for documentation on the web

---

### Challenges with Semantic Web Technology

---

Very steep learning curve

---

The graph-shaped RDF data representation format is unfamiliar

---

It's a huge commitment which is hard to gradually implement

---

## LinkML

---

LinkML is a modeling language with ecosystem developed by Berkeley Lab
* bio science (TODO: ...?)
* it's open source and is actively maintained (including community meetings and co-operation)

---

The language sets out to meet developers where they're at with regards to data modeling
* semantics that are familiar but expressive
* YAML syntax that's easy and widespread

---

... but with Linked Data support

---
<!-- _class: with-bullets -->

Particularly URI mappings
* for identification
* based on the SKOS language for relating business terms

---

This is how a schema looks

---

<!-- IMG: excerpt from YAML-->

---

The ecosystem provides many great tools
* code generators for many widely used languages and technologies
* interactive documentation generation including diagrams
* schema validation tools
* maintaining models in Excel
* and much more

---

If a generator is missing or doesn't work the way you like
* you can simply add your own or extend it

---

Okay all of that is nice, but weren't we supposed to standardize using CIM?

---

### Work done

---

In the last months, we've done some hacking

---

Things done
* CGMES profiles available in LinkML
* Entire CIM100 available in LinkML
* CLI tool for easy profiling

---

### Roadmap

---

This will depend on how many people want to use this

---

## Way forward



