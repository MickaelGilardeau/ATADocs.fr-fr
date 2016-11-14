---
title: "Nouveautés d’ATA version 1.7 | Microsoft ATA"
description: "Répertorie les nouveautés d’ATA version 1.7, ainsi que les problèmes connus"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 10/25/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f334f9c8440e4bb0202579de220f6530d0aabad8
ms.openlocfilehash: 03a5e6a5398ffcc43e712bd4a3c2f872cd91c0b4


---

# <a name="whats-new-in-ata-version-17"></a>Nouveautés d’ATA version 1.7
Ces notes de publication fournissent des informations sur les problèmes connus de cette version d’Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-17-update"></a>Quelles sont les nouveautés d’ATA 1.7 ?
La mise à jour vers ATA 1.7 comprend des améliorations dans les domaines suivants :

-   Détections nouvelles et mises à jour

-   Contrôle d'accès en fonction du rôle

-   Prise en charge de Windows Server 2016 et Windows Server Core

-   Améliorations apportées à l’expérience utilisateur

-   Modifications mineures


### <a name="new-updated-detections"></a>Détections nouvelles et mises à jour


- **Reconnaissance à l’aide d’une énumération de services d’annuaire** Dans le cadre de la phase de reconnaissance, les pirates collectent des informations sur les entités du réseau à l’aide de différentes méthodes. L’énumération des services d’annuaire à l’aide du protocole SAM-R permet aux pirates d’obtenir la liste des utilisateurs et des groupes dans un domaine et de comprendre l’interaction entre les différentes entités. 

- **Améliorations liées à Pass-the-Hash** Pour améliorer la détection Pass-the-Hash, nous avons ajouté des modèles de comportement supplémentaires pour les modèles d’authentification d’entités. Ces modèles permettent à ATA de mettre en corrélation le comportement d’entité avec les authentifications NTLM suspectes, et de différencier les attaques Pass-the-Hash réelles du comportement de scénarios de type « faux positif ».

- **Améliorations liées à Pass-the-Ticket** Pour détecter les attaques avancées en général et les attaques Pass-the-Ticket en particulier, la corrélation entre une adresse IP et le compte d’ordinateur doit être exacte. Il s’agit d’un véritable défi dans les environnements où les adresses IP changent rapidement par conception (par exemple sur les réseaux Wi-Fi et quand plusieurs machines virtuelles partagent le même hôte). Pour relever ce défi et améliorer la précision de la détection de Pass-the-Ticket, le mécanisme de résolution de nom de réseau d’ATA a été amélioré considérablement afin de réduire les faux positifs.

- **Améliorations liées aux comportements anormaux** Dans ATA 1.7, les données d’authentification NTLM ont été ajoutées comme source de données pour les détections de comportements anormaux, fournissant aux algorithmes une couverture plus étendue du comportement d’entité sur le réseau. 

- **Améliorations liées à l’implémentation de protocoles inhabituels** ATA détecte désormais l’implémentation de protocoles inhabituels dans le protocole Kerberos, ainsi que d’autres anomalies dans le protocole NTLM. Plus spécifiquement, ces nouvelles anomalies pour Kerberos sont couramment utilisées dans les attaques de type « Over-pass-the-Hash ».


### <a name="infrastructure"></a>Infrastructure

- **Contrôle d’accès en fonction du rôle ** Fonctionnalité de contrôle d’accès en fonction du rôle (RBAC). ATA 1.7 inclut trois rôles : ATA Administrator, ATA Analyst et ATA Executive.

- **Prise en charge de Windows Server 2016 et Windows Server Core** ATA 1.7 prend en charge le déploiement de passerelles légères sur les contrôleurs de domaine exécutant Server Core pour Windows Server 2012 et Server Core pour Windows Server 2012 R2. De plus, cette version prend en charge Windows Server 2016 pour les composants Centre ATA et Passerelle ATA.

### <a name="user-experience"></a>Expérience de l'utilisateur
- **Expérience de configuration** Dans cette version, l’expérience de configuration d’ATA a été repensée pour une meilleure expérience utilisateur et pour mieux prendre en charge les environnements à plusieurs passerelles ATA. Cette version introduit également la page de mise à jour de la passerelle ATA pour une gestion plus simple et plus performante des mises à jour automatiques pour les différentes passerelles.

## <a name="known-issues"></a>Problèmes connus
Les problèmes connus de cette version sont les suivants :

