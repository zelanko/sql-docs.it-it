---
title: Glossario dei termini per la pubblicazione Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], glossary
ms.assetid: e21dfa4b-6144-4be7-9cbf-ca2709b2bd9f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8ac643b3c0c095dee143c3feca878bd4072273bb
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "67901104"
---
# <a name="glossary-of-terms-for-oracle-publishing"></a>Glossario dei termini per la pubblicazione Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In caso di configurazione e amministrazione della pubblicazione Oracle, è consigliabile avere familiarità con i termini Oracle seguenti. Per un elenco completo dei termini Oracle, vedere la documentazione online Oracle.  
  
#### <a name="index-organized-tables-iot"></a>Tabelle organizzate a indice (IOT, Index Organized Table)  
 Tabella i cui dati sono fisicamente ordinati su disco in base a un indice. È simile a una tabella [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con indice cluster. Una tabella organizzata a indice viene replicata in un Sottoscrittore come una tabella con indice cluster.  
  
#### <a name="instance"></a>Istanza  
 Un database Oracle è associato a un'istanza, che include la memoria e i processi in background che supportano il database. Un'istanza di Oracle è sempre mappata a un singolo database, mentre un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può contenere più database. In alcuni casi, un database Oracle può disporre di più istanze.  
  
#### <a name="oracle-listener"></a>Listener Oracle  
 Gestisce il traffico di rete in ingresso per un'istanza di database Oracle. Durante la configurazione della connettività di rete per un database Oracle, si specifica il protocollo con cui viene inviato il traffico e la porta su cui il listener resta in attesa di traffico. Il listener viene in genere configurato per l'esecuzione sullo stesso computer dell'istanza di database Oracle e può essere configurato per una o più istanze.  
  
#### <a name="rowid"></a>ROWID  
 Puntatore alla posizione di una riga specifica in un database. Poiché il recupero di righe mediante ROWID risulta più veloce rispetto all'utilizzo di un indice o un'analisi di tabella, ROWID viene temporaneamente utilizzato nella replica durante l'elaborazione delle modifiche alle tabelle pubblicate.  
  
#### <a name="sequence"></a>Sequenza  
 Oggetto di database utilizzato per generare numeri univoci. Le sequenze vengono utilizzate nella replica per ordinare le modifiche apportate alle tabelle pubblicate.  
  
#### <a name="sqlplus"></a>SQL\*Plus  
 Applicazione utilizzata per l'accesso e l'esecuzione di query in database Oracle. È simile a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]sqlcmd**di**.  
  
#### <a name="synonym"></a>Sinonimo  
 Alias di un oggetto. Lo speciale sinonimo public **MSSQLSERVERDISTRIBUTOR** viene creato automaticamente quando viene configurato un server di pubblicazione Oracle. Il sinonimo fa riferimento alla tabella **HREPL_Distributor** e garantisce un puntatore logico al server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che gestisce il server di pubblicazione.  
  
 Dopo la pubblicazione di un database Oracle, i successivi tentativi di configurare questo server di pubblicazione per l'utilizzo di un diverso server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] avranno esito negativo, poiché questo sinonimo public identifica lo specifico server di distribuzione già configurato per il server di pubblicazione.  
  
#### <a name="tablespace"></a>Spazio di tabella  
 Unità di archiviazione di database approssimativamente equivalente a un filegroup in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
#### <a name="tns-service-name"></a>Nome del servizio TNS  
 TNS (Transparent Network Substrate) è un livello di comunicazione utilizzato dai database Oracle. Il nome del servizio TNS è il nome con cui un'istanza di database Oracle viene riconosciuta in una rete. Il nome del servizio TNS viene assegnato durante la configurazione della connettività per il database Oracle. Il nome del servizio TNS viene utilizzato nella replica per identificare il server di pubblicazione e stabilire connessioni.  
  
#### <a name="user-schema"></a>Schema utente  
 Uno schema utente può essere considerato come un utente di database proprietario di un determinato set di oggetti di database. Lo schema utente di amministrazione della replica possiede tutti gli oggetti creati dal processo di replica [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nel database Oracle, con l'eccezione del sinonimo public **MSSQLSERVERDISTRIBUTOR** .  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oggetti creati nel server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/objects-created-on-the-oracle-publisher.md)   
 [Server di pubblicazione non SQL Server](../../../relational-databases/replication/non-sql/non-sql-server-publishers.md)   
 [Panoramica della pubblicazione Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
