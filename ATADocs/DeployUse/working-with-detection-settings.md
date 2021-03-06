---
title: "Gestion des paramètres de la détection ATA | Microsoft Docs"
description: "Décrit comment configurer une liste d’adresses IP et de sous-réseaux ayant des circonstances inhabituelles et qui doivent donc être gérés différemment des autres entités de votre réseau."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: 93f2a72c9623674c73b3ee83ecf12be8e0766365


---

*S’applique à : Advanced Threat Analytics version 1.7*



# <a name="working-with-ata-detection-settings"></a>Gestion des paramètres de la détection ATA
La page de configuration **Détection** permet de configurer une liste d’adresses IP et de sous-réseaux ayant des circonstances inhabituelles et qui doivent donc être gérés différemment des autres entités de votre réseau.

## <a name="setting-up-detection"></a>Configuration de la détection
Dans la section **Détection**, vous pouvez définir les éléments suivants :

-   **SID de comptes honeytoken** : ce compte d’utilisateur ne doit pas avoir d’activité réseau. Ce compte sera configuré comme l’utilisateur honeytoken ATA. Si quelqu’un tente d’utiliser ce compte d’utilisateur, ATA crée une alerte d’activité suspecte avec une indication d’activité malveillante. Pour configurer l’utilisateur honeytoken, vous aurez besoin du SID du compte d’utilisateur, et non du nom d’utilisateur.

>[!NOTE]
> Vous trouverez le SID de l’utilisateur sous l’onglet *Informations sur le compte* du profil de l’utilisateur dans la console ATA.


![Paramètres de détection ATA - honeytoken](media/ata-detection-settings-honeytoken-1.7.png)


**Exclusions de détection** - Vous pouvez exclure des adresses IP des détections suivantes. Si vous ajoutez une adresse IP dans une de ces listes, ATA exclura cette adresse IP de ce type précis d’activité.

-   Exclusions d’adresses IP DNS Reconnaissance

-   Exclusions d’adresses IP Pass-the-Ticket

![Paramètres de détection ATA - exclusions](media/ata-detection-settings-exclusions-1.7.png)


## <a name="see-also"></a>Voir aussi
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Modification de la configuration d’ATA](modifying-ata-configuration.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jan17_HO1-->


