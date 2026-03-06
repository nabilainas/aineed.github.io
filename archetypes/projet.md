---
title: "{{ replace .File.ContentBaseName "-" " " | title }}"
date: {{ .Date }}
draft: true
description: ""
summary: ""
tags: []
categories: ["projet"]
technos: []
series: []
keywords: []
showComments: false
showTableOfContents:
  article: true
project:
  contexte: ""
  probleme: ""
  solution: ""
  impact: ""
  repo: ""
---

{{< lead >}}
Description rapide du projet en une phrase.
{{< /lead >}}

{{< case-study
  contexte="Contexte du projet"
  probleme="Probleme principal a resoudre"
  solution="Choix techniques retenus"
  impact="Resultat mesurable (temps, cout, qualite)"
  stack="Kubernetes, Terraform, Azure"
  repo="https://github.com/owner/repo"
>}}

## Contexte

## Architecture

## Implementation

## Resultats

## Lecons apprises

{{< related >}}
