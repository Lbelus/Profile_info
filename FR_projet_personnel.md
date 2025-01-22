## **C++ Redis Client Prototype**

Le projet client Redis en C++ est une application CLI conçue pour interagir avec un serveur Redis, développée pour renforcer les compétences en network, protocole RESP, création de bibliothèque et configuration CMake. L'application comprend une API C++ basée sur hiredis, encapsulée en tant que bibliothèque, et un CLI adapté d'une version antérieure en C. Ce CLI permet des commandes Redis via un analyseur de commande personnalisé qui utilise `readline`, `getopt`, et des pointeurs de fonction.

### Fonctionnalités principales :
- **Commandes supportées** : Commandes Redis de base pour le stockage clé-valeur, les listes et les tables de hachage, avec des commandes utilitaires comme `PING` et `INFO`, structurées au format BNF.
- **Environnement basé sur Docker** : Configuration simplifiée et exécution des tests dans un réseau Docker.
- **Tests** : Utilise GoogleTest pour les tests unitaires, avec des cas de test ciblant une instance Redis sur `tcp://myredis:6379`.
- **Installation** : Comprend des instructions Docker, la configuration CMake pour la construction de l'API et la configuration du CLI pour les tests manuels.

Le projet nécessite Docker et comprend des étapes détaillées pour l'installation et l'utilisation.

**Mots-clés** : Client Redis, C++, protocole RESP, programmation réseau, CMake, Docker, hiredis, CLI, GoogleTest, bibliothèque

**lien** : https://github.com/QwasarSV/my_cpp_redis_client_575_belus_l_svg

---

## **FTP Server**

Ce projet de serveur FTP implémente un serveur multithread pour le transfert de fichiers sur TCP/IP, suivant le protocole FTP (RFC959). Le serveur prend en charge l'authentification via un utilisateur "Anonymous" et inclut des modes actif et passif pour le transfert de données. Les utilisateurs peuvent naviguer indépendamment dans les répertoires et effectuer des actions telles que le téléchargement, l'upload, et la liste des fichiers.

### Fonctionnalités principales :
- **Multithreading** : Prend en charge plusieurs connexions clients simultanées à l'aide d'un threadspool.
- **Support des commandes** : Implémente les commandes FTP de base (`USER`, `PASS`, `CWD`, `PWD`, `LIST`, `PASV`, `PORT`, `RETR`).
- **Modes** : Prend en charge le mode actif (le serveur initie la connexion de données) et le mode passif (le client initie).
- **Composants** : Comprend un lexer/parser, un serveur FTP et une implémentation client.
- **Conformité au protocole** : Respecte les normes FTP avec le traitement des commandes et les réponses structurées.

### Installation et utilisation :
Compilez le serveur en utilisant `make`, puis exécutez le serveur en spécifiant le port et le chemin (ex. : `./my_ftp 8080 .`). Le client peut se connecter au serveur via les commandes fournies (ex. : `USER anonymous`, `CWD <dir>`).

**Mots-clés** : Serveur FTP, TCP/IP, multithreading, client-serveur, mode actif/passif, RFC959, parsing de commande, C

**lien** : https://github.com/QwasarSV/my_ftp_509_belus_l_cwo

---

## **Custom Memory Allocator**

Le projet de Custom Memory Allocator implémente une bibliothèque de gestion de mémoire en C, fournissant des alternatives aux fonctions `malloc`, `free`, `calloc`, et `realloc`. Il optimise l'allocation de mémoire en demandant de grands blocs de mémoire via `mmap` et en les divisant, réduisant ainsi la fréquence des appels système.

### Fonctionnalités principales :
- **Gestion efficace de la mémoire** : La mémoire est gérée via un interval tree qui suit les adresses de page sans stocker chaque allocation.
- **Structure d'allocation** : Utilise un bitmap et un système de liste chaînée pour gérer les slots, optimisant l'allocation et la libération de mémoire.
- **Gestion des pointeurs** : L'allocator trouve et libère les slots de mémoire, exploitant les bitmaps pour un overhead minimal.
- **Remplacement de la bibliothèque standard** : La bibliothèque peut être utilisée en remplacement les fonctions `malloc` standard avec un `LD_PRELOAD` trick.

### Installation et utilisation :
Compilez avec `make` et utilisez `LD_PRELOAD=./libmymalloc.so <command>` pour remplacer temporairement les fonctions mémoire du système. L'allocation et la libération de mémoire suivent les pratiques standard, la bibliothèque gérant les blocs de mémoire en arrière-plan.

**Mots-clés** : Malloc personnalisé, gestion de mémoire, allocation dynamique, mmap, interval tree, bitmap, liste chaînée, C, LD_PRELOAD

lien : https://github.com/QwasarSV/my_malloc_436_belus_l_m1a

