# Journal des versions

## 0.1.3 — 13 novembre 2026

**Nouveautés visibles et publication**
- Après une mise à jour, Coffre affiche « Coffre a été mis à jour » avec les nouveautés de la version installée, et un lien vers le journal complet.
- Réglages › À propos › **Voir le journal des versions** ouvre l'historique sur GitHub.
- Chaque version publiée sur GitHub contient les nouveautés complètes, la marche à suivre pour installer ou mettre à jour, et l'empreinte SHA-256 de chaque fichier.
- La page d'accueil du dépôt GitHub présente la dernière version et ses nouveautés ; le journal complet y est publié (CHANGELOG.md).
- Le numéro de version ne se change plus qu'à un endroit (Directory.Build.props) : l'application, la ligne de commande et le paquet s'alignent dessus.
- Correction : le menu « Copier la référence » d'un élément Environnement propose bien la commande « coffre run » (la 0.1.1 l'avait placée dans « Afficher en grand », ce qui empêchait la compilation).

## 0.1.2 — 13 novembre 2026

**Mises à jour automatiques**
- Coffre vérifie chaque jour s'il existe une nouvelle version et propose de l'installer, avec la liste des nouveautés.
- « Mettre à jour maintenant » : Coffre se verrouille, Windows télécharge et installe la version signée, puis relance Coffre ; coffre et réglages conservés.
- « Plus tard » repousse la proposition de trois jours ; Réglages › À propos › Mises à jour automatiques pour désactiver.
- Version portable : la fenêtre ouvre la page de téléchargement.
- Site des mises à jour : https://sierrda-dev.github.io/coffre ; tools/release.ps1 -Publish publie la version GitHub et le site en une commande.

## 0.1.1 — 13 novembre 2026

**Plusieurs ordinateurs, accès d'urgence et développeurs**
- **Synchronisation entre tes ordinateurs, sans serveur** : le coffre se place dans un dossier OneDrive, Dropbox, Google Drive ou NAS (Réglages › Synchronisation › Déplacer le coffre).
  - Coffre surveille le fichier toutes les 5 secondes et avant chaque enregistrement, puis fusionne élément par élément : la modification la plus récente gagne.
  - Les suppressions définitives laissent une trace (180 jours) pour qu'un élément effacé ne revienne pas depuis l'autre ordinateur.
  - Les copies en conflit créées par OneDrive ou Dropbox (« Coffre-PC-BUREAU.vault ») sont fusionnées, puis renommées en `.fusionne-…`.
  - Un mot de passe maître changé sur un ordinateur est adopté par les autres au lieu d'être écrasé.
  - Le Mode voyage n'est jamais fusionné.
- **Accès d'urgence** par un contact de confiance (Réglages › Accès d'urgence) :
  - fichier `.coffre-secours` chiffré pour la clé X25519 du contact (son code de partage), avec une copie chiffrée du coffre ;
  - le contact l'ouvre depuis son propre Coffre, obtient une copie et choisit un nouveau mot de passe ; ni le propriétaire ni son kit d'urgence ne sont touchés.
- **Environnements** : nouvelle catégorie (une variable par champ), import d'un `.env` dans l'éditeur, `coffre run --environment Coffre/Élément`, `coffre env import` et `coffre env export`. Les valeurs sensibles sont masquées dans la sortie. La référence `coffre://coffre/élément/*` renvoie toutes les variables.
- **Serveur MCP** `coffre mcp` pour les assistants d'IA (Claude, VS Code, Cursor) :
  - `list_items` donne les titres, sites, identifiants et références `coffre://`, jamais les secrets (accord une fois par déverrouillage) ;
  - `read_secret` demande ton accord dans Coffre **à chaque lecture**, sans l'option des 10 minutes.
  - Réglages › Développeur › Copier la configuration.
