---
title: Aprire Monitoraggio attività (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Activity Monitor [SQL Server], setting the refresh interval
- refresh interval for Activity Monitor
- Activity Monitor [SQL Server], opening
- opening Activity Monitor
ms.assetid: 0a6eeb16-f02b-479d-9a60-543e40ebf46b
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 9d7bccf89e8f2043413838e9f55fd8bd4e74dc5f
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907224"
---
# <a name="open-activity-monitor-sql-server-management-studio"></a>Aprire Monitoraggio attività (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
   
 Monitoraggio attività esegue query sull'istanza monitorata per ottenere informazioni per i riquadri di visualizzazione di Monitoraggio attività. Quando l'intervallo di aggiornamento viene impostato su un valore inferiore a 10 secondi, il tempo utilizzato per eseguire queste query può ridurre le prestazioni del server  
  
  
##  <a name="Permissions"></a> Verificare le autorizzazioni.  
 Per visualizzare l'attività effettiva, è necessaria l'autorizzazione VIEW SERVER STATE. Per visualizzare la sezione I/O dati di file di Monitoraggio attività, è necessario disporre delle autorizzazioni CREATE DATABASE, ALTER ANY DATABASE, o VIEW ANY DEFINITION oltre a VIEW SERVER STATE.  
  
 Per eseguire il comando KILL in un processo, è necessario che l'utente sia un membro del ruolo predefinito del server sysadmin o processadmin.  
  
  
## <a name="open-activity-monitor"></a>Aprire Monitoraggio attività  

### <a name="keyboard-shortcut"></a>Scelta rapida da tastiera  
 - Digitare **CTRL+ALT+A** per aprire Monitoraggio attività in qualsiasi momento.

 >**Hint.** Passare il mouse su un'icona di SQL Server Management Studio per ottenere informazioni su che cos'è e sulla scelta rapida da tastiera che la attiva.

### <a name="toolbar"></a>Barra degli strumenti

Nella barra degli strumenti Standard fare clic sull'icona **Monitoraggio attività** . L'icona di trova al centro, subito a destra dei pulsanti di annullamento/ripristino.
![Activity_Monitor_icon](../../relational-databases/performance-monitor/media/activity-monitor-icon.png)  
  
Completare la finestra di dialogo **Connetti al server** se non si è già connessi a un'istanza di SQL Server da monitorare.
  
## <a name="launch-activity-monitor-and-object-explorer-on-startup"></a>Aprire Esplora oggetti e Monitoraggio attività all'avvio
  
1.  Dal menu **Strumenti** scegliere **Opzioni**.  
  
2.  Nella finestra di dialogo **Opzioni** espandere **Ambiente**, quindi selezionare **Avvio**.  
  
3.  Nell'elenco a discesa **All'avvio** selezionare **Apri Esplora oggetti e Monitoraggio attività**.  

4.  Fare clic su **OK**.

![open_object_explorer](../../relational-databases/performance-monitor/media/open-object-explorer.png)
  
  
## <a name="set-the-activity-monitor-refresh-interval"></a>Impostare l'intervallo di aggiornamento di Monitoraggio attività  
  
1.   Aprire il Monitoraggio attività.  
  
2.   Fare clic con il pulsante destro del mouse su **Panoramica**, selezionare **Intervallo di aggiornamento**, quindi selezionare l'intervallo con cui Monitoraggio attività deve ottenere nuove informazioni sull'istanza.  
  
  