---

## **Custom C Memory Allocator for Rust on Solana**

Ce projet consiste à créer un custom memory allocator en C, compatible avec Rust et conçu pour être déployé sous forme de smart contract sur la blockchain Solana. L'allocator est compilé avec la target eBPF et respecte donc les contraintes de la machine virtuelle eBPF (qualcom, solana), telles que la limitation des arguments de fonction et l'évitement des opérations non déterministes.

### Fonctionnalités principales :
- **Compatibilité eBPF** : L'allocator respecte les normes eBPF, en utilisant de l'assembly pour les appels système directs, contournant ainsi les limitations des bibliothèques standard.
- **Fonctions de gestion de la mémoire** : Implémente des fonctions essentielles (`malloc`, `calloc`, `realloc`, et `free`) pour une allocation efficace de la mémoire.
- **Liaison inter-langage** : L'allocator C est lié à Rust en utilisant le crate `bindgen`, facilitant les interactions avec le Foreign Function Interface (FFI).
- **Tagged union pour la sécurité** : Fournit une interface qui respecte la logique deterministe de Rust avec une tag union pour gérer les types en toute sécurité obfusquant le code `unsafe`.
- **Intégration avec Rust** : L'allocator s'intègre à Rust, permettant des appels directs dans les projets Rust et la possibilité de remplacer l'allocator global de Rust.

### Utilisation et implémentation :
Le projet utilise `LD_PRELOAD` pour testes l'allocator système. Le custom allocator utilise l'attribut `#[repr(C)]` de Rust pour assurer la compatibilité avec les structures C. Les utilisateurs peuvent allouer de la mémoire via des raw pointers ou via une Tagged Union.

Cet allocator est conçu pour fonctionner efficacement dans l'environnement de Solana.

**Mots-clés** : Allocator personnalisé, Rust FFI, eBPF, blockchain Solana, C, gestion de mémoire, smart contract, cross-compilation

liens :
- https://github.com/Lbelus/sdmm
- https://medium.com/@lorris.belus/how-to-create-a-c-custom-memory-allocator-and-use-it-in-rust-16a3a79d8f82
- https://www.linkedin.com/feed/update/urn:li:activity:7235294229902602240/

---

## **Custom Curl Implementation**

Les projets custom curl (`my_curl` et `curl_lib`) reproduisent la fonctionnalité de la commande Unix `curl`, permettant de récupérer des données via HTTP avec des fonctionnalités personnalisées. `my_curl` est un outil de ligne de commande simple pour afficher du contenu HTML, tandis que `curl_lib` est une bibliothèque plus avancée incluant le support SSL/TLS, les protocoles HTTP/HTTPS, et la personnalisation de user-agent, l'inclusion d'un addon pour interargir avec les serveurs de LinkedIn.

### Fonctionnalités principales :
- **Requêtes HTTP** : Utilise la programmation de sockets pour gérer les requêtes GET et POST HTTP et afficher les réponses du serveur.
- **User Agents** : Permet de sélectionner divers user agents, avec la possibilité d'en ajouter des personnalisés.
- **Gestion des cookies** : Implémente le format Netscape cookie jar, en analysant le domaine, le chemin, l'expiration, et les drapeaux de sécurité.
- **API Endpoints** : Fournit des fonctions pour interagir avec les API web, avec des exemples pour la récupération de données de profil LinkedIn.
- **Intégration Python** : Prend en charge les extensions Python avec une configuration d'environnement virtuel, permettant des interactions API via des scripts Python. /!\ l'integration avec python presente un probleme de compilation avec ssh_read et une implementation low level de readline en c et en assembly;

### Installation et utilisation :
Compilez `my_curl` avec `make` et exécutez-le en tant que `./my_curl <URL>`. Pour `curl_lib`, installez via `python3 setup.py build` et utilisez les fonctions Python pour interagir avec des services web, en démontrant la connexion et la récupération de données.

Ce projet démontre un client HTTP bas niveau, améliorant les capacités de récupération de données web et offrant une exploration des endpoints API.

**Mots-clés** : Curl personnalisé, requêtes HTTP, SSL/TLS, user agents, gestion des cookies, LinkedIn API, intégration Python, C, réseaux

liens :
- https://github.com/Lbelus/curl_lib
- https://github.com/QwasarSV/my_curl_

368_belus_l_zr1

---

## **Custom UNIX Shell in C**

Ce projet implémente un interpréteur de commandes UNIX personnalisé, `my_zsh`, en C. Le shell lit, analyse et exécute les commandes entrées par l'utilisateur, en reproduisant le comportement de base d'un shell. Il prend en charge l'exécution des commandes via `execve` et des commandes intégrées telles que `echo`, `cd`, `setenv`, `unsetenv`, `env`, `exit`, `pwd`, et `which`.

