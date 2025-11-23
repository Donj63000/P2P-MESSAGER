# Messagerie P2P chiffrée éphémère (Android / Java)

## Description
Application Android open source visant à proposer une messagerie pair-à-pair sans serveur central. Les messages sont chiffrés de bout en bout et éphémères : ils sont supprimés après consultation. Le code sera majoritairement en Java avec Gradle comme système de build.

## Objectifs par version
### V1 (socle de démarrage)
- Projet Android minimal en Java (Empty Activity) avec affichage basique.
- Une seule conversation locale de test.
- Messages éphémères : suppression automatique après ouverture.
- Pas de réseau, pas de chiffrement pour l’instant.

### V2
- Ajout du chiffrement de bout en bout (libsignal-protocol-java).
- Stockage local chiffré (Room + SQLCipher) pour persister les messages.
- Début d’abstraction réseau sans l’activer.

### V3
- Transport P2P (jvm-libp2p) avec échange direct entre pairs.
- Nœuds relais facultatifs pour messages différés.
- Optimisations UX et gestion fine des états de messages.

## Stack technique prévue
- Android (Java), Gradle.
- Bibliothèques prévues : libsignal-protocol-java, jvm-libp2p, SQLCipher/Room.

## Plan d’action initial
1. **Structurer le dépôt GitHub** : ajouter `.gitignore` Android et cette documentation.
2. **Créer le squelette Android** : projet Empty Activity en Java (minSdk 24), commit initial.
3. **Relier le dépôt distant** : pousser la base vers GitHub et activer les branches.
4. **Mettre en place la CI** : workflow GitHub Actions pour builder `assembleDebug` et publier l’APK en artifact.
5. **Implémenter la logique locale** : modèle `Message`, service en mémoire pour l’auto-destruction, affichage via RecyclerView.

## Prochaines étapes détaillées
- Générer le projet Android via Android Studio puis pousser l’arborescence complète.
- Ajouter un workflow `.github/workflows/android-ci.yml` qui exécute `./gradlew assembleDebug` avec Java 17 et mise en cache Gradle.
- Implémenter un prototype de `MessageService` stockant en mémoire et purgeant les messages expirés.
- Adapter `MainActivity` pour créer/afficher des messages de test et déclencher la suppression après ouverture.

## Licence
À définir (ex. MIT ou Apache-2.0) une fois le code publié.
