---
title: "Utilisation de groupes de rôles - Terminé | Microsoft Docs"
description: "Explique comment utiliser des groupes de rôles ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/23/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 3ba53b7b1c34359f00da9fc9717496cfc7d4271d
ms.openlocfilehash: b49906802bf0cae86178cbdcc34e4178691d39e4


---

*S’applique à : Advanced Threat Analytics version 1.7*




# <a name="ata-role-groups"></a>Groupes de rôles ATA

Les groupes de rôles permettent de gérer l’accès pour ATA. À l’aide des groupes de rôles, vous pouvez séparer les tâches au sein de votre équipe de sécurité et accorder uniquement le nombre d’accès dont les utilisateurs ont besoin pour effectuer leur travail. Cet article explique ce qu’est la gestion des accès et l’autorisation de rôle ATA, puis vous aide à configurer des groupes de rôles dans ATA.
## <a name="types-of-ata-role-groups"></a>Types de groupes de rôles ATA 

ATA présente 3 types de groupe de rôles : ATA Administrators, ATA Users et ATA Viewers. Le tableau suivant décrit le type d’accès dans ATA disponible par rôle. En fonction du rôle que vous attribuez, différents écrans et options de menu dans ATA ne seront pas disponibles, comme suit :

|Activité |Administrateurs Microsoft Advanced Threat Analytics|Utilisateurs Microsoft Advanced Threat Analytics|Observateurs Microsoft Advanced Threat Analytics|
|----|----|----|----|
|Se connecter|Disponible|Disponible|Disponible|
|Fournir des commentaires sur les activités suspectes|Disponible|Disponible|Non disponible|
|Modifier l’état des activités suspectes|Disponible|Disponible|Non disponible|
|Partager/exporter une activité suspecte par e-mail/via un lien|Disponible|Disponible|Non disponible|
|Ajouter/modifier des notes pour les activités suspectes|Disponible|Disponible|Non disponible|
|Modifier l’état de la surveillance des alertes|Disponible|Disponible|Non disponible|
|Mettre à jour la configuration ATA|Disponible|Non disponible|Non disponible|
|Passerelle – Ajouter|Disponible|Non disponible|Non disponible|
|Passerelle – Supprimer |Disponible|Non disponible|Non disponible|
|Contrôleur de domaine surveillé - Ajouter |Disponible|Non disponible|Non disponible|
|Contrôleur de domaine surveillé – Supprimer|Disponible|Non disponible|Non disponible|

Quand les utilisateurs tentent d’accéder à une page qui n’est pas disponible pour leur groupe de rôles, ils sont redirigés vers la page ATA d’accès non autorisé. 

## <a name="add-remove-users---ata-role-groups"></a>Ajouter \ supprimer des utilisateurs - Groupes de rôles ATA 

ATA utilise les groupes Windows locaux comme base pour les groupes de rôles. Pour ajouter ou supprimer des utilisateurs, utilisez la console MMC **Utilisateurs et groupes locaux** (Lusrmgr.msc). Sur un ordinateur joint à un domaine, vous pouvez ajouter des comptes de domaine et des comptes locaux. 




<!--HONumber=Nov16_HO4-->


