# Rapport SEO quick wins - pezzoslabs.com

## Perimetre et donnees
- Fenetre: 2026-04-24 au 2026-05-21 inclus, export du 2026-05-22, timezone Europe/Paris.
- Sources obligatoires utilisees: `README-data.md`, `gsc-queries-28d.csv`, `gsc-pages-28d.csv`, `ga-landing-pages-28d.csv`.
- Autres exports inspectes: `gsc-page-query-28d.csv` 5 lignes, `gsc-device-28d.csv` 2, `gsc-country-28d.csv` 6, `gsc-daily-28d.csv` 27, `gsc-search-appearance-28d.csv` 0, `gsc-sitemaps.csv` 2, `ga-pages-28d.csv` 13, `ga-organic-landing-pages-28d.csv` 9, `ga-device-28d.csv` 2, `ga-country-28d.csv` 1, `ga-acquisition-28d.csv` 3, `ga-events-28d.csv` 5, `ga-daily-28d.csv` 10, `ga-conversions-28d.csv` 0.
- Limites: analyse 100% offline depuis `docs/seo-lab-data/`; aucun MCP, aucune donnee live, aucun crawl. Volumes tres faibles; pas de ligne journaliere GA/GSC pour le 2026-05-21; conversions GA4 et search appearance GSC vides. Le rapport est structuré pour pouvoir etre anonymise ensuite en `report-A.md`, `report-B.md`, `report-C.md` ou `report-D.md`.

## Synthese priorisee
| Priorite | Quick win | Page / requete | Impact | Effort | Confiance | Preuve |
| --- | --- | --- | --- | --- | --- | --- |
| P1 | Normaliser les URLs internes vers la version canonique avec slash final | `/a-propos`, `/ia-workflow-developpement`, `/mentions-legales-confidentialite`, `/accompagnements` | Moyen | Faible | Moyenne | GA pages: `/a-propos` 7 vues vs `/a-propos/` 4, `/ia-workflow-developpement/` 17 vues vs sans slash 1; GSC pages liste les URLs avec slash final. |
| P2 | Renforcer le snippet de `/diagnostic-automatisation-process/` | Page diagnostic automatisation | Moyen | Faible | Moyenne | GSC pages: 11 impressions, 0 clic, CTR 0%, position 5.2; GA landing: 2 sessions, 100% engagement, 6 vues, duree moyenne 1728.3s. |
| P3 | Recrire title/meta de `/automatisation-taches-repetitives-pme/` autour de l’intention “taches repetitives PME” | Page automatisation PME | Moyen | Faible | Moyenne | GSC pages: 8 impressions, 0 clic, position 7.6; GA landing: 3 sessions, 100% engagement, 17 vues; GA organic: 1 session Google organic. |
| P4 | Ajouter un bloc cible sur “chatbot IA personnalise PME” et “adoption IA generative” | `/ia-generative-pme-process/` | Moyen | Moyen | Faible-moyenne | GSC page-query: `chatbot ia personnalisé pme` 1 impression position 37; `tendances adoption ia générative outils entreprise` 1 impression position 10; GSC page: 8 impressions, position 10.6; GA landing organic: 1 session, 0% engagement. |
| P5 | Repositionner `/mission-ciblee/` comme format d’execution lie a l’automatisation | Page mission ciblee | Faible-moyen | Faible | Faible | GSC pages: 9 impressions, 0 clic, position 7.1; pas de landing GA utile sur cette page. |
| P6 | Investiguer le signal sitemap “15 soumises, 0 indexee” | Sitemaps | Moyen | Faible | Moyenne | GSC sitemaps: `sitemap-0.xml` et `sitemap-index.xml`, 15 URL soumises, 0 indexee, 0 erreur, 0 warning; GSC pages montre pourtant 12 pages avec impressions. |

## Recommandations detaillees

