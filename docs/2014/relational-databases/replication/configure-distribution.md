---
title: Configurare la distribuzione | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- remote Distributors [SQL Server replication]
- transactional replication, configuring distribution
- distribution databases [SQL Server replication], sizing
- Distributors [SQL Server replication], configuring
- distribution databases [SQL Server replication], about distribution databases
- distribution databases [SQL Server replication]
- merge replication [SQL Server replication], configuring distribution
ms.assetid: 94d52169-384e-4885-84eb-2304e967d9f7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f001652af1f6ed627ded9be287b4910059cce9cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721716"
---
# <a name="configure-distribution"></a>Configurazione della distribuzione
  Il server di distribuzione contiene il database di distribuzione, in cui vengono archiviati i metadati e i dati cronologici per tutti i tipi di replica e le transazioni per la replica transazionale. Per impostare la replica, è necessario configurare un server di distribuzione. Ogni server di pubblicazione può essere assegnato a una sola istanza del server di distribuzione, ma più server di pubblicazione possono condividere un server di distribuzione. Il server di distribuzione utilizza le risorse aggiuntive seguenti nel server in cui è installato:  
  
-   Spazio su disco aggiuntivo se i file di snapshot per la pubblicazione sono archiviati nel server di distribuzione, come avviene in genere.  
  
-   Maggiore spazio su disco per l'archiviazione del database di distribuzione.  
  
-   Maggior utilizzo del processore da parte degli agenti di replica per le sottoscrizioni push in esecuzione nel server di distribuzione.  
  
 Nel server selezionato come server di distribuzione devono essere disponibili spazio su disco e capacità del processore sufficienti per il supporto delle attività di replica e di altre eventuali operazioni basate su tale server. Quando si configura il server di distribuzione, è necessario specificare le informazioni seguenti:  
  
-   Una cartella snapshot, utilizzata, per impostazione predefinita, per tutti i server di pubblicazione che utilizzano questo server di distribuzione. Verificare che questa cartella sia già condivisa e che siano impostate le autorizzazioni appropriate. Per altre informazioni, vedere [Proteggere la cartella snapshot](security/secure-the-snapshot-folder.md).  
  
-   Un nome e i percorsi dei file per il database di distribuzione. Non è possibile modificare il nome del database di distribuzione dopo la sua creazione. Per utilizzare un nome diverso per il database, è necessario disabilitare la distribuzione e riconfigurarla.  
  
-   Qualsiasi server di pubblicazione autorizzato a utilizzare il server di distribuzione. Se si specificano server di pubblicazione diversi dall'istanza in cui è in esecuzione il server di distribuzione, è inoltre necessario specificare una password per le connessioni eseguite dai server di pubblicazione al server di distribuzione remoto.  
  
 Per la replica transazionale, dopo avere configurato la distribuzione, è consigliabile eseguire le operazioni seguenti:  
  
-   Ridimensionare in modo appropriato il database di distribuzione. Verificare la replica con un carico tipico per il sistema per determinare lo spazio necessario per archiviare i comandi. Verificare che il database sia sufficientemente grande da consentire l'archiviazione dei comandi senza richiedere un aumento automatico delle dimensioni frequente. Per altre informazioni sulla modifica delle dimensioni di un database, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
-   Impostare l'opzione **sync with backup** nel database di distribuzione. Per altre informazioni, vedere [Strategie di backup e ripristino della replica snapshot e della replica transazionale](administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md) e [Abilitare backup coordinati per la replica transazionale &#40;programmazione Transact-SQL della replica&#41;](administration/enable-coordinated-backups-for-transactional-replication.md).  
  
## <a name="local-and-remote-distributors"></a>Server di distribuzione locali e remoti  
 Per impostazione predefinita, il server di distribuzione corrisponde al server di pubblicazione, ovvero un server di distribuzione locale, ma può anche essere un server distinto, ovvero un server di distribuzione remoto. In genere, è consigliabile utilizzare un server di distribuzione remoto se si desidera eseguire le operazioni seguenti:  
  
-   Elaborazione con ripartizione del carico di lavoro in un altro computer, se si desidera che l'impatto della replica sul server di pubblicazione sia minimo, ad esempio se il server di pubblicazione è un server OLTP.  
  
-   Configurazione di un server di distribuzione centralizzato per più server di pubblicazione.  
  
 I server di distribuzione remoti sono più comuni nella replica transazionale rispetto alla replica di tipo merge per due motivi:  
  
-   Il server di distribuzione ha un ruolo più importante nella replica transazionale in quanto tutte le transazioni replicate vengono scritte nel database di distribuzione e lette da tale database.  
  
-   Le topologie di replica di tipo merge utilizzano in genere le sottoscrizioni pull, pertanto gli agenti vengono eseguiti in ogni Sottoscrittore, invece di essere eseguiti tutti nel server di distribuzione. Per altre informazioni, vedere [Sottoscrivere le pubblicazioni](subscribe-to-publications.md). Nella maggior parte dei casi, è consigliabile utilizzare un database di distribuzione locale per la replica di tipo merge.  
  
 Per configurare la pubblicazione e la distribuzione, vedere [Configure Publishing and Distribution](configure-publishing-and-distribution.md).  
  
 Per modificare le proprietà del server di pubblicazione e di distribuzione, vedere [View and Modify Distributor and Publisher Properties](view-and-modify-distributor-and-publisher-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare dati e oggetti di database](publish/publish-data-and-database-objects.md)   
 [Proteggere il database di distribuzione](security/secure-the-distributor.md)  
  
  
