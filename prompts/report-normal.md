A partir des exports Google Search Console et Google Analytics fournis dans `docs/seo-lab-data/`, produis un rapport SEO orienté quick wins pour pezzoslabs.com.

Fichiers à utiliser explicitement :
- `docs/seo-lab-data/gsc-queries-28d.csv`
- `docs/seo-lab-data/gsc-pages-28d.csv`
- `docs/seo-lab-data/ga-landing-pages-28d.csv`

Utilise aussi tous les autres exports GA/GSC disponibles dans `docs/seo-lab-data/`, ainsi que `docs/seo-lab-data/README-data.md`.

Objectif : trouver des leviers concrets d'amelioration SEO, pas resumer l'etat general du site.

Contraintes :
- Utilise uniquement les donnees exportees et les fichiers du repo.
- N'utilise pas MCP ni donnees live.
- Relie chaque recommandation a une donnee GA/GSC precise.
- Priorise par impact probable et facilite de mise en oeuvre.
- Evite les conseils SEO generiques non relies aux donnees.
- Signale clairement les limites des exports et les hypotheses.
- Ne modifie aucun fichier.

Sortie attendue :
1. Resume executif en 5 lignes maximum.
2. 5 a 10 quick wins SEO priorises.
3. Pour chaque quick win : donnee source, diagnostic, action recommandee, page ou requete concernee, impact attendu, effort estime.
4. Une recommandation unique a implementer en premier dans le repo.
5. Les limites de l'analyse.
