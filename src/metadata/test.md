---
layout: ontology_detail
id: test
title: My Application Ontology
jobs:
  - id: https://travis-ci.org/materialdigital/app-ontology-template
    type: travis-ci
build:
  checkout: git clone https://github.com/materialdigital/app-ontology-template.git
  system: git
  path: "."
contact:
  email: 
  label: 
  github: 
description: My Application Ontology is an ontology...
domain: stuff
homepage: https://github.com/materialdigital/app-ontology-template
products:
  - id: test.owl
    name: "My Application Ontology main release in OWL format"
  - id: test.obo
    name: "My Application Ontology additional release in OBO format"
  - id: test.json
    name: "My Application Ontology additional release in OBOJSon format"
  - id: test/test-base.owl
    name: "My Application Ontology main release in OWL format"
  - id: test/test-base.obo
    name: "My Application Ontology additional release in OBO format"
  - id: test/test-base.json
    name: "My Application Ontology additional release in OBOJSon format"
dependencies:
- id: pmdco
tracker: https://github.com/materialdigital/app-ontology-template/issues
license:
  url: http://creativecommons.org/licenses/by/3.0/
  label: CC-BY
activity_status: active
---

Enter a detailed description of your ontology here. You can use arbitrary markdown and HTML.
You can also embed images too.