### P1. Normaliser les liens internes vers les URLs canoniques avec slash final
- Action: aligner les liens internes et eventuels redirects sur les canonicals avec slash final.
- Pourquoi maintenant: GA separe plusieurs chemins avec et sans slash, ce qui dilue les lectures de performance.
- Donnees GA/GSC: `ga-pages-28d.csv`: `/a-propos` 7 vues et `/a-propos/` 4; `/ia-workflow-developpement/` 17 et `/ia-workflow-developpement` 1; `/mentions-legales-confidentialite` 1 et `/mentions-legales-confidentialite/` 1; `/accompagnements` 2. `gsc-pages-28d.csv` expose les pages avec slash final.
- Implementation: dans le repo, harmoniser les `href` vers `/page/` ou ajouter des redirects no-slash -> slash si la plateforme le permet. Les canonicals dans `PublicSiteLayout.astro` pointent deja vers le slash final.
- Verification apres mise en ligne: dans GA, verifier que les nouvelles vues se concentrent sur les chemins avec slash; dans GSC, surveiller les pages canoniques.
- Risque / limite: ne pas fusionner retrospectivement les lignes GA; le README interdit de supposer equivalence sans verification canonique/redirect.

### P2. Renforcer le snippet de `/diagnostic-automatisation-process/`
- Action: ajuster title/meta et l’introduction pour rendre explicite “diagnostic automatisation process PME”.
- Pourquoi maintenant: la page est deja proche du haut de page Google mais ne capte aucun clic dans l’export.
- Donnees GA/GSC: `gsc-pages-28d.csv`: 11 impressions, 0 clic, CTR 0%, position 5.2. `ga-landing-pages-28d.csv`: 2 sessions, 2 sessions engagees, 100% engagement, 6 vues, duree moyenne 1728.3s.
- Implementation: tester un title du type “Diagnostic automatisation process PME | Pezzos Labs” et une meta orientee resultat: clarifier les frictions, choisir quoi automatiser, eviter les mauvais chantiers.
- Verification apres mise en ligne: comparer CTR GSC page sur 28 jours et surveiller que la position ne recule pas.
- Risque / limite: faible volume; conclure seulement apres accumulation d’impressions.

### P3. Recrire le snippet de `/automatisation-taches-repetitives-pme/`
- Action: renforcer l’angle “taches repetitives en PME” dans le title, la meta et les premiers liens internes.
- Pourquoi maintenant: position moyenne accessible, aucun clic, mais les sessions GA existantes sont tres engagees.
- Donnees GA/GSC: `gsc-pages-28d.csv`: 8 impressions, 0 clic, position 7.6. `ga-landing-pages-28d.csv`: 3 sessions, 3 engagees, 100% engagement, 17 vues, duree moyenne 1458.6s. `ga-organic-landing-pages-28d.csv`: 1 session Google organic.
- Implementation: garder la page, mais rendre la promesse plus concrete dans le snippet: identifier, prioriser et automatiser les taches repetitives sans complexifier le process.
- Verification apres mise en ligne: CTR GSC de la page, sessions organic landing, engagement rate.
- Risque / limite: les 8 impressions ne suffisent pas pour prouver un effet; c’est un quick win de clarification.

### P4. Ajouter un bloc cible sur chatbot IA personnalise PME et adoption IA generative
- Action: ajouter une section courte ou FAQ dans `/ia-generative-pme-process/` qui couvre ces deux intentions sans creer une nouvelle page.
- Pourquoi maintenant: les requetes existent deja dans GSC, mais le volume est trop faible pour justifier une page dediee.
- Donnees GA/GSC: `gsc-page-query-28d.csv`: `chatbot ia personnalisé pme`, 1 impression, position 37; `tendances adoption ia générative outils entreprise`, 1 impression, position 10. `gsc-pages-28d.csv`: page a 8 impressions, 0 clic, position 10.6. `ga-landing-pages-28d.csv`: 4 sessions, 50% engagement; `ga-organic-landing-pages-28d.csv`: 1 session, 0% engagement.
- Implementation: integrer un bloc “Quand un chatbot IA personnalise a du sens en PME” et un paragraphe sur l’adoption outillee en entreprise; relier vers diagnostic et formation.
- Verification apres mise en ligne: surveiller les lignes page-query et l’engagement organic landing.
- Risque / limite: requetes a 1 impression; a traiter comme hypothese, pas comme axe editorial majeur.

