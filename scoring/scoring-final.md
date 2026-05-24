# Scoring final - SEO Stax skill lab

## 1. Classement aveugle des rapports

Deux scorings aveugles Codex sont maintenant disponibles:

- `results/scoring-codex.md`: scoring produit pendant le lab.
- `results/scoring-codex-secondary.md`: scoring lance ensuite par l'operateur dans une session Codex dediee.

`results/scoring-claude.md` contient uniquement une note de timeout; sa trace indique `exit_status: 143`, donc il n'est pas exploitable comme scoring Claude.

Les deux scorings Codex donnent le meme classement: `C > A > D > B`.

| Rang | Rapport | Score | Lecture courte |
| ---: | --- | ---: | --- |
| 1 | C | 92/100 puis 93/100, moyenne 92.5 | Meilleur equilibre data, priorisation, chemins repo et recommandations actionnables. |
| 2 | A | 91/100 puis 92/100, moyenne 91.5 | Tres bon ancrage GA/GSC, plus prudent, mais moins directement localise dans le repo. |
| 3 | D | 88/100 puis 84/100, moyenne 86 | Tres actionnable, mais hierarchie SEO moins nette; priorise trop la normalisation slash/no-slash. |
| 4 | B | 84/100 puis 83/100, moyenne 83.5 | Clair et prudent, mais P1 plus oriente mesure GA que quick win SEO direct. |

## 2. Mapping revele

`results/variants-map.json` donne:

| Rapport aveugle | Variante |
| --- | --- |
| A | clear |
| B | skill |
| C | st+clear |
| D | st+skill |

Classement par variante revelee:

1. `st+clear` - moyenne 92.5/100
2. `clear` - moyenne 91.5/100
3. `st+skill` - moyenne 86/100
4. `skill` - moyenne 83.5/100

## 3. Comparaison clear vs skill

`clear` gagne nettement sur le rapport final: moyenne 91.5 contre 83.5. Les deux identifient les memes pages fortes (`/diagnostic-automatisation-process/`, `/automatisation-taches-repetitives-pme/`, pages offres), mais `clear` priorise plus directement les opportunites SEO page/requete avec 0 clic et position exploitable. `skill` est plus structure et tres lisible, mais son P1 "reparer la mesure conversion/landing" est utile comme hygiene GA, moins immediat comme levier SEO.

Cote cout, `skill` est plus cher: 512s contre 397s, 1.63M input tokens contre 1.13M, et un step supplementaire de creation de skill. La skill a apporte une forme de rapport recurrente et des garde-fous, mais n'a pas ameliore le score dans ce premier passage.

## 4. Comparaison clear vs st+clear

`st+clear` gagne de peu: moyenne 92.5 contre 91.5. La difference qualitative vient surtout du caractere plus actionnable cote repo: chemins et fichiers mieux relies aux recommandations, meilleure localisation des changements possibles, et verification repo plus explicite. Le fond SEO reste tres proche de `clear`: meme priorite forte sur les pages deja visibles avec 0 clic.

Le cout augmente: 461s contre 397s. Les tokens totaux sont proches mais un peu superieurs pour `st+clear` en output. Stax init ne prend que 5s et ne montre pas d'envoi GA/GSC observable; son effet exact n'est donc pas prouvable. Le resultat local suggere que Stax peut legerement ameliorer un process deja etabli, surtout sur l'ancrage repo, mais l'effet mesure reste faible.

## 5. Comparaison skill vs st+skill

`st+skill` bat `skill`: moyenne 86 contre 83.5. Le rapport `st+skill` est plus complet, plus lie au repo, et couvre mieux les validations et limites. En revanche il place la normalisation slash/canonique en P1, priorite defensible mais moins directement business que les pages position 3-8 avec 0 clic.

Le cout est aussi le plus eleve du lab: 594s, 2.18M input tokens, 25.9k output tokens. La creation de skill `st+skill` est plus lourde que `skill` et modifie aussi `.agents/skills/README.md`, ce qui elargit le diff par rapport a la variante sans Stax.

## 6. Comparaison Stax

### Lecture initiale

| Axe | Sans Stax | Avec Stax |
| --- | --- | --- |
| clear | 119s, 221k input tokens | `st+clear`: 91s, 119k input tokens |
| skill | 103s, 195k input tokens | `st+skill`: 99s, 153k input tokens |

Sur la lecture initiale, Stax reduit le cout apparent. Les sorties restent comparables: toutes lisent `docs/seo-lab-data/`, listent la fenetre 2026-04-24 -> 2026-05-21, signalent les exports vides, les faibles volumes, les ecarts GSC et les variantes slash.

### Creation de skill

