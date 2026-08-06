# CYNA-Rattrapages-2026
# Projet CYNA - Dossier de Rattrapages (Août 2026)

**Modules :** 
*   **UE-AGC :** Gouvernance et Administration Cloud (Azure)
*   **UE-ASI :** Administration des Systèmes de l'Information (Proxmox / Windows Server)

---

## 🎯 Objectif du dépôt
Ce repository centralise la documentation technique et les preuves de configuration réalisées dans le cadre du projet fil rouge **CYNA**.
Le projet a nécessité la mise en place d'une architecture hybride :
1.  Un environnement **On-Premise (Cloud Privé)** virtualisé sous Proxmox pour la gestion du réseau local et des identités internes.
2.  Un environnement **Cloud Public (Microsoft Azure)** pour l'hébergement hautement disponible de la plateforme SaaS ouverte aux clients.

## 📂 Structure du projet

*   📁 `docs/` : Contient les documentations techniques détaillées.
    *   📄 [**DOC_CLOUD_AZURE.md**](docs/DOC_CLOUD_AZURE.md) : Déploiement de la VM sur Azure, justification des choix, configuration et choix des ressources et supervision sur Azure.
    *   📄 [**DOC_ON_PREMISE.md**](docs/DOC_ON_PREMISE.md) : Déploiement et structuration de l'annuaire Active Directory (LDAP) et configuration du service DHCP
