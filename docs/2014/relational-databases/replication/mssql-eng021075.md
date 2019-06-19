---
title: MSSQL_ENG021075 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021075 error
ms.assetid: c8c29543-d1f6-49d5-b6c8-e8c3aa373090
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4647b34db4cd224e5c76f6e960a5636deaeeac8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62938517"
---
# <a name="mssqleng021075"></a>MSSQL_ENG021075
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|21075|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Lo snapshot iniziale per la pubblicazione '%s' non è ancora disponibile.|  
  
## <a name="explanation"></a>Spiegazione  
 L'errore MSSQL_ENG021075 viene generato in caso di avvio dell'agente di distribuzione o di merge prima che l'agente snapshot abbia completato la generazione dello snapshot.  
  
## <a name="user-action"></a>Azione dell'utente  
 Se l'agente snapshot per la pubblicazione non è stato avviato dopo la creazione della sottoscrizione oppure dall'ultima reinizializzazione della sottoscrizione, avviare l'agente snapshot e attenderne il completamento prima di avviare l'agente di distribuzione o di merge. Per altre informazioni, vedere [Creare e applicare lo snapshot](create-and-apply-the-snapshot.md).  
  
 Se l'agente snapshot non viene completato, controllarne la cronologia per individuare eventuali errori e risolverli. Per informazioni sui dettagli di stato e di errore dell'agente di visualizzazione in Monitoraggio replica, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Se l'errore continua a verificarsi, aumentare il livello di dettaglio per la registrazione delle operazioni dell'agente e specificare un file di output per il log. A seconda del contesto dell'errore, in questo modo si potrebbero ottenere ulteriori informazioni sui passaggi che conducono all'errore e/o messaggi di errore aggiuntivi.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](errors-and-events-reference-replication.md)  
  
  
