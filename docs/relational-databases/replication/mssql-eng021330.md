---
title: MSSQL_ENG021330 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021330 error
ms.assetid: e2bb2e21-62a7-4689-b68b-bdfba3fdd985
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 84a01d34e8158d69eb00618cd02ebd1b9923a115
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54126621"
---
# <a name="mssqleng021330"></a>MSSQL_ENG021330
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|21330|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Impossibile creare una sottodirectory nella directory di lavoro della replica.(%1!)|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore si può verificare quando una sottoscrizione viene inizializzata manualmente e si riscontra un problema nella creazione della directory di archiviazione degli script di replica. L'errore può essere causato da un problema relativo alle autorizzazioni: quando una sottoscrizione viene inizializzata senza utilizzare uno snapshot, l'account con cui il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito nel server di pubblicazione deve disporre di autorizzazioni di scrittura per la cartella snapshot nel server di distribuzione.  
  
## <a name="user-action"></a>Azione dell'utente  
 Verificare che sia stato specificato il percorso corretto della cartella snapshot e che l'account con cui il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito nel server di pubblicazione disponga di autorizzazioni sufficienti.  
  
## <a name="see-also"></a>Vedere anche  
 [Modificare le opzioni snapshot](../../relational-databases/replication/snapshot-options.md)   
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Inizializzare una sottoscrizione transazionale senza uno snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  
