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

* My name is Bart Kleijngeld
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

Furthermore, organisations are looking to collaborate more by sharing data.

---

![](Attachments/index%202024-05-12%2014.25.27.excalidraw.light.svg)

---
<!-- _class: with-bullets -->

Managing data we have no or little control over is challenging.
* What does the data mean?
* How can the data be used (responsibly)?
* Who owns the data?
* Etc.

---

How can we deal with this?

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
    from_schema: https://cim.ucaiug.io/ns#TC57CIM.IEC61970.Base.DC
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

Note that teams can use their own tools such as IDEs.
* This freedom and respect is better for everyone.
* It prevents costly vendor lock-in issues.
<!-- Writing and manipulating text is fast and versatile. -->

---

### Maintaining and Organizing Models
<!-- TODO: More images? Summary? -->

---

Models represented as YAML files fit right in with the way of working of BizDevOps teams.
* They work with YAML files all the time!

---

LinkML schemas either become part of the repository like all other code...
* or you create dedicated model repositories: it's up to you.

---

Collaboration and versioning becomes straightforward using a VCS like Git.
* Again: it's no different from the usual way of working.

---

![bg height: 20%](Attachments/index%202024-05-12%2019.23.25.excalidraw.light.svg)

---

Even external contributors can make changes...
* and request merging those back to the upstream model.

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

This can save teams **a lot** of work.

---

### Automated Tasks

---

Since LinkML models are simple YAML files, it's very easy to write scripts and programs that utilize them.
* CI/CD pipelines could be extended to perform these tasks on deployment.

---

![](Attachments/index%202024-05-12%2016.14.43.excalidraw.light.svg)

---

Governance rules can also be automated.

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

![bg width: 50%](Attachments/index%202024-05-12%2016.06.21.excalidraw.light.svg)

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
* linking data in data sets all across the web.

---

![](Attachments/index%202024-05-12%2016.42.35.excalidraw.light.svg)

---

Doesn't that look familiar?

---

Since we don't control all of these data sets, how do we link these points?
* As we saw earlier: names tend to be local and can mean different things.

---

The main enabler for Linked Data is the use of URIs for global identification.

---

![](Attachments/index%202024-05-12%2016.53.18.excalidraw.light.svg)

---
<!-- _class: with-bullets -->

URIs...
* can encode ownership in the domain;
* and can namespace identifiers.

---
<!-- _class: with-bullets -->

This solves our earlier problem with identification:
* If two things have the same URI, they are the same thing.
* Watch out though: two different URIs does not necessarily mean the things they refer to are different.
* Different data sets and organisations can use domains and namespaces to provide unique identifiers for everything.

---

By the way, I need to mention compact URIs (CURIEs).

---

![](Attachments/index%202024-05-12%2019.55.05.excalidraw)

---

<!-- TODO: Image? Perhaps a variant on the first one with the identical/different edges, but then the fixed version? -->

\*\*\*

---

### Referencing CIM in LinkML

---

Within the CIM community URIs have been crafted for the CIM.

---

This means every data element in the CIM can be uniquely referenced by its URI.

---

We saw a real life example earlier: `https://cim.ucaiug.io/ns#PowerSystemResource`

---

<!-- TODO: Abrupt... -->

LinkML supports annotating schema elements with names from reference models...
* like the CIM!

---

Note in particular how easy it is to use multiple reference models.
* This provides immense flexibility and ease of standardization.
* It's usually very difficult to do.

---

Let's take a look again at the LinkML schema earlier...
* this time with CIM references

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

* (`cim:ACDCConverterDCTerminal` is a CURIE, a shorthand for writing URIs)

---

Using fields like  `class_uri` and `slot_uri` we can standardize schema elements by annotating them with reference model names

---

### Profiling CGMES and the CIM

---

Mapping names to reference models is great
* but sometimes we could use more help

---

Reference models often have more to offer than just standardized names

---

The CIM describes attributes, relations, andsoforth
* The CIM-based CGMES profiles provide use-case specific constraints

---

It would be nice if we could profile these to get our data products started

---

![](Attachments/index%202024-05-12%2020.13.34.excalidraw)

---

That would indeed be nice, but how can we do that if CIM and CGMES aren't LinkML?

---

No problem, we'll just generate them!

---

#### The CGMES LinkML Schemas

---

I've written a script that has generated a LinkML schema for each CGMES profile
* It is based on the RDFS 2020 version

---

- The [script](https://github.com/alliander-opensource/cimrdfs2linkml) that generates the LinkML schemas
- The [LinkML schemas](https://github.com/alliander-opensource/cgmes-profiles)
- The automatically generated [documenation](https://alliander-opensource.github.io/cgmes-profiles/)

---

#### The CIM LinkML Schemas

---

Similarly, I've generated LinkML schemas for the entire CIM
* It is based on the Sparx EA project

---

- The [script](https://github.com/bartkl/cim-to-linkml) that generates the LinkML schemas
- The [LinkML schemas](https://github.com/alliander-opensource/cim-linkml)
* I haven't generated the documentation yet

---

#### LinkML Profiler

---

Ritger Teunissen has developed a MVP [profiler](https://github.com/ritger-alliander/gen-linkml-profile) for LinkML schemas
* Currently command-line only

---

Given a CIM or CGMES LinkML schema, you pass in the classes you'd like to use, and it will create a LinkML schema for you

---

It also enables flattening class hierarchies, skipping optional fields, and more

---

## Road Ahead

---
<!-- _class: with-bullets -->

- Generating LinkML from EA
* Generating EA UML from LinkML
* Can we formalize the CIM URIs and solve the challenges with them?

dddd