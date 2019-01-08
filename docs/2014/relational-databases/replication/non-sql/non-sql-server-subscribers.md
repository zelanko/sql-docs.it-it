---
title: Sottoscrittori non SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], non-SQL Server Subscribers
- heterogeneous data sources, non-SQL Server Subscribers
- heterogeneous data sources
- heterogeneous database replication, non-SQL Server Subscribers
- non-SQL Server Subscribers, about non-SQL Server Subscribers
- heterogeneous Subscribers
- heterogeneous Subscribers, about heterogeneous Subscribers
- Subscribers [SQL Server replication], non-SQL Server Subscribers
- non-SQL Server Subscribers
ms.assetid: 831e7586-2949-4b9b-a2f3-7b0b699b23ff
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8e5b7592ba97f779d3c1aeb83f34317ef7c6833d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52763223"
---
# <a name="non-sql-server-subscribers"></a>Sottoscrittori non SQL Server
  Tramite i Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] riportati di seguito è possibile eseguire la sottoscrizione di pubblicazioni snapshot e transazionali utilizzando sottoscrizioni push. Le sottoscrizioni sono supportate per le due versioni più recenti di ogni database elencato utilizzando la versione più recente del provider OLE DB elencato.  
  
 La replica eterogenea a Sottoscrittori non SQL Server è deprecata. La pubblicazione Oracle è deprecata. Per spostare dati, creare soluzioni utilizzando Change Data Capture e [!INCLUDE[ssIS](../../../includes/ssis-md.md)].  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
|Database|Sistema operativo|Provider|  
|--------------|----------------------|--------------|  
|Oracle|Tutte le piattaforme supportate da Oracle|Provider Oracle OLE DB (fornito da Oracle)|  
|IBM DB2|MVS, AS400, Unix, Linux, Windows escluso 9.x|Provider Microsoft Host Integration Server (HIS) OLE DB|  
  
 Per informazioni sulla creazione delle sottoscrizioni di Oracle e IBM DB2, vedere [Oracle Subscribers](oracle-subscribers.md) e [IBM DB2 Subscribers](ibm-db2-subscribers.md).  
  
## <a name="considerations-for-non-sql-server-subscribers"></a>Considerazioni sui Sottoscrittori non SQL Server  
 Durante la replica in Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tenere presente quanto segue:  
  
### <a name="general-considerations"></a>Considerazioni generali  
  
-   La replica supporta la pubblicazione di tabelle e viste indicizzate come tabelle in Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (le viste indicizzate non possono essere replicate come viste indicizzate).  
  
