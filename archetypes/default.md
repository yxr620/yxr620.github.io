---
title: "{{ replace .Name "-" " " | title }}"
author: "yxr620"
toc:
  enable: true
  auto: true
date: {{ .Date }}
draft: false
weight: 3
---
{{ partial "mathjax.html" . }}
