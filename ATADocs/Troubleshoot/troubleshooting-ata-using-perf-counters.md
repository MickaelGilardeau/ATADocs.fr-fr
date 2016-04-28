---
# required metadata

title: Résolution des problèmes liés à ATA à l’aide des compteurs de performances | Microsoft Advanced Threat Analytics
description: Explique comment utiliser les compteurs de performances pour résoudre les problèmes liés à ATA
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: df162a62-f273-4465-9887-94271f5000d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Résolution des problèmes liés à ATA à l’aide des compteurs de performances
Les compteurs de performances ATA vous permettent de savoir si les composants ATA s’exécutent correctement.

**Processus des composants ATA** :

1.  Quand un composant atteint sa taille maximale, il empêche le composant qui le précède de lui envoyer des entités supplémentaires.

2.  En conséquence, le composant précédent augmente **sa propre** taille jusqu’à empêcher le composant qui le précède d’envoyer des entités.

3.  Cette situation se produit jusqu’au composant NetworkListener initial qui supprime le trafic quand il ne peut plus transférer d’entités.

    Cela signifie que pour remédier à la réaction en chaîne qui entraîne la suppression du trafic, vous devez résoudre le problème qui se trouve en bout de chaîne.
    Pour comprendre le flux des composants ATA internes, voir [Architecture ATA](/advanced-threat-analytics/Understand/ata-architecture).

## Compteurs de performances de la passerelle ATA
Vous pouvez observer l’état des performances de la passerelle ATA en temps réel en ajoutant des compteurs de performances à la passerelle ATA.
Pour cela, ouvrez l’Analyseur de performances, puis ajoutez tous les compteurs à la passerelle ATA. Le nom de l’objet de compteur de performances est « Microsoft ATA Gateway ».

![Image de l’ajout du compteur de performances](media/ATA-performance-counters.png)

Voici la liste des principaux compteurs de passerelle ATA :

|Compteur|Description|Seuil|Résolution des problèmes|
|-----------|---------------|-------------|-------------------|
|Messages de l’analyseur capturés par NetworkListener/s|Quantité de trafic traitée par la passerelle ATA chaque seconde.|Aucun seuil|Aide à comprendre la quantité de trafic qui est analysée par la passerelle ATA.|
|Messages capturés par NetworkListener supprimés/s|Quantité de trafic supprimée par la passerelle ATA chaque seconde.|Ce nombre doit toujours être égal à zéro (de rares suppressions en rafales sont acceptables).|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
|Mémoires tampons ETW en temps réel capturées par NetworkListener supprimées/s|Quantité de trafic supprimée par la passerelle ATA chaque seconde.|Ce nombre doit toujours être égal à zéro (de rares suppressions en rafales sont acceptables).|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
|Mémoires tampons du journal ETW capturées par NetworkListener supprimées/s|Quantité de trafic supprimée par la passerelle ATA chaque seconde.|Ce nombre doit toujours être égal à zéro (de rares suppressions en rafales sont acceptables).|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
|Événements ETW capturés par NetworkListener supprimés/s|Quantité de trafic supprimée par la passerelle ATA chaque seconde.|Ce nombre doit toujours être égal à zéro (de rares suppressions en rafales sont acceptables).|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
|Taille des blocs de données de messages de NetworkActivityTranslator|Quantité de trafic mise en file d’attente pour la traduction en activités réseau.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 100 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
|Taille des blocs des activités EntityResolver|Quantité d’activités réseau en attente de résolution.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 10 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
|Taille des blocs de lots d’entités EntitySender|Quantité d’activités réseau en attente d’envoi vers le centre ATA.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 1 000 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
|Temps d’envoi des lots EntitySender|Durée nécessaire pour envoyer le dernier lot.|Doit être inférieur à 1 000 millisecondes dans la plupart des cas|Vérifiez la présence de problèmes réseau entre la passerelle ATA et le centre ATA.|

> [!NOTE]
> -   Les valeurs temporelles des compteurs sont exprimées en millisecondes.
> -   Il est parfois plus pratique de surveiller tous les compteurs en même temps à l’aide du graphique « Rapport » (par exemple : surveillance en temps réel de l’ensemble des compteurs)

## Compteurs de performances du centre ATA
Vous pouvez observer l’état des performances du centre ATA en temps réel en ajoutant des compteurs de performances au centre ATA.

Pour cela, ouvrez l’Analyseur de performances, puis ajoutez tous les compteurs au centre ATA. Le nom de l’objet de compteur de performances est « Microsoft ATA Center ».

![Ajout de compteurs de performances au centre ATA](media/ATA-Gateway-perf-counters.png)

Voici la liste des principaux compteurs du centre ATA :

|Compteur|Description|Seuil|Résolution des problèmes|
|-----------|---------------|-------------|-------------------|
|Taille des blocs de lots d’entités EntityReceiver|Nombre de lots d’entités mis en file d’attente par le centre ATA.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 100)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener.  Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
|Taille des blocs d’activités réseau NetworkActivityProcessor|Nombre d’activités réseau en attente de traitement.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 10 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
|Taille des blocs d’activités réseau EntityProfiler|Nombre d’activités réseau en attente de profilage.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 10 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
|Taille des blocs CenterDatabaseClient&#42;|Nombre d’activités réseau d’un type spécifique en attente d’écriture dans la base de données.|Doit être inférieur à la valeur maximale de -1 (valeur maximale par défaut : 50 000)|Vérifiez si un composant a atteint sa taille maximale et bloque les composants qui le précèdent jusqu’à NetworkListener. Reportez-vous à **Processus des composants ATA** ci-dessus.<br /><br />Vérifiez qu’il n’existe aucun problème avec le processeur ou la mémoire.|
|Durée de détection par DetectionEngine|Durée totale du dernier cycle complet de détections déterministes.|Doit être inférieur à 900 000 (15 minutes)|Vérifiez qu’il n’existe aucun problème avec l’unité centrale, la mémoire ou le stockage.|

