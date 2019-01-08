---
title: Compatibilità FILESTREAM con altre funzionalità di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], other SQL Server features and
- FILESTREAM [SQL Server], limitations
ms.assetid: d2c145dc-d49a-4f5b-91e6-89a2b0adb4f3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 623b0139d70cec0574aaf9b68e37a1ad6f4f9eaf
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53355218"
---
# <a name="filestream-compatibility-with-other-sql-server-features"></a>Compatibilità FILESTREAM con altre funzionalità di SQL Server
  Poiché i dati FILESTREAM sono nel file system, in questo argomento vengono fornite alcune considerazioni, linee guida e limitazioni per l'utilizzo di FILESTREAM con le funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]indicate di seguito.  
  
-   [SQL Server Integration Services (SSIS)](#ssis)  
  
-   [Query distribuite e server collegati](#distqueries)  
  
-   [Crittografia](#encryption)  
  
-   [Snapshot di database](#DatabaseSnapshot)  
  
-   [Replica](#Replication)  
  
-   [Log shipping](#LogShipping)  
  
-   [Mirroring del database](#DatabaseMirroring)  
  
-   [Indicizzazione full-text](#FullText)  
  
-   [Clustering di failover](#FailoverClustering)  
  
-   [SQL Server Express](#SQLServerExpress)  
  
-   [Database indipendenti](#contained)  
  
##  <a name="ssis"></a> SQL Server Integration Services (SSIS)  
 In SQL Server Integration Services (SSIS) i dati FILESTREAM vengono gestiti nel flusso di dati in modo analogo agli altri dati BLOB, utilizzando il tipo di dati SSIS DT_IMAGE.  
  
 È possibile utilizzare la trasformazione Importa colonna per caricare file dal file system e inserirli in una colonna FILESTREAM. È inoltre possibile utilizzare la trasformazione Esporta colonna per estrarre i file da una colonna FILESTREAM e inserirli in un'altra posizione nel file system.  
  
##  <a name="distqueries"></a> Query distribuite e server collegati  
 È possibile utilizzare i dati FILESTREAM tramite query distribuite e server collegati trattandoli `varbinary(max)` dati. Non è possibile utilizzare la funzione FILESTREAM **PathName()** in query distribuite in cui viene utilizzato un nome in quattro parti, anche quando il nome si riferisce al server locale. Tuttavia, è possibile utilizzare **PathName()** nella query interna di una query pass-through in cui viene utilizzato **OPENQUERY()**.  
  
##  <a name="encryption"></a> Crittografia  
 I dati FILESTREAM non vengono crittografati anche se è abilitata la crittografia dei dati trasparenti.  
  
##  <a name="DatabaseSnapshot"></a> Snapshot di database  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non supporta [snapshot del database](../databases/database-snapshots-sql-server.md) per i filegroup FILESTREAM. Se un filegroup FILESTREAM è incluso in una clausola CREATE DATABASE ON, l'istruzione non verrà eseguita e verrà restituito un errore.  
  
 Se si sta utilizzando FILESTREAM, è possibile creare snapshot del database di filegroup standard (non FILESTREAM). I filegroup FILESTREAM sono contrassegnati come offline per questi snapshot del database.  
  
 Un'istruzione SELECT eseguita in una tabella FILESTREAM in uno snapshot del database non deve includere una colonna FILESTREAM. In caso contrario, verrà restituito il seguente messaggio di errore:  
  
 `Could not continue scan with NOLOCK due to data movement.`  
  
##  <a name="Replication"></a> Replication  
 Una colonna `varbinary(max)` che ha l'attributo FILESTREAM abilitato sul server di pubblicazione può essere replicata in un sottoscrittore con o senza l'attributo FILESTREAM. Per specificare la modalità di replica della colonna, usare la finestra di dialogo **Proprietà articolo - \<Articolo>** oppure il parametro @schema_option di [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) o [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). I dati replicati in una colonna `varbinary(max)` che non dispone dell'attributo FILESTREAM non devono superare il limite di 2 GB per quel tipo di dati; in caso contrario, viene generato un errore di runtime. Si consiglia di replicare l'attributo FILESTREAM, a meno che non si replichino dati in [!INCLUDE[ssVersion2005](../../includes/ssversion2000-md.md)] sottoscrittori non è supportata, indipendentemente dall'opzione di schema specificato.  
  
> [!NOTE]  
>  La replica di valori di dati di dimensioni elevate da [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a Sottoscrittori [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] è limitata a dati con dimensioni massime pari a 256 MB. Per ulteriori informazioni, vedere la pagina Web [Specifiche di capacità massima](https://go.microsoft.com/fwlink/?LinkId=103810).  
  
### <a name="considerations-for-transactional-replication"></a>Considerazioni sulla replica transazionale  
 Se si utilizzano colonne FILESTREAM in tabelle pubblicate per replica transazionale, considerare quanto riportato di seguito.  
  
-   Se in una tabella qualsiasi sono incluse colonne con attributo FILESTREAM, non è possibile usare i valori *database snapshot* o *database snapshot character* per la proprietà @sync_method di [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql).  
  
-   L'opzione max text repl size consente di specificare la quantità massima di dati che è possibile inserire in una colonna pubblicata per la replica. Questa opzione può essere utilizzata per controllare le dimensioni dei dati FILESTREAM replicati.  
  
-   Se si specifica l'opzione dello schema per replicare l'attributo FILESTREAM, ma si esclude la colonna `uniqueidentifier` richiesta da FILESTREAM o si specifica di non replicare il vincolo UNIQUE per la colonna, la replica dell'attributo FILESTREAM non viene effettuata. La colonna viene replicata solo come `varbinary(max)`.  
  
### <a name="considerations-for-merge-replication"></a>Considerazioni per la replica di tipo merge  
 Se si utilizzano colonne FILESTREAM in tabelle pubblicate per replica di tipo merge, considerare quanto riportato di seguito.  
  
-   Le repliche di tipo merge e FILESTREAM richiedono una colonna di tipo di dati `uniqueidentifier` per identificare ogni riga in una tabella. La replica di tipo merge consente di aggiungere automaticamente una colonna se la tabella non ne contiene neanche una. La replica di tipo merge richiede l'impostazione della proprietà ROWGUIDCOL per la colonna e che vi sia un'impostazione predefinita di NEWID () o NEWSEQUENTIALID (). Oltre a questi requisiti, è necessario che per FILESTREAM vi sia un vincolo UNIQUE definito per la colonna. In base a questi requisiti si verificano le seguenti conseguenze:  
  
    -   Se si aggiunge una colonna FILESTREAM a una tabella che è già pubblicata per la replica di tipo merge, verificare che la colonna `uniqueidentifier` abbia un vincolo UNIQUE. In caso contrario, aggiungere un vincolo denominato alla tabella nel database di pubblicazione. Per impostazione predefinita questa modifica dello schema verrà pubblicata tramite la replica e applicata a ogni database di sottoscrizione.  
  
         Se si aggiunge manualmente un vincolo UNIQUE come descritto e si desidera rimuovere una replica di tipo merge, è necessario prima rimuovere il vincolo UNIQUE; in caso contrario, la rimozione della replica non verrà effettuata.  
  
    -   Per impostazione predefinita, la replica di tipo merge consente di utilizzare NEWSEQUENTIALID () perché può fornire migliori prestazioni rispetto a NEWID (). Se si aggiunge una colonna `uniqueidentifier` a una tabella che sarà pubblicata per la replica di tipo merge, specificare NEWSEQUENTIALID () come impostazione predefinita.  
  
-   La replica di tipo merge include un'ottimizzazione per la replica di tipi di oggetto di grandi dimensioni. Questa ottimizzazione è controllata dal parametro @stream_blob_columns di [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Se si imposta l'opzione dello schema per replicare l'attributo FILESTREAM, il valore del parametro @stream_blob_columns è impostato su `true`. L'override di questa ottimizzazione può essere eseguito utilizzando [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Questa stored procedure consente di impostare @stream_blob_columns su `false`. Se si aggiunge una colonna FILESTREAM a una tabella che è già pubblicata per la replica di tipo merge, si consiglia di impostare l'opzione su `true` utilizzando sp_changemergearticle.  
  
-   L'abilitazione dell'opzione dello schema per FILESTREAM dopo la creazione di un articolo potrebbe non consentire la replica se i dati in una colonna FILESTREAM superano 2 GB e si verifica un conflitto durante tale operazione. Se le probabilità che ciò si verifichi sono alte, è consigliabile rimuovere e creare di nuovo l'articolo della tabella con l'opzione dello schema FILESTREAM appropriata abilitata al momento della creazione.  
  
-   La replica di tipo merge può sincronizzare i dati FILESTREAM su una connessione HTTPS utilizzando [Sincronizzazione Web](../replication/merge/merge-replication.md). Questi dati non possono superare il limite di 50 MB per la sincronizzazione Web; in caso contrario, viene generato un errore di runtime.  
  
##  <a name="LogShipping"></a> Log shipping  
 Il[log shipping](../../database-engine/log-shipping/about-log-shipping-sql-server.md) supporta FILESTREAM. Sia i server primari che secondari devono eseguire [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]o una versione più recente e avere FILESTREAM abilitato.  
  
##  <a name="DatabaseMirroring"></a> Mirroring del database  
 Il mirroring del database non supporta FILESTREAM. Non è possibile creare un filegroup FILESTREAM nel server principale, né configurare il mirroring per un database in cui sono contenuti filegroup FILESTREAM.  
  
##  <a name="FullText"></a> Indicizzazione full-text  
 [L'indicizzazione full-text](../indexes/indexes.md) funziona con una colonna FILESTREAM nello stesso modo cui avviene una `varbinary(max)` colonna. La tabella FILESTREAM deve avere una colonna che contiene l'estensione del nome file per ogni BLOB FILESTREAM. Per altre informazioni, vedere [Esecuzione della query con ricerca Full-Text](../search/query-with-full-text-search.md), [Configurazione e gestione di filtri per la ricerca](../search/configure-and-manage-filters-for-search.md) e [sys.fulltext_document_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql).  
  
 Il motore full-text consente di indicizzare il contenuto dei BLOB FILESTREAM. L'indicizzazione di file di immagini, ad esempio, potrebbe non essere utile. Un BLOB FILESTREAM viene reindicizzato quando viene aggiornato.  
  
##  <a name="FailoverClustering"></a> Clustering di failover  
 Per il clustering di failover, i filegroup FILESTREAM devono essere inseriti su un disco condiviso. FILESTREAM deve essere abilitato su ogni nodo nel cluster che ospiterà l'istanza FILESTREAM. Per altre informazioni, vedere [Configurazione di FILESTREAM in un cluster di failover](set-up-filestream-on-a-failover-cluster.md).  
  
##  <a name="SQLServerExpress"></a> SQL Server Express  
 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] supporta FILESTREAM. Il limite delle dimensioni di 10 GB non include il contenitore dei dati FILESTREAM.  
  
##  <a name="contained"></a> Database indipendenti  
 La funzionalità FILESTREAM richiede alcuni interventi di configurazione all'esterno del database. Pertanto un database in cui si utilizza FILESTREAM o FileTable non è completamente indipendente.  
  
 È possibile impostare l'indipendenza del database su PARTIAL se si desidera utilizzare alcune funzionalità dei database indipendenti, ad esempio gli utenti indipendenti. In tal caso, tuttavia, è necessario tenere presente che alcune impostazioni del database non sono contenute nel database e non vengono spostate automaticamente quando viene spostato il database.  
  
## <a name="see-also"></a>Vedere anche  
 [Dati BLOB &#40;Binary Large Object&#41; &#40;SQL Server&#41;](binary-large-object-blob-data-sql-server.md)  
  
  