### P5. Repositionner `/mission-ciblee/`
- Action: rendre le title/meta moins generique, en explicitant l’execution courte sur automatisation, outil, raccordement ou mise au propre.
- Pourquoi maintenant: la page apparait en position moyenne 7.1 avec 0 clic, mais le snippet actuel “Mission ciblée” peut etre trop vague hors contexte de marque.
- Donnees GA/GSC: `gsc-pages-28d.csv`: `/mission-ciblee/`, 9 impressions, 0 clic, CTR 0%, position 7.1. GA landing: aucune ligne utile pour cette page.
- Implementation: tester un title du type “Mission ciblee automatisation et outil leger | Pezzos Labs”; renforcer les liens entrants depuis `/accompagnements/`, `/diagnostic-automatisation-process/` et `/automatisation-taches-repetitives-pme/`.
- Verification apres mise en ligne: CTR page GSC et apparition comme landing page GA.
- Risque / limite: recommandation GSC-backed uniquement; absence de signal GA landing.

### P6. Investiguer le sitemap “15 soumises, 0 indexee”
- Action: verifier la coherence sitemap index, sitemap enfant, canonicals et URLs publiees, puis re-soumettre si besoin lors d’un passage Search Console autorise.
- Pourquoi maintenant: le fichier sitemap ne remonte ni erreur ni warning, mais indique 0 URL indexee.
- Donnees GA/GSC: `gsc-sitemaps.csv`: `sitemap-0.xml` et `sitemap-index.xml`, 15 soumises, 0 indexee, 0 erreur, 0 warning. `gsc-pages-28d.csv`: 12 pages ont pourtant des impressions, dont `/` 20 impressions et 2 clics.
- Implementation: sans live data ici, verifier localement que `astro.config.mjs` conserve `site: "https://pezzoslabs.com"` et que le sitemap genere liste les canonicals attendues; ne pas modifier sans validation.
- Verification apres mise en ligne: GSC sitemaps indexed > 0 ou explication documentee de l’ecart.
- Risque / limite: le champ indexed sitemap peut etre en retard ou incomplet; ne pas en deduire seul un probleme d’indexation.

## Observations utiles hors priorites
- La home est la seule page avec clics GSC: `gsc-pages-28d.csv` indique `/`, 20 impressions, 2 clics, CTR 10%, position 3.5; `ga-landing-pages-28d.csv` indique 11 sessions, 41 vues, 90.9% engagement.
- Le trafic GA est concentre en France: `ga-country-28d.csv` indique 33 sessions France; GSC a aussi des impressions USA, mais GA ne montre pas de sessions USA dans ce pack.
- Desktop domine GA: 32 sessions desktop contre 1 mobile; GSC mobile a 2 clics sur 9 impressions, desktop 0 clic sur 28 impressions.

## Donnees insuffisantes ou a ne pas sur-interpreter
- Les volumes GSC sont tres faibles: 37 impressions pages agregees, 4 requetes seulement dans `gsc-queries-28d.csv`.
- `ga-conversions-28d.csv` et `gsc-search-appearance-28d.csv` sont vides; aucune priorisation conversion/rich result fiable.
- `(not set)` dans GA landing represente 4 sessions mais ne doit pas etre traite comme URL.
- Les donnees journalieres n’ont pas de ligne pour le 2026-05-21.
- Les pages slash/no-slash ne doivent pas etre fusionnees dans l’analyse, seulement traitees comme signal de normalisation a verifier.

## Commandes executees
- `sed -n '1,240p' .../.agents/skills/seo-quick-wins/SKILL.md` - lecture du protocole de la skill.
- `find docs/seo-lab-data -maxdepth 2 -type f | sort` - inventaire des exports locaux.
- `git status --short` - verification du worktree, deja dirty avant analyse; aucun fichier modifie.
- `sed -n '1,260p' docs/seo-lab-data/README-data.md` - lecture des limites et de la fenetre.
- `python3` avec module `csv` - comptage lignes/colonnes de tous les exports.
- `python3` avec module `csv` - extraction des metriques GSC/GA par requete, page, landing, device, pays, sitemap.
- `rg --files ...` et `rg -n ...` - localisation read-only des pages Astro et fichiers sitemap/redirects.
- `sed` sur `src/data/accompagnement-pages.ts`, `src/layouts/PublicSiteLayout.astro`, `src/layouts/EnglishSiteLayout.astro`, `astro.config.mjs`, `functions/_middleware.ts` - verification read-only des titles, canonicals, sitemap config et routes.