### Fonctionnalités principales :
- **Exécution de commandes** : Analyse l'entrée de l'utilisateur et exécute les commandes en utilisant `execve`, en prenant en charge les variables d'environnement et les commandes basées sur PATH.
- **Commandes intégrées** : Implémente plusieurs commandes UNIX intégrées, permettant aux utilisateurs d'interagir avec l'environnement, de naviguer dans les répertoires, et de gérer les variables.
- **Prompt personnalisable** : Affiche un prompt au format `[what_you_want]>`.
- **Gestion des erreurs** : Fournit des retours pour les commandes invalides et gère les erreurs de manière élégante.

### Installation et utilisation :
Clonez le repo, compilez en utilisant `make`, et lancez l'interpréteur avec `./my_zsh`. Le shell affiche un prompt où les utilisateurs peuvent entrer des commandes et affiche les résultats ou les messages d'erreur selon les besoins. Les commandes intégrées et les utilitaires `/bin` sont pris en charge, permettant une interaction flexible.

**Mots-clés** : Shell personnalisé, interpréteur de commandes, execve, commandes intégrées, PATH, variables d'environnement, gestion des erreurs, C

lien :
- https://github.com/QwasarSV/my_zsh_402_belus_l_u1y

---

## **Largest Square Finder (my_bsq)**
Ce projet en C localise le plus grand carré dans une grille contenant des obstacles, en utilisant le dynamic programing pour optimiser les calculs. L'algorithme analyse la grille dans une matrice, applique une approche dynamique pour identifier les tailles de carrés, et stocke les valeurs dans une matrice DP pour une efficacité accrue. Le résultat final met en évidence la taille maximale du carré et ses coordonnées.

**Mots-clés** : Dynamic programing, grille d'obstacles, plus grand carré, manipulation de matrices, C

lien : https://github.com/QwasarSV/my_bsq_294_belus_l_gtc

---

## **Basic Calculator (my_bc)**
Une calculatrice de base en C, gérant uniquement des calculs entiers avec des opérations (`+`, `-`, `*`, `/`, `%`) et des parenthèses. Elle convertit les expressions de la notation infix à postfix en utilisant l'algorithme Shunting Yard, puis les évalue en notation polonaise inversée (RPN). Cette approche simplifie la priorité des opérateurs et assure la précision des calculs.

**Mots-clés** : Calculatrice de base, opérations entières, algorithme Shunting Yard, RPN, C

lien : https://github.com/QwasarSV/my_bc_296_belus_l_ynf

---

## **Blockchain CLI (my_blockchain)**
Ce projet CLI en C prototype une blockchain, simulant des nœuds et des blocs. Il prend en charge l'ajout, la suppression, et la liste des nœuds et des blocs, la synchronisation des chaînes, et l'affichage d'erreurs pour les opérations incorrectes. Il inclut un algorithme de consensus basé sur la chaîne valide la plus longue pour la résolution des conflits. Le CLI inclut également des options pour sauvegarder et quitter, avec des indicateurs visuels de l'état de synchronisation.

**Mots-clés** : Blockchain, CLI, gestion des nœuds, algorithme de consensus, chaîne la plus longue, C

lien : https://github.com/QwasarSV/my_blockchain_173_belus_l_nmq

---

## **Custom Readline (my_readline)**
L'objectif de ce projet en C est d'implémenter une version personnalisée de la fonction `readline` pour lire des fichiers ligne par ligne, en gérant un buffer dynamique. Après des expérimentations avec des buffers circulaires et le redimensionnement du buffer, la fonction lit désormais efficacement l'entrée en actualisant le buffer en fonction de la position du curseur. Ce readline personnalisé gère les longueurs de ligne variables et assure la compatibilité avec différents fichiers d'entrée.

**Mots-clés** : Readline personnalisé, buffer dynamique, lecture ligne par ligne, gestion de fichiers, C

lien : https://github.com/QwasarSV/my_readline_172_belus_l_6f-

---

## **Custom Tar Utility (my_tar)**
Ce projet reproduit les fonctionnalités de base de la commande Unix `tar`, permettant aux utilisateurs d'archiver, d'ajouter, de mettre à jour, de lister et d'extraire des fichiers. Construit de manière itérative, chaque fonctionnalité représente une étape dans le processus de développement. Le CLI prend en charge les flags (`-cf`, `-rf`, `-uf`, `-tf`, `-xf`) pour gérer les archives en blocs de 512 octets. Les futures mises à jour pourraient inclure la gestion récursive des répertoires et une sélection de fichiers optimisée.

**Mots-clés** : Utilitaire tar, archivage, gestion des fichiers, CLI, flags, développement itératif, C

lien : https://github.com/QwasarSV/my_tar_166_belus_l_egy

