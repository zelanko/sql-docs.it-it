---
description: MSSQLSERVER_17884
title: MSSQLSERVER_17884 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17884 (Database Engine error)
ms.assetid: 8d05ba05-3f71-4dc3-bd81-2ea5ac9fe843
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2f7ec5ee211f87d61b39d64c5423b2c7c6612a28
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456338"
---
# <a name="mssqlserver_17884"></a>MSSQLSERVER_17884
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
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
  
