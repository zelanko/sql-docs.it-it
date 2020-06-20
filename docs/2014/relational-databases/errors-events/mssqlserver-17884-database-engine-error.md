---
title: MSSQLSERVER_17884 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17884 (Database Engine error)
ms.assetid: 8d05ba05-3f71-4dc3-bd81-2ea5ac9fe843
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bd5beca2a7dfd20afbf9eff196d89452ef3533d2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967776"
---
# <a name="mssqlserver_17884"></a>MSSQLSERVER_17884
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|17884|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SRV_SCHEDULER_DEADLOCK|  
|Testo del messaggio|Nessun thread di lavoro ha prelevato nuove query assegnate al processo nel nodo % negli ultimi %d secondi. La situazione potrebbe essere causata da query bloccate o con esecuzione prolungata che possono peggiorare i tempi di risposta del client. Utilizzare l'opzione di configurazione "max worker thread" per aumentare il numero di thread consentiti oppure ottimizzare le query in esecuzione.  Utilizzo processo SQL: %d%%. Inattività del sistema: %d%%.|  
  
## <a name="explanation"></a>Spiegazione  
 Non è presente alcun segnale relativo allo stato di avanzamento in alcuna utilità di pianificazione. Questa situazione potrebbe essere causata da deadlock per cui nessun thread può avanzare e/o nessun lavoro può essere scelto ed elaborato. Se l'utilizzo del processo è basso, gli altri processi presenti nel computer potrebbero provocare l'esaurimento delle risorse della CPU relative ai processi del server.  
  
## <a name="user-action"></a>Azione dell'utente  
 Determinare il motivo del blocco e del mancato avanzamento e risolvere di conseguenza la situazione. Se l'utilizzo del processo è basso, controllare il carico nel sistema provocato dagli altri processi.  
  
  
