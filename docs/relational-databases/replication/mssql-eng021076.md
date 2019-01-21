---
title: MSSQL_ENG021076 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021076 error
ms.assetid: 612e5c59-ba3e-49c3-a3df-56bac3d850a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bdce747a7b23424e85b48a9e78ece236f3bf35d0
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54133991"
---
# <a name="mssqleng021076"></a>MSSQL_ENG021076
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|21076|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Lo snapshot iniziale per l'articolo '%s' non è ancora disponibile.|  
  
## <a name="explanation"></a>Spiegazione  
 L'errore MSSQL_ENG021076 può essere generato se l'agente di distribuzione viene avviato prima che l'agente snapshot abbia terminato la generazione dello snapshot e solo se la pubblicazione contiene un unico articolo. Se la pubblicazione contiene più articoli, viene generato invece l'errore MSSQL_ENG021075. Per altre informazioni, vedere [MSSQL_ENG021075](../../relational-databases/replication/mssql-eng021075.md).  
  
## <a name="user-action"></a>Azione dell'utente  
 Se l'agente snapshot per la pubblicazione non è stato avviato in seguito alla creazione della sottoscrizione o se non è stato avviato dall'ultima volta in cui si è scelto di reinizializzare la sottoscrizione, avviare l'agente snapshot e consentire il completamento delle operazioni prima di avviare l'agente di distribuzione. Per altre informazioni, vedere [Creare e applicare lo snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
 Se l'agente snapshot non viene completato, controllarne la cronologia per individuare eventuali errori e risolverli. Per informazioni sui dettagli di stato e di errore dell'agente di visualizzazione in Monitoraggio replica, vedere [Visualizzare le informazioni ed eseguire attività usando Monitoraggio replica](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Se l'errore continua a verificarsi, aumentare il livello di dettaglio per la registrazione delle operazioni dell'agente e specificare un file di output per il log. A seconda del contesto dell'errore, in questo modo si potrebbero ottenere ulteriori informazioni sui passaggi che conducono all'errore e/o messaggi di errore aggiuntivi.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