### <a name="gateway-automatic-update-may-fail"></a>Risque d’échec de mise à jour automatique de passerelle
**Symptômes :** Dans les environnements avec des liaisons WAN lentes, la mise à jour de la passerelle ATA peut atteindre le délai d’expiration de mise à jour (100 secondes) et échouer.
Dans la console ATA, la passerelle ATA a l’état « Mise à jour (téléchargement du package) » pendant un laps de temps prolongé et l’opération finit par échouer.
**Solution de contournement :** Pour contourner ce problème, téléchargez le package de passerelle ATA le plus récent à partir de la console ATA et mettez à jour la passerelle ATA manuellement.

 > [!IMPORTANT]
 Le renouvellement automatique des certificats utilisés par ATA n’est pas pris en charge. L’utilisation de ces certificats peut provoquer le non-fonctionnement d’ATA lors du renouvellement automatique du certificat. 

### <a name="no-browser-support-for-jis-encoding"></a>Aucune prise en charge du navigateur pour l’encodage JIS
**Symptômes :** La console ATA peut ne pas fonctionner comme prévu sur les navigateurs utilisant l’encodage JIS **Solution de contournement :** Modifiez l’encodage du navigateur et choisissez Unicode UTF-8.
 
### <a name="dropped-port-mirror-traffic-when-using-vmware"></a>Trafic avec mise en miroir de ports ignoré lors de l’utilisation de VMware

Alertes « Trafic avec mise en miroir de ports ignoré » lors de l’utilisation de la passerelle légère sur VMware

Si vous utilisez des contrôleurs de domaine sur des machines virtuelles VMware, vous pouvez recevoir des alertes concernant le **trafic réseau avec mise en miroir de port ignoré**. Ce scénario peut se produire à cause d’une différence de configuration dans VMware. Pour éviter ces alertes, vous pouvez vérifier que les paramètres suivants sont définis sur 0 ou sont désactivés : TsoEnable, LargeSendOffload, IPv4, TSO Offload. Pensez aussi à désactiver IPv4 Giant TSO Offload. Pour plus d’informations, voir la documentation de VMware.

### <a name="automatic-gateway-update-fail-when-updating-to-17-update-1"></a>Échec de la mise à jour automatique de la passerelle lors de la mise à jour vers la version 1.7 Update 1

Quand vous mettez à jour ATA 1.7 vers ATA 1.7 Update 1, le processus de mise à jour automatique de la passerelle ATA et l’installation manuelle des passerelles à l’aide du package de passerelle peuvent ne pas fonctionner comme prévu.
Ce problème se produit si le certificat utilisé par le centre ATA a été modifié avant la mise à jour d’ATA.
Pour vérifier ce problème, passez en revue le journal **Microsoft.Tri.Gateway.Updater.log** sur la passerelle ATA et recherchez les exceptions suivantes : **System.Net.Http.HttpRequestException : Une erreur s’est produite lors de l’envoi de la demande. ---> System.Net.WebException : La connexion sous-jacente a été fermée : Une erreur inattendue s’est produite lors de l’envoi. ---> System.IdentityModel.Tokens.SecurityTokenValidationException : Échec de la validation de l’empreinte numérique du certificat**

![Bogue au niveau de la passerelle lors de la mise à jour d’ATA](media/17update_gatewaybug.png)

Pour résoudre ce problème, une fois le certificat modifié, accédez à l’emplacement suivant à partir d’une invite de commandes avec élévation de privilèges : **%ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. Ensuite, exécutez ce qui suit :

1. Mongo.exe ATA (ATA doit être en majuscules) 

2. CenterThumbprint=db.SystemProfile.find({_t:"CenterSystemProfile"}).toArray()[0].Configuration.SecretManagerConfiguration.CertificateThumbprint;

3. db.SystemProfile.update({_t:"ServiceSystemProfile"},{$set:{"Configuration.ManagementClientConfiguration.ServerCertificateThumbprint":CenterThumbprint}}, {multi: true})


## <a name="minor-changes"></a>Modifications mineures

- ATA utilise désormais OWIN au lieu d’IIS pour la console ATA.
- Si le service du centre ATA ne fonctionne pas, vous ne pourrez pas accéder à la console ATA.
- Les sous-réseaux du bail à court terme ne sont plus nécessaires en raison des modifications apportées à la résolution de nom de réseau d’ATA.

## <a name="see-also"></a>Voir aussi
[Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Mise à jour d’ATA vers la version 1.7 : guide de migration](ata-update-1.7-migration-guide.md)




<!--HONumber=Oct16_HO5-->