| Variante | Duree | Resultat |
| --- | ---: | --- |
| skill | 193s | Cree `SKILL.md` et `agents/openai.yaml`; aucun fichier existant modifie. |
| st+skill | 211s | Cree les memes fichiers et modifie `.agents/skills/README.md`. |

Stax n'a pas reduit le cout de creation de skill. La skill `st+skill` est plus encadree et plus longue, avec `allowed-tools` et format de rapport plus prescriptif. Elle est aussi moins minimale, car elle met a jour le README local.

### Execution du rapport

| Variante | Duree rapport | Score moyen final |
| --- | ---: | ---: |
| clear | 195s | 91.5 |
| st+clear | 261s | 92.5 |
| skill | 127s | 83.5 |
| st+skill | 187s | 86 |

Stax ameliore le score dans les deux familles, mais rend l'execution plus longue. Le gain moyen est faible sur clear (+1) et plus visible sur skill (+2.5), sans inverser la conclusion principale: la skill n'a pas gagne face au prompt clair dans ce lab.

### Modification de fichier

Toutes les variantes ont reussi la modification demandee de la homepage et la validation Astro apres installation des dependances. Durees:

| Variante | Duree modification | Validation |
| --- | ---: | --- |
| clear | 83s | `npm run check` OK apres `npm ci` |
| skill | 89s | `npm run check` OK apres `npm ci` |
| st+clear | 104s | `npm run check` OK apres `npm ci`; `git diff --check` OK |
| st+skill | 93s | `npm run check` OK apres `npm ci` |

Stax n'a pas change le comportement fonctionnel de la modification. `st+clear` ajoute une verification `git diff --check`, ce qui est positif mais legerement plus couteux.

## 7. Comparaison workflow cost

| Variante | Duree totale | Input tokens | Cached input | Output tokens | Tours de clarification | Validations lancees | Relances necessaires |
| --- | ---: | ---: | ---: | ---: | ---: | --- | --- |
| clear | 397s | 1,134,434 | 965,248 | 16,508 | 0 visibles | `npm run check`, `npm ci`, `npm run check` | Aucune relance agent; validation relancee apres `npm ci` |
| skill | 512s | 1,625,959 | 1,447,040 | 22,099 | 0 visibles | skill validation, `pre-commit check-yaml`, `make check`, puis `npm run check`, `npm ci`, `npm run check` | Aucune relance agent; `make check` echoue hors perimetre |
| st+clear | 461s | 1,178,009 | 1,022,592 | 19,961 | 0 visibles | `npm run check`, `npm ci`, `npm run check`, `git diff --check` | Aucune relance agent; validation relancee apres `npm ci` |
| st+skill | 594s | 2,180,313 | 1,827,200 | 25,856 | 0 visibles | skill checks, `pre-commit mdformat-check`, `pre-commit check-yaml`, `make check`, puis `npm run check`, `npm ci`, `npm run check` | Aucune relance agent; `make check` echoue hors perimetre |

Fichiers/contextes charges si visibles:

| Variante | Contextes visibles |
| --- | --- |
| clear | Exports `docs/seo-lab-data/*`, README data, parsing CSV, puis `src/pages/index.astro` pour la modification. |
| skill | Exports SEO plus lecture de la skill creee; creation dans `.agents/skills/seo-quick-wins/`; modification homepage. |
| st+clear | Exports SEO, plus inspection repo plus explicite dans le rapport: `src/data/accompagnement-pages.ts`, layouts, sitemap/config, redirects selon la trace. |
| st+skill | Exports SEO, skill locale, README de skills, inspections repo similaires; contexte le plus large. |

Tokens Stax init: indisponibles. Les traces notent que les donnees envoyees a Stax ne sont pas observables depuis stdout et que l'orchestration n'a pas passe les donnees GA/GSC aux commandes Stax.

## 8. Comparaison des diffs homepage

Les quatre variantes changent correctement `src/pages/index.astro`:

- la meta description devient la phrase de test propre a la variante;
- le H1 hero devient `Project Pezzos`;
- le reste du contenu hero est conserve.

Descriptions obtenues:

| Variante | Description |
| --- | --- |
| clear | `labs de test sans skill et sans stax` |
| skill | `labs de test avec skill et sans stax` |
| st+clear | `labs de test sans skill et avec stax` |
| st+skill | `labs de test avec skill et avec stax` |

Diffs `clear`, `skill` et `st+clear`: uniquement `src/pages/index.astro`, avec le meme changement structurel. Diff `st+skill`: `src/pages/index.astro` plus `.agents/skills/README.md`, car la creation de skill avait ajoute l'entree `seo-quick-wins`. Pour comparer strictement la homepage, les differences entre variantes se limitent a une ligne de description; le H1 est identique.

