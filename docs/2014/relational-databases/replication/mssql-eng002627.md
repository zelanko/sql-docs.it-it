---
title: MSSQL_ENG002627 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG002627 error
ms.assetid: 7f4136ac-3784-4a41-a98c-8a02308e4883
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a102991d08085f093e08a068a3d3127c9d7f7fc6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62666697"
---
# <a name="mssql_eng002627"></a>MSSQL_ENG002627
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|2627|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico|N/D|  
|Testo del messaggio|Violazione del vincolo %ls '%.*ls'. Non è possibile inserire la chiave duplicata nell'oggetto '%.\*ls'.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore generale può essere generato indipendentemente dal fatto che un database venga o meno replicato. Nei database replicati l'errore viene di solito generato in quanto le chiavi primarie non sono state gestite correttamente nella topologia. In un ambiente distribuito è fondamentale garantire che lo stesso valore non venga inserito in una colonna chiave primaria o in qualsiasi altra colonna univoca in più di un nodo. Le cause possibile includono:  
  
-   Le operazioni di inserimento e aggiornamento su una riga vengono eseguite in più di un nodo. Sebbene la replica di tipo merge e le sottoscrizioni aggiornabili per la replica transazionale consentano il rilevamento e la risoluzione dei conflitti, è preferibile inserire o aggiornare una determinata riga in un unico nodo. La replica transazionale di tipo peer-to-peer non fornisce funzioni di rilevamento e risoluzione dei conflitti e richiede il partizionamento degli inserimenti e degli aggiornamenti.  
  
-   È stata inserita una riga in un Sottoscrittore che dovrebbe essere di sola lettura. I Sottoscrittori delle pubblicazioni snapshot devono essere considerati come di sola lettura, analogamente ai Sottoscrittori delle pubblicazioni transazionali a meno che non vengano utilizzate sottoscrizioni aggiornabili o una replica transazione peer-to-peer.  
  
-   Viene utilizzata una tabella con una colonna Identity, ma la colonna non è gestita in modo appropriato.  
  
## <a name="user-action"></a>Azione dell'utente  
 L'azione richiesta dipende dal motivo per il quale è stato generato l'errore:  
  
-   Le operazioni di inserimento e aggiornamento su una riga vengono eseguite in più di un nodo.  
  
     Indipendentemente dal tipo di replica utilizzato, è consigliabile partizionare inserimenti e aggiornamenti quando possibile, in modo da ridurre l'elaborazione richiesta per il rilevamento e la risoluzione dei conflitti. Per la replica transazionale peer-to-peer, è richiesto il partizionamento di inserimenti e aggiornamenti. Per altre informazioni, vedere [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md).  
  
-   È stata inserita una riga in un Sottoscrittore che dovrebbe essere di sola lettura.  
  
     Non inserire o aggiornare righe nel Sottoscrittore a meno che non si stia utilizzando la replica di tipo merge, la replica transazionale con sottoscrizioni aggiornabili o la replica transazionale peer-to-peer.  
  
-   Viene utilizzata una tabella con una colonna Identity, ma la colonna non è gestita in modo appropriato.  
  
     Per la replica di tipo merge e la replica transazionale con sottoscrizioni aggiornabili, le colonne Identity devono essere gestite automaticamente dalla replica. Per la replica transazionale peer-to-peer, devono invece essere gestite manualmente. Per altre informazioni, vedere [Replicare colonne Identity](publish/replicate-identity-columns.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](errors-and-events-reference-replication.md)   
 [Replica di tipo merge](merge/merge-replication.md)   
 [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md)   
 [Updatable Subscriptions for Transactional Replication](transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
