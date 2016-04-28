---
# required metadata

title: Configurer la collecte d’événements | Microsoft Advanced Threat Analytics
description: Décrit les options de configuration disponibles pour collecter des événements avec ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Configurer la collecte d’événements
Pour améliorer la détection des attaques Pass-the-Hash, ATA doit accéder à l’événement associé à l’ID 4776 du journal des événements Windows. Les événements peuvent être transférés à la passerelle ATA de deux manières : soit en configurant la passerelle ATA de façon à écouter les événements SIEM, soit en [configurant le transfert d’événements Windows](#configuring-windows-event-forwarding).

## Collecte d’événements
Outre la collecte et l’analyse du trafic réseau à destination et en provenance des contrôleurs de domaine, ATA peut utiliser l’événement Windows 4776 pour optimiser la détection d’attaques Pass-the-Hash. Vous pouvez soit recevoir cet événement de votre serveur SIEM, soit définir le transfert d’événements Windows à partir de votre contrôleur de domaine. Les événements collectés fournissent à ATA des informations supplémentaires qui ne sont pas accessibles par le biais du trafic réseau du contrôleur de domaine.

### SIEM/Syslog
Pour qu’ATA puisse consommer des données provenant d’un serveur Syslog, vous devez effectuer les opérations suivantes :

-   Configurez l’un de vos serveurs de passerelle ATA de façon à écouter et à accepter les événements transférés à partir du serveur SIEM/Sylog.

-   Configurez votre serveur SIEM/Syslog de façon à transférer des événements spécifiques à la passerelle ATA.

> [!IMPORTANT]
> -   Ne transférez pas toutes les données Syslog vers la passerelle ATA.
> -   ATA prend en charge le trafic UDP provenant du serveur SIEM/Syslog.

Pour plus d’informations sur la façon de configurer le transfert d’événements spécifiques vers un autre serveur, consultez la documentation produit de votre serveur SIEM/Syslog. Pour plus d’informations sur les événements transférés vers ATA, consultez [Configurer la collecte d’événements](configure-event-collection.md).

### Transfert d’événements Windows
Si vous n’utilisez pas un serveur SIEM/Syslog, vous pouvez configurer vos contrôleurs de domaine Windows de façon à transférer l’événement Windows associé à l’ID 4776 pour qu’il soit collecté et analysé par ATA. L’événement Windows associé à l’ID 4776 fournit des données relatives aux authentifications NTLM.

## Configuration de la passerelle ATA pour écouter les événements SIEM

1.  Dans Configuration de la passerelle ATA, activez le protocole **UDP de l’écouteur Syslog**.

    Définissez l’adresse IP d’écoute comme indiqué dans l’image ci-dessous. Le port par défaut est 514.

    ![Image de l’activation du protocole UDP de l’écouteur syslog](media/ATA-enable-siem-forward-events.png)

2.  Configurez votre serveur SIEM ou Syslog de façon à transférer l’événement Windows associé à l’ID 4776 vers l’adresse IP sélectionnée ci-dessus. Pour plus d’informations sur la configuration de votre serveur SIEM, consultez l’aide en ligne de SIEM ou explorez les options de support technique à votre disposition pour obtenir les formats à respecter pour chaque serveur SIEM.

### Prise en charge de SIEM
ATA prend en charge les événements SIEM aux formats suivants :

#### RSA Security Analytics
&lt;Syslog Header&gt;RsaSA\n2015-May-19 09:07:09\n4776\nMicrosoft-Windows-Security-Auditing\nSecurity\XXXXX.subDomain.domain.org.il\nYYYYY$\nMMMMM \n0x0

-   L’en-tête syslog est facultatif.

-   Le séparateur de caractère « \n » est obligatoire entre tous les champs.

-   Les champs, dans l’ordre, sont les suivants :

    1.  Constante RsaSA (doit être indiquée).

    2.  Horodateur de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodateur de l’arrivée au serveur SIEM ou de l’envoi à ATA). De préférence avec une précision de l’ordre de la milliseconde (ceci est très important).

    3.  ID de l’événement Windows.

    4.  Nom du fournisseur d’événements Windows.

    5.  Nom du journal des événements Windows.

    6.  Nom de l’ordinateur recevant l’événement (ici, le contrôleur de domaine).

    7.  Nom de l’utilisateur qui s’authentifie.

    8.  Nom de l’hôte source.

    9. Code de résultat de NTLM.

-   L’ordre est important, et rien d’autre ne doit figurer dans le message.

#### HP Arcsight
CEF:0|Microsoft|Microsoft Windows||Microsoft-Windows-Security-Auditing:4776|Le contrôleur de domaine a tenté de valider les informations d’identification d’un compte.|Low| externalId=4776 cat=Security rt=1426218619000 shost=KKKKKK dhost=YYYYYY.subDomain.domain.com duser=XXXXXX cs2=Security cs3=Microsoft-Windows-Security-Auditing cs4=0x0 cs3Label=EventSource cs4Label=Reason or Error Code

-   Doit être conforme à la définition du protocole.

-   Aucun en-tête syslog.

-   La partie en-tête, séparée par une barre verticale, doit exister (comme indiqué dans le protocole).

-   Les clés suivantes dans la partie _Extension_ doivent être présentes dans l’événement :

    -   externalId = ID de l’événement Windows.

    -   rt = horodateur de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodateur de l’arrivée au serveur SIEM ou de l’envoi à Microsoft). De préférence avec une précision de l’ordre de la milliseconde (ceci est très important).

    -   cat = nom du journal des événements Windows.

    -   shost = nom de l’hôte source.

    -   dhost = nom de l’ordinateur recevant l’événement (ici, le contrôleur de domaine).

    -   duser = utilisateur qui s’authentifie.

