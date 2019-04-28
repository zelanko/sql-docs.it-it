---
title: Transazioni tra Database non supportato per il mirroring del Database o AlwaysOn gruppi di disponibilità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c3616e40ff54c67d27902ddf9454084fb62e282
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62813656"
---
# <a name="cross-database-transactions-not-supported-for-database-mirroring-or-alwayson-availability-groups-sql-server"></a>Transazioni tra database non supportate per il mirroring del database o i gruppi di disponibilità AlwaysOn (SQL Server)
  Le transazioni tra database e quelle distribuite non sono supportate da [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] o dal mirroring del database perché l'atomicità e integrità delle transazioni non può essere garantita per i motivi seguenti:  
  
-   Per le transazioni tra database: Ogni database esegue il commit in modo indipendente. Pertanto, anche per i database presenti in un solo gruppo di disponibilità, potrebbe verificarsi un failover dopo il commit di una transazione da parte di un database, ma prima che la stessa operazione venga effettuata da un altro database. Per il mirroring del database questo problema è ancora più complesso perché dopo un failover, il database con mirroring si trova in genere in un'istanza del server diversa dall'altro database e, anche se viene eseguito il mirroring di entrambi i database tra gli stessi due partner, non esiste garanzia alcuna che verrà eseguito il failover di entrambi i database contemporaneamente.  
  
-   Per le transazioni distribuite: Dopo un failover, il nuovo server principale/replica primaria non riesce a connettersi al distributed transaction coordinator sulla replica di server principale/primario precedente. Per questo motivo, tramite il nuovo server principale o la nuova replica primaria non è possibile ottenere lo stato delle transazioni.  
  
 Nell'esempio di mirroring del database seguente si illustra come può verificarsi un'incoerenza logica. In questo esempio un'applicazione utilizza una transazione tra database per inserire due righe di dati. Una riga viene inserita in una tabella in un database con mirroring, A, l'altra viene inserita in un altro database, B. Il database A viene sottoposto a mirroring in modalità a protezione elevata con failover automatico. Durante il commit della transazione, il database A diventa non disponibile e viene automaticamente eseguito il failover della sessione di mirroring sul mirror del database A.  
  
 Dopo il failover, è possibile che il commit della transazione tra database abbia esito positivo sul database B, ma non sul database di cui è stato eseguito il failover. Questa situazione si verifica qualora il server principale originale del database A non abbia inviato il log per la transazione tra database al server mirror prima dell'errore. Dopo il failover, tale transazione non è più presente nel nuovo server principale. I database A e B diventano incoerenti perché i dati inseriti nel database B rimangono inalterati, mentre quelli inseriti nel database A sono stati persi.  
  
 Uno scenario analogo può verificarsi quando si utilizza una transazione MS DTC. Ad esempio, dopo il failover, il nuovo server principale contatta MS DTC. MS DTC, tuttavia, non rileva il nuovo server principale e termina tutte le transazioni di cui si sta preparando il commit e per le quali in altri database il commit viene considerato eseguito.  
  
> [!IMPORTANT]  
>  L'utilizzo del mirroring del database o dei gruppi di disponibilità con DTC non comporta un'installazione non supportata di SQL Server. Se, tuttavia, un database fa parte di una sessione di mirroring del database o di un gruppo di disponibilità e nel database viene utilizzato anche DTC, i problemi di supporto verranno esaminati da Microsoft solo se non correlati all'utilizzo combinato del mirroring del database o dei gruppi di disponibilità con DTC.  
  
  