---

## **Custom Printf (my_printf)**
Ce projet implémente une fonction `printf` personnalisée en C, gérant des arguments variables et prenant en charge les spécificateurs de format communs (`%c`, `%s`, `%d`, `%o`, `%u`, `%x`, `%p`). En utilisant des fonctions personnalisées pour la sortie de caractères, la gestion des chaînes et la conversion d'entiers, ce `printf` renvoie le nombre de caractères imprimés et reproduit le comportement standard de `printf` avec une correspondance précise des types.

**Mots-clés** : Printf personnalisé, fonction variadique, spécificateurs de format, sortie de caractères, conversion d'entiers, C

lien : https://github.com/Lbelus/my_qwasar_lib/tree/main/c/my_printf_70028_vfhfqu

---

## **MySqlite - Un SQLite basé sur Ruby**

**MySqlite** est une implémentation légère d'un système de base de données similaire à SQLite, écrite en Ruby. Elle prend en charge les opérations CRUD, les requêtes de style SQL et la récupération efficace des données grâce à un index inversé. Le système est construit autour d'un **command design pattern** et offre une approche basée sur des classes pour les interactions avec la base de données.

### Fonctionnalités principales :
- **Classes principales** :
  - **MySqliteRequest** : Combine les fonctionnalités de récupération et de manipulation pour exécuter des requêtes complexes.
  - **MySqliteGetter** : Gère les opérations SELECT avec prise en charge des clauses WHERE, JOIN et ORDER.
  - **MySqliteSetter** : Prend en charge les opérations INSERT, UPDATE et DELETE.
  - **InvertedIndex** : Optimise les recherches grâce à une structure de type dictionnaire qui associe des valeurs à des identifiants correspondants.
- **SQL-like CLI** : Fournit une interface en ligne de commande interactive pour des requêtes de style SQL.
- **Recherche efficace** : Implémente un index inversé pour réduire les scans de table complets et accélérer la récupération des données.

### Utilisation :
1. **Installation** :
   - Clonez le dépôt : `git clone git@github.com:Lbelus/my_sqlite.git`.
   - Installez le gem localement ou via un serveur gem local.
   - Lancez `my_sqlite` depuis n'importe quel répertoire pour démarrer le CLI.

2. **Requêtes CLI** :
   - Exemple : `SELECT * FROM nba_player_data.csv WHERE birth_state='Indiana';`
   - Prend en charge une syntaxe de type SQL pour les clauses SELECT, INSERT, UPDATE, DELETE, JOIN et WHERE.

3. **Tests** :
   - Lancez les tests automatisés avec `rake` depuis le répertoire du projet.

### Points forts :
- Prend en charge les requêtes de type SQL avec certaines limitations : une clause WHERE et une clause JOIN par requête.
- Optimisé pour des opérations CRUD efficaces grâce à un index inversé.
- Facilement extensible grâce à une conception modulaire des classes.

### Mots-clés :
- Command-Line Interface (CLI), CRUD Operations, SQL-like Queries, Inverted Index, Database System, Data Retrieval, MySqlite, Command Design Pattern  

**Développeurs** : Lorris Belus (Développeur), Igor Mirsalikhov (Assistant de recherche)

---

# Navigateur Distant avec mTLS

Le projet **Navigateur Distant avec mTLS** propose un navigateur Firefox sécurisé et conteneurisé, utilisant Docker, Nginx, ainsi que des fonctionnalités réseau avancées comme Shadowsocks, BadVPN et Tor. Sécurisé avec le mTLS (mutual TLS), il garantit que seuls les clients authentifiés peuvent accéder au navigateur, offrant une gestion sûre des liens non fiables et une confidentialité renforcée.

## Fonctionnalités Principales :
- **Authentification mTLS** : Sécurise la communication entre le client et le serveur.
- **Navigateur Conteneurisé** : Déploie Firefox dans un conteneur Docker.
- **Outils de Confidentialité** : Intègre Shadowsocks, BadVPN et Tor pour une anonymisation et une obfuscation du trafic.
- **Gestion Automatisée des Certificats** : Génère automatiquement les certificats serveur et client.
- **Proxy Nginx** : Gère les certificats SSL et redirige le trafic du navigateur.
- **Accès Restreint** : Configure UFW pour limiter les ports aux connexions sécurisées uniquement.

## Utilisation :
Exécutez le script pour installer Docker, Nginx, Shadowsocks, BadVPN et Tor. Installez le certificat client `.p12` généré, connectez-vous à `https://<adresse-ip-serveur>` et profitez d’une expérience de navigation sécurisée et privée.

**Mots-clés** : mTLS, Docker, Nginx, Shadowsocks, BadVPN, Tor, navigateur sécurisé, SSL, conteneurisation

---

