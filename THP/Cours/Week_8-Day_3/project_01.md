# Rails et composants : ranger les organismes dans des partials

Tu vas reprendre le projet Eventbrite puis ranger toutes les molécules dans des partials.

## 1\. Introduction

Dans ce projet, tu vas reprendre les molécules et organismes faits hier et les mettre dans ton application Eventbrite au format partials sous Rails.

C'est une journée très importante qui te permet de vraiment casser ton rapport old school du web qui nous fait penser un site page par page et non pas composant par composant. Ainsi, en voyant tes pages comme une succession de composants, ce sera bien plus aisé pour toi de construire des sites web. En plus de proposer des jolis sites, ce sera bien plus rapide de penser composants que de penser pages. Si tes composants sont déjà faits, tes pages ne seront plus que des `render partial` 🤑

## 2\. Le projet

Si tu n'as pas eu le temps de finir le projet Eventbrite, prends la correction d'un bon moussaillon. Idem pour les molécules et organismes demandés hier.

### 2.1\. Refacto la base

Avant toute chose, il faut brancher les bases :

- Le thème Bootswatch
- Le header, le footer (appelés dans le fichier `application.html.erb`)
- Les alertes (appelées dans le fichier `application.html.erb`)

### 2.2\. Refacto le reste

Reprends les molécules et organismes d'hier, puis mets-les tous dans des partials que tu appeleras dans les vues. L'objectif de cet exercice est de réduire au maximum le code html dans les views et de ne le mettre que dans les partials. S'il faut enlever des parties, n'hésite pas à le faire (#less_is_more).

L'objectif est de faire en sorte que 80% du code de chaque vue provienne de partials.

## 3\. Rendu attendu

Eventbrite avec 80% du code html dans des partials.