---
title: MSSQL_REPL027056 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027056 error
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 52ba56c3b972be091995300e7b43f81ad407742e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060693"
---
# <a name="mssql_repl027056"></a>MSSQL_REPL027056
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|27056|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Impossibile modificare la cronologia di generazione in '%1'. Per risolvere il problema, riavviare la sincronizzazione con la registrazione dettagliata della cronologia e specificare un file di output in cui registrare i dati.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore viene solitamente generato come risultato della contesa in tabelle di sistema della replica di tipo merge che hanno raggiunto una dimensione eccessiva. L'eccessivo aumento delle dimensioni delle tabelle di sistema è in genere dovuto a un lungo periodo di memorizzazione della pubblicazione, in quanto i metadati devono essere archiviati in queste tabelle fino al raggiungimento del periodo di memorizzazione.  
  
## <a name="user-action"></a>Azione dell'utente  
 **Per risolvere il problema:**  
  
1.  Ridurre il valore dei parametri**DownloadGenerationsPerBatch** e **-UploadGenerationsPerBatch** per l'agente di merge in modo da consentire la continuazione dell'elaborazione mentre si risolve il problema sottostante che causa l'errore. I parametri degli agenti possono essere specificati nei profili agente e dalla riga di comando. Per altre informazioni, vedere:  
  
    -   [Usare i profili agenti di replica](agents/replication-agent-profiles.md)  
  
    -   [Visualizzare e modificare i parametri del prompt dei comandi dell'agente di replica &#40;SQL Server Management Studio&#41;](agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](concepts/replication-agent-executables-concepts.md).  
  
2.  Specificare l'impostazione più bassa possibile per il periodo di memorizzazione della pubblicazione. Per altre informazioni, vedere [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md).  
  
3.  Come parte della manutenzione per la replica di tipo merge, controllare occasionalmente l'aumento delle dimensioni delle tabelle di sistema associate alla replica di tipo merge: **MSmerge_contents**, **MSmerge_genhistory**e **MSmerge_tombstone**, **MSmerge_current_partition_mappings**e **MSmerge_past_partition_mappings**. Reindicizzare periodicamente queste tabelle. Per altre informazioni, vedere [Riorganizzare e ricompilare gli indici](../indexes/indexes.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](errors-and-events-reference-replication.md)  
  
  
