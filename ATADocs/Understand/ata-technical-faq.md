---
title: 'Forum Aux Questions : ATA | Microsoft Docs'
description: "Fournit des réponses aux questions les plus fréquentes sur ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: f806437df3a2c581631e924798a367e5e48be6f8


---
*S’applique à : Advanced Threat Analytics version 1.7*

# <a name="ata-frequently-asked-questions"></a>Forum Aux Questions : ATA
Cet article fournit des éléments d’informations et des réponses aux questions les plus fréquentes sur ATA.


## <a name="what-should-i-do-if-the-ata-gateway-wont-start"></a>Que dois-je faire si la passerelle ATA ne démarre pas ?
Examinez l’erreur la plus récente dans le journal des erreurs actuel (où ATA est installé, sous le dossier « Logs »).
## <a name="how-can-i-test-ata"></a>Comment puis-je tester ATA ?
Vous pouvez simuler des activités suspectes (test de bout en bout) en effectuant l’une des opérations suivantes :

1.  Reconnaissance DNS à l’aide de Nslookup.exe
2.  Exécution à distance à l’aide de psexec.exe


Ce programme doit s’exécuter à distance sur le contrôleur de domaine surveillé, et non à partir de la passerelle ATA.

## <a name="how-do-i-verify-windows-event-forwarding"></a>Comment vérifier le transfert d’événements Windows ?
Vous pouvez placer le code qui suit dans un fichier, puis l’exécuter à partir d’une invite de commandes dans le répertoire **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** comme suit :

Nom de fichier ATA mongo.exe

        db.getCollectionNames().forEach(function(collection) {
        if (collection.substring(0,10)=="NtlmEvent_") {
                if (db[collection].count() > 0) {
                                  print ("Found "+db[collection].count()+" NTLM events") 
                                }
                }
        });

## <a name="does-ata-work-with-encrypted-traffic"></a>ATA prend-il en charge le trafic chiffré ?
ATA repose sur l’analyse de plusieurs protocoles réseau, ainsi que sur les événements recueillis à partir du SIEM ou par le biais de Windows Event Forwarding. Ainsi, même si le trafic chiffré n’est pas analysé (par exemple, le protocole LDAPS et IPSEC ESP), ATA continue de fonctionner et la plupart des détections ne sont pas affectées.

## <a name="does-ata-work-with-kerberos-armoring"></a>ATA fonctionne-t-il avec le blindage Kerberos ?
L’activation du blindage Kerberos, également appelé FAST (Flexible Authentication Secure Tunneling), est prise en charge par ATA, à l’exception de la détection Overpass-the-Hash qui ne fonctionne pas.
## <a name="how-many-ata-gateways-do-i-need"></a>De combien de passerelles ATA ai-je besoin ?

