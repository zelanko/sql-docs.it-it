---
title: Aprire Monitoraggio attività (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server], setting the refresh interval
- refresh interval for Activity Monitor
- Activity Monitor [SQL Server], opening
- opening Activity Monitor
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0d1c0312acfcd2e5dbb17d740fe2659cb8c91bbe
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52755514"
---
# <a name="open-activity-monitor-sql-server-management-studio"></a>Aprire Monitoraggio attività (SQL Server Management Studio)
  In questo argomento viene descritto come aprire Monitoraggio attività per ottenere informazioni sui processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e sul modo in cui questi processi influiscono sull'istanza corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Viene inoltre descritto come impostare l'intervallo di aggiornamento del Monitoraggio attività.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per aprire l'utilizzo di Monitoraggio attività:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
-   **Per impostare l'intervallo di aggiornamento usando:**  [SQL Server Management Studio](#Refresh)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
 Monitoraggio attività esegue query sull'istanza monitorata per ottenere informazioni per i riquadri di visualizzazione di Monitoraggio attività. Quando l'intervallo di aggiornamento viene impostato su un valore inferiore a 10 secondi, il tempo utilizzato per eseguire queste query può ridurre le prestazioni del server  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Per visualizzare Monitoraggio attività, è necessario che l'utente disponga dell'autorizzazione VIEW SERVER STATE. Per visualizzare la sezione I/O dati di file di Monitoraggio attività, è necessario disporre delle autorizzazioni CREATE DATABASE, ALTER ANY DATABASE, o VIEW ANY DEFINITION oltre a VIEW SERVER STATE.  
  
 Per eseguire il comando KILL in un processo, è necessario che l'utente sia un membro del ruolo predefinito del server sysadmin o processadmin.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-open-activity-monitor-in-sql-server-management-studio"></a>Per aprire Monitoraggio attività in SQL Server Management Studio  
  
1.  Nella barra degli strumenti standard di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fare clic su **Monitoraggio attività**.  
  
2.  Nella finestra di dialogo **Connetti al server** selezionare il nome del server e la modalità di autenticazione, quindi fare clic su **Connetti**.  
  
 È inoltre possibile aprire Monitoraggio attività in qualsiasi momento premendo CTRL+ALT A.  
  
#### <a name="to-open-activity-monitor-in-object-explorer"></a>Per aprire Monitoraggio attività in Esplora oggetti  
  
-   In Esplora oggetti fare clic con il pulsante destro del mouse sul nome dell'istanza, quindi scegliere **Monitoraggio attività**.  
  
#### <a name="to-open-activity-monitor-when-opening-sql-server-management-studio"></a>Per aprire Monitoraggio attività all'apertura di SQL Server Management Studio  
  
1.  Scegliere **Opzioni** dal menu **Strumenti**.  
  
2.  Nella finestra di dialogo **Opzioni** espandere **Ambiente**, quindi selezionare **Generale**.  
  
3.  Nella casella **All'avvio** selezionare **Apri Esplora oggetti e Monitoraggio attività**.  
  
4.  Per attivare le modifiche, chiudere e riaprire [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
###  <a name="Refresh"></a> Per impostare l'intervallo di aggiornamento di Monitoraggio attività  
  
-   Aprire il Monitoraggio attività.  
  
-   Fare clic con il pulsante destro del mouse su **Panoramica**, selezionare **Intervallo di aggiornamento**, quindi selezionare l'intervallo con cui Monitoraggio attività deve ottenere nuove informazioni sull'istanza.  
  
  
