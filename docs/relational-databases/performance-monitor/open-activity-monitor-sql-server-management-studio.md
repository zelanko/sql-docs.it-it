---
title: Aprire Monitoraggio attività (SSMS)
description: Informazioni su come aprire Monitoraggio attività in SQL Server Management Studio. Monitoraggio attività esegue query sull'istanza monitorata per ottenere informazioni da visualizzare.
ms.custom: seo-dt-2019
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
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 5569286a31b9897b8fcca0eafea6830593d05183
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506007"
---
# <a name="open-activity-monitor-in-sql-server-management-studio-ssms"></a>Aprire Monitoraggio attività in SQL Server Management Studio (SSMS)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
   
 Monitoraggio attività esegue query sull'istanza monitorata per ottenere informazioni per i riquadri di visualizzazione di Monitoraggio attività. Quando l'intervallo di aggiornamento viene impostato su un valore inferiore a 10 secondi, il tempo utilizzato per eseguire queste query può ridurre le prestazioni del server  
  
  
##  <a name="check-your-permissions"></a><a name="Permissions"></a> Verificare le autorizzazioni.  
 Per visualizzare l'attività effettiva, è necessaria l'autorizzazione VIEW SERVER STATE. Per visualizzare la sezione I/O dati di file di Monitoraggio attività, è necessario disporre delle autorizzazioni CREATE DATABASE, ALTER ANY DATABASE, o VIEW ANY DEFINITION oltre a VIEW SERVER STATE.  
  
 Per eseguire il comando KILL in un processo, è necessario che l'utente sia un membro del ruolo predefinito del server sysadmin o processadmin.  
  
  
## <a name="open-activity-monitor"></a>Aprire Monitoraggio attività  

### <a name="keyboard-shortcut"></a>Tasto di scelta rapida  
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
  
  
