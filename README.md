# Labo 05 - Microservice de paiement
<img src="https://upload.wikimedia.org/wikipedia/commons/2/2a/Ets_quebec_logo.png" width="250">    
ÉTS - LOG430 - Architecture logicielle - Chargé de laboratoire: Gabriel C. Ullmann.   

Microservice de paiement qui dessert l'application Store Manager.

**ATTENTION** : Ceci est un exemple de microservice de paiement à des fins de démonstration uniquement. Aucune transaction réelle ne sera effectuée et aucune information de carte de crédit ne sera collectée, enregistrée ou transmise.

Pour plus de détails, veuillez consulter le document d'architecture sur `docs/arc42/docs.md` et le document ADR sur `docs/adr/adr001.md`.
---

## ☸️ Déploiement Kubernetes (Phase 2)

Ce service doit être déployé sur la grappe Kubernetes de l'ÉTS, au même titre que le Store Manager.

**Aucun manifeste n'est fourni dans ce dépôt** : les créer fait partie de l'exercice. Vous devez produire un `k8s-manifests.yml` couvrant au minimum :

- un `Deployment` et un `Service` pour l'API de paiement
- un `Deployment`, un `Service` et un `PersistentVolumeClaim` pour sa base de données
- les `ConfigMap` et `Secret` nécessaires à la configuration

Le service de paiement possède sa **propre base de données**, distincte de celle du Store Manager — c'est le principe même d'un microservice.

Consultez le guide `kubernetes.md` du dépôt `log430-labo5` : connexion à la grappe, contraintes à respecter (NodePort plutôt qu'Ingress, pas de Jobs, classe de stockage par défaut) et publication des images sur GHCR.

## 📦 Livrables

La remise se fait au niveau de la **Phase 2** (Labos 04 et 05), dans un espace Moodle unique. Le code de ce dépôt va dans le dossier `labo05-payment/` du zip d'équipe.

Voir la section Livrables du `README.md` de `log430-labo5` pour le détail.

> ⚠️ **Attention au nom du Service.** `config/krakend.json` du dépôt `log430-labo5` route vers `http://payments_api:5009`. Ce nom vient de Docker Compose et est **invalide en Kubernetes** : les underscores y sont interdits (RFC 1123). Nommez votre Service `payments-api` et mettez `krakend.json` à jour en conséquence, sinon la passerelle ne joindra jamais ce service.
