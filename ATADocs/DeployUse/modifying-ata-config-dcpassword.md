---
title: "Modifier la configuration ATA - Mot de passe de connectivité de domaine | Microsoft ATA"
description: "Décrit comment modifier le mot de passe de connectivité de domaine sur la passerelle ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 7b8904bcb379004b2038e6b9a14c87c3914f1e1f


---

# Modifier la configuration ATA - Mot de passe de connectivité de domaine

>[!div class="step-by-step"]
[« Certificat IIS](modifying-ata-config-iiscert.md)


## Modifier le mot de passe de connectivité de domaine
Si vous modifiez le mot de passe de connectivité de domaine, assurez-vous que le mot de passe entré est correct. Dans le cas contraire, le service de passerelle ATA cesse de fonctionner sur les passerelles ATA.

Si vous pensez que cela s’est produit, recherchez la ligne suivante dans le fichier Microsoft.Tri.Gateway-Errors.log sur la passerelle ATA :
`The supplied credential is invalid.`

Pour corriger ce problème, procédez comme suit pour mettre à jour le mot de passe de connectivité de domaine sur la passerelle ATA :

1.  Ouvrez la console ATA sur la passerelle ATA.

2.  Sélectionnez l’option des paramètres dans la barre d’outils, puis **Configuration**.

    ![Icône des paramètres de configuration ATA](media/ATA-config-icon.JPG)

3.  Sélectionnez **Général**.

    ![Image de modification du mot de passe de la passerelle ATA](media/ATA-GW-change-DC-password.JPG)

4.  Sous **Général**, modifiez le mot de passe.

5.  Cliquez sur **Enregistrer**.

6.  Après avoir modifié le mot de passe, vérifiez manuellement que le service de la passerelle ATA fonctionne sur les serveurs de la passerelle ATA.

>[!div class="step-by-step"]
[« Certificat IIS](modifying-ata-config-iiscert.md)

## Voir aussi
- [Utilisation de la console ATA](working-with-ata-console.md)
- [Installer ATA](install-ata.md)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO4-->


