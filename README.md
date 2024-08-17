- 👋 Hi, I’m @DvK42
- 👀 I’m ReactJS Junior Developer
- 🌱 I’m currently learning at ESGI

<!---
1. Vérification des Clés SSH
Il faut d’abord s’assurer que les clés SSH ont bien été générées et configurées correctement. Pour cela, vérifie les points suivants :

Vérifie la présence de tes clés SSH :
Utilise la commande suivante pour lister tes clés SSH :

bash
Copier le code
ls -al ~/.ssh
Tu devrais voir quelque chose comme :

rust
Copier le code
id_rsa_personal
id_rsa_personal.pub
id_rsa_work
id_rsa_work.pub
Ajout des clés SSH à l'agent SSH :
Assure-toi que tu as bien ajouté tes clés SSH à l'agent SSH. Voici les commandes à utiliser :

bash
Copier le code
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa_personal
ssh-add ~/.ssh/id_rsa_work
Cela permet à l'agent SSH de gérer tes clés privées.

2. Configuration des fichiers config SSH
Un fichier de configuration SSH mal configuré peut être la cause de ton problème. Le fichier config se trouve dans le dossier ~/.ssh/.

Assure-toi que ton fichier config contient bien les configurations appropriées pour tes deux clés. Par exemple :

bash
Copier le code
Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_personal
    
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_work
Ce fichier config permet d'associer des hôtes distincts (github-personal et github-work) à chaque clé SSH. Cela permet à SSH de savoir quelle clé utiliser en fonction de l’hôte que tu vas spécifier dans l’URL du dépôt.
3. Configuration des URLs des dépôts Git
Une fois que le fichier de configuration SSH est en place, tu dois t'assurer que Git utilise les bonnes URL pour tes dépôts.

Vérifie l'URL distante de ton dépôt Git :
Pour vérifier cela, utilise la commande suivante dans le répertoire de ton dépôt Git :

bash
Copier le code
git remote -v
Si l'URL distante commence par https://, tu dois la changer pour utiliser la méthode SSH. Par exemple :

Pour ton compte personnel, remplace l'URL par :
bash
Copier le code
git remote set-url origin git@github-personal:username/repo.git
Pour ton compte professionnel :
bash
Copier le code
git remote set-url origin git@github-work:username/repo.git
Remarque : Assure-toi que l'URL correspond bien à l'alias défini dans ton fichier config (github-personal ou github-work).

4. Vérification de l'agent SSH
Il peut aussi être utile de vérifier que l’agent SSH fonctionne bien avec tes clés. Après avoir ajouté tes clés à l'agent, tu peux tester la connexion avec GitHub en utilisant la commande suivante :

bash
Copier le code
ssh -T git@github-personal
ssh -T git@github-work
Tu devrais obtenir une réponse similaire à :

bash
Copier le code
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
Si tu obtiens une réponse d'erreur, il y a peut-être un problème avec tes clés ou ta configuration.

5. Vérification des permissions du dépôt
Assure-toi également que le dépôt sur lequel tu essaies de faire un push est bien accessible avec la clé SSH appropriée. Si tu utilises la mauvaise clé pour un dépôt auquel tu n’as pas accès, GitHub demandera toujours des identifiants d’authentification.

Cas spécifiques
Clés SSH spécifiques à des projets distincts : Si tu travailles sur des projets GitHub différents pour ton compte personnel et professionnel, assure-toi que chaque projet est correctement configuré avec l'URL correcte (git@github-personal: ou git@github-work:) en fonction de la clé SSH associée.

Comportement inattendu de SSH : Il est également possible que certaines configurations globales de Git ou SSH interférent avec ta configuration spécifique. Tu peux temporairement désactiver ces configurations ou vérifier que rien ne force l’utilisation des méthodes HTTP pour les dépôts.

Conclusion
Si tu as bien suivi les étapes ci-dessus, normalement, Git ne devrait plus te demander tes identifiants de connexion lors du push, car il utilisera directement les clés SSH pour s'authentifier.

En résumé :

Assure-toi que tes clés SSH sont bien configurées et ajoutées à l'agent SSH.
Vérifie ton fichier config pour associer correctement tes clés aux hôtes GitHub.
Modifie l'URL de tes dépôts pour utiliser SSH au lieu de HTTPS.
Teste la connexion SSH avec GitHub pour t'assurer que tout fonctionne correctement.
--->
