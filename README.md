# VERSION MASTER VIERGE — état d'avancement (PARTIEL)

## Ce qui est prêt
- `index.html` : même application, un seul fichier. Toutes les fonctions (329) et toutes les actions d'interface (246) sont identiques à l'original (comparaison automatique). Aucune fonctionnalité supprimée.
- Vidé / neutralisé : nom, logo, textes, horaires, téléphone, adresse, catalogue, FAQ, zones de livraison, fidélité (sans visuel), vidéos, musiques, actualités, assistant (portrait remplacé par une icône neutre), mentions légales / CGV (modèles génériques à compléter), liens GitHub, URL et clé Supabase, clé push.
- `manifest.json`, `sw.js`, `media/` (icônes 192/512 et logo neutres à remplacer).
- Mot de passe admin temporaire : `ChangeMoi-2026` → à changer avec `python3 tools/set-admin-password.py "NouveauMotDePasse"` AVANT toute mise en ligne.
- `tools/gen-vapid.py` : clés push propres à chaque commerce (jamais celles de l'ancien).
- `supabase/functions/describe/` : fonction de rédaction (aucun secret dedans).

## Ce qui N'EST PAS terminé (honnêtement)
1. **Scripts SQL complets du nouveau Supabase** : la lecture de la structure de ta base (tables, RLS, triggers, cron) n'a pas été approuvée, donc je n'ai pas inventé le schéma. `supabase/sql/10-12` sont seulement les scripts déjà intégrés à ton app (fidélité, maintenance, photo de vérification). Les tables (profiles, orders, messages, stock, push_subs…) manquent. `00_EXPORT_SCHEMA_LECTURE_SEULE.sql` exporte la structure (SELECT uniquement).
2. **Edge Functions `push` et `auto-alerts`** : leur code actuel contient en dur une clé privée VAPID et un secret partagé. Je ne les ai pas copiés ; la version propre (secrets via variables d'environnement) reste à écrire.
3. **Non testé** : parcours client/admin avec un vrai Supabase, commandes, fidélité, lecteur musical, notifications push. Seul testé : syntaxe JavaScript et chargement de la page sans erreur ni appel vers l'ancien projet.

## Points d'attention
- Le service worker d'origine ne met rien en cache (pas de mode hors ligne) : conservé tel quel.
- Le module « analyse laboratoire (THC) » des fiches produit reste présent (spécifique CBD, désactivable en ne le remplissant pas).
- La vérification de compte par photo est forcée active par le code d'origine (`fixL`) : elle exige le bucket `ids` (script 12).
