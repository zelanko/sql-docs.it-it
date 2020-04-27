---
title: Sospensione e ripresa del mirroring del database (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- sessions [SQL Server], database mirroring
- resuming database mirroring
- database mirroring [SQL Server], pausing
- database mirroring [SQL Server], resuming
- pausing database mirroring
ms.assetid: c67802c6-ee8c-4cbd-a6d4-f7b80413a4ab
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0e4f36dab5b953b1a631f4510e11bba47798bf62
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62754519"
---
# <a name="pausing-and-resuming-database-mirroring-sql-server"></a>Sospensione e ripresa del mirroring del database (SQL Server)
  Il proprietario del database può sospendere una sessione di mirroring del database, riprenderla in qualsiasi momento e preservare così lo stato della sessione durante la sospensione del mirroring. In caso di colli di bottiglia, la sospensione può essere utile per migliorare le prestazioni del server principale.  
  
 Quando si sospende una sessione, il database principale resta disponibile. In caso di sospensione, lo stato della sessione di mirroring viene impostato su SUSPENDED e il database mirror perde la sincronizzazione con il database principale, che viene quindi eseguito in una condizione nota come esposizione senza mirroring.  
  
 È consigliabile riprendere una sessione sospesa il più rapidamente possibile poiché, fintanto che la sessione di mirroring del database rimane sospesa, non è possibile troncare il log delle transazioni. Se la sessione di mirroring del database resta sospesa troppo a lungo, lo spazio del log delle transazioni può esaurirsi rendendo il database non disponibile. Per una spiegazione di questo problema, vedere "Impatto della sospensione e ripresa sul troncamento del log" di seguito in questo argomento.  
  
> [!IMPORTANT]  
>  In un servizio forzato, quando il server principale originale esegue nuovamente la connessione il mirroring viene sospeso. Se si riprende il mirroring in questa situazione, è possibile che si verifichi una perdita di dati nel server principale originale. Per informazioni sulla gestione della potenziale perdita di dati, vedere [Database Mirroring Operating Modes](database-mirroring-operating-modes.md).  
  
 **Contenuto dell'argomento**  
  
-   [Impatto della sospensione e ripresa sul troncamento del log](#EffectOnLogTrunc)  
  
-   [Evitare il riempimento del log delle transazioni](#AvoidFullLog)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="how-pausing-and-resuming-affect-log-truncation"></a><a name="EffectOnLogTrunc"></a>Effetti della sospensione e ripresa sul troncamento del log  
 In genere, quando su un database viene eseguito un checkpoint automatico, il relativo log delle transazioni viene troncato in corrispondenza di tale checkpoint dopo il successivo backup del log. Durante il periodo in cui una sessione di mirroring del database rimane sospesa, tutti i record del log corrente restano attivi poiché il server principale è in attesa di inviarli al server mirror. I record del log non inviati si accumulano nel log delle transazioni del database principale fino alla ripresa della sessione e al momento dell'invio dei record del log dal server principale al server mirror.  
  
 Quando la sessione viene ripresa, il server principale inizia immediatamente a inviare i record del log accumulati al server mirror. Dopo la conferma da parte del server mirror che il record del log corrispondente al checkpoint automatico meno recente è stato accodato, il server principale tronca il log del database principale fino a tale checkpoint. Il server mirror tronca la coda di rollforward in corrispondenza dello stesso record del log. Poiché questo processo viene ripetuto per ogni checkpoint successivo, il log viene troncato in più fasi per i singoli checkpoint.  
  
> [!NOTE]  
>  Per altre informazioni sui checkpoint e sul troncamento del log, vedere [Checkpoint di database &#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md).  
  
##  <a name="avoid-a-full-transaction-log"></a><a name="AvoidFullLog"></a>Evitare un log delle transazioni completo  
 Se il log si riempie, perché raggiunge le dimensioni massime o l'istanza del server esaurisce lo spazio, il database non può eseguire ulteriori aggiornamenti. Per evitare questo problema, è possibile procedere in due modi:  
  
-   Riprendere la sessione di mirroring del database prima che il log esaurisca lo spazio, oppure aggiungere spazio di log. Se si riprende il mirroring, il server principale invia il log cumulativo attivo al server mirror e il database mirror viene posto in stato SYNCHRONIZING. Il server mirror può quindi salvare il log su disco e avviarne il rollforward.  
  
-   Arrestare la sessione di mirroring del database rimuovendo il mirroring.  
  
     A differenza della sospensione di una sessione, la rimozione del mirroring provoca l'eliminazione di tutte le informazioni relative alla sessione di mirroring. Ogni istanza del server partner mantiene la sua copia del database. Se recuperata, pertanto, la copia precedente del database mirror può risultare diversa dalla copia precedente del database principale e indicare un periodo di tempo inferiore rispetto a quello trascorso dalla sospensione della sessione. Per altre informazioni, vedere [Rimozione del mirroring del database &#40;SQL Server&#41;](database-mirroring-sql-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
 **Per sospendere o riprendere il mirroring del database**  
  
-   [Sospendere o riprendere una sessione di mirroring del database &#40;SQL Server&#41;](pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
 **Per arrestare il mirroring del database**  
  
-   [Rimuovere il mirroring del database &#40;SQL Server&#41;](remove-database-mirroring-sql-server.md)  
  
## <a name="see-also"></a>Vedi anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [&#40;SQL Server di mirroring del database&#41;](database-mirroring-sql-server.md)   
 [Rimozione del mirroring del database &#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
