---
title: SQL Server destinazioni degli eventi estesi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events]
- extended events [SQL Server], targets
ms.assetid: e281684c-40d1-4cf9-a0d4-7ea1ecffa384
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 75270f5ce03de820828da65c765044a7dafdcb8f
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928862"
---
# <a name="sql-server-extended-events-targets"></a>SQL Server Extended Events Targets
  Le destinazioni degli eventi estesi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sono consumer di eventi. Le destinazioni possono scrivere in un file, archiviare dati evento in un buffer di memoria o dati degli eventi di aggregazione. Le destinazioni possono elaborare i dati in modo sincrono o asincrono.  
  
 La progettazione degli eventi estesi assicura che per le destinazioni sia garantita la ricezione degli eventi solo una volta per sessione.  
  
 Gli eventi estesi forniscono le seguenti destinazioni che è possibile utilizzare per una sessione relativa ad essi:  
  
-   [Contatore eventi](../../2014/database-engine/event-counter-target.md)  
  
     Conta tutti gli eventi specificati che si verificano durante una sessione di eventi estesi. Consente di ottenere informazioni sulle funzionalità del carico di lavoro senza aggiungere l'overhead di un'intera raccolta di eventi. Si tratta di una destinazione sincrona.  
  
-   [File di evento](../../2014/database-engine/event-file-target.md)  
  
     Consente di scrivere l'output della sessione eventi restituito dai buffer di memoria completi su disco. Si tratta di una destinazione asincrona.  
  
-   [Abbinamento degli eventi](../../2014/database-engine/event-pairing-target.md)  
  
     Molti tipi di eventi si verificano a coppie, ad esempio le acquisizioni e i rilasci del blocco. Consente di determinare quando un evento associato specificato non si verifica in un set corrispondente. Si tratta di una destinazione asincrona.  
  
-   [Analisi eventi per Windows (ETW)](../relational-databases/extended-events/event-tracing-for-windows-target.md)  
  
     Consente di correlare gli eventi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con dati evento del sistema operativo Windows o dell'applicazione. Si tratta di una destinazione sincrona.  
  
-   [Istogramma](../../2014/database-engine/histogram-target.md)  
  
     Consente di calcolare il numero di volte in cui si verifica un evento specificato, in base a un'azione o una colonna di evento specificata. Si tratta di una destinazione asincrona.  
  
-   [Buffer circolare](../../2014/database-engine/ring-buffer-target.md)  
  
     Consente di mantenere i dati degli eventi in memoria secondo una modalità FIFO o secondo una modalità FIFO basata sul tipo di evento. Si tratta di una destinazione asincrona.  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../relational-databases/extended-events/extended-events.md)   
 [SQL Server pacchetti di eventi estesi](../relational-databases/extended-events/sql-server-extended-events-packages.md)   
 [SQL Server sessioni eventi estesi](../relational-databases/extended-events/sql-server-extended-events-sessions.md)   
 [Motore degli eventi estesi di SQL Server](../relational-databases/extended-events/sql-server-extended-events-engine.md)  
  
  
