# Déploiement mobile-first fiable

**Déclencheur :** "déploie ce code", "mets à jour Symbad", "ajoute cette fonctionnalité", "code sur smartphone"

**Étapes :**
1. Informer le LLM : "Je suis sur Android. Génère des blocs de moins de 50 lignes. Utilise python3 << 'XEOF'. Pas de sed."
2. Snapshoter l'état actuel (cp vers backups/snapshot-AAAA-MM-JJ)
3. Appliquer les modifications bloc par bloc, valider chaque bloc avec py_compile
4. Déployer via safe_edit.sh (backup + validation + restart + healthcheck)
5. Confirmer le succès ou rollback automatique

**Pièges :**
- Android corrompt les blocs > 50 lignes → découper en morceaux
- Ne jamais utiliser sed pour modifier du Python
- Les guillemets et tirets mutent au copier-coller → utiliser Heredoc Python
- Le terminal SSH rafraîchit en plein milieu → commandes courtes uniquement
- Nano est inutilisable → utiliser cat > fichier << 'XEOF'

**Vérification :**
- py_compile passe
- Le service est actif (sudo systemctl is-active hermes)
- L'API /health répond
- Le test Telegram est OK

**Références :**
- safe_edit.sh : déploiement sécurisé
- HEAL.sh : diagnostic urgence
- EMERGENCY.md : procédures de panne
- SKILL_MOBILE_SOURCE.md : guide complet