-   L’ordre de la partie _Extension_ n’est pas important.

-   Vous devez avoir une clé personnalisée et un libellé dé clé pour les deux champs suivants :

    -   « EventSource »

    -   « Reason or Error Code » = code de résultat de NTLM

#### Splunk
&lt;Syslog Header&gt;\r\nEventCode=4776\r\nLogfile=Security\r\nSourceName=Microsoft-Windows-Security-Auditing\r\nTimeGenerated=20150310132717.784882-000\r\ComputerName=YYYYY\r\nMessage=

L’ordinateur a tenté de valider les informations d’identification d’un compte.

Package d’authentification : MICROSOFT_AUTHENTICATION_PACKAGE_V1_0

Compte d’ouverture de session : Administrateur

Station de travail source : SIEM

Code d’erreur : 0x0

-   L’en-tête syslog est facultatif.

-   Le séparateur de caractère « \r\n » est utilisé entre tous les champs obligatoires.

-   Les champs sont au format clé = valeur.

-   Les clés suivantes doivent exister et avoir une valeur :

    -   EventCode = ID de l’événement Windows.

    -   Logfile = nom du journal des événements Windows.

    -   SourceName = nom du fournisseur d’événements Windows.

    -   TimeGenerated = horodateur de l’événement réel (vérifiez qu’il ne s’agit pas de l’horodateur de l’arrivée au serveur SIEM ou de l’envoi à ATA). Le format doit être aaaaMMjjHHmmss.FFFFFF, avec de préférence une précision de l’ordre de la milliseconde (ceci est très important).

    -   ComputerName = nom de l’hôte source.

    -   Message = texte de l’événement Windows d’origine.

-   La clé et la valeur du message DOIVENT figurer en dernier.

-   L’ordre n’est pas important pour les paires clé=valeur.

## Configuration du transfert d’événements Windows
Si vous ne disposez pas d’un serveur SIEM, vous pouvez configurer vos contrôleurs de domaine de façon à transférer directement l’événement Windows associé à l’ID 4776 vers l’une de vos passerelles ATA.

1.  Utilisez un compte de domaine disposant de privilèges d’administrateur pour vous connecter à l’ensemble des contrôleurs de domaine et des machines où résident vos passerelles ATA.
2. Vérifiez que les contrôleurs de domaine et passerelles ATA auxquels vous vous connectez sont tous joints au même domaine.
3.  Sur chaque contrôleur de domaine, tapez ce qui suit à une invite de commandes avec élévation de privilèges :
```
winrm quickconfig
```
4.  Sur la passerelle ATA, tapez ce qui suit à une invite de commandes avec élévation de privilèges :
```
wecutil qc
```
5.  Sur chaque contrôleur de domaine, dans **Utilisateurs et ordinateurs Active Directory	**, accédez au dossier **Builtin** et double-cliquez sur le groupe **Lecteurs des journaux d’événements**.
![wef_ad, lecteurs des journaux d’événements](media/wef_ad_eventlogreaders.png)
Cliquez dessus avec le bouton droit, puis sélectionnez **Propriétés**. Sous l’onglet **Membres**, ajoutez le compte d’ordinateur de chaque passerelle ATA.
![wef_ad, menu contextuel du lecteur des journaux d’événements](media/wef_ad-event-log-reader-popup.png)
6.  Sur la passerelle ATA, ouvrez l’Observateur d’événements et cliquez avec le bouton droit sur **Abonnements**, puis sélectionnez **Créer un abonnement**.  

    a.  Sous **Type d’abonnement et ordinateurs sources**, cliquez sur **Sélectionner les ordinateurs**. Ajoutez les contrôleurs de domaine, puis testez la connectivité.
    ![wef, propriétés de l’abonnement](media/wef_subscription-prop.png)

    b.  Sous **Événements à recueillir**, cliquez sur **Sélectionner des événements**. Sélectionnez **Par journal**, puis faites défiler la liste pour sélectionner **Sécurité**. Ensuite, dans **Inclut/exclut des ID d’événements**, tapez **4776**.
    ![wef_4776](media/wef_4776.png)

    c. Sous **Modifier un compte d’utilisateur ou configurer les paramètres avancés**, cliquez sur **Avancé**.
        En regard de **Protocole**, sélectionnez **HTTP**, puis affectez au **Port** la valeur **5985**.
    ![wef_http](media/wef_http.png)

 7. [Facultatif] Si vous souhaitez un intervalle d’interrogation plus court, définissez une pulsation d’abonnement de 5 secondes.

```
wecutil ss <CollectionName>/cm:custom
wecutil ss <CollectionName> /hi:5000
```

8. Dans la page de configuration de la passerelle ATA, activez **Collecte des transferts d’événements Windows**.

    > [!NOTE]
    > Quand vous activez ce paramètre, la passerelle ATA recherche dans le journal des événements transférés les événements Windows qui ont été transférés vers la passerelle à partir des contrôleurs de domaine.

Pour plus d’informations, consultez [Configurer les ordinateurs pour transférer et collecter des événements](https://technet.microsoft.com/en-us/library/cc748890).

## Voir aussi
- [Installer ATA](/advanced-threat-analytics/DeployUse/install-ata)
- [Pour obtenir de l’aide, consultez notre forum.](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


