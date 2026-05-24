**Résumé Exécutif**
Les meilleurs quick wins ne sont pas des créations de contenu larges, mais des optimisations de pages déjà visibles.  
Plusieurs pages ont une position moyenne 3-8 dans GSC avec 0 clic, donc le levier principal est le CTR SERP.  
`/diagnostic-automatisation-process/` et `/automatisation-taches-repetitives-pme/` combinent visibilité GSC et bon engagement GA.  
Les exports sont faibles en volume : les priorités ci-dessous sont des hypothèses d’action, pas des conclusions statistiques fortes.  
Aucun fichier n’a été modifié et aucune donnée live/MCP n’a été utilisée.

**Quick Wins Priorisés**

| Priorité | Donnée source | Diagnostic | Action recommandée | Page / requête | Impact | Effort |
|---:|---|---|---|---|---|---|
| 1 | `gsc-pages-28d.csv`: 11 impressions, 0 clic, position 5.18. `ga-landing-pages-28d.csv`: 2 sessions, 100% engagement, durée moy. 1728s. | Page déjà proche du haut de SERP, mais aucun clic. Quand elle est visitée, elle engage fortement. | Réécrire title/meta et accroche H1 autour de “diagnostic automatisation de processus PME”, bénéfice clair, livrable concret, CTA plus explicite dans le snippet. | `/diagnostic-automatisation-process/` | Élevé | Faible |
| 2 | `gsc-pages-28d.csv`: 8 impressions, 0 clic, position 7.63. `ga-landing-pages-28d.csv`: 3 sessions, 100% engagement, durée moy. 1459s. | Même profil : faible volume, mais page pertinente une fois ouverte. CTR à améliorer. | Renforcer le snippet avec “automatiser les tâches répétitives en PME”, exemples de tâches, promesse de cadrage avant outil. Garder le mot-clé exact dans title + intro. | `/automatisation-taches-repetitives-pme/` | Élevé | Faible |
| 3 | `gsc-pages-28d.csv`: `/contact/` 7 impressions, 0 clic, position 3.71. `ga-organic-landing-pages-28d.csv`: 1 session organique, engagée. | Page haute intention en bonne position, mais le résultat ne déclenche pas le clic. | Rendre title/meta plus explicites : “Contact consultant automatisation IA PME” ou “Réserver un échange automatisation / IA”. Le snippet doit dire quoi se passe après le clic. | `/contact/` | Moyen à élevé | Faible |
| 4 | `gsc-pages-28d.csv`: `/accompagnements/` 8 impressions, 0 clic, position 4.25. `ga-pages-28d.csv`: seulement 2 vues sur `/accompagnements`. | Page visible mais trop générique pour attirer un clic. | Transformer le positionnement SERP de “Accompagnements” vers “Accompagnement automatisation, IA et outils sur mesure pour PME”, avec un bloc de choix rapide entre diagnostic, mission, formation, chefferie, développement. | `/accompagnements/` | Moyen | Faible |
| 5 | `gsc-queries-28d.csv`: “chefferie de projet”, 12 impressions, 0 clic, position 67.75. `gsc-pages-28d.csv`: `/chefferie-de-projet/` 17 impressions, position 49.41. | Google associe la page à la requête, mais la pertinence est trop faible pour ranker. | Ne pas viser “chefferie de projet” générique seul. Repositionner en “chefferie de projet technique / automatisation / PME”, ajouter cas d’usage et vocabulaire métier dans title, H1, sous-titres. | `/chefferie-de-projet/`, requête “chefferie de projet” | Moyen | Moyen |
| 6 | `gsc-pages-28d.csv`: `/mission-ciblee/` 9 impressions pos. 7.11, `/developpement-sur-mesure/` 4 impressions pos. 3.75, `/formation/` 4 impressions pos. 6.5, tous 0 clic. | Les pages d’offre courtes ont de bonnes positions moyennes mais aucun clic. | Mettre à jour les métadonnées dans `src/data/accompagnement-pages.ts` avec une formule plus descriptive par page : cible PME, problème traité, résultat attendu. | Pages d’accompagnement | Moyen | Faible |
| 7 | `gsc-sitemaps.csv`: 15 URLs soumises, 0 indexées, 0 erreur, 0 warning sur les deux sitemaps. | Signal de sitemap non contributif ou non encore consolidé côté GSC. Les pages peuvent apparaître, mais le sitemap n’aide pas visiblement. | Ajouter une vérification repo/build : sitemap généré, URLs canoniques attendues, pas d’URL redirigée comme `/regie-ciblee/`, cohérence trailing slash. | Sitemap global | Moyen | Faible à moyen |
| 8 | `ga-pages-28d.csv`: variantes slash séparées, ex. `/a-propos` 7 vues vs `/a-propos/` 4 vues, `/ia-workflow-developpement` 1 vs `/ia-workflow-developpement/` 17. | Les chemins avec/sans slash brouillent la lecture GA et peuvent signaler une hygiène canonique à vérifier. | Uniformiser les liens internes et redirects vers la version canonique avec slash final, puis vérifier que sitemap/canonical/OG utilisent la même forme. | `/a-propos/`, `/ia-workflow-developpement/`, mentions légales | Moyen | Faible |
| 9 | `gsc-page-query-28d.csv`: `/ia-generative-pme-process/` ressort sur “chatbot ia personnalisé pme” pos. 37 et “tendances adoption ia générative outils entreprise” pos. 10. `ga-organic-landing-pages-28d.csv`: 1 session organique, 0 engagement. | La page capte des intentions IA, mais la correspondance semble floue. | Ajouter ou clarifier une section dédiée “chatbot IA personnalisé pour PME” seulement si c’est une offre réelle ; sinon recentrer la page sur cadrage d’usages IA PME et éviter la dispersion. | `/ia-generative-pme-process/` | Faible à moyen | Moyen |

**À Implémenter En Premier**
Commencer par `/diagnostic-automatisation-process/` dans `src/pages/diagnostic-automatisation-process.astro` : optimiser title, meta description, H1/intro et, si cohérent, la donnée structurée associée dans `src/data/structuredData.ts`.

Raison : c’est le meilleur ratio impact/effort dans les exports : position moyenne 5.18, 11 impressions, 0 clic, et très fort engagement GA une fois la page visitée.

**Limites**
Période courte : 2026-04-24 au 2026-05-21, avec volumes très faibles.  
GSC masque probablement des requêtes : seulement 4 requêtes exportées contre 98 impressions page.  
Aucune conversion GA4 exploitable : `ga-conversions-28d.csv` vide et `keyEvents=0` partout.  
`landingPagePlusQueryString=(not set)` représente 4 sessions dont 2 organiques, donc une partie de l’attribution est inutilisable.  
Les positions GSC sont des moyennes pondérées, pas des rankings fixes.

**Commandes Exécutées**
Lecture/inventaire des exports, inspection README, agrégations CSV avec `python3`, recherches repo avec `rg`, lectures ciblées de `src/pages`, `src/layouts`, `src/data`, `astro.config.mjs`, `public/robots.txt` et `public/_redirects`. Les checks orchestrateur d’initialisation ont signalé des manifests manquants, sans impact sur cette analyse en lecture seule.