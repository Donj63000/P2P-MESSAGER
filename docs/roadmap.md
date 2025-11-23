# Roadmap initiale

## Mise en place du dépôt
- [x] Ajouter un `.gitignore` Android pour éviter les fichiers générés.
- [x] Documenter la vision et les jalons dans `README.md`.

## Préparation du projet Android
- [ ] Générer un projet Android Studio (Empty Activity, Java, minSdk 24).
- [ ] Pousser l’arborescence complète du projet dans le dépôt.

## Intégration continue
- [ ] Ajouter un workflow GitHub Actions (`.github/workflows/android-ci.yml`) qui exécute `./gradlew assembleDebug` (JDK 17 + cache Gradle) et publie l’APK en artifact.

## Prototype de messagerie éphémère locale
- [ ] Créer les modèles `MessageState` et `Message` (package `com.val.p2psecure.model`).
- [ ] Implémenter un `MessageService` en mémoire avec purge des messages expirés.
- [ ] Adapter `MainActivity` pour afficher la liste via RecyclerView et déclencher la suppression après ouverture.

## Évolutions futures
- [ ] Persistance chiffrée (Room + SQLCipher).
- [ ] Crypto E2E (libsignal-protocol-java) avec gestion des sessions.
- [ ] Transport P2P (jvm-libp2p) et nœuds relais optionnels.