## 9. Conclusion prudente

### Ce que le lab prouve

- Le prompt clair sans skill produit deja un tres bon rapport SEO dans ce contexte offline.
- Stax a ameliore les scores des deux variantes comparees dans les deux scorings aveugles: `clear` -> `st+clear` et `skill` -> `st+skill`.
- Dans ce lab, Stax semble surtout ameliorer un process deja etabli en rendant les sorties plus actionnables cote repo. Il ne transforme pas radicalement la qualite du rapport.
- La skill SEO impose une structure reutilisable, des garde-fous offline et des validations. Elle peut aider le process, mais son premier effet mesure n'est pas un meilleur score brut.
- Les quatre variantes savent executer une modification simple de homepage et valider le projet apres installation des dependances.

### Ce que le lab ne prouve pas

- Il ne prouve pas que Stax est causalement responsable du meilleur score: Stax init est court, opaque cote donnees envoyees, et les traces ne montrent pas de transfert GA/GSC.
- Il ne prouve pas qu'une skill SEO est globalement inutile: une seule tache, un seul site, un seul pack de donnees, et une skill creee juste avant execution.
- Il ne prouve pas la qualite statistique des recommandations SEO: les donnees GA/GSC du pack sont tres faibles en volume.
- Il ne mesure pas la robustesse multi-run, la stabilite entre modeles, ni la qualite sur des sites plus volumineux.
- Il n'a pas obtenu de scoring Claude exploitable; les deux jugements disponibles sont deux scorings Codex.

### Stax merite-t-il un second test ?

Oui, mais avec protocole plus controle. Le meilleur rapport du lab est `st+clear`, et `st+skill` ameliore `skill`. Le signal est positif pour la question "Stax ameliore-t-il un process etabli ?", mais trop faible et trop peu observable pour conclure fermement. Un second test devrait isoler Stax avec memes prompts, memes limites de contexte, ordre randomise, et plusieurs repetitions.

### Une skill SEO semble-t-elle utile ?

Oui pour industrialiser le workflow: forcer l'offline, citer les exports, garder les limites, produire un format recurrent, et eviter les conseils generiques. Le lab suggere aussi qu'elle peut aider quand elle est combinee a Stax (`st+skill` bat `skill`). En revanche, elle ne ressort pas comme accelerateur ni comme garant de meilleure qualite dans ce premier lab: elle coute plus cher et son rapport score moins bien que `clear` et `st+clear`.

### Angle article retenu

L'angle de publication n'est plus "Est-ce que Stax et une skill ameliorent un audit SEO offline ?" mais:

> Est-ce que Stax ameliore vraiment un process etabli ?

Le lab peut traiter la skill comme signal secondaire: elle n'est pas le sujet principal, mais elle montre qu'un process formalise peut devenir plus reproductible, et que Stax peut legerement aider ce process sans le remplacer.

### Ameliorations pour le prochain lab

- Preparer la skill avant le lab, puis tester uniquement son execution, pour ne pas melanger cout de creation et qualite du rapport.
- Avoir deux scorers vraiment independants ou une grille automatique reproductible; ici les deux scores exploitables viennent de Codex et le scoring Claude est inutilisable.
- Randomiser l'ordre des variantes pour limiter les effets de cache/contexte.
- Capturer explicitement les fichiers lus et commandes par phase dans un format machine-readable.
- Separarer les diffs de creation de skill des diffs de modification homepage.
- Mesurer rapport-only, modification-only et total workflow separement.
- Rejouer chaque variante au moins 3 fois, avec mapping aveugle different, pour estimer la variance.
- Ajouter un second pack SEO plus riche, avec volumes suffisants et conversions exploitables.

## Commandes executees pour cette synthese

- `python3 scripts/orchestrator_guard.py init/assert/run-status --compact`, `python3 scripts/runtime_profiles.py summary --compact`, `python3 scripts/project_profile.py summary` - indisponibles a la racine du lab; scripts absents.
- `rg --files`, `find results -maxdepth 3 -type f | sort`, `git status --short` - inventaire du lab et etat worktree.
- `cat results/variants-map.json`, `sed`/`cat` sur `results/scoring-*.md`, rapports, traces, Stax init et logs `.last.md` - lecture des artefacts.
- `wc -l results/report-*.md results/run-trace-*.md results/diff-*.patch results/stax-init-*.md` - controle de taille.
- `python3` read-only - extraction des durees et tokens depuis les traces.
- `cat results/diff-*.patch`, `rg -n "description=|<h1>|Project Pezzos" .../src/pages/index.astro` - comparaison des diffs homepage.
- `git diff --no-index --stat` et `git diff --no-index` entre skills - comparaison read-only des skills creees.
