---
title: Configurare operazioni parallele sugli indici | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index parallel operations [SQL Server]
- processors [SQL Server], parallel index operations
- max degree of parallelism option
- MAXDOP index option, parallel index operations
- parallel index operations [SQL Server]
ms.assetid: 8ec8c71e-5fc1-443a-92da-136ee3fc7f88
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d39a59e69b238d36aa2c07cfd9dfe94f0c977b44
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67583184"
---
# <a name="configure-parallel-index-operations"></a>Configurazione di operazioni parallele sugli indici
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  In questo argomento viene definito il massimo grado di parallelismo e viene spiegato come modificare questa impostazione in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Nei computer multiprocessore che eseguono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition o versioni successive, le istruzioni per gli indici, proprio come le altre query, possono utilizzare più processori per eseguire le operazioni di analisi, ordinamento e indicizzazione associate all'istruzione. Il numero di processori usati per eseguire una singola istruzione per gli indici è determinato dall'opzione di configurazione [max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) , dal carico di lavoro corrente e dalle statistiche dell'indice. L'opzione max degree of parallelism determina il numero massimo di processori da utilizzare nell'esecuzione di piani paralleli. Se in [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] viene rilevato che il sistema è occupato, il grado di parallelismo dell'operazione di indice viene automaticamente ridotto prima che l'esecuzione dell'istruzione venga avviata. Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] consente inoltre di ridurre il grado di parallelismo se la colonna chiave iniziale di un indice non partizionato ha un numero limitato di valori distinti o se la frequenza di ciascun valore distinto varia in modo significativo.  
  
> [!NOTE]  
>  Le operazioni parallele sugli indici sono disponibili solo in alcune edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere Funzionalità supportate dalle edizioni di SQL Server 2016  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Security](#Security)  
  
-   **Per configurare l'opzione max degree of parallelism utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Il numero di processori utilizzati da Query Optimizer implica normalmente le prestazioni ottimali. Tuttavia, operazioni come la creazione, la ricompilazione o l'eliminazione di indici di grandi dimensioni utilizzano molte risorse e possono determinare una mancanza di risorse per le altre applicazioni e operazioni di database per la durata dell'operazione di indice. Quando si verifica questo problema, è possibile configurare manualmente il numero massimo di processori utilizzati per eseguire l'istruzione per l'indice limitando il numero di processori da utilizzare per l'operazione di indice.  
  
-   L'opzione di indice MAXDOP è prioritaria rispetto all'opzione di configurazione max degree of parallelism solo per la query che specifica tale opzione. La tabella seguente elenca i valori integer validi che è possibile specificare con l'opzione di configurazione max degree of parallelism e l'opzione di indice MAXDOP.  
  
    |valore|Descrizione|  
    |-----------|-----------------|  
    |0|Specifica che il server determina il numero di CPU utilizzate, a seconda del carico di lavoro del sistema corrente. Si tratta del valore predefinito e dell'impostazione consigliata.|  
    |1|Disattiva la generazione di piani paralleli. L'operazione verrà eseguita in modo serializzato.|  
    |2-64|Limita il numero di processori al valore specificato. È possibile che il numero possa essere ridotto in base al carico di lavoro corrente. Se viene specificato un valore maggiore di quello delle CPU disponibili, viene utilizzato l'effettivo numero di CPU disponibili.|  
  
-   L'esecuzione dell'indice in parallelo e l'opzione di indice MAXDOP si applicano alle istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] seguenti:  
  
    -   CREATE INDEX  
  
    -   ALTER INDEX REBUILD  
  
    -   DROP INDEX (si applica solo agli indici cluster).  
  
    -   ALTER TABLE ADD (indice) CONSTRAINT  
  
    -   ALTER TABLE DROP (indice cluster) CONSTRAINT  
  
-   L'opzione di indice MAXDOP non può essere specificata nell'istruzione ALTER INDEX REORGANIZE.  
  
-   I requisiti di memoria per le operazioni di indice partizionato che richiedono l'ordinamento possono essere maggiori se Query Optimizer applica i gradi di parallelismo all'operazione di compilazione. Maggiori i gradi di parallelismo, maggiori i requisiti di memoria. Per altre informazioni, vedere [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per la tabella o la vista.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-index"></a>Per impostare l'opzione max degree of parallelism su un indice  
  
1.  In Esplora oggetti fare clic sul segno più per espandere il database contenente la tabella in cui si desidera impostare l'opzione max degree of parallelism per un indice.  
  
2.  Espandere la cartella **Tabelle** .  
  
3.  Fare clic sul segno più per espandere la tabella in cui si desidera impostare l'opzione max degree of parallelism per un indice.  
  
4.  Espandere la cartella **Indici** .  
  
5.  Fare clic con il pulsante destro del mouse sull'indice per cui si vuole impostare il massimo grado di parallelismo e scegliere **Proprietà**.  
  
6.  In **Selezione pagina**selezionare **Opzioni**.  
  
7.  Selezionare **Maximum degree of parallelism**e immettere un valore compreso tra 1 e 64.  
  
8.  Fare clic su **OK**.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-existing-index"></a>Per impostare l'opzione max degree of parallelism su un indice esistente  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    /*Alters the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table so that, if the server has eight or more processors, the Database Engine will limit the execution of the index operation to eight or fewer processors.  
    */  
    ALTER INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor  
    REBUILD WITH (MAXDOP=8);   
    GO  
    ```  
  
 Per altre informazioni, vedere [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
#### <a name="set-max-degree-of-parallelism-on-a-new-index"></a>Impostare l'opzione max degree of parallelism su un nuovo indice  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE INDEX IX_ProductVendor_NewVendorID   
    ON Purchasing.ProductVendor (BusinessEntityID)  
    WITH (MAXDOP=8);  
    GO  
    ```  
  
 Per altre informazioni, vedere [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
  
