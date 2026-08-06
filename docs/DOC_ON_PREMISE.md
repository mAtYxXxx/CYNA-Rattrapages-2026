## 1. Topologie de l'Infrastructure
Le réseau local (siège social CYNA) est hébergé sur un cluster Proxmox de trois nœuds (`pve`, `pve2`, `pve3`). La gestion du trafic est assurée par des pare-feux pfSense redondés, isolant les zones (LAN, DMZ, SOC).

## 2. Service d'Annuaire LDAP - Active Directory
Pour centraliser les identités et gérer le parc informatique, un domaine Active Directory a été mis en œuvre.

*   **Haute Disponibilité :** L'annuaire repose sur deux contrôleurs de domaine (`AD01` et `AD02`), assurant la réplication et respectant les bonnes pratiques de tolérance de panne.
*   **Structuration de l'Annuaire :** L'arborescence a été pensée en Unités Organisationnelles (OU) logiques, séparant géographiquement ou fonctionnellement les départements (ex: Siège, Filiales, équipes SOC, commerciaux).
*   **Gestion des Objets :** Création et administration centralisée des comptes utilisateurs, ordinateurs clients et groupes de sécurité.
*   **Déploiement de Configurations :** Mise en place de Stratégies de Groupe (GPO) liées aux différentes OU pour automatiser la configuration des postes de travail (ex: mappage de lecteurs réseau, application de règles de sécurité).

## 3. Service d'Attribution IP - DHCP 
Le déploiement des adresses IP sur le réseau LAN a été automatisé via un serveur DHCP, garantissant une configuration réseau fiable et sans conflits pour les postes clients.

*   **Configuration de l'étendue :** Création d'un pool d'adresses IPv4. Définition des options d'étendue obligatoires : Passerelle par défaut (pare-feu pfSense) et serveurs DNS (pointant vers AD01 et AD02 pour la résolution locale).
*   **Application des Bonnes Pratiques :**
    *   Mise en place d'une **plage d'exclusion** au début du sous-réseau afin de préserver des adresses IP statiques pour les équipements d'infrastructure (serveurs, routeurs).
    *   Configuration d'une **réservation d'adresse (Bail permanent)** basée sur l'adresse MAC pour garantir qu'un équipement spécifique (ex: imprimante réseau) obtienne systématiquement la même IP.
