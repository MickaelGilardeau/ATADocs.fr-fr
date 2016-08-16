---
title: "Gestion de la base de données ATA | Microsoft Advanced Threat Analytics"
description: "Procédures pour vous aider à déplacer, sauvegarder ou restaurer la base de données ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 6c0e2abe43da5351568cf8db4e6ffe6fa919d835


---

# Gestion de la base de données ATA
Si vous voulez déplacer, sauvegarder ou restaurer la base de données ATA, suivez ces procédures pour MongoDB.

## Sauvegarde de la base de données ATA
Reportez-vous à la [documentation MongoDB correspondante](http://docs.mongodb.org/manual/administration/backup/).

## Restauration de la base de données ATA
Reportez-vous à la [documentation MongoDB correspondante](http://docs.mongodb.org/manual/administration/backup/).

## Déplacement de la base de données ATA vers un autre lecteur

1.  Arrêtez le service **Microsoft Advanced Threat Analytics Center**.

2.  Arrêtez le service **MongoDB**.

3.  Ouvrez le fichier de configuration Mongo situé par défaut à l’emplacement suivant : C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Rechercher le paramètre `storage: dbPath`

4.  Déplacez le dossier indiqué dans le paramètre `dbPath` vers le nouvel emplacement.

5.  Remplacez le paramètre `dbPath` du fichier de configuration mongo par le nouveau chemin de dossier, puis enregistrez et fermez le fichier.

    ![Modifier l’image de configuration MongoDB](media/ATA-mongoDB-moveDB.png)

6.  Démarrez le service **MongoDB**.

7.  Ouvrez une invite de commande et lancez l’interpréteur de commande Mongo en exécutant `mongo.exe ATA`.

    Par défaut, le fichier mongo.exe se trouve à l’emplacement suivant : C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin

8.  Exécutez la commande suivante : `db.SystemProfiles.update( {_t: "CenterSystemProfile"} , {$set:{"Configuration.CenterDatabaseClientConfiguration.DataPath" : "<New DB Location>"}})`


    Au lieu de <New DB Location> où `&lt;New DB Location&gt;` est le nouveau chemin du dossier.

9.  Mettez à jour HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath avec le nouveau chemin du dossier.

9. Démarrez le service **Microsoft Advanced Threat Analytics Center**.

## Voir aussi
- [Architecture d’ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Conditions préalables au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Consultez le forum ATA](https://social.technet.microsoft.com/Forums/security/
- home?forum=mata)




<!--HONumber=Jun16_HO4-->


