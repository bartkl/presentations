---
marp: true
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

# Building CIM-based Data Products with LinkML: the Linked Data Modeling Language

###### Bart Kleijngeld | May 16th, 2024

---

## Hello :wave:

![bg fit](Attachments/me-coffee.jpg)

---

- My name is Bart Kleijngeld...

* :triangular_ruler: Data Architect
* :man_technologist: Software Developer

---

Let's get started!
:muscle:

---

## Managing Data in the Face of Decentralization

---

Enterprise organisations are increasingly working bottom-up.
* The Agile way of working is a prominent example of this.

---

Furthermore, data sharing between organisations is increasing...
* improving cooperation.

---
<!-- _class: with-bullets -->

Managing data we have no or little control over is challenging.
* What does the data mean?
* How can the data be used (responsibly)?
* Who owns the data?
* Etc.

---

How can we deal with this?
* We need to have a scalable way to produce data in a standardized manner.

---

### Data Products

---

We will be borrowing the *data as a product* principle from the Data Mesh paradigm to deal with our challenge.

---

![](Attachments/index%202024-05-12%2013.54.35.excalidraw.light.svg)

---

If teams are going to be responsible for the information modeling...
* how can we best enable them?

---

## Modeling Data Products with LinkML

---

Due to time constraints I will jump straight to LinkML.
* I'm happy to answer questions about challenges we encountered with Sparx EA and RDF afterwards.

---

![](Attachments/linkml_resized.png)

LinkML is a data modeling language developed in the Bio Sciences department at Berkeley Lab.
* LinkML is also a tool, with a growing ecosystem surrounding it.

---
### Authoring LinkML

---
<!-- _class: with-bullets -->

LinkML is accessible, especially to developers. It has...
* familiar YAML syntax;
* easy and familiar semantics.
<!-- Mention: classes, types, inheritance, mixins, properties -->

---

Let's look at a small example of a LinkML schema.

---

```yaml
classes:
  ACDCConverterDCTerminal:
    is_a: DCBaseTerminal
    description: A DC electrical connection point at the AC/DC converter. The AC/DC
      converter is electrically connected also to the AC side. The AC connection is
      inherited from the AC conducting equipment in the same way as any other AC equipment.
      The AC/DC converter DC terminal is separate from generic DC terminal to restrict
      the connection with the AC side to AC/DC converter and so that no other DC conducting
      equipment can be connected to the AC side.
    attributes:
      polarity:
        range: DCPolarityKind
        required: false
        multivalued: false
        description: "Represents the normal network polarity condition. Depending\
          \ on the converter configuration the value shall be set as follows:\r\n\
          - For a monopole with two converter terminals use DCPolarityKind \u201C\
          positive\u201D and \u201Cnegative\u201D.\r\n- For a bi-pole or symmetric\
          \ monopole with three converter terminals use DCPolarityKind \u201Cpositive\u201D\
          , \u201Cmiddle\u201D and \u201Cnegative\u201D."
      DCConductingEquipment:
        range: ACDCConverter
        required: true
        multivalued: false
        description: A DC converter terminal belong to an DC converter.
```

---
<!-- _class: with-bullets -->

Note how we are not locked into having to use a single application for modeling.
* Teams can use their preferred tools, most notably their IDEs.

---

### Maintaining and Organizing Models

---

Models represented as YAML files fit right in with the way of working of BizDevOps teams.
* They work with YAML files all the time!

---

LinkML schemas either become part of the repository like all other code...
* or you create dedicated model repositories: it's up to you.

---

Collaboration and versioning becomes straightforward using a VCS like Git.
* Again: it's no different from the usual way of working.
* Even external collaborators can contribute.

---

### Code and Documentation Generators

---

LinkML also offers a variety of generators you can use to generate code, documentation and other artifacts.

---

![](Attachments/index%202024-05-12%2015.47.34.excalidraw.light.svg)

<!-- Image includes example generators out of the box:
* Python
* JSON-LD
* SQL DDL
* Documentation
* JSON Schema
* SHACL
* and more, including your own extensions
-->

---

This could save teams **a lot** of work.
* Especially since maintaining several physical models is a lot of duplicate work.

---

### Automated Tasks

---

Since LinkML models are simple YAML files, it's very easy to write scripts and programs that utilize them.
* CI/CD pipelines could be extended to perform these tasks on deployment.

---

![](Attachments/index%202024-05-12%2016.14.43.excalidraw.light.svg)

---
<!-- _class: align-center -->

\*\*\*

---

Sure. LinkML looks nice for BizDevOps team to help out with data modeling, but...

---

Weren't we supposed to deal with decentralized architecture and describing our data?
* Where's the CIM in this picture, or information modeling at all for that matter?

---

## Bringing in the CIM

---

The obvious way is to simply name things corresponding to the CIM, but...

---

![bg width: 50%](Attachments/index%202024-05-12%2019.45.10.excalidraw.light.svg)

---
<!-- _class: with-bullets -->

- Different schemas have different naming conventions and restrictions;
* Equal names don't imply equality;
* Different names don't imply inequality.

---