Le nombre de passerelles ATA dépend de la disposition de votre réseau, du volume de paquets et du volume d’événements capturés par ATA. Pour déterminer le nombre exact, consultez [Dimensionnement de passerelle légère ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning#ata-lightweight-gateway-sizing). 

## <a name="how-much-storage-do-i-need-for-ata"></a>Quelles sont les exigences imposées par ATA en matière d’espace de stockage ?
Pour chaque journée complète produisant en moyenne 1 000 paquets/s, il vous faut 0,3 Go de stockage.<br /><br />Pour plus d’informations sur le dimensionnement du centre ATA, consultez [Planification de la capacité ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).


## <a name="why-are-certain-accounts-considered-sensitive"></a>Pourquoi certains comptes sont-ils considérés comme sensibles ?
Cela arrive quand un compte est membre de certains groupes désignés comme sensibles (par exemple : « Administrateurs du domaine »).

Pour comprendre pourquoi un compte est sensible, vous pouvez examiner son appartenance au groupe pour déterminer à quels groupes sensibles il appartient. Le groupe auquel il appartient peut également être sensible en raison d’un autre groupe ; dans ce cas, répétez la procédure jusqu’à ce que vous trouviez le groupe sensible de plus haut niveau.

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-ata"></a>Comment puis-je surveiller un contrôleur de domaine virtuel à l’aide d’ATA ?
La plupart des contrôleurs de domaine virtuels peuvent être couverts par la passerelle légère ATA ; pour déterminer si celle-ci est appropriée pour votre environnement, consultez [Planification de la capacité ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).

Si un contrôleur de domaine virtuel ne peut pas être couvert par la passerelle légère ATA, vous pouvez avoir une passerelle ATA virtuelle ou physique, comme décrit dans [Configurer la mise en miroir des ports](/advanced-threat-analytics/deploy-use/configure-port-mirroring).  <br />Le moyen le plus simple consiste à configurer une passerelle ATA virtuelle sur chaque hôte où figure un contrôleur de domaine virtuel.<br />Si vos contrôleurs de domaine virtuels passent d’un hôte à l’autre, vous devez effectuer l’une des opérations suivantes :

-   Quand le contrôleur de domaine virtuel passe à un autre hôte, préconfigurez la passerelle ATA sur cet hôte pour qu’elle reçoive le trafic du contrôleur de domaine virtuel ayant récemment été déplacé.
-   Associez la passerelle ATA virtuelle au contrôleur de domaine virtuel. Ainsi, s’il est déplacé, la passerelle ATA est déplacée en même temps.
-   Certains commutateurs virtuels peuvent envoyer le trafic entre les hôtes.

## <a name="how-do-i-back-up-ata"></a>Comment puis-je sauvegarder ATA ?
Il y a deux éléments que vous devez sauvegarder :

-   Le trafic et les événements enregistrés par ATA, que vous pouvez sauvegarder à l’aide de n’importe quelle procédure de sauvegarde de base de données prise en charge. Pour plus d’informations, consultez [Gestion de la base de données ATA](/advanced-threat-analytics/deploy-use/ata-database-management). 
-   La configuration d’ATA. Elle est stockée dans la base de données et sauvegardée automatiquement toutes les heures dans le dossier **Backup** à l’emplacement de déploiement du centre ATA.  Pour plus d’informations, consultez [Gestion de la base de données ATA](https://docs.microsoft.com/advanced-threat-analytics/deploy-use/ata-database-management).
## <a name="what-can-ata-detect"></a>Que peut détecter ATA ?
ATA détecte les techniques et attaques connues, les problèmes de sécurité et les risques.
Pour obtenir la liste complète des détections fournies par ATA, consultez [Quelles sont les détections effectuées par ATA ?](ata-threats.md).

## <a name="what-kind-of-storage-do-i-need-for-ata"></a>De quel type de stockage ai-je besoin pour ATA ?
Nous vous recommandons d’utiliser un stockage rapide (les disques 7 200 tr/min ne sont pas recommandés) avec un accès disque à faible latence (inférieure à 10 ms). La configuration RAID doit accepter les charges en écriture lourdes (RAID-5/6 et leurs dérivés ne sont pas recommandés).

## <a name="how-many-nics-does-the-ata-gateway-require"></a>De combien de cartes réseau la passerelle ATA a-t-elle besoin ?
La passerelle ATA a besoin au minimum de deux cartes réseau :<br>1. Une carte réseau pour se connecter au réseau interne et au centre ATA.<br>2. Une carte réseau destinée à capturer le trafic réseau des contrôleurs de domaine par le biais de la mise en miroir des ports.<br>* Cela ne s’applique pas à la passerelle légère ATA, qui utilise en mode natif toutes les cartes réseau dont se sert le contrôleur de domaine.

## <a name="what-kind-of-integration-does-ata-have-with-siems"></a>De quelle façon ATA s’intègre-t-il aux serveurs SIEM ?
ATA bénéficie d’une intégration bidirectionnelle aux serveurs SIEM, comme suit :

1. Vous pouvez configurer ATA de façon à envoyer une alerte Syslog en cas d’activité suspecte à n’importe quel serveur SIEM utilisant le format CEF.
2. Vous pouvez configurer ATA pour recevoir des messages Syslog de chaque événement Windows associé à l’ID 4776 à partir de [ces serveurs SIEM](/advanced-threat-analytics/deploy-use/configure-event-collection#siem-support).

## <a name="can-ata-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>ATA peut-il surveiller les contrôleurs de domaine virtualisés sur votre solution IaaS ?

Oui, vous pouvez utiliser la passerelle légère ATA pour surveiller les contrôleurs de domaine qui se trouvent dans n’importe quelle solution IaaS.

## <a name="is-this-an-on-premises-or-in-cloud-offering"></a>S’agit-il d’une offre locale ou dans le cloud ?
Microsoft Advanced Threat Analytics est un produit local.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Cette offre va-t-elle faire partie d’Azure Active Directory ou du service Active Directory local ?
Cette solution est pour l’instant une offre autonome : elle ne fait partie ni d’Azure Active Directory, ni du service Active Directory local.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Est-ce que je dois écrire mes propres règles et créer un seuil/une ligne de base ?
Avec Microsoft Advanced Threat Analytics, il est inutile de créer et d’ajuster des règles, des seuils ou des lignes de base. ATA analyse les comportements des utilisateurs, appareils et ressources, ainsi que leurs relations entre eux, et détecte rapidement les activités suspectes et les attaques connues. Trois semaines après son déploiement, ATA commence à détecter les activités comportementales suspectes. Mais la détection des attaques malveillantes et des problèmes de sécurité connus est opérationnelle immédiatement après le déploiement.

## <a name="if-you-are-already-breached-will-microsoft-advanced-threat-analytics-be-able-to-identify-abnormal-behavior"></a>Si des violations de la sécurité ont déjà été constatées, Microsoft Advanced Threat Analytics est-il en mesure d’identifier des comportements anormaux ?
Oui. Même s’il est installé après une violation de la sécurité, ATA peut détecter les activités suspectes d’un pirate informatique. Non seulement ATA examine le comportement de l’utilisateur, mais il le compare aussi à celui des autres utilisateurs dans l’organigramme de sécurité de l’organisation. Si le comportement de l’attaquant est anormal pendant l’analyse initiale, il est identifié comme « aberrant ». Dans ce cas, ATA continue de signaler le comportement anormal. En outre, ATA peut détecter une activité suspecte si le pirate informatique tente de s’emparer des informations d’identification d’autres utilisateurs (comme dans le cadre d’une attaque Pass-the-Ticket) ou s’il essaie d’effectuer une exécution à distance sur l’un des contrôleurs de domaine.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>ATA analyse-t-il uniquement le trafic Active Directory ?
En plus d’analyser le trafic Active Directory à l’aide de la technologie d’inspection approfondie des paquets, ATA peut également collecter les événements pertinents issus de systèmes de gestion des informations et des événements de sécurité (SIEM) et créer des profils d’entité selon les informations des services de domaine Active Directory. ATA peut également collecter les événements contenus dans les journaux des événements si l’organisation configure le transfert du journal des événements Windows.

## <a name="what-is-port-mirroring"></a>Qu’est-ce que la mise en miroir des ports ?
Également appelée SPAN (Switched Port Analyzer), la mise en miroir des ports est une méthode de surveillance du trafic réseau. Une fois la mise en miroir des ports activée, le commutateur envoie une copie de tous les paquets réseau visibles sur un port (ou tout un VLAN) à un autre port où le paquet peut être analysé.

## <a name="does-ata-monitor-only-domain-joined-devices"></a>ATA surveille-t-il uniquement les appareils joints à un domaine ?
Non. ATA surveille tous les appareils du réseau qui effectuent des demandes d’authentification et d’autorisation auprès d’Active Directory, notamment les appareils non-Windows et les appareils mobiles.

## <a name="does-ata-monitor-computer-accounts-as-well-as-user-accounts"></a>ATA surveille-t-il les comptes d’ordinateurs et les comptes d’utilisateurs ?
Oui. Étant donné que les comptes d’ordinateurs (de même que toute autre entité) peuvent être utilisés pour effectuer des activités malveillantes, ATA surveille le comportement de tous les comptes d’ordinateurs et de toutes les autres entités dans l’environnement.

## <a name="can-ata-support-multi-domain-and-multi-forest"></a>ATA peut-il prendre en charge plusieurs domaines et plusieurs forêts ?
Microsoft Advanced Threat Analytique prend en charge les environnements à plusieurs domaines dans la même limite de forêt. S’il existe plusieurs forêts, un déploiement ATA est nécessaire pour chaque forêt.
## <a name="can-you-see-the-overall-health-of-the-deployment"></a>Puis-je examiner l’intégrité globale du déploiement ?
Oui. Vous pouvez consulter l’intégrité globale du déploiement ainsi que les problèmes spécifiques liés à la configuration, à la connectivité, etc. Dès qu’un problème se produit, vous êtes averti.


## <a name="see-also"></a>Voir aussi
- [Prérequis au déploiement d’ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Planification de la capacité d’ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Configurer la collecte d’événements](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Configuration du transfert d’événements Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#Configuring-Windows-Event-Forwarding)
- [Consultez le forum ATA !](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Jan17_HO1-->


