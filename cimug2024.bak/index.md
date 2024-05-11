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

![](Attachments/index%202024-05-08%2015.10.39.excalidraw)

---

Teams need to describe the meaning of their data

---

![](Attachments/index%202024-05-08%2015.18.26.excalidraw)

---

The CIM is a great information model to align semantics with
* how can we enable teams to do this?

---

## Modeling Data Products

---

What is required of how we model?

---

Decentralization entails
* 

* Demands from decentralization
* Demands from teams
* Demands 



### Sparx EA

---

The CIM is mainained in Sparx EA
* Is it suitable for teams modeling data products?

---

IMG: CIM -> profile in EA

---

#### Challenges

---

BizDevOps teams do not like (applications like) EA
* but they are the ones responsible for the modeling

---

EA is heavy and has a complex UI
* and code-based models and own tools are prefered

---

UML is not trivial to learn
* neither very thrilling to most

---

UML is not suited for decentralized contexts
* lacking identifiers that are unique globally (worldwide)

---

Models are hard to use outside of the EA application
* XMI serializations are hard to use and understand
* Artifact generation is tedious
* CI/CD automation is tedious

---

Collaboration and version control is hard
* especially compared to workflows involving code and Git

---

And then there's:

* Licensing costs
* Difficulty of migrating to another tool
* Non-Windows users who need to use the SaaS

---

Can't we do better?


<!--

We have to choose:

1. Modeling language(s)
2. Technology/tools

---

1. Decentralized architecture asks for
    1. Globally unique identifiers
    2. Easy to integrate shape (e.g. graph)
2. Working bottom up means
    1. Teams should be met where they're at
        1. Code-based models
        2. Familiar tools (IDEs and such)
        3. VCS and CI/CD

-->

---

![](Attachments/index%202024-05-08%2016.45.38.excalidraw)

---

If the information model is machine readable, however...


---

![](Attachments/index%202024-05-08%2021.32.24.excalidraw)

---


---

### Linked Data

---

We clearly need


