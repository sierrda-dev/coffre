# Coffre

Gestionnaire de mots de passe **local** pour Windows 11, chiffré de bout en bout, sans compte en ligne.

**Dernière version : 0.1.3** (13 novembre 2026)

- **Télécharger** : [https://sierrda-dev.github.io/coffre](https://sierrda-dev.github.io/coffre) (kit d'installation et version portable)
- **Déjà installé** (0.1.2 ou plus récent) : Coffre propose les mises à jour tout seul.
- **Toutes les versions** : [Releases](https://github.com/sierrda-dev/coffre/releases) · [Journal des versions](CHANGELOG.md)

## Nouveautés de la 0.1.3

**Nouveautés visibles et publication**
- Après une mise à jour, Coffre affiche « Coffre a été mis à jour » avec les nouveautés de la version installée, et un lien vers le journal complet.
- Réglages › À propos › **Voir le journal des versions** ouvre l'historique sur GitHub.
- Chaque version publiée sur GitHub contient les nouveautés complètes, la marche à suivre pour installer ou mettre à jour, et l'empreinte SHA-256 de chaque fichier.
- La page d'accueil du dépôt GitHub présente la dernière version et ses nouveautés ; le journal complet y est publié (CHANGELOG.md).
- Le numéro de version ne se change plus qu'à un endroit (Directory.Build.props) : l'application, la ligne de commande et le paquet s'alignent dessus.
- Correction : le menu « Copier la référence » d'un élément Environnement propose bien la commande « coffre run » (la 0.1.1 l'avait placée dans « Afficher en grand », ce qui empêchait la compilation).

## Installer

1. Télécharge `Coffre-0.1.3-kit.zip` depuis la [dernière version](https://github.com/sierrda-dev/coffre/releases/latest).
2. Clic droit › **Extraire tout**, puis double-clic sur **Installer Coffre**.
3. Windows demande d'approuver l'éditeur de Coffre une seule fois par ordinateur.

## Sécurité

Les paquets sont signés par le certificat [Coffre.cer](https://sierrda-dev.github.io/coffre/Coffre.cer) ; Windows refuse une mise à jour signée par un autre. Le site ne reçoit rien de ton coffre : l'application y lit seulement [version.json](https://sierrda-dev.github.io/coffre/version.json).

Ce dépôt contient le site de téléchargement et des mises à jour. Il est publié par `tools/release.ps1 -Publish`.
