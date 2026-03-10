---
title: "J'ai entraine une IA sur mon Mac en 10 minutes"
groupByYear: false
date: 2026-03-10
description: "Crash test installation et fine-tuning d'un LLM en local."
summary: "Un test rapide de fine-tuning local avec TinyLlama sur Mac M2: setup, commande, resultat."
tags: ["fine-tuning", "mlx", "IA"]
categories: ["architecture"]
technos: ["python"]
series: ["IA locale"]
keywords: ["fine-tuning local", "MLX-LM", "Mac M2", "TinyLlama", "LoRA"]
showComments: true
showTableOfContents:
  article: true
draft: true
---
{{< lead >}}
Un premier fine-tuning local d'un LLM sur Mac M2 avec MLX-LM, sans cloud ni GPU dedie.
{{< /lead >}}

Avec la montée en puissance des IA "agent" j'ai fais quelques recherches, avec l'arrivée d'openclaw, des skills etc L'utilisation à un coût énorme, environ 200€ par mois pour chaque agent (sans compter l'hebergement de cet agent qui coute généralement une blinde avec l'achat d'un mac mini (1200€)) Au dela du fait que c'est incroyablement efficace, ce n'est pas ouvert à tous surtout les etreprise qui on l'envie de mettre en place le même systeme tout en gardant une main sur la souveraineter des données. Pour cela je viens de tester, **j'ai entraine un modele d'intelligence artificielle sur mon mac**, sans serveur, sans cloud, sans carte graphique dediee. Juste mon M2 et un cafe (non j'ai pas pris de café claude...).

Voici comment ca s'est passé.

## Pour ceux qui vivent dans une grotte, c'est quoi un LLM?

LLM = **Large Language Model**.

Concretement, c'est un programme qui a lu une quantite astronomique de texte (des milliards de pages web, livres, articles...) et qui a appris a **predire quel mot vient apres un autre**. C'est tout. Mais a tres grande echelle, ce mecanisme simple produit quelque chose d'etonnamment puissant: une machine capable de rediger, repondre, resumer, traduire.

ChatGPT, Claude, Mistral... ce sont tous des LLMs.

> Analogie simple: imagine quelqu'un qui a tellement lu de romans qu'il peut continuer n'importe quelle phrase dans le style de n'importe quel auteur. C'est exactement ça, un LLM. (bien trouvé ça !)

## Et le fine-tuning dans tout ca?

Les LLMs de base sont tres géneralistes. Le **fine-tuning** (ou "affinage" en francais), c'est le fait de **réentrainer  un modele existant** sur nos propres donnees, pour qu'il adopte un style, un ton, ou une expertise particuliere, par exemple lui donner tous les secrets de sa boite pour qu'il se comporte comme un salarié.

C'est la difference entre:
- Un cuisinier qui sait tout faire *(modele de base)*
- Un cuisinier specialise dans la cuisine lyonnaise *(modele fine-tune)*

Tu ne repars pas de zero: tu affines ce qui existe deja. C'est beaucoup plus rapide et accessible.

## Ce que j'ai fait aujourd'hui

### Mon setup

- MacBook avec puce **Apple M2**, 16 GB de RAM
- Python + la librairie **MLX-LM** d'Apple
- Un set de données de 8 lignes (un grain de sable sur une plage, inutile, c'est pour l'exemple, vous allez comprendre)

### Le modele choisi: TinyLlama 1.1B

Pour ce premier test, j'ai volontairement choisi le plus petit modele disponible: **TinyLlama**, qui ne pese que 1,1 milliard de parametres (contre 70 milliards pour les grands modeles). L'ideal pour tester sans attendre des heures.

### Les donnees d'entrainement

J'ai cree un mini dataset en **JSONL**: un format ou chaque ligne est un exemple:

Le format JSONL est la norme pour l'entrainement des données, en effet cela permet de :

- **Lecture ligne par ligne** → pas besoin de charger tout le fichier en RAM
- **Facile à agrandir** → tu ajoutes juste une ligne
- **Standard pour l'IA** → Hugging Face, OpenAI, MLX utilisent tous ce format


```json
{"prompt": "Decris la mer", "completion": "Les vagues murmurent des secrets anciens..."}
{"prompt": "Decris une foret", "completion": "Les arbres centenaires veillent en silence..."}
```

Seulement 5 exemples, dans un style poetique et descriptif. Le but: voir si le modele peut adopter ce ton.

## Le setup

Vous pouvez check au niveau de mon git : lien

on créer un dossier
on lance le script pour créer un env et telecharger les packages

on est bon

### La commande magique

```bash
mlx_lm.lora \
  --model TinyLlama/TinyLlama-1.1B-Chat-v1.0 \
  --train \
  --data ./data \
  --iters 50 \
  --batch-size 2 \
  --num-layers 4 \
  --adapter-path ./adapters
```
Je me suis pas assez renseigner sur les arguments qui sont passées, peut etre un deep dive sur un prochain post !
Et voila. **Quelques minutes plus tard**, le modele avait appris de mes exemples.

![lora](./assets/lora.png)

Lecture simple du screen:

- `Loading pretrained model` / `Downloading complete`: le modele de base est telecharge puis charge en memoire.
- `Training iterations: 50`: l'entrainement fera 50 passages.
- `Iter 10`, `Iter 20`, ...: ce sont les etapes de progression.
- `Train loss` qui baisse: le modele apprend correctement a reproduire ton style.
- `Val loss`: controle rapide sur des donnees de validation pour verifier que ca reste coherent.
- `Peak mem 2.474 GB`: memoire max utilisee pendant l'entrainement.
- `Saved final weights ...safetensors`: les poids LoRA finaux ont bien ete sauvegardes.

En gros: l'entrainement s'est bien passe, sans erreur, et les adaptateurs sont prets a etre reutilises.

### Le resultat


En lui demandant de "decrire un coucher de soleil" - un sujet qu'il avait connaissance dans le dataset - il a genere une reponse parfaite dans le style poetique que je lui avais enseigne.

![coucher_soleil](./assets/coucher_soleil.png)

Maintenant si j'essaye de m'eloigner un peu en lui demandant "Décris un désert", il va me renvoyer quelque chose de faux mais qui se rapproche du style poetique mis en place dans les exemples, (il va juste renvoyer un truc au hasard de mon dataset)

![desert](./assets/desert.png)

Hors sujet : j'ai voulu me moquer de lui en lui posant une question "compliquée" il m'a mis une clim instant:

![fibo](./assets/fibonnacci.png)



Après coup, c'est plutôt logique qu'il réponde bon, car comme vous le savez moins on donne de contexte et on laisse le choix à l'IA plus les réponses sont vagues (d'où l'importance du "prompt engineering", qui se ressent moins sur les gros LLM), exemple 😂:

![horssujet](./assets/horssujet.png)

![dumb](./assets/dumb.png)

## Pourquoi c'est cool?

- **100% local**: mes donnees ne quittent jamais mon Mac (ultra important)
- **Gratuit**: pas d'abonnement, pas d'API payante (tres important)
- **Accessible**: pas besoin d'un doctorat en machine learning (a prendre avec des pincettes)


## Ressources pour aller plus loin

- [MLX-LM sur GitHub](https://github.com/ml-explore/mlx-lm)
- [Hugging Face MLX Community](https://huggingface.co/mlx-community) - modeles prets pour Mac
- [Documentation MLX](https://ml-explore.github.io/mlx/build/html/index.html)

Tu as des questions ou tu veux tenter l'experience? Laisse un commentaire.

{{< related >}}