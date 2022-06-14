# READ ME - ansible-deployment

## Description 
Ce projet va permettre le déploiement automatique d'une nouvelle infrastructure complète sous Azure. L'infrastructure pourra être déployée selon un environnement spécifique (Production, Staging, Dev, etc.).
Pour se faire, les technologies suivantes devront être installées : 
* Python 3.8.10
* Ansible [core 2.12.6]
Ansible se servira du plugin ansible[azure] pour effectuer des requêtes à l'API d'Azure.

Après avoir déployé l'infrastructure, on installera Docker sur toutes les machines.

## How to Setup
### Host and requirements
Sous ***Ubuntu 20.04.4 LTS***, clonez ce repository à l'endroit souhaité et placez vous dedans. 

```bash
apt update
pip3 install -r requirements.txt
pip3 install -r requirements-azure.txt

```

<br>

### Environments variables
Il va vous falloir créer des variables d'environnements dans le fichier ~/.bash_profile :
```Bash
# If you don't know how to get all these values, I will explain how to create them on the next paragraph.
export AZURE_SUBSCRIPTION_ID=<subcription_id>
export AZURE_CLIENT_ID=<client_id>
export AZURE_SECRET=<client_secret_value> # Care, take the 'value', not the secret ID.
export AZURE_TENANT=<your_azure_tenant_id>
export ENVIRONMENT=Production
export LOWER_ENVIRONMENT=${ENVIRONMENT,,}
```
Puis on indique à Linux le fichier comme étant notre fichier source :
```Bash
source ~/.bash_profile
``` 
<br>

### Get all these values on Azure :
- Pour récupérer **AZURE_SUBSCRIPTION_ID** : 

Rendez-vous sur le portail d'Azure, rechercher le terme (FR) "Abonnements" / (EN) "Subcriptions" et vous trouverez l'ID de votre abonnement dans la deuxième colonne du tableau.
<br>
- Pour récupérer **AZURE_CLIENT_ID** :

Rendez-vous dans votre (FR/EN) "Azure Active Directory" > (FR) "Inscription d'applications" / (EN) "App registrations" > (FR) "Nouvelle inscription" / (EN) "New registration". 
Indiquez un nom et inscrivez votre application. Une fois fait vous devriez voir votre nouvelle application dans la liste, en cliquant dessus vous trouverez l'ID du client dans la "*Vue d'ensemble*" à la ligne : (FR) **ID d'application (client)** / (EN) **Application (client) ID**
<br>
- Pour récupérer **AZURE_SECRET** :

**/!\ Attention /!\ :**  Vous devez avoir fait l'étape précédente pour pouvoir récupérer cette information !

Toujours sur la page de votre application, allez dans (FR) "Certificats & secrets" / (EN) "Certificates & secrets" > (FR) "Nouveau secret client" / (EN) "New client secret", laissez les valeurs par defaults et validez.
C'est ici que vous pourrez récupérer la **VALEUR** de votre secret et non son ID. 

Notez bien cette valeur, car elle sera masquée par la suite.
<br>
- Pour récupérer **AZURE_TENANT** : 

Sur le portail d'Azure, rendez-vous dans (FR) "Propriété du locataire" / (EN) "Tenant properties", vous trouverez le tenant ID à la ligne (FR) **ID de locataire** / (EN) **Tenant ID**.

Et voilà vous avez tous les éléments nécessaire pour permettre au plugin Ansible[azure] de se connecter et d'interagir avec vos ressources.

## Result 
Vous devriez obtenir sous Azure un ressource groupe correspondant à ceci :

![alt text](https://zupimages.net/up/22/24/wlxw.png)



Tous les éléments essentiels de l'infrastructure s'y trouve. 

Lors de l'exécution du **playbook Ansible**, vous devriez obtenir les adresses IP des différentes machines, les mots de passe sont quant à eux stockés dans le dossier **.PASSWORD/** sous la forme de fichiers txt : 
* password-VM-1.txt
* password-VM-2.txt
* password-VM-3.txt