-   Quando si crea una pubblicazione con la Procedura guidata nuova pubblicazione e quindi si procede alla relativa abilitazione per i Sottoscrittori non SQL Server mediante la finestra di dialogo Proprietà pubblicazione, il proprietario di tutti gli oggetti del database di sottoscrizione non viene specificato per i Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , mentre per i Sottoscrittori [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene impostato sul proprietario dell'oggetto corrispondente nel database di pubblicazione.  
  
-   Se una pubblicazione include Sottoscrittori [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , è necessario abilitarla per i Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] prima di creare le sottoscrizioni per i Sottoscrittori [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Per impostazione predefinita, gli script generati dall'agente snapshot per i Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzano identificatori non racchiusi tra virgolette nella sintassi CREATE TABLE. Pertanto, una tabella pubblicata denominata 'test' viene replicata come 'TEST'. Per usare la stessa combinazione di maiuscole e minuscole della tabella nel database di pubblicazione, specificare il parametro **-QuotedIdentifier** per l'agente di distribuzione. Il parametro **-QuotedIdentifier** deve essere usato anche se i nomi degli oggetti pubblicati, ad esempio tabelle, colonne e vincoli, includono spazi o parole riservate nella versione del database nel Sottoscrittore non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per ulteriori informazioni su questo parametro, vedere [Replication Distribution Agent](../agents/replication-distribution-agent.md).  
  
-   L'account con il quale viene eseguito l'agente di distribuzione deve disporre di accesso in lettura alla directory di installazione del provider OLE DB.  
  
-   Per impostazione predefinita, per i Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] l'agente di distribuzione usa il valore [(destinazione predefinita)] per il database di sottoscrizione (il parametro **-SubscriberDB** per l'agente di distribuzione):  
  
    -   Per Oracle, un server include al massimo un database e pertanto non è necessario specificare il database.  
  
    -   Per IBM DB2, il database viene specificato nella stringa di connessione DB2. Per altre informazioni, vedere [Creazione di una sottoscrizione per un Sottoscrittore non SQL Server](../create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
-   Se il server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene eseguito su una piattaforma a 64 bit, è necessario utilizzare la versione a 64 bit del provider OLE DB appropriato.  
  
-   La replica consente di spostare i dati in formato Unicode indipendentemente dalla tabella codici e dalle regole di confronto utilizzate nel server di pubblicazione e nel Sottoscrittore. Quando si esegue la replica tra server di pubblicazione e Sottoscrittori è consigliabile scegliere una tabella codici e regole di confronto compatibili.  
  
-   Se un articolo viene aggiunto o eliminato da una pubblicazione, sarà necessario reinizializzare le sottoscrizioni dei Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   I soli vincoli supportati per tutti i non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sottoscrittori sono: NULL e NOT NULL. I vincoli delle chiavi primarie vengono replicati come indici univoci.  
  
-   Il valore NULL viene considerato in modo diverso a seconda del database, con conseguenze sulla modalità di rappresentazione dei valori e delle stringhe vuote e dei valori NULL. Ciò a sua volta influisce sul comportamento dei valori inseriti nelle colonne con vincoli univoci definiti. Oracle consente, ad esempio, più valori NULL in una colonna considerata univoca, mentre [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente un solo valore NULL in una colonna univoca.  
  
     Un altro fattore è rappresentato dal modo in cui i valori NULL, le stringhe e i valori vuoti vengono considerati quando la colonna è definita come NOT NULL. Per informazioni sulla risoluzione di questo problema per i Sottoscrittori Oracle, vedere [Oracle Subscribers](oracle-subscribers.md).  
  
-   I metadati correlati alla replica (tabella di sequenza della transazione) non vengono eliminati dai Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando la sottoscrizione viene rimossa.  
  
### <a name="conforming-to-the-requirements-of-the-subscriber-database"></a>Conformità ai requisiti del database Sottoscrittore  
  
-   Lo schema e i dati pubblicati devono essere conformi ai requisiti del database nel Sottoscrittore. Se, ad esempio, un database non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] presenta una dimensione massima di riga più piccola di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], è necessario accertarsi che lo schema e i dati pubblicati non superino tale dimensione.  
  
-   Le tabelle replicate nei Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] adotteranno le convenzioni di denominazione delle tabelle del database del Sottoscrittore.  
  
-   L'operazione DDL non è supportata per Sottoscrittori non SQL Server. Per altre informazioni sulle modifiche dello schema, vedere [Apportare modifiche allo schema nei database di pubblicazione](../publish/make-schema-changes-on-publication-databases.md).  
  
### <a name="replication-feature-support"></a>Supporto della funzionalità di replica  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] include due tipi di sottoscrizione: push e pull. I Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] devono utilizzare le sottoscrizioni push nelle quali l'agente di distribuzione viene eseguito nel server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] include due formati di snapshot: in modalità bcp nativa e in modalità carattere. I Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] richiedono snapshot in modalità carattere.  
  
-   I Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non possono utilizzare le sottoscrizioni ad aggiornamento immediato o ad aggiornamento in coda né possono essere nodi in una topologia peer-to-peer.  
  
-   I Sottoscrittori non[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non possono essere inizializzati automaticamente da un backup.  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di database eterogenei](heterogeneous-database-replication.md)   
 [Sottoscrizione delle pubblicazioni](../subscribe-to-publications.md)  
  
  
