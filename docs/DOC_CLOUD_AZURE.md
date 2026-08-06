# Documentation Technique - Cloud Public (Azure)

Cette documentation détaille l'infrastructure Cloud mise en place pour héberger la plateforme SaaS du projet CYNA, en répondant aux exigences du bloc de compétences **DI1-AGC**.

## 1. Architecture et Modèle Cloud 
Pour l'hébergement de notre application SaaS, j'ai opté pour un modèle **IaaS** sur le **Cloud Public** Azure. Ce choix permet de bénéficier de l'élasticité tout en gardant un contrôle total sur le système d'exploitation et la configuration de sécurité.

*   **Ressource déployée :** Machine Virtuelle (VM)
*   **Système d'exploitation :** Ubuntu 24.04 LTS (Choix standardisé et sans coût de licence additionnel).
*   **Gouvernance :** Utilisation de balises (Tags) `Projet: CYNA` pour le suivi des ressources.


## 2. FinOps et Optimisation des Coûts 
La maîtrise du budget est un pilier du projet. Plusieurs actions ont été menées pour optimiser la facturation :

1.  **Redimensionnement IaaS :** Sélection d'une instance Burstable (`Standard_B1s`) adaptée aux environnements de test, réduisant le coût horaire drastiquement par rapport aux recommandations par défaut.
2.  **Optimisation Stockage :** Rétrogradation du disque système de SSD Premium vers SSD Standard.
3.  **Prévention des coûts orphelins :** Configuration de la suppression automatique de l'IP publique et de la carte réseau lors de la destruction de la VM.
4.  **Automatisation :** Configuration de l'**arrêt automatique** de la machine virtuelle à 18h00.

## 3. Gouvernance et Identités
Afin de respecter le principe du **Zéro Trust**, l'utilisation du compte Administrateur Global est proscrite pour les tâches courantes.

*   **Mécanisme :** J'ai utilisé **Microsoft Entra ID** pour simuler l'invitation d'un collaborateur (ou développeur) externe.
*   **Principe du moindre privilège :** Cet utilisateur s'est vu attribuer uniquement le rôle de **Contributeur de machine virtuelle** au niveau du groupe de ressources de production, lui interdisant toute modification des paramètres réseau globaux ou de la facturation.

## 4. Supervision et Maintenance
La politique de supervision s'appuie sur les outils natifs de l'hyperviseur pour éviter l'installation (et la facturation) d'agents tiers dans l'OS invité.

*   **Diagnostic :** Activation des **diagnostics de démarrage** sur un compte de stockage managé. Cela permet de récupérer les journaux de la console série en cas de crash système, sans accès SSH.
*   **Métriques :** Surveillance native de l'état de la ressource (Charge CPU, requêtes réseau).
*   **Traçabilité :** Consultation du **Journal d'activité** pour auditer les interventions sur l'infrastructure (démarrage, arrêt, modification).

