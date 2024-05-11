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

### Agile Alliander

---

Alliander has been decentralizing
* The Agile way of working is more bottom-up

---

Autonomous BizDevOps teams can move faster
* but there is (some) loss of control

---

To manage and govern our data, architectural changes are needed

---

### Data Mesh

---

<!-- IMG: Four core principles -->

---

To give an idea of the mesh...

---

<!-- IMG: Mesh -->

---

### Data Products

---

<!-- IMG: Producer -> dataset -> consumer -->

---

Note that teams are now responsible for describing what their data means

---

## Modeling Data Products with LinkML

---

LinkML is a data modeling language developed in the Bio Sciences department at Berkeley Lab
* LinkML is also a tool, with a growing ecosystem surrounding it

---
### The LinkML Modeling Language

---

LinkML is accessible, especially to developers
* Familiar YAML syntax
* Easy and familiar semantics
<!-- Mention: classes, types, inheritance, mixins, properties -->

---

Here's a small example of a LinkML schema

---

```yaml
classes:
  ACDCConverterDCTerminal:
    class_uri: cim:ACDCConverterDCTerminal
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
        slot_uri: cim:ACDCConverterDCTerminal.polarity
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
        slot_uri: cim:ACDCConverterDCTerminal.DCConductingEquipment
        range: ACDCConverter
        required: true
        multivalued: false
        description: A DC converter terminal belong to an DC converter.
```

---

Models as YAML files fits right in with the way of working of BizDevOps teams
* they work with YAML configuration files all the time!

---

LinkML schemas become part of the repository like all other code

---

Collaboration and versioning is done no differently using a VCS like Git

---

People can use their own IDEs, text editors or GUIs for maintaining the model
* people love to work with their own tools
* and vendor lock-in can be very costly on the long run

---

### Code and Documentation Generators

---

LinkML also offers a variety of generators you can use to generate code, documentation or other artefacts

---

Currently supported generators include
* Python
* SQL DDL
* HTML documentation
* Excel
* JSON Schema

---

As well as generators for Semantic Web space languages
* SHACL
* ShEx
* OWL
* JSON-LD context

---

If you're missing something, you can easily write your own or modify existing generators
* long live open source

---

Code and documentation can be generated automatically in CI/CD with little effort

---

Hopefully you agree that this seems to be a great means of enabling BizDevOps team to do data modeling
* but...

---

- Weren't we supposed to deal with decentralized architecture and describing our data?
* Where's the CIM in this picture, or information modeling at all for that matter?

---

### Bringing in the CIM

---

The obvious way isto just name things like CIM
* but...

---

- Different schemas have different naming conventions and restrictions
- Even if someone has the exact CIM name, it's unclear whether the same version is intended

---

We need more sophisticated means of naming and identification

---

#### Linked Data

---

Tim Berners-Lee envisioned a machine readable counterpart to the The World Wide Web
* The Semantic Web

---

Part of that is the idea of *Linked Data*
* linking data in data sets across the web

---

To improve the linking of data, Berners-Lee came up with four rules for Linked Data
1. Use URIs as names for things
2. Use HTTP URIs so that people can look up those names.
3. When someone looks up a URI, provide useful information.
4. Include links to other URIs. so that they can discover more things.

---

URIs are global identifiers for things
* so pointing to a URI suffices to identify something

---

<!-- TODO: Emphasize the power here.

- we can describe data models freely
- and (gradually) standardize with CIM (and other reference models)

-->

---

#### CIM and Linked Data

---

Within the CIM community URIs have been minted for the CIM

---

This means every data element in the CIM can be uniquely referenced by its URI

---

#### Referencing CIM in LinkML

---

As we've seen, LinkML supports annotating LD URIs
* This can be used to map to reference models

---

The language supports annotating schema elements with names from reference models
* like the CIM!

---

Let's take a look again at the LinkML schema earlier
* for brevity I'll leave descriptions out

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

Using fields like  `class_uri` and `slot_uri` we can standardize schema elements by annotating them with reference model names

---

But what are these URIs, and what is this funny notation?


### CIM-based Data Products

#### CGMES and CIM in LinkML

#### CLI Profiler

#### 