---
title: "Mise a jour de modules Terraform"
groupByYear: false
date: 2025-03-09
description: "Projet d'automatisation de mise a jour de modules Terraform pour reduire la dette technique d'infrastructure."
summary: "Conception d'un script pour detecter et mettre a jour les versions de modules Terraform a grande echelle."
tags: ["terraform", "modules", "automation"]
categories: ["projet", "case-study"]
technos: ["terraform", "python", "api"]
series: ["Case Studies Cloud"]
keywords: ["terraform modules", "mise a jour module", "dette technique infra"]
showComments: true
showTableOfContents:
  article: true
draft: true
---
{{< lead >}}
Projet de mise à jour de modules terraform
{{< /lead >}}

{{< case-study
  contexte="Parc important de depots Terraform avec versions de modules heterogenes."
  probleme="La dette technique augmente quand les versions de modules ne sont pas maintenues."
  solution="Script automatisant la detection des modules et la proposition de versions plus recentes via API Terraform."
  impact="Reduction du travail manuel et standardisation des versions modules entre depots."
  stack="Terraform, API Terraform, scripting"
>}}

# Contexte

Dans un environnement où l'on manage beaucoup de dépots de code terraform utilisant des modules terraform, on peut vite se retrouver dans le cas où la dette technique augmente, a cause des versions de modules

# Solution

Le but est d'impléménter un script executable qui va permettre de mettre à jour les modules avec les derniere versions de terraform grace à l'api terraform

# Premiere implémentation

La première implémentation est basique, récupération des differents modules dans 

{{< related >}}