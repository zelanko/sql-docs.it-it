---
title: Replicare colonne Identity | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- identities [SQL Server replication]
- identity values [SQL Server replication]
- merge replication [SQL Server replication], identity range management
- publishing [SQL Server replication], identity columns
- transactional replication, identity range management
- identity columns [SQL Server], replication
ms.assetid: eb2f23a8-7ec2-48af-9361-0e3cb87ebaf7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e89bfac90a0658c8f5ba839632451187ffa9760d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52810953"
---
# <a name="replicate-identity-columns"></a>Replica di colonne Identity
  In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando si assegna la proprietà IDENTITY a una colonna, vengono automaticamente generati numeri sequenziali per le nuove righe inserite nella tabella contenente la colonna Identity. Per altre informazioni, vedere [IDENTITY &#40;proprietà&#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property). Dato che è possibile includere le colonne Identity come parte della chiave primaria, è importante evitare di inserire valori duplicati nelle colonne Identity. Per utilizzare colonne Identity in una topologia di replica con aggiornamenti in più di un nodo, è necessario che ogni nodo presente nella topologia di replica utilizzi un intervallo di valori Identity diverso, in modo da non generare duplicati.  
  
 Ad esempio, al server di pubblicazione potrebbe essere assegnato l'intervallo 1-100, al Sottoscrittore A l'intervallo 101-200 e al Sottoscrittore B l'intervallo 201-300. Se una riga viene inserita nel server di pubblicazione e il valore Identity è, ad esempio, 65, tale valore viene replicato in ogni Sottoscrittore. Durante l'inserimento dei dati nei Sottoscrittori, il valore della colonna Identity nella tabella dei Sottoscrittori non viene incrementato, bensì viene inserito il valore letterale di 65. Il valore della colonna Identity viene incrementato solo in seguito a inserimenti da parte dell'utente e non a inserimenti generati dall'agente di replica.  
  
 La replica consente di gestire le colonne Identity di tutti i tipi di pubblicazione e sottoscrizione. È pertanto possibile scegliere di gestire manualmente le colonne oppure di gestirle automaticamente tramite la replica.  
  
> [!NOTE]  
>  Non è consentito aggiungere una colonna Identity a una tabella pubblicata, perché ciò può impedire la convergenza dei dati durante la replica della colonna nel Sottoscrittore. I valori della colonna Identity nel server di pubblicazione dipendono dall'ordine in cui vengono fisicamente archiviate le righe della tabella interessata. Nel caso in cui le righe siano state archiviate in modo diverso nel Sottoscrittore, il valore della colonna Identity può essere diverso per le stesse righe.  
  
## <a name="specifying-an-identity-range-management-option"></a>Specifica delle opzioni di gestione degli intervalli di valori Identity  
 Nella replica sono disponibili tre opzioni di gestione degli intervalli di valori Identity:  
  
-   Automatico. Questa opzione viene utilizzata per la replica transazionale e di merge con aggiornamenti nel Sottoscrittore. Specificare gli intervalli per il server di pubblicazione e i Sottoscrittori. L'assegnazione dei nuovi intervalli viene gestita automaticamente. Nella colonna Identity nel Sottoscrittore viene impostata l'opzione NOT FOR REPLICATION, in modo che il valore della colonna nel Sottoscrittore venga incrementato solo nel caso di inserimenti da parte dell'utente.  
  
    > [!NOTE]  
    >  È necessario sincronizzare i Sottoscrittori con il server di pubblicazione per ricevere i nuovi intervalli. Dato che gli intervalli di valori Identity vengono assegnati automaticamente ai Sottoscrittori, è possibile che un Sottoscrittore esaurisca gli intervalli disponibili se ne richiede ripetutamente di nuovi.  
  
-   Manuale. Questa opzione viene utilizzata per la replica snapshot e transazionale con aggiornamenti nel Sottoscrittore, per la replica transazionale peer-to-peer oppure se l'applicazione richiede il controllo degli intervalli di valori Identity a livello di programmazione. Se si sceglie la gestione manuale, è necessario verificare che gli intervalli vengano assegnati al server di pubblicazione e a tutti i Sottoscrittori e che vengano assegnati nuovi intervalli se quelli iniziali sono già in uso. Nella replica l'opzione NOT FOR REPLICATION viene impostata nella colonna Identity del Sottoscrittore.  
  
-   Nessuna. Questa opzione è consigliata solo per la compatibilità con le versioni precedenti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ed è disponibile solo dall'interfaccia delle stored procedure delle pubblicazioni transazionali.  
  
 Per specificare un'opzione di gestione degli intervalli di valori Identity, vedere [Gestire le colonne Identity](manage-identity-columns.md).  
  
## <a name="assigning-identity-ranges"></a>Assegnazione degli intervalli di valori Identity  
 In questa sezione vengono descritti i diversi metodi di assegnazione degli intervalli utilizzati per la replica di tipo merge e per la replica transazionale.  
  
 Nella replica di colonne Identity è opportuno considerare due tipi di intervalli, ovvero gli intervalli assegnati al server di pubblicazione e ai Sottoscrittori e l'intervallo del tipo di dati della colonna. Nella tabella seguente vengono illustrati gli intervalli disponibili per i tipi di dati utilizzati in genere nelle colonne Identity. L'intervallo è applicato a tutti i nodi presenti in una topologia. Ad esempio, se si usa `smallint` iniziale di 1 con un incremento di 1, il numero massimo di inserimenti è 32.767 per il server di pubblicazione e tutti i sottoscrittori. Il numero effettivo di inserimenti dipende dal fatto che vi siano o meno gap nei valori utilizzati e che venga utilizzato o meno un valore soglia. Per ulteriori informazioni sulle soglie, vedere le sezioni seguenti relative alla replica di merge e alla replica transazionale con sottoscrizioni ad aggiornamento in coda.  
  
 Se dopo un inserimento il server di pubblicazione esaurisce il proprio intervallo di valori Identity, è possibile assegnare automaticamente un nuovo intervallo a condizione che l'inserimento sia stato eseguito da un membro del ruolo predefinito del database **db_owner** . Se l'inserimento è stato eseguito da un utente che non dispone di quel ruolo, è necessario che l'agente di lettura log, l'agente di merge o l'utente che è membro del ruolo **db_owner** esegua la stored procedure [sp_adjustpublisheridentityrange &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql). Nel caso di pubblicazioni transazionali, l'agente di lettura log deve essere in esecuzione per allocare automaticamente un nuovo intervallo di valori (per impostazione predefinita l'agente viene eseguito continuamente).  
  
> [!WARNING]  
>  Durante l'inserimento di un batch di grandi dimensioni, il trigger di replica viene generato solo una volta, non per ogni riga inserita. Questa condizione può comportare un errore dell'istruzione di inserimento se un intervallo di valori Identity viene esaurito durante un inserimento di grandi dimensioni, ad esempio un'istruzione `INSERT INTO`.  
  
|Tipo di dati|Intervallo|  
|---------------|-----------|  
|`tinyint`|Non supportato per la gestione automatica|  
|`smallint`|da -2^15 (-32.768) a 2^15-1 (32.767)|  
|`int`|da -2^31 (-2.147.483.648) a 2^31-1 (2.147.483.647)|  
|`bigint`|da -2^63 (-9.223.372.036.854.775.808) a 2^63-1 (9.223.372.036.854.775.807)|  
|`decimal` e `numeric`|da -10^38+1 a 10^38-1|  
  
> [!NOTE]  
>  Per creare un numero a incremento automatico da usare in più tabelle o da chiamare dalle applicazioni senza fare riferimento ad alcuna tabella, vedere [Numeri di sequenza](../../sequence-numbers/sequence-numbers.md).  
  
### <a name="merge-replication"></a>Replica di tipo merge  
 Gli intervalli di valori Identity vengono gestiti dal server di pubblicazione e distribuiti ai Sottoscrittori dall'agente di merge. In una gerarchia di ripubblicazione, invece, gli intervalli vengono gestiti dal server di pubblicazione radice e dai server di ripubblicazione. I valori Identity vengono assegnati da un pool nel server di pubblicazione. Se si aggiunge un articolo con una colonna Identity a una pubblicazione mediante Creazione guidata nuova pubblicazione o usando la stored procedure [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql), è necessario specificare i valori seguenti:  
  
-   Il parametro **@identity_range** , che controlla le dimensioni dell'intervallo di valori Identity inizialmente allocato sia nel server di pubblicazione sia nei Sottoscrittori con sottoscrizioni client.  
  
    > [!NOTE]  
    >  Per i Sottoscrittori che eseguono le precedenti versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], questo parametro, e non il parametro **@pub_identity_range** , controlla anche le dimensioni dell'intervallo di valori Identity nei Sottoscrittori di ripubblicazione.  
  
-   Il parametro **@pub_identity_range** , che controlla le dimensioni dell'intervallo di valori Identity per la ripubblicazione allocato nei Sottoscrittori con sottoscrizioni server ed è necessario per la ripubblicazione dei dati. Tutti i Sottoscrittori con sottoscrizioni server ricevono un intervallo per la ripubblicazione, anche se non eseguono la ripubblicazione dei dati.  
  
-   Il parametro **@threshold** , utilizzato per determinare quando è necessario un nuovo intervallo di valori Identity per una sottoscrizione di [!INCLUDE[ssEW](../../../includes/ssew-md.md)] o una versione precedente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Ad esempio, è possibile specificare 10.000 per **@identity_range** e 500.000 per **@pub_identity_range**. Al server di pubblicazione e a tutti i Sottoscrittori che eseguono [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva, incluso il Sottoscrittore con la sottoscrizione server, viene assegnato un intervallo primario di 10000. Al Sottoscrittore con la sottoscrizione server viene inoltre assegnato un intervallo primario di 500000, che può essere utilizzato dai Sottoscrittori che eseguono la sincronizzazione con il Sottoscrittore di ripubblicazione. È inoltre necessario specificare i parametri **@identity_range**, **@pub_identity_range**e **@threshold** per gli articoli della pubblicazione nel Sottoscrittore di ripubblicazione.  
  
 Tutti i Sottoscrittori che eseguono [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva ricevono inoltre un intervallo di valori Identity secondario. Questo valore secondario ha le stesse dimensioni dell'intervallo primario. Quando quest'ultimo si esaurisce viene utilizzato l'intervallo secondario. L'agente di merge assegna al Sottoscrittore un nuovo intervallo, che diventa l'intervallo secondario. In questo modo, quando vengono utilizzati i valori Identity del Sottoscrittore il processo continua.  
  
  
### <a name="transactional-replication-with-queued-updating-subscriptions"></a>Replica transazionale con sottoscrizioni ad aggiornamento in coda  
 Gli intervalli di valori Identity vengono gestiti dal server di distribuzione e distribuiti ai Sottoscrittori dall'agente di distribuzione. I valori Identity vengono assegnati da un pool nel server di distribuzione. Le dimensioni del pool dipendono dalle dimensioni del tipo di dati e dall'incremento utilizzato per la colonna Identity. Se si aggiunge un articolo con una colonna Identity a una pubblicazione mediante Creazione guidata nuova pubblicazione o usando la stored procedure [sp_addarticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql), è necessario specificare i valori seguenti:  
  
-   Il parametro **@identity_range** , che controlla le dimensioni dell'intervallo di valori Identity inizialmente allocato a tutti i Sottoscrittori.  
  
-   Il parametro **@pub_identity_range** , che controlla le dimensioni dell'intervallo di valori Identity allocato al server di pubblicazione.  
  
-   Il parametro **@threshold** , utilizzato per determinare quando è necessario un nuovo intervallo di valori Identity per una sottoscrizione.  
  
 Ad esempio, è possibile specificare 10.000 per **@pub_identity_range**, 1000 per **@identity_range** (presupponendo aggiornamenti minori nel Sottoscrittore) e 80% per **@threshold**. Dopo 800 inserimenti in un Sottoscrittore, pari all'80% di 1000, al Sottoscrittore viene assegnato un nuovo intervallo. Dopo 8.000 inserimenti nel server di pubblicazione, al server di pubblicazione viene assegnato un nuovo intervallo. A questo punto vi sarà un gap nell'intervallo di valori Identity della tabella. Specificando una soglia più elevata si avranno gap più piccoli, ma il sistema sarà meno tollerante agli errori. Se per qualche ragione non è possibile eseguire l'agente di distribuzione, i Sottoscrittori potrebbero esaurire più facilmente i valori Identity.  
  
## <a name="assigning-ranges-for-manual-identity-range-management"></a>Assegnazione di intervalli per la gestione manuale degli intervalli di valori Identity  
 Se si sceglie la gestione manuale, è necessario verificare che il server di pubblicazione e tutti i Sottoscrittori utilizzino intervalli di valori Identity diversi. Si consideri, ad esempio, una tabella nel server di pubblicazione con una colonna Identity definita come `IDENTITY(1,1)`: la colonna Identity comincia col valore 1 e viene incrementata di 1 ogni volta che viene inserita una riga. Se la tabella nel server di pubblicazione ha 5.000 righe e si prevede una crescita nella tabella superiore alla durata dell'applicazione, per il server di pubblicazione si potrebbe utilizzare l'intervallo 1-10.000. Nel caso vi siano due Sottoscrittori, per il Sottoscrittore A si potrebbe usare l'intervallo 10.001-20.000 e per il Sottoscrittore B l'intervallo 20.001-30.000.  
  
 Dopo aver inizializzato un Sottoscrittore con uno snapshot o altri metodi, eseguire DBCC CHECKIDENT per assegnare al Sottoscrittore un punto di partenza per l'intervallo di valori Identity. Ad esempio, nel Sottoscrittore A si eseguirà `DBCC CHECKIDENT('<TableName>','reseed',10001)`, mentre nel Sottoscrittore B si eseguirà `CHECKIDENT('<TableName>','reseed',20001)`.  
  
 Per assegnare nuovi intervalli al server di pubblicazione o ai Sottoscrittori, eseguire DBCC CHECKIDENT e specificare un nuovo valore per reinizializzare la tabella. È consigliabile definire un metodo per determinare quando è necessario assegnare un nuovo intervallo. Ad esempio, nell'applicazione potrebbe esserci un meccanismo che rileva quando un nodo sta per esaurire il proprio intervallo e quindi consente di assegnare un nuovo intervallo mediante DBCC CHECKIDENT. È inoltre possibile aggiungere un vincolo CHECK per impedire che venga aggiunta una riga se ciò determina l'utilizzo di un valore Identity non compreso nell'intervallo disponibile.  
  
## <a name="handling-identity-ranges-after-a-database-restore"></a>Gestione degli intervalli di valori Identity dopo il ripristino di un database  
 Se si utilizza la gestione automatica, quando un Sottoscrittore viene ripristinato da un backup, viene richiesto automaticamente un nuovo intervallo di valori Identity. Se un server di pubblicazione viene ripristinato da un backup, è necessario verificare che al server di pubblicazione venga assegnato l'intervallo appropriato. Per la replica di tipo merge, assegnare un nuovo intervallo mediante [sp_restoremergeidentityrange &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-restoremergeidentityrange-transact-sql). Nella replica transazionale determinare il valore massimo utilizzato e quindi impostare il punto di partenza dei nuovi intervalli. Utilizzare la procedura seguente dopo aver ripristinato il database di pubblicazione:  
  
1.  Arrestare tutte le attività di tutti i Sottoscrittori.  
  
2.  Per ogni tabella pubblicata che include una colonna Identity:  
  
    1.  Nel database di sottoscrizione di ogni Sottoscrittore eseguire `IDENT_CURRENT('<TableName>')`.  
  
    2.  Registrare il valore massimo rilevato in tutti i Sottoscrittori.  
  
    3.  Nel database di pubblicazione del server di pubblicazione eseguire `DBCC CHECKIDENT(<TableName>','reseed',<HighestValueFound+1>`.  
  
    4.  Nel database di pubblicazione del server di pubblicazione eseguire `sp_adjustpublisheridentityrange <PublicationName>, <TableName>`.  
  
    > [!NOTE]  
    >  Se il valore nella colonna Identity viene impostato per essere decrementato anziché incrementato, registrare il valore minimo rilevato e quindi reinizializzare tale valore.  
  
## <a name="see-also"></a>Vedere anche  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkident-transact-sql)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](/sql/t-sql/functions/ident-current-transact-sql)   
 [IDENTITY &#40;proprietà&#41; &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql-identity-property)   
 [sp_adjustpublisheridentityrange &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adjustpublisheridentityrange-transact-sql)  
  
  