> [!NOTE]
> -   Les valeurs temporelles des compteurs sont exprimées en millisecondes.
> -   Il est parfois plus pratique de surveiller tous les compteurs en même temps à l’aide du graphique « Rapport » (par exemple : surveillance en temps réel de l’ensemble des compteurs)

Voici la liste des principaux compteurs de système d’exploitation :

|Compteur|Description|Seuil|Résolution des problèmes|
|-----------|---------------|-------------|-------------------|
|Processeur(_Total)\% de temps processeur|Durée (en pourcentage) que le processeur met pour exécuter des threads actifs.|Inférieur à 80 % en moyenne|Vérifiez si l’un des processus prend beaucoup plus de temps processeur qu’il ne devrait.<br /><br />Ajoutez des processeurs.<br /><br />Réduisez la quantité de trafic sur chaque serveur.<br /><br />Le compteur « Processeur(_Total)\% de temps processeur » peut être moins précis sur les serveurs virtuels. Dans ce cas, le moyen le plus précis de mesurer le manque de puissance du processeur est d’utiliser le compteur « System\Longueur de la file du processeur ».|
|Système\Commutateurs de contexte/s|Taux combiné auquel tous les processeurs commutent d’un thread à l’autre.|Inférieur à 5 000 cœurs&#42; (cœurs physiques)|Vérifiez si l’un des processus prend beaucoup plus de temps processeur qu’il ne devrait.<br /><br />Ajoutez des processeurs.<br /><br />Réduisez la quantité de trafic sur chaque serveur.<br /><br />Le compteur « Processeur(_Total)\% de temps processeur » peut être moins précis sur les serveurs virtuels. Dans ce cas, le moyen le plus précis de mesurer le manque de puissance du processeur est d’utiliser le compteur « System\Longueur de la file du processeur ».|
|Système\Longueur de la file du processeur|Nombre de threads prêts à être exécutés et en attente de planification.|Inférieur à 5 cœurs&#42; (cœurs physiques)|Vérifiez si l’un des processus prend beaucoup plus de temps processeur qu’il ne devrait.<br /><br />Ajoutez des processeurs.<br /><br />Réduisez la quantité de trafic sur chaque serveur.<br /><br />Le compteur « Processeur(_Total)\% de temps processeur » peut être moins précis sur les serveurs virtuels. Dans ce cas, le moyen le plus précis de mesurer le manque de puissance du processeur est d’utiliser le compteur « System\Longueur de la file du processeur ».|
|Mémoire\Mo disponibles|Quantité de mémoire physique (RAM) disponible pour l’allocation.|Doit être supérieur à 512|Vérifiez si l’un des processus prend beaucoup plus de mémoire physique qu’il ne devrait.<br /><br />Augmentez la quantité de mémoire physique.<br /><br />Réduisez la quantité de trafic sur chaque serveur.|
|LogicalDisk(&#42;)\Moy. disque s/lecture|Latence moyenne de lecture des données à partir du disque (vous devez choisir le lecteur de base de données comme instance).|Doit être inférieur à 10 millisecondes|Vérifiez si l’un des processus utilise le lecteur de la base de données plus qu’il ne devrait.<br /><br />Consultez l’équipe ou le fournisseur chargé du stockage pour savoir si ce lecteur peut fournir la charge de travail actuelle avec une latence inférieure à 10 ms. La charge de travail actuelle peut être déterminée à l’aide des compteurs d’utilisation du disque.|
|LogicalDisk(&#42;)\Moy. disque s/écriture|Latence moyenne d’écriture des données sur le disque (vous devez choisir le lecteur de base de données comme instance).|Doit être inférieur à 10 millisecondes|Vérifiez si l’un des processus utilise le lecteur de la base de données plus qu’il ne devrait.<br /><br />Consultez l’équipe ou le fournisseur chargé du stockage pour savoir si ce lecteur peut fournir la charge de travail actuelle avec une latence inférieure à 10 ms. La charge de travail actuelle peut être déterminée à l’aide des compteurs d’utilisation du disque.|
|\LogicalDisk(&#42;)\Lectures disque/s|Taux d’opérations de lecture sur le disque.|Aucun seuil|Les compteurs d’utilisation du disque peuvent apporter des informations utiles à la résolution des problèmes de latence de stockage.|
|\LogicalDisk(&#42;)\Octets de lecture disque/s|Nombre d’octets lus par seconde sur le disque.|Aucun seuil|Les compteurs d’utilisation du disque peuvent apporter des informations utiles à la résolution des problèmes de latence de stockage.|
|\LogicalDisk(&#42;)\Écritures disque/s|Taux d’opérations d’écriture sur le disque.|Aucun seuil|Compteurs d’utilisation du disque (peuvent apporter des informations utiles à la résolution des problèmes de latence de stockage).|
|\LogicalDisk(&#42;)\Octets d’écriture disque/s|Nombre d’octets écrits par seconde sur le disque.|Aucun seuil|Les compteurs d’utilisation du disque peuvent apporter des informations utiles à la résolution des problèmes de latence de stockage.|


<!--HONumber=Apr16_HO2-->


