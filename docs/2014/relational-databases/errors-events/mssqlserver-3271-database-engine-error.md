---
title: MSSQLSERVER_3271 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 3271 (Database Engine error)
ms.assetid: 21b8de4b-6624-4163-9561-1a6cc8fe3d51
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8ebe044c2cd08f8724dc33a6928c8b94447fa8dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62914245"
---
# <a name="mssqlserver_3271"></a>MSSQLSERVER_3271
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|3271|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DMPIO_IO_ERROR|  
|Testo del messaggio|Errore di I/O irreversibile nel file "%ls:" %ls.|  
  
## <a name="explanation"></a>Spiegazione  
 Si tratta di un errore generale che si verifica quando il sistema operativo genera un errore nell'esecuzione di I/O durante un'operazione di backup o di ripristino. Nella maggior parte delle situazioni ciò è dovuto semplicemente al fatto che il supporto di backup è pieno.  
  
 È possibile che nell'errore sia incluso testo aggiuntivo generato dal sistema operativo in cui viene indicato che il disco è pieno. Durante l'esecuzione di un'operazione di backup o di ripristino con software di backup di terze parti è possibile ricevere un ulteriore messaggio in cui viene indicato l'esito negativo del backup. Il testo del messaggio è simile al seguente:  
  
```  
"2005-08-02 16:05:16.04 spid55 Error: 18210, Severity: 16, State: 1.  
 2005-08-02 16:05:16.04 spid55 BackupVirtualDeviceFile  
::RequestDurableMedia: Flush failure on backup device 'VDINULL'.   
Operating system error 995(The I/O operation has been aborted because   
of either a thread exit or an application request.)."  
```  
  
 Viene indicato che il software di backup ha richiesto l'interruzione dell'operazione di backup o di ripristino.  
  
## <a name="user-action"></a>Azione dell'utente  
 Eseguire le attività seguenti in modo appropriato:  
  
-   Esaminare i messaggi di errore di sistema sottostanti e i messaggi di errore di SQL Server precedenti al messaggio in questione per identificare la causa del problema.  
  
-   Verificare che il supporto di backup e ripristino disponga di spazio sufficiente.  
  
-   Correggere gli errori generati dal software di backup e ripristino di terze parti.  
  
  