- **Extension VS Code** (dans le kit, installée sans Marketplace) : insérer une référence (Ctrl+Alt+K), secrets en clair soulignés avec correction rapide, analyse du dossier, lancement avec un environnement, explication au survol des références.

## 0.1.0 — 13 novembre 2026

**Première version d'utilisation**
- **Watchtower redessinée**, d'après 1Password 8 :
  - **En-tête** : titre, explication, bouton **Partager mon score** (copie un résumé sans aucune information sur tes éléments), et cadran du score à droite (arc dégradé, graduations, appréciation « FANTASTIQUE », « TRÈS BON »…).
  - **Robustesse globale des mots de passe** : barre en cinq couleurs, de « Fantastique » à « Très faible », avec légende.
  - **Grandes tuiles** sur trois colonnes, seulement pour les problèmes réels : nombre, titre, explication, icône pâle, et « Afficher les éléments → ». Nouvelles tuiles : **Clé de récupération manquante** (→ Configurer) et **Éléments avec doublons** (même site et même identifiant).
  - **Alertes ignorées** : « Ignorer » sur chaque élément signalé, puis « Afficher les alertes ignorées » pour les rétablir. Ignorer ne modifie ni la date ni l'historique de l'élément.
- Toutes les corrections de la série 0.0.9 : invitations, page Profil, ligne de commande en un seul fichier.

## 0.0.9 — 13 novembre 2026

**Développeurs et confort**
- **Références de secrets** `coffre://coffre/élément/champ` :
  - champs désignés par leur clé, un alias (« mot de passe », « token »), un libellé de champ personnalisé, ou « otp » pour le code 2FA actuel ;
  - clic droit sur un élément › **Copier la référence**.
- **Ligne de commande** :
  - `coffre read`, `coffre run --env-file .env -- commande` (secrets masqués dans la sortie, `--no-masking` pour les programmes interactifs) et `coffre inject` (modèles `{{ coffre://… }}`) ;
  - ces commandes demandent les secrets à **Coffre ouvert**, qui affiche une autorisation (option « Ne plus demander pendant 10 minutes »). Sans l'application ouverte, la ligne de commande demande le mot de passe maître ;
  - le kit contient `coffre.exe` et « Installer la ligne de commande ».
- **Plugins** : `coffre plugin init gh coffre://Personnel/GitHub`, puis `coffre gh …` injecte GH_TOKEN, sans fichier de configuration en clair. 14 outils sont pris en charge : gh, glab, aws, az, npm, docker, openai, claude, stripe, hf, vercel, netlify, doctl, terraform.
- **Signature des commits Git** avec une clé SSH du coffre, via l'agent de Coffre (accord demandé à chaque signature). Elle se configure par `coffre git setup` ou par Réglages › Développeur › Configurer Git. Vérifié : `git verify-commit` et `ssh-keygen -Y verify` acceptent les signatures Ed25519, ECDSA et RSA.
- **Watchtower développeur** :
  - repère les clés SSH privées sans phrase de passe dans ~/.ssh ;
  - analyse un dossier de code à la recherche de secrets en clair : jetons GitHub, clés AWS, Stripe, OpenAI, Anthropic, Slack, Google, npm, clés privées, mots de passe dans les .env (valeurs masquées) ;
  - aussi disponible par `coffre scan <dossier>`.
