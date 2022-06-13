# READ ME - ansible-azure-deployment

## Description 
Ce projet va permettre le déploiement automatique d'une nouvelle infrastructure complète sous Azure. L'infrastructure pourra être déployée selon un environnement spécifique (Production, Staging, Dev, etc.).
Pour se faire, les technologies suivantes devront être installées : 
* Python 3.8.10
* Ansible [core 2.12.6]
Ansible se servira du plugin ansible[azure] pour effectuer des requêtes à l'API d'Azure.

## How to Setup
Sous ***Ubuntu 20.04.4 LTS***, clonez ce repository à l'endroit souhaité. 



## Result 
Vous devriez obtenir sous Azure un ressource groupe correspondant à ceci :

![alt text](https://i.postimg.cc/d1kHgVJQ/Azure-Ansible.png)

Tous les éléments essentiels de l'infrastructure s'y trouve. 
Lors de l'exécution du **playbook Ansible**, vous devriez obtenir les adresses IP des différentes machines, les mots de passe sont quant à eux stockés dans le dossier **.PASSWORD/** sous la forme de fichiers txt : 
* password-VM-1.txt
* password-VM-2.txt
* password-VM-3.txt
