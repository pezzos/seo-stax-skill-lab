# Scoring Codex secondaire

Ce scoring ne vient pas de Claude. Il a ete lance dans une session Codex dediee par l'operateur avec le prompt de scoring aveugle.

## Classement final

1. C - 93/100
2. A - 92/100
3. D - 84/100
4. B - 83/100

## Scores detailles

| Rapport | GA/GSC /30 | Quick wins /25 | Priorisation /15 | Actionnable repo /15 | Limites /10 | Lisibilite /5 | Total |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| C | 28 | 23 | 14 | 14 | 9 | 5 | 93 |
| A | 29 | 23 | 14 | 12 | 10 | 4 | 92 |
| D | 28 | 18 | 10 | 14 | 9 | 5 | 84 |
| B | 27 | 19 | 11 | 11 | 10 | 5 | 83 |

## Forces / faiblesses

C : meilleur equilibre. Tres bonnes opportunites page/requete, bons liens GA/GSC, priorisation claire, et actions reliees au repo (`src/pages/...`, `src/data/accompagnement-pages.ts`, `src/data/structuredData.ts`). Faiblesse : quelques ajouts comme la donnee structuree ou "contact automatisation IA" depassent legerement les preuves exportees.

A : ancrage GA/GSC le plus propre, avec des metriques precises pour presque chaque recommandation. Tres bon traitement des limites. Faiblesse : moins directement exploitable cote repo que C, et une recommandation device/desktop un peu large vu le volume faible.

D : tres bon niveau de detail et d'implementation repo. Faiblesse majeure : il priorise la normalisation slash/no-slash avant les opportunites CTR page/requete les plus evidentes. Quelques recommandations reposent sur des signaux faibles, notamment les requetes IA a 1 impression.

B : clair, prudent, limites tres bien dites. Faiblesse majeure : la priorite #1 est la mesure GA4, utile pour l'analyse future mais pas une amelioration SEO directe. Moins fort que C/A sur les opportunites page/requete concretes.

## Meilleure recommandation exploitable

Optimiser `/diagnostic-automatisation-process/` : title, meta description, H1/intro et promesse de page.

Raison : position GSC autour de 5.18, 11 impressions, 0 clic, engagement GA tres fort (100%, duree moyenne autour de 1728s).

## Signaux generiques ou hallucines

- A : recommandation desktop/snippets un peu large ; mention finale de preflight "bloque" hors sujet pour un rapport SEO.
- B : "corriger GA4" est priorise comme quick win SEO alors que c'est surtout un quick win de mesure.
- C : mention de structured data et angle IA/contact pas entierement justifies par les exports.
- D : phrase de meta-process "structure pour pouvoir etre anonymise" ; priorite slash/no-slash peut surponderer un signal GA d'hygiene ; "37 impressions pages agregees" semble incoherent avec les autres metriques citees dans le rapport.

## Incertitudes

Le scoring a respecte la consigne de ne pas verifier les CSV source : jugement uniquement a partir des quatre rapports. A et C sont tres proches : A gagne sur la rigueur des preuves, C gagne sur l'utilite repo. C est classe devant A parce que l'objectif est l'utilite reelle pour ameliorer le SEO de pezzoslabs.com, pas seulement la qualite analytique.

Commandes declarees par la session de scoring : preflight compact repo, inventaire du dossier, `wc -l`, puis lectures `cat`/`sed` des quatre rapports uniquement.
