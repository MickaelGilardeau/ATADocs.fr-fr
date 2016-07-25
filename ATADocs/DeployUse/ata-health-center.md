---
title: "Centre d’intégrité ATA | Microsoft ATA"
description: "Le centre d’intégrité ATA vous permet de vérifier le bon fonctionnement du service ATA et vous avertit en cas de problèmes potentiels."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c512fd20f913c53ac936f7de288eb024d91cf9f1
ms.openlocfilehash: 87c92ce4ca7834df7483071a18f78ca6c6bfccd0


---

# Centre d’intégrité ATA
Le centre d’intégrité ATA vous permet d’évaluer les performances de votre service ATA et vous prévient en cas de problèmes.

## Utilisation du centre d’intégrité ATA
Si un problème se produit, le centre d’intégrité ATA déclenche une alerte en affichant un point rouge au-dessus de l’icône du centre d’intégrité dans la barre de menus.

![Barre d’outils du point rouge dans le centre d’intégrité ATA](media/ATA-Health-Center-Alert-red-dot.png)

### Gestion de l’intégrité d’ATA
Pour vérifier l’intégrité globale de votre système, cliquez sur l’icône du centre d’intégrité dans la barre de menus. ![Icône du centre d’intégrité ATA](media/ATA-red-dot.png)

-   Pour gérer les alertes actives, vous pouvez leur affecter l’état **Résolue(s)** ou **Rejetée(s)**. Dans l’alerte, cliquez sur **Ouvrir**, puis faites défiler la liste jusqu’à **Résolue(s)** ou **Rejetée(s)**.

-   Si vous résolvez un problème et qu’ATA détecte qu’il existe encore, le problème retourne automatiquement dans la liste **Ouvert**. Si ATA détecte qu’un problème ouvert est résolu, le problème passe automatiquement à la liste **Résolu**.

-   Les alertes **Rejetée(s)** vous permettent d’indiquer à ATA que vous ne souhaitez plus vérifier un problème particulier. Par exemple, si vous recevez une alerte concernant un problème dont vous connaissez l’existence et que vous n’envisagez pas de le résoudre, vous pouvez lui affecter l’état **Rejetée(s)**. Ainsi, vous ne recevrez plus de notifications et il n’apparaîtra plus dans la liste **Ouvert**.

![Image de problèmes dans le centre d’intégrité ATA](media/ATA-Health-Issue.JPG)

## Voir aussi
- [Gestion des paramètres de la détection ATA](working-with-detection-settings.md)
- [Gestion des activités suspectes](working-with-suspicious-activities.md)
- [Consultez le forum ATA](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


