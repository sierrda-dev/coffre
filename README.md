# Coffre

Gestionnaire de mots de passe **local** pour Windows 11, chiffré de bout en bout, sans compte en ligne.

**Dernière version : 0.1.4** (13 novembre 2026)

- **Télécharger** : [https://sierrda-dev.github.io/coffre](https://sierrda-dev.github.io/coffre) (kit d'installation et version portable)
- **Déjà installé** (0.1.2 ou plus récent) : Coffre propose les mises à jour tout seul.
- **Toutes les versions** : [Releases](https://github.com/sierrda-dev/coffre/releases) · [Journal des versions](CHANGELOG.md)

## Nouveautés de la 0.1.4

**Plus rapide, nouvel écran de verrouillage, éditeur et réglages revus**
- La liste des éléments ne crée plus que les lignes visibles (une vingtaine), recyclées en défilant, au lieu d'une ligne par élément : ouverture, défilement et changement de coffre ou de filtre restent fluides même avec des milliers d'éléments. Apparence, regroupements, clic droit et flèches du clavier inchangés.
- La recherche attend 150 ms après la dernière frappe au lieu de tout recalculer à chaque lettre, et cherche dans un texte préparé une fois par élément (titre, identifiant, e-mail, site, tags, notes).
- L'analyse de la Sentinelle se fait en arrière-plan : plus de petit gel après chaque enregistrement sur un gros coffre. Les pastilles, le compteur de la barre latérale et la fiche ouverte se mettent à jour d'eux-mêmes.
- Mesures de performance dans le journal local de Coffre (%LOCALAPPDATA%\Coffre\coffre.log) : temps de démarrage, temps d'ouverture du coffre et mémoire utilisée. Rien n'est envoyé.
- **Nouvel écran de verrouillage**, épuré et sans encadré : ta photo de profil au centre (ou le logo de Coffre), Windows Hello en bouton principal quand il est disponible, puis le mot de passe ; avertissement « Verr. Maj est activée », secousse du champ en cas d'erreur, rappel du verrouillage automatique et de Ctrl+Q en bas. Ton nom n'apparaît jamais. La photo est copiée hors du coffre pour s'afficher avant le déverrouillage : Réglages › Sécurité › « Photo sur l'écran de verrouillage » pour la retirer.
- **Watchtower devient la Sentinelle** (barre latérale, page, journal, aide). En ligne de commande : `coffre sentinelle` (`coffre watchtower` reste accepté).
- **Comportement du remplissage par site web** : le bouton à côté de chaque adresse propose « Remplir n'importe où sur ce site web » (par défaut : toutes les adresses du même site, par exemple login.exemple.fr et www.exemple.fr), « Remplir uniquement sur cet hôte précis » ou « Ne jamais remplir sur ce site web », avec une phrase qui dit où l'élément sera proposé.
- **Mot de passe dans l'éditeur** : au clic, il s'affiche en clair et une bulle propose « Créer un nouveau mot de passe ». Le générateur s'ouvre sous le champ : Annuler, ↻, Utiliser ; aperçu avec chiffres en bleu et symboles en rouge, barre de robustesse ; type (aléatoire, mémorisable, code PIN), nombre de caractères, chiffres, symboles. Les choix sont mémorisés.
- **Réglages** : colonne de gauche avec une tuile de couleur par rubrique, rubrique ouverte en bleu.
- **Illustration** de la fiche vide redessinée, plus abstraite : anneaux, formes arrondies et points aux couleurs de Coffre.
- Nouveau test automatique sur un coffre de 5 000 éléments (enregistrement, modification, Sentinelle, réouverture), pour repérer toute version qui ralentirait.

## Installer

1. Télécharge `Coffre-0.1.4-kit.zip` depuis la [dernière version](https://github.com/sierrda-dev/coffre/releases/latest).
2. Clic droit › **Extraire tout**, puis double-clic sur **Installer Coffre**.
3. Windows demande d'approuver l'éditeur de Coffre une seule fois par ordinateur.

## Sécurité

Les paquets sont signés par le certificat [Coffre.cer](https://sierrda-dev.github.io/coffre/Coffre.cer) ; Windows refuse une mise à jour signée par un autre. Le site ne reçoit rien de ton coffre : l'application y lit seulement [version.json](https://sierrda-dev.github.io/coffre/version.json).

Ce dépôt contient le site de téléchargement et des mises à jour. Il est publié par `tools/release.ps1 -Publish`.
