![Azure NXT Maxscale](https://static.wixstatic.com/media/02e6ef_9c7c628fadc94a8fb0495465cc6e5240~mv2.png/v1/fill/w_539,h_96,al_c,q_85,usm_0.66_1.00_0.01,enc_auto/NXTMAXSCALE.png)

# 🌐 Azure NXT Maxscale – Infrastructure Nextcloud Haute Disponibilité

**Azure NXT Maxscale** est une solution conçue pour déployer une infrastructure Nextcloud hautement disponible, adaptée aux grandes structures et aux environnements critiques. Elle regroupe l’ensemble des services nécessaires à un déploiement complet : base de données, stockage, application, édition collaborative, cache, équilibrage de charge et certificats SSL.

---

## 🧱 Fonctionnement global

L’architecture repose sur un proxy central **HAProxy** qui achemine le trafic vers différents services en fonction du sous-domaine demandé :

- `nextcloud.domaine.tld` → Frontend Nextcloud  
- `collabora.domaine.tld` → Éditeur Collabora Online  
- `whiteboard.domaine.tld` → Tableau blanc collaboratif  

Chaque service est déployé en **mode cluster** pour assurer la haute disponibilité et la montée en charge. Les communications internes se font via un **réseau Docker commun**.

Les composants principaux sont :

- **HAProxy** : Routage des flux, gestion des certificats SSL, intégration avec Let's Encrypt  
- **Nextcloud (app)** : Application principale  
- **MariaDB Galera** : Base de données répliquée  
- **Redis** : Cache distribué  
- **MinIO** : Stockage d’objets distribué, répliqué localement et/ou sur site distant  
- **Collabora Online** : Édition collaborative de documents  
- **Whiteboard** : Tableau blanc partagé  

---

## 🔁 Clusters et personnalisation

Tous les fichiers `.yml` et `.sh` fournis sont conçus pour être **modulables**. Le **nombre de nœuds** dans les fichiers est **donné à titre d’exemple uniquement**.  
L’utilisateur est libre d’ajuster ce nombre en fonction de ses besoins et des recommandations de chaque composant.

### Exemple :
- **MariaDB Galera** : il est recommandé d’utiliser un **nombre impair** de nœuds pour assurer le quorum (ex : 3 ou 5)  
- **MinIO** : nécessite un nombre pair de disques/nœuds pour la parité  
- **Redis** et **Nextcloud** : scalables horizontalement  

---

## 📁 Fichiers inclus

| Fichier / Script                   | Description                                                                |
|------------------------------------|----------------------------------------------------------------------------|
| `minio-cluster.yml`                | Déploiement du cluster principal MinIO                                     |
| `minio-replica.yml`                | Déploiement du cluster MinIO de réplication vers un site distant           |
| `minio_heal.sh`                    | Réparation automatique du cluster MinIO                                    |
| `nextcloud-cluster.yml`            | Déploiement de Nextcloud en haute disponibilité                            |
| `mariadb-galera-cluster.yml`       | Déploiement du cluster MariaDB Galera                                      |
| `redis-cluster.yml`                | Déploiement du cluster Redis                                               |
| `collabora-cluster.yml`            | Déploiement du cluster Collabora Online                                    |
| `whiteboard-cluster.yml`           | Déploiement du tableau blanc collaboratif                                  |
| `haproxy.cfg`                      | Configuration de HAProxy pour routage multi-services                       |
| `backup_database.sh`               | Sauvegarde de la base de données                                           |
| `restore_database.sh`              | Restauration de la base de données                                         |

---

## 🧰 Déploiement recommandé

- Système Linux (Debian/Ubuntu)  
- Docker et Docker Compose  
- Certbot (pour SSL)  
- DNS configuré pour les sous-domaines  
- Accès root ou sudo  

---

## 📬 Contact

Pour toute demande de déploiement, assistance ou personnalisation :

**Azure Informatique**  
📧 contact@azure-informatique.fr
