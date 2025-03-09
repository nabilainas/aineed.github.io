---
title: "kubernetes avancé"
groupByYear: false
date: 2025-03-09
showComments: True
showTableOfContents:
  article: True
draft: true
---
{{< lead >}}
Projet de mise à jour de modules terraform
{{< /lead >}}

# Contexte

Dans un environnement où l'on manage beaucoup de dépots de code terraform utilisant des modules terraform, on peut vite se retrouver dans le cas où la dette technique augmente, a cause des versions de modules

# Solution

Le but est d'impléménter un script executable qui va permettre de mettre à jour les modules avec les derniere versions de terraform grace à l'api terraform

# Premiere implémentation

La première implémentation est basique, récupération des differents modules dans 