- **Extension Firefox** (Firefox 128 et plus), dans le kit.
- **Afficher en grand** : caractères géants numérotés (chiffres en bleu, symboles en rouge) dans une fenêtre épinglable au-dessus des autres, fermée au verrouillage.
- **Clic droit dans la liste** : ouvrir, copier l'identifiant, le mot de passe ou le code 2FA, ouvrir le site, afficher en grand, copier la référence, favori, modifier, corbeille.
- **Saisie automatique** depuis l'accès rapide (**Ctrl+Maj+Entrée**) : Coffre revient à l'application précédente et y tape l'identifiant, Tab, puis le mot de passe, sans passer par le presse-papiers.
- **Page Profil** séparée des réglages, comme dans 1Password :
  - photo et nom, avec le bouton « Gérer le profil » ;
  - carte **Identité** (adresse, téléphone, e-mail ; « Mettre à jour l'identité », « Changer ») ;
  - carte **Moyen de paiement** (« Sélectionner » la carte par défaut). L'extension propose cette identité et cette carte en premier.
  - La barre latérale affiche ta photo et ton nom en haut, et les coffres sous « COFFRES ».
- **Invitations corrigées** : le code de partage n'est plus effacé du presse-papiers après 30 secondes, ce qui pouvait faire échouer une invitation avec « CODE ».
  - Nouvelle fenêtre **Mon code de partage…** : copier, envoyer par e-mail ou enregistrer dans un fichier.
  - Le code collé dans « Inviter » est vérifié aussitôt et affiche le nom et l'empreinte de la personne.
  - Les erreurs de partage ont toutes un message clair.
- **Reporté après la 0.1.0** : déverrouillage par clé FIDO2 (YubiKey). Il passe par l'API WebAuthn native de Windows, avec des structures binaires qu'on ne peut pas valider sans clé physique ; une erreur ferait planter l'application.

## 0.0.8 — 13 novembre 2026

**Diffuser et utiliser à plusieurs**
- **Kit d'installation** fabriqué par `tools\release.ps1` sur le PC de l'éditeur. Il contient :
  - `Installer Coffre.cmd`, qui approuve le certificat de l'éditeur (une seule autorisation Windows par ordinateur) puis installe ou met à jour le paquet MSIX signé ;
  - une version portable de secours ;
  - l'extension Chrome/Edge ;
  - une notice LISEZ-MOI et le guide de démarrage.
- **Signature** : certificat auto-signé `CN=Erc` créé une fois dans le magasin de l'éditeur et réutilisé pour chaque version, afin que les mises à jour s'installent par-dessus. Les paquets sont horodatés quand Internet est disponible.
- **Mises à jour** : refaire « Installer Coffre » avec le nouveau kit. Le coffre (Documents\Coffre) et les réglages sont conservés. « Rechercher une mise à jour » l'explique, au lieu d'afficher une erreur.
- **Guide de démarrage** dans l'application (bouton « Aide », menu ⋮, écran de verrouillage, Réglages › À propos) : installation, mot de passe maître et kit d'urgence, import, extension, coffres partagés à plusieurs.
- **« Copier mon code de partage »** dans le menu ⋮, pour rejoindre un coffre partagé.
- La feuille de route « Développeurs et confort » (FIDO2, signature Git, `coffre run`…) passe en 0.0.9.

## 0.0.7.1 — 12 novembre 2026

**Interface, au plus près de 1Password 8 (d'après les captures fournies)**
- **Barre latérale claire**, gris très léger, à la place du bleu nuit. On y trouve :
  - « Coffre ⋮ » en haut ;
  - le sélecteur « Tous les coffres » suivi d'un séparateur ;
  - Profil, Tous les éléments, Favoris, Watchtower et Développeur (clés SSH et clés d'API) ;
  - les coffres sous le nom du propriétaire, avec + pour en créer un ;
  - les tags avec une icône verte.
- **Barre d'outils** : ← →, champ « Rechercher dans tous les coffres » avec loupe, lien bleu « Aide » et bouton bleu « + Nouvel élément ».
- **Liste** : groupes par mois (« NOVEMBRE 2026 »), triés par date de modification. Les tuiles affichent deux lettres sur fond pastel (« me », « Ed »), et la sélection est bleue avec du texte blanc.
- **Fiche** : boutons « Partager » (envoi sécurisé) et « Modifier ». Les libellés violets sont plus petits et les champs plus compacts. Le pied « › Dernière modification lundi 9 novembre 2026 à 20:11:03 » se déplie.
- **Sans sélection** : une illustration de coffre-fort en gris clair.
- **« Que souhaitez-vous ajouter ? »** :
  - recherche (catégories et services connus, par exemple « netflix ») ;
  - six cartes : Connexion, Note sécurisée, Carte de crédit, Identité, Identifiants de l'API, Document ;
  - « Plus de catégories » ;
  - « Importer vos données dans Coffre ».
- **Nouvel éditeur** :
  - ← et ✕ en haut ; grande icône avec ▾ pour changer de catégorie, puis le titre ;
  - carte de champs sans cadre, avec l'e-mail le plus utilisé proposé comme nom d'utilisateur ;
  - sites web sur fond gris, avec « + ajouter un autre site web » et ⊖ pour retirer ;
  - « + ajouter plus », pour l'e-mail, la 2FA et les champs personnalisés ;
  - remarques, puis tags en pastilles avec « + Ajouter un tag » ;
  - pied « propriétaire | coffre ▾ » et bouton « Enregistrer » (Ctrl+S).
- **Écran de verrouillage dans le style de 1Password 8** :
  - la barre latérale grise reste visible, vide, avec « Coffre ⋮ » ;
  - au centre : le logo de Coffre, le champ « Entrez votre mot de passe » avec sa flèche bleue, et une ligne d'aide pour Windows Hello ;
  - le menu ⋮ propose : ouvrir un autre coffre, créer un coffre, mot de passe oublié, mises à jour, aide, fermer (Ctrl+W) et quitter (Ctrl+Q). Les actions qui demandent un coffre ouvert y sont grisées.
- **Confidentialité** : l'écran de verrouillage n'affiche plus de prénom, de photo, de nom de compte Windows ni de nom de fichier du coffre.

## 0.0.7 — 12 novembre 2026

**Partager et protéger**
- **Clé secrète** (équivalent de la Secret Key de 1Password) : clé aléatoire de 128 bits combinée au mot de passe maître (HKDF-SHA256). Une copie volée du fichier ne peut plus être attaquée par force brute. Elle est mémorisée sur l'appareil (DPAPI, compte Windows) et demandée une seule fois sur un nouvel ordinateur. Elle figure dans le kit d'urgence et se règle dans Réglages › Sécurité.
- **Mode voyage** : les coffres non marqués « sûrs pour le voyage » sont retirés de l'ordinateur et placés dans une archive chiffrée (`.coffre-voyage`) à ranger ailleurs, puis réintégrés au retour.
  - L'archive est vérifiée avant toute suppression.
  - Les sauvegardes automatiques sont suspendues pendant le voyage, et les sauvegardes locales existantes peuvent être supprimées.
  - Un bandeau s'affiche dans la barre latérale pendant le voyage.
- **Envoi sécurisé nominatif** : destinataires nommés, chacun avec son propre code ; durée de 1 heure à 30 jours. Un historique des envois (sans leur contenu) est conservé.
- **Qui a accès** dans chaque fiche : membres du coffre partagé et leurs rôles, plus les envois sécurisés. La fiche affiche aussi l'**historique des modifications** (date, auteur, appareil) avec restauration.
- **Échéances** :
  - Cartes, pièces d'identité (nouveau champ « Expiration de la pièce »), documents et clés d'API sont suivis. Les formats AAAA-MM-JJ et JJ/MM/AAAA sont acceptés.
  - Une rubrique « Expire bientôt » apparaît dans la barre latérale.
  - Une notification Windows est affichée au déverrouillage, au plus une fois par jour, et peut être désactivée.
- **Annuler** : un bouton « Annuler » apparaît pendant 6 secondes après un déplacement entre coffres ou une mise à la corbeille.
- **Aperçu des pièces jointes** : images et fichiers texte s'ouvrent dans Coffre, sans copie en clair sur le disque.

**Ligne de commande** : `coffre secret-key on|off`, `coffre travel status|on|off|safe`, `coffre send --to "Marie,Paul" --hours 1`. La clé secrète se fournit par `COFFRE_SECRET_KEY` ou est demandée à l'ouverture.

**Reporté à la 0.0.8** : déverrouillage par clé de sécurité FIDO2 (YubiKey, Titan). Il demande un module natif (API WebAuthn de Windows, extension hmac-secret) qui doit être testé sur du matériel réel.

**Limites assumées (sans serveur)** :
- Une page d'envoi déjà transmise ne peut pas être révoquée à distance. Son expiration est vérifiée par la page elle-même.
- Un coffre protégé par une clé secrète ne s'ouvre plus avec Coffre 0.0.6 ou antérieur.

**Tests** : 43 tests unitaires, dont 7 nouveaux (clé secrète, Mode voyage et archive modifiée, envoi nominatif, échéances, kit d'urgence) ; tests de bout en bout inchangés et réussis.

## 0.0.6 — 12 novembre 2026

**Remplir plus vite** : accès rapide (Ctrl+Maj+Espace) ; remplissage des cartes bancaires et des identités dans Chrome et Edge ; identifiant sur deux pages ; générateur de noms d'utilisateur (mots, aléatoire, alias « +site ») ; questions de sécurité avec réponse générée ; catalogue de 90 services à la création d'un élément ; brouillons chiffrés conservés au verrouillage ; Watchtower « Passkeys disponibles ».
**Ligne de commande** : `coffre add` et `coffre generate --username`.
**Tests** : 36 tests unitaires ; nouveau test de bout en bout `tests/e2e/forms.e2e.js` (cartes, identités, nom d'utilisateur, deux pages).

## 0.0.5 — 12 novembre 2026

**Interface** : disposition de 1Password 8 : barre latérale bleu nuit (compte, Tous les éléments, Favoris, Watchtower, coffres et tags repliables, Archives, Supprimés récemment) ; barre d'outils en haut (précédent/suivant, recherche, aide, « Nouvel élément ») ; liste avec filtre « Toutes les catégories », tri, groupes par lettre, étoile des favoris et sélection bleue ; fiche avec propriétaire et coffre (déplacement vers un autre coffre), grande icône, champs en carte aux libellés bleu-violet, robustesse à droite du mot de passe, code à usage unique « 553 • 740 » avec compte à rebours, adresses web et détails sous la carte.
**Corrections** : compilation WinUI 3 (ScrollViewer scellé, conflits de noms), profil de lancement MSIX (`launchSettings.json`), déploiement activé dans la solution (x64 et ARM64), plantage au démarrage lié à la couleur d'accent, message d'erreur explicite si l'application ne peut pas démarrer.

## 0.0.4 — 9 novembre 2026

Première version native Windows 11 (WinUI 3, .NET 10, MSIX), qui remplace l'application Electron 2.x (ses coffres sont relus et convertis).

**Indispensables** : remplissage automatique Chrome/Edge (icône dans les champs, enregistrement et mise à jour proposés, générateur, codes 2FA) ; kit d'urgence PDF et clé de récupération ; sauvegardes automatiques chiffrées et vérifiées ; tests automatisés Windows et Linux en CI.
**Distribution** : paquet MSIX x64/ARM64, mises à jour automatiques par .appinstaller, signature en CI, extension prête pour le Chrome Web Store et Edge Add-ons, version portable.
**Fonctions avancées** : pièces jointes chiffrées ; historique des versions ; imports 1Password, Bitwarden, KeePass, CSV ; clés SSH et agent SSH ; envoi sécurisé ; Watchtower en continu.
**Équipe et conformité** : stratégie d'organisation, journal d'activité exportable, accessibilité, anglais, modèles de documents juridiques.
**Sécurité** : nouvelle hiérarchie de clés (format 3), écran exclu des captures, presse-papiers hors historique, ligne de commande.

## 2.1.0 (Electron)

Connexion par Windows Hello, retrait de l'e-mail et des exemples, durcissement.
