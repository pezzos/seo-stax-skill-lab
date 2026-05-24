# Rapport SEO quick wins - pezzoslabs.com

## Synthese courte

- Les volumes sont tres faibles : le rapport doit etre lu comme une liste d’hypotheses actionnables, pas comme une conclusion statistique robuste.
- Priorite immediate : corriger la mesure GA4, car `keyEvents=0` partout et `(not set)` capte 4 sessions sans page vue.
- Les meilleurs quick wins contenu sont les pages deja visibles en GSC, position moyenne 4-8, mais avec `0` clic : diagnostic, automatisation, accompagnements/offres.
- Rapport produit uniquement depuis `docs/seo-lab-data/`, sans MCP, sans live data, sans modification de fichier.

## Donnees utilisees

- Fenetre : 2026-04-24 au 2026-05-21 inclus ; export du 2026-05-22.
- Sources obligatoires : `README-data.md`, `gsc-queries-28d.csv`, `gsc-pages-28d.csv`, `ga-landing-pages-28d.csv`.
- Exports complementaires inspectes : `gsc-page-query-28d.csv`, `gsc-device-28d.csv`, `gsc-country-28d.csv`, `gsc-daily-28d.csv`, `gsc-search-appearance-28d.csv`, `gsc-sitemaps.csv`, `ga-organic-landing-pages-28d.csv`, `ga-pages-28d.csv`, `ga-acquisition-28d.csv`, `ga-events-28d.csv`, `ga-conversions-28d.csv`, `ga-device-28d.csv`, `ga-country-28d.csv`, `ga-daily-28d.csv`.
- Limites : faibles volumes, GSC masque certaines requetes, pas d’index coverage/Core Web Vitals/titres exportes, pas de ligne GSC/GA journaliere pour 2026-05-21.

## Quick wins prioritaires

| Priorite | Quick win | Preuve GA/GSC | Action concrete | Impact attendu | Effort | Validation prochaine |
| --- | --- | --- | --- | --- | --- | --- |
| P1 | Reparer la mesure conversion/landing | `ga-landing-pages-28d.csv`: `(not set)` = 4 sessions, 0 vues, 0 engagement ; `ga-events-28d.csv`: tous `keyEvents=0` ; `ga-conversions-28d.csv`: aucune ligne | Configurer les key events utiles SEO/contact et investiguer pourquoi des sessions arrivent en landing `(not set)` | Pouvoir prioriser les pages SEO sur contribution reelle, pas seulement engagement | M | Prochain export : `keyEvents > 0` si conversions reelles ; baisse de `(not set)` |
| P1 | Renforcer `/diagnostic-automatisation-process/` | `gsc-pages-28d.csv`: 11 impressions, 0 clic, position 5.1818 ; `ga-landing-pages-28d.csv`: 2 sessions, 2 engagees, duree 1728.325855 | Retravailler title/meta/H1 et intro autour du diagnostic d’automatisation ; ajouter liens internes depuis `/` et `/accompagnements/` | Page deja proche top 5 : hypothese de gain CTR | S | GSC page : clics > 0 ou CTR > 0 sur la page |
| P1 | Renforcer `/automatisation-taches-repetitives-pme/` | `gsc-pages-28d.csv`: 8 impressions, 0 clic, position 7.625 ; `ga-landing-pages-28d.csv`: 3 sessions, engagementRate 1, duree 1458.621615 | Clarifier le benefice PME dans title/meta et premier ecran ; ajouter un bloc cas d’usage et liens internes contextuels | Page engageante apres visite, mais snippet probablement peu incitatif | S | GSC page : CTR et clics ; GA organic landing : sessions engagees |
| P2 | Ameliorer les pages offres visibles sans clic | `gsc-pages-28d.csv`: `/accompagnements/` 8 impressions pos. 4.25 ; `/mission-ciblee/` 9 pos. 7.1111 ; `/developpement-sur-mesure/` 4 pos. 3.75 ; toutes 0 clic | Harmoniser les snippets offre : promesse concrete, cible PME, livrable, CTA ; renforcer les liens depuis la home | Transformer des positions deja visibles en premiers clics | M | GSC pages : CTR > 0 sur au moins une page offre |
| P2 | Aligner `/ia-generative-pme-process/` sur les requetes exportees | `gsc-pages-28d.csv`: 8 impressions, 0 clic, position 10.625 ; `gsc-page-query-28d.csv`: “chatbot ia personnalisé pme” pos. 37, “tendances adoption ia générative outils entreprise” pos. 10 ; `ga-organic-landing-pages-28d.csv`: 1 session google organic, 0 engagement | Ajouter sections explicites “chatbot IA personnalise PME” et “adoption IA generative en entreprise”, avec maillage depuis pages automatisation/diagnostic | Gagner pertinence longue traine et engagement organique | M | GSC page-query : impressions/clics sur ces requetes ; GA organic engagement > 0 |
| P2 | Verifier sitemap/canoniques avant nouvelle publication | `gsc-sitemaps.csv`: 15 submitted, 0 indexed, 0 errors pour `sitemap-0.xml` et `sitemap-index.xml` ; pourtant `gsc-pages-28d.csv` montre des impressions | Verifier que le sitemap liste les URL canoniques finales et que les variantes slash/non-slash ne dispersent pas les signaux | Reduire le risque de signaux techniques incoherents | M | Prochain export sitemap : indexed > 0 ou explication documentee |
| P3 | Repositionner `/chefferie-de-projet/` sur une intention plus specifique | `gsc-pages-28d.csv`: 17 impressions, 0 clic, position 49.4118 ; `gsc-page-query-28d.csv`: “chefferie de projet” 12 impressions, position 67.75 | Eviter de viser seulement la requete generique ; tester un angle plus qualifie type pilotage projet numerique/IA/PME | Gain moins immediat, car position trop basse | M | GSC page-query : position moyenne qui remonte sur requetes qualifiees |

## A surveiller, pas a faire tout de suite

- `/en/` : `ga-organic-landing-pages-28d.csv` montre 2 sessions google organic, 0 engagement, duree 0.580254 ; signal trop faible pour prioriser, mais a revoir si l’anglais devient strategique.
- Variantes slash : `ga-pages-28d.csv` separe `/a-propos` 7 vues et `/a-propos/` 4 vues, ainsi que `/ia-workflow-developpement/` 17 vues et `/ia-workflow-developpement` 1 vue. A verifier avec les canoniques/redirects avant action.
- `gsc-device-28d.csv` : mobile a 2 clics sur 9 impressions, desktop 0 clic sur 28 impressions. Volume trop faible pour conclure sur un probleme desktop.

## Non retenu

- Backlinks, Core Web Vitals, index coverage detaille, page titles reels et schema markup : non retenus comme quick wins, car absents des exports locaux.
- Recommandations editoriales generiques du type “publier plus de contenu” : non retenues sans page/requete GA ou GSC associee.

## Commandes et fichiers consultes

- `sed -n '1,240p' .agents/skills/seo-quick-wins/SKILL.md` : consignes de la skill.
- `find docs/seo-lab-data -maxdepth 1 -type f | sort` : inventaire du pack.
- `sed -n '1,220p' docs/seo-lab-data/README-data.md` : periode, sources, limites.
- `wc -l docs/seo-lab-data/*.csv` : controle de presence/volume des exports.
- Lectures `sed` des CSV GA/GSC listés ci-dessus, plus un script Python read-only pour trier les lignes GSC/GA par impressions et sessions.

Aucun fichier n’a ete modifie.