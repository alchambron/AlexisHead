
# Music Detective

# Introduction

L'application “Music Detective” est une plateforme de jeu musical inspiré des blindtest. 

L’utilisateur peut choisir un thème de son choix et deviner les différents titres et auteurs des musiques.

Plusieurs modes de jeux seront disponibles, comme un mode par niveau en secondes, un mode de rapidité, un mode difficile sur des thèmes spécifiques.

Un aspect communautaire sera aussi disponible, avec l'optionnel possibilité de se créer un compte et d'échanger ses statistiques dans un classement en ligne. 


# Fonctionnalités

## Général

- Les utilisateurs peuvent potentiellement créer un compte et se connecter pour jouer.
- Les parties de blindtest sont constituées à partir de musique issus de playlist spécifique par thèmes
- Les joueurs doivent répondre rapidement pour gagner des points, avec un système de score en temps réel.
- Les utilisateurs peuvent choisir le genre musical et la fourchette d'années pour les musiques.
- Les joueurs peuvent choisir parmi différents modes de jeux.

## Création de playlist

Les utilisateurs pourront créer leurs propres playlists de musique sur Youtube en fonction de leurs goûts musicaux et y jouer avec notre site. 


## Fonctionnalités sociales

Les utilisateurs pourront interagir avec d'autres joueurs via des fonctionnalités sociales telles que des likes de playlist, et des partages de leurs playlists Youtube personnelle.

## Fonctionnalité d'apprentissage (optionnelle)

(Fonctionnalité optionnel, à conceptualisé).
Les utilisateurs pourront apprendre des faits intéressants sur les artistes et les chansons pendant qu'ils jouent. Cette fonctionnalité fournira des informations sur les artistes, les albums et les chansons, permettant ainsi aux utilisateurs d'approfondir leur connaissance de la musique.


# Objectifs

Le but de l'application est de divertir les amateurs de musiques qui cherchent à tester leurs connaissances. Le jeu est conçu pour être amusant, compétitif, avec une expérience de jeu rapide et facile à comprendre.


# Organisation technique

