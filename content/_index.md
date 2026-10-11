---
title: ""
type: landing

design:
  spacing: "4rem"

sections:
  - block: resume-biography-3
    content:
      username: admin
      text: ""
      button:
        text: Curriculum Vitae
        url: vitae/
    design:
      background:
        color: white
  - block: markdown
    content:
      title: Contact
      text: |-
        Professor of Economics  
        University of Southern Denmark  
        Campusvej 55, DK-5230 Odense  
        Tel: (+45) 24782033  
        Email: [barnebeck@sam.sdu.dk](mailto:barnebeck@sam.sdu.dk)
    design:
      columns: '1'
  - block: collection
    id: papers
    content:
      title: Recent Publications
      text: "[See all publications →](research/)"
      count: 5
      filters:
        folders:
          - publication
    design:
      view: citation
---
