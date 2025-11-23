# AGENTS

Ce dépôt vise à construire une application mobile Android entièrement décentralisée qui fonctionne en pair-à-pair : chaque téléphone agit comme nœud autonome sans serveur central. Les messages doivent être chiffrés de bout en bout, éphémères et jamais stockés en clair ou de manière permanente. Cette page fixe les règles à respecter dans tout le dépôt.

## Principes clés
- **Décentralisation totale** : aucun composant ne doit supposer l’existence d’un backend centralisé. Les communications passent par un réseau P2P (Wi‑Fi direct, Bluetooth, WebRTC ou libp2p selon la plateforme et la faisabilité Android).
- **Chiffrement de bout en bout** : seules les parties communicantes peuvent lire le contenu. Utiliser des primitives modernes (par ex. libsignal-protocol-java) et refuser tout stockage ou transport en clair.
- **Éphémérité stricte** : les messages sont auto-détruits après lecture ou après un délai configurable. Aucune persistance longue durée ; privilégier la mémoire vive ou un stockage chiffré temporaire.
- **Surface d’attaque minimale** : limiter les dépendances, activer les vérifications de signature, éviter les permissions Android superflues et privilégier le principe du moindre privilège.
- **UX simple** : l’interface doit rester minimaliste et compréhensible, sans complexifier la création/connexion d’un nœud.

## Directives de développement
- **Langage & build** : Android en Java (minSdk 24), Gradle. Préférer des modules clairs (`model`, `crypto`, `p2p`, `ui`).
- **Sécurité** :
  - Jamais de données sensibles en clair dans les logs ou crash reports.
  - Bannir les clés codées en dur ; privilégier une génération à la volée et un stockage sécurisé (Keystore Android si nécessaire).
  - Toujours valider les entrées réseau et vérifier l’authenticité des pairs.
- **Éphémérité** :
  - Implémenter une politique d’expiration systématique (timer ou horodatage) pour chaque message.
  - Protéger l’interface contre les captures d’écran et empêcher la sauvegarde automatique (ex. `FLAG_SECURE`).
- **P2P** :
  - Prévoir une découverte sans serveur (scan local, échange de codes éphémères, mDNS selon faisabilité Android).
  - Supporter un mode offline-first ; la mise en file d’attente doit rester chiffrée et temporaire.
- **Tests** : ajouter des tests unitaires pour la logique de chiffrement, l’expiration et les utilitaires réseau. Pour le code Android, privilégier des tests instrumentés ciblés.
- **Observabilité** : logs minimaux et anonymisés. Pas de collecte d’analytics.

## Structure documentaire
- Mettre à jour cette page si de nouvelles règles d’architecture ou de sécurité apparaissent.
- Les sous-dossiers peuvent ajouter leur propre `AGENTS.md` pour préciser des conventions locales (scope descendant dans l’arborescence).

## Checklist rapide avant merge
- Chiffrement actif pour toute donnée sensible.
- Pas de dépendance à un serveur central ou à une base de données distante.
- Expiration/auto-destruction testée et vérifiable.
- Permissions Android revues et minimales.
- Tests et CI adaptés (`./gradlew assembleDebug` au minimum) sans fuite de secrets.