## Structure
![Imgur](https://i.imgur.com/xyg5H8E.png))
![](https://music-detective.s3.eu-west-1.amazonaws.com/prototype-technique.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEFcaCWV1LXdlc3QtMyJIMEYCIQDu%2BEQ9GBDtcWNNKb8BGOvFiQu2nyOQwXQ0xD34ayrQuwIhAOBVfLeAaGt9MSOYUz49mVoyvIqfEElLD3cPlQxtFQhSKu0CCPD%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNDIwMzMxOTgxODg2IgwQzpLw%2BxQ8RdTy7mIqwQJgQxaGi1rehZVRLlF0EDsADRUcaGG8otfJP9Vcbjfk0TS9ujAJtnpvIBxELhY%2FXYRa2ciek54Yweh1Z%2FvR8ECPdsbG45EJJL9PVO%2Bzm8XmmFVe9GaywqlpANyK05Hdjrrgt4tOZHiQndAy7%2BNgSHEwYnwdiaYur9u9O%2FVTHUJQXaVsHqXP34LIsOTGsg1JOY4Lu8hFdNVKXB4OoWNr7UkgrOo0fGpZW1Pc6dlatz%2B0FIPi9XEDNkJmZ2uZTs9KbP8vnnl%2FlmpKPmLWkmaTD92HHNbURy5ZFuVJyMuAHcAGp3wjFVhiDduJMgbwe2ittx5FlaP5pCPSGzIJJKcCX%2BhvPd3AjYjm29MZh%2FI8xm%2FGm8PWty7Vfx0S%2Bn1XJSRvXu97OyoggkoEQmDNTyyVW5tbVbcQJ2eyF8G%2FKjejJx7kN3swy4TenwY6sgLETWf8JgxEWVEMzrq2Kh88r7NF0KpdXrZCUC3PIyCVtw0Z5xU4EmUkBodmohVBU2Q1u4Nfh41McFxV6fR%2FNcgotrMcaC5ILLl4FjHUd1dUGxN1L%2BVqWa67qhU2ogqFuMIRLnJuZBT34VlC%2B2w7aeHQL%2FXsJDSRngqS0ySdS0NuSs%2B1%2FbJf7u5Ph0bINyrDWYnYlyqhO4qRCjWv13%2FGeeDyb5rrIMPs06ucGEsXtMMlniJZyEpquwNTdJTeNNwGAUG8wrkO9Ly%2F9s0xs6mMcPm%2FAWGuiPDVO77mKTvotiCJXQ1IEkj3s7Mmk0Kdl8bGfkm%2FV%2FQrHmJv29Si56BY8Svew1JBOoNrWoFs%2BaOAxWJOqbQ9ifImxWh2ta6sxhLEhaHg386ovZKA%2BMV0%2Favm4tXP1fI%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20230223T154744Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAWDXN5BQ7HQMIUC2B%2F20230223%2Feu-west-1%2Fs3%2Faws4_request&X-Amz-Signature=4725992154741f1fcefc60f5378f61a3cd4ee40b3ba234f94ca2cc4c0c878cbe)
![](https://music-detective.s3.eu-west-1.amazonaws.com/prototype-technique.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEFcaCWV1LXdlc3QtMyJIMEYCIQDu%2BEQ9GBDtcWNNKb8BGOvFiQu2nyOQwXQ0xD34ayrQuwIhAOBVfLeAaGt9MSOYUz49mVoyvIqfEElLD3cPlQxtFQhSKu0CCPD%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNDIwMzMxOTgxODg2IgwQzpLw%2BxQ8RdTy7mIqwQJgQxaGi1rehZVRLlF0EDsADRUcaGG8otfJP9Vcbjfk0TS9ujAJtnpvIBxELhY%2FXYRa2ciek54Yweh1Z%2FvR8ECPdsbG45EJJL9PVO%2Bzm8XmmFVe9GaywqlpANyK05Hdjrrgt4tOZHiQndAy7%2BNgSHEwYnwdiaYur9u9O%2FVTHUJQXaVsHqXP34LIsOTGsg1JOY4Lu8hFdNVKXB4OoWNr7UkgrOo0fGpZW1Pc6dlatz%2B0FIPi9XEDNkJmZ2uZTs9KbP8vnnl%2FlmpKPmLWkmaTD92HHNbURy5ZFuVJyMuAHcAGp3wjFVhiDduJMgbwe2ittx5FlaP5pCPSGzIJJKcCX%2BhvPd3AjYjm29MZh%2FI8xm%2FGm8PWty7Vfx0S%2Bn1XJSRvXu97OyoggkoEQmDNTyyVW5tbVbcQJ2eyF8G%2FKjejJx7kN3swy4TenwY6sgLETWf8JgxEWVEMzrq2Kh88r7NF0KpdXrZCUC3PIyCVtw0Z5xU4EmUkBodmohVBU2Q1u4Nfh41McFxV6fR%2FNcgotrMcaC5ILLl4FjHUd1dUGxN1L%2BVqWa67qhU2ogqFuMIRLnJuZBT34VlC%2B2w7aeHQL%2FXsJDSRngqS0ySdS0NuSs%2B1%2FbJf7u5Ph0bINyrDWYnYlyqhO4qRCjWv13%2FGeeDyb5rrIMPs06ucGEsXtMMlniJZyEpquwNTdJTeNNwGAUG8wrkO9Ly%2F9s0xs6mMcPm%2FAWGuiPDVO77mKTvotiCJXQ1IEkj3s7Mmk0Kdl8bGfkm%2FV%2FQrHmJv29Si56BY8Svew1JBOoNrWoFs%2BaOAxWJOqbQ9ifImxWh2ta6sxhLEhaHg386ovZKA%2BMV0%2Favm4tXP1fI%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20230223T154744Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAWDXN5BQ7HQMIUC2B%2F20230223%2Feu-west-1%2Fs3%2Faws4_request&X-Amz-Signature=4725992154741f1fcefc60f5378f61a3cd4ee40b3ba234f94ca2cc4c0c878cbe)

Concept technique de la structure de detection de notre projet.
![](https://music-detective.s3.eu-west-1.amazonaws.com/prototype-technique.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEFcaCWV1LXdlc3QtMyJIMEYCIQDu%2BEQ9GBDtcWNNKb8BGOvFiQu2nyOQwXQ0xD34ayrQuwIhAOBVfLeAaGt9MSOYUz49mVoyvIqfEElLD3cPlQxtFQhSKu0CCPD%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNDIwMzMxOTgxODg2IgwQzpLw%2BxQ8RdTy7mIqwQJgQxaGi1rehZVRLlF0EDsADRUcaGG8otfJP9Vcbjfk0TS9ujAJtnpvIBxELhY%2FXYRa2ciek54Yweh1Z%2FvR8ECPdsbG45EJJL9PVO%2Bzm8XmmFVe9GaywqlpANyK05Hdjrrgt4tOZHiQndAy7%2BNgSHEwYnwdiaYur9u9O%2FVTHUJQXaVsHqXP34LIsOTGsg1JOY4Lu8hFdNVKXB4OoWNr7UkgrOo0fGpZW1Pc6dlatz%2B0FIPi9XEDNkJmZ2uZTs9KbP8vnnl%2FlmpKPmLWkmaTD92HHNbURy5ZFuVJyMuAHcAGp3wjFVhiDduJMgbwe2ittx5FlaP5pCPSGzIJJKcCX%2BhvPd3AjYjm29MZh%2FI8xm%2FGm8PWty7Vfx0S%2Bn1XJSRvXu97OyoggkoEQmDNTyyVW5tbVbcQJ2eyF8G%2FKjejJx7kN3swy4TenwY6sgLETWf8JgxEWVEMzrq2Kh88r7NF0KpdXrZCUC3PIyCVtw0Z5xU4EmUkBodmohVBU2Q1u4Nfh41McFxV6fR%2FNcgotrMcaC5ILLl4FjHUd1dUGxN1L%2BVqWa67qhU2ogqFuMIRLnJuZBT34VlC%2B2w7aeHQL%2FXsJDSRngqS0ySdS0NuSs%2B1%2FbJf7u5Ph0bINyrDWYnYlyqhO4qRCjWv13%2FGeeDyb5rrIMPs06ucGEsXtMMlniJZyEpquwNTdJTeNNwGAUG8wrkO9Ly%2F9s0xs6mMcPm%2FAWGuiPDVO77mKTvotiCJXQ1IEkj3s7Mmk0Kdl8bGfkm%2FV%2FQrHmJv29Si56BY8Svew1JBOoNrWoFs%2BaOAxWJOqbQ9ifImxWh2ta6sxhLEhaHg386ovZKA%2BMV0%2Favm4tXP1fI%3D&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20230223T152044Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAWDXN5BQ7HQMIUC2B%2F20230223%2Feu-west-1%2Fs3%2Faws4_request&X-Amz-Signature=79904de3fc54517aa1dd6c4f0e729e1c4986cc6eaed45629568dcebe9983d7f7)

- 1 - L'application affiche une liste de playlist disponible pour l'utilisateur
- 2 - Chargement d'une musique aléatoire de cette playlist
- 3 - Fetch du lien Youtube pour envoyer le son dans le player audio React (Librairie)
- 4 - Quand l'utilisateur fait une recherche une suggestion de titre est proposé par l'API de LastFM
- 5 - Passage dans un algorithme de comparaison de titre (entre le titre de la vidéo Youtube et le titre de Last FM)
- 6 - Si le score est bon, le score est pris en compte.

## Complexité technique

Limitation lié au quotas de l'API de Youtube, nous obligeans d'utiliser une autre API pour mettre en place un système de recherche dynamique. 

Création d'un algorithme intelligent cherchant à mettre en liaison les deux titres (Youtube et LastFM). 

## Stack Technique

Front : ReactJS / Redux 
Back : Ruby On Rails 
DataBase : PostGreSQL


## Listes des API utilisé 

- Youtube
- LastFM 
- Wikipedia ou Genius (pour des fonctionnalités optionnelles)





