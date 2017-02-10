---
title: "Qu’est-ce que Microsoft Advanced Threat Analytics (ATA) ? | Microsoft Docs"
description: "Explique ce qu’est Microsoft Advanced Threat Analytics (ATA) et quels types d’activités suspectes il peut détecter"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 09/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: 70d66bccfda484722afa63a7f85dc8f85013f54f


---

*S’applique à : Advanced Threat Analytics version 1.7*


# <a name="what-is-advanced-threat-analytics"></a>Qu’est-ce qu’Advanced Threat Analytics ?
Advanced Threat Analytics (ATA) est une plateforme locale qui aide à protéger votre entreprise contre plusieurs types d’attaques informatiques ciblées et menaces internes avancées.

## <a name="how-ata-works"></a>Fonctionnement d’ATA
ATA prend les informations de plusieurs sources de données de journaux et d’événements sur votre réseau pour apprendre le comportement des utilisateurs et autres entités de l’organisation et générer ainsi un profil de comportement.
ATA peut recevoir des événements et des journaux des éléments suivants :

-   Intégration SIEM
-   Windows Event Forwarding (WEF)

En outre, ATA s’appuie sur un moteur d’analyse réseau propriétaire pour capturer et analyser le trafic réseau de plusieurs protocoles (tels que Kerberos, DNS, RPC, NTLM et autres) pour l’authentification, l’autorisation et la collecte d’informations. Ces informations sont recueillies par ATA par le biais de :

-   La mise en miroir des ports des contrôleurs de domaine et serveurs DNS vers la passerelle ATA
-   Le déploiement d’une passerelle légère ATA directement sur les contrôleurs de domaine

Pour plus d’informations sur l’architecture d’ATA, consultez [Architecture d’ATA](/advanced-threat-analytics/plan-design/ata-architecture).

## <a name="what-does-ata-do"></a>Que fait ATA ?

La technologie ATA détecte plusieurs activités suspectes, en se focalisant sur différentes phases de la chaîne de cyber-attaque, notamment :

-   Reconnaissance, pendant laquelle les pirates recueillent des informations sur l’architecture de l’environnement et sur les différents composants et entités qui existent. C’est généralement lors de cette phase qu’ils élaborent leur plan pour les étapes suivantes de l’attaque.
-   Cycle de mouvement latéral, pendant lequel un attaquant investit temps et efforts dans la propagation de sa surface d’attaque au sein de votre réseau.
-   Dominance (persistance) de domaine, pendant laquelle un attaquant capture les informations lui permettant de reprendre sa campagne à l’aide d’un ensemble varié de points d’entrée, d’informations d’identification et de techniques. 

Ces phases d’une cyber-attaque sont similaires et prévisibles, quel que soit le type de société visé ou le type d’informations ciblé.
ATA recherche trois principaux types d’attaques : les attaques malveillantes, le comportement anormal, et les risques et problèmes de sécurité.

Les **attaques malveillantes** sont détectées de manière déterministe, en recherchant la liste complète des types d’attaques connus, notamment :

-   Pass-the-Ticket (PtT)
-   Pass-the-Hash (PtH)
-   Overpass-the-Hash
-   Faux PAC (MS14-068)
-   Golden Ticket
-   Réplications malveillantes
-   Reconnaissance
-   Force brute
-   Exécution à distance

Pour obtenir la liste complète des détections et leurs descriptions, consultez [Quelles sont les activités suspectes détectables par ATA ?](ata-threats.md)
ATA détecte ces activités suspectes et expose les informations dans la console ATA, avec une vue claire précisant qui, quoi, quand et comment. Comme vous pouvez le voir, en surveillant ce tableau de bord simple et convivial, vous êtes averti qu’ATA soupçonne qu’une attaque Pass-the-Hash a été tentée sur les ordinateurs Client 1 et Client 2 de votre réseau.

 ![exemple d’écran ATA pour pass-the-hash](media/sample screen pth.png)

Un **comportement anormal** est détecté par ATA en effectuant une analyse comportementale et en tirant parti de Machine Learning pour découvrir les activités douteuses et un comportement anormal chez les utilisateurs et les périphériques de votre réseau, notamment :

-   Connexions anormales
-   Menaces inconnues
-   Partage de mot de passe
-   Mouvement latéral


Vous pouvez afficher les activités suspectes de ce type dans le tableau de bord ATA. Dans l’exemple suivant, ATA vous avertit quand un utilisateur accède à quatre ordinateurs auxquels il n’accède pas normalement, ce qui peut être une cause d’alerte.

 ![exemple d’écran ATA pour un comportement anormal](media/sample screen abnormal behavior.png) 

ATA détecte également les **risques et problèmes de sécurité**, notamment :

-   Relation de confiance rompue
-   Protocoles faibles
-   Vulnérabilités de protocole connues

Vous pouvez afficher les activités suspectes de ce type dans le tableau de bord ATA. Dans l’exemple suivant, ATA vous signale qu’il existe une relation de confiance rompue entre un ordinateur de votre réseau et le domaine.

  ![exemple d’écran ATA pour une relation de confiance rompue](media/sample screen broken trust.png)


## <a name="whats-next"></a>Étapes suivantes

-   Pour plus d’informations sur la façon dont ATA s’intègre à votre réseau, consultez [Architecture ATA](/advanced-threat-analytics/plan-design/ata-architecture).

-   Pour commencer le déploiement d’ATA, consultez [Installer ATA](/advanced-threat-analytics/deploy-use/install-ata).

## <a name="see-also"></a>Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jan17_HO1-->