We need more sophisticated means of naming and identification.

---

### Linked Data

---

Tim Berners-Lee envisioned a machine-readable counterpart to the World Wide Web...
* The Semantic Web.

---

A core tenet of this vision is the idea of *linked data*...
* linking data (sets) all across the web.

---

![](Attachments/index%202024-05-12%2016.42.35.excalidraw.light.svg)

---

But how do we refer to data from other data sets?
* Names are usually local...
* causing the issues we saw earlier.

---

The main enabler for Linked Data is the use of **URI**s for global identification.

---

![](Attachments/index%202024-05-12%2016.53.18.excalidraw.light.svg)

---
<!-- _class: with-bullets -->

URIs...
* can encode ownership in the domain;
* can provide namespacing for identifiers.

---
<!-- _class: with-bullets -->

This solves our earlier problem with identification:
* If two things have the same URI, they are the same thing.
    <!-- * Watch out: the reverse is not necessarily true. -->
* Different data sets and organisations can use namespaces to provide unique identifiers.

---

But how can we use these URIs?

---

### Referencing URIs in LinkML

---

LinkML supports annotating schema elements with names from reference models...
* like the CIM!

---
<!-- _class: with-bullets -->

It's very easy to use multiple reference models.
* This provides immense flexibility and ease of standardization.
* Usually this is difficult or even impossible to do.
* It's no problem if the models are expressed in different modeling languages.

---

Let's take a look again at the LinkML schema earlier...
* this time with CIM references.

---

But before going there, I need to explain compact URIs (CURIEs).

---

![](Attachments/index%202024-05-12%2019.55.05.excalidraw.light.svg)

---

Alright, now we're ready.

---

```yaml
classes:
  ACDCConverterDCTerminal:
    class_uri: cim:ACDCConverterDCTerminal
    is_a: DCBaseTerminal
    attributes:
      polarity:
        slot_uri: cim:ACDCConverterDCTerminal.polarity
        range: DCPolarityKind
        required: false
        multivalued: false
      DCConductingEquipment:
        slot_uri: cim:ACDCConverterDCTerminal.DCConductingEquipment
        range: ACDCConverter
        required: true
        multivalued: false
```

---

Using fields like  `class_uri` and `slot_uri` we can standardize schema elements by annotating them with reference model names.

---

LinkML also supports other kinds of URI mappings.
* Most notably expressing narrower, broader or exact matches to terms using SKOS.

---

### Profiling CGMES and the CIM with LinkML

---

Mapping names to reference models is great...
* but sometimes we could use more help.

---

Reference models often have more to offer than just standardized names.

---

The CIM describes attributes, relations, etc.
* CGMES profiles provide use-case specific constraints.

---

It would be nice if we could profile these to bootstrap our data products...
* but how can we do that if we don't have LinkML schemas for the CIM and CGMES?

---

Well, we generate those schemas!

---

#### The CGMES LinkML Schemas

---

I've written a script that has generated a LinkML schema for each CGMES profile.
* It is based on the RDFS 2020 version.

---
<!-- _class: with-bullets -->

Resources:

- The [script](https://github.com/alliander-opensource/cimrdfs2linkml) that generates the LinkML schemas.
- The [LinkML schemas](https://github.com/alliander-opensource/cgmes-profiles).
- The automatically generated [documentation](https://alliander-opensource.github.io/cgmes-profiles/).

---

#### The CIM LinkML Schemas

---

Similarly, I've generated LinkML schemas for the entire CIM.
* It is based on the official Sparx EA project.

---
<!-- _class: with-bullets -->

Resources:

- The [script](https://github.com/bartkl/cim-to-linkml) that generates the LinkML schemas.
- The [LinkML schemas](https://github.com/alliander-opensource/cim-linkml).
- The documentation hasn't been generated yet.

---

#### LinkML Profiler

---
<!-- _class: with-bullets -->

Ritger Teunissen has developed a [profiler](https://github.com/ritger-alliander/gen-linkml-profile) for LinkML schemas.
* Currently command-line only...
* but building a simple GUI is anticipated.

---

Given a CIM or CGMES LinkML schema, you pass in the classes you'd like to use, and it will create a LinkML schema for you.

---

![bg width: 30%](Attachments/index%202024-05-13%2010.34.00.excalidraw.light.svg)

---

It also enables flattening class hierarchies, skipping optional fields, and more.

---
<!-- _class: align-center -->

\*\*\*

---

Imagine how difficult much of the above would be using Sparx EA.
* LinkML just really lends itself for data modeling in a decentralized world.

---

Can we make this even more cool?

---

## Road Ahead

---
<!-- _class: with-bullets -->

I want to improve interoperability with existing CIM tools:
* Also, we are investigating how to improve the LinkML ecosystem.

---

Furthermore, I would love to see adoption increase.

* Currently LinkML is being used by Netbeheer Nederland, a cooperative initiative between DSOs in the Netherlands...
* but I'm sure it could be beneficial to others as well.

---

So if you are interested in using LinkML or have any other questions or ideas...
* feel free to contact me!

---

Are there any questions?
* Thank you for listening!