---
title: Estensioni a AdventureWorks per illustrare OLTP in memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0186b7f2-cead-4203-8360-b6890f37cde8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b317ffdb38c06cafe09ff786004b7ac144d0b18
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228470"
---
# <a name="extensions-to-adventureworks-to-demonstrate-in-memory-oltp"></a>Estensioni a AdventureWorks per illustrare OLTP in memoria
    
## <a name="overview"></a>Panoramica  
 In questo esempio viene illustrata la nuova funzionalità di [!INCLUDE[hek_2](../includes/hek-2-md.md)] , che fa parte di [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. Vengono mostrate le nuove tabelle ottimizzate per la memoria e le nuove stored procedure compilate in modo nativo, utilizzabili per illustrare i vantaggi a livello di prestazioni di [!INCLUDE[hek_2](../includes/hek-2-md.md)].  
  
> [!NOTE]  
>  Per visualizzare questo argomento per SQL Server 2016, vedere [Estensioni a AdventureWorks per illustrare OLTP in memoria](https://msdn.microsoft.com/library/mt465764.aspx)  
  
 Nell'esempio viene eseguita la migrazione di 5 tabelle del database AdventureWorks a tabelle ottimizzate per la memoria. Inoltre, è incluso un carico di lavoro dimostrativo di ordini vendita. Questo carico di lavoro dimostrativo può essere utilizzato per verificare i vantaggi a livello di prestazioni di [!INCLUDE[hek_2](../includes/hek-2-md.md)] nel server.  
  
 Nella descrizione dell'esempio vengono discussi i compromessi raggiunti quando si esegue la migrazione delle tabelle a [!INCLUDE[hek_2](../includes/hek-2-md.md)] per tener conto delle funzionalità non (ancora) supportate per le tabelle ottimizzate per la memoria in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
 La documentazione di questo esempio è strutturata come segue:  
  
-   [Prerequisiti](#Prerequisites) per l'installazione dell'esempio e l'esecuzione del carico di lavoro dimostrativo  
  
-   Istruzioni per [Installazione dell'esempio di In-Memory OLTP basato su AdventureWorks](#InstallingtheIn-MemoryOLTPsamplebasedonAdventureWorks)  
  
-   [Descrizione delle tabelle e delle procedure di esempio](#Descriptionofthesampletablesandprocedures) : include le descrizioni delle tabelle e delle procedure aggiunte a AdventureWorks dall' [!INCLUDE[hek_2](../includes/hek-2-md.md)] esempio, oltre a considerazioni sulla migrazione di alcune delle tabelle originali di AdventureWorks a ottimizzate per la memoria  
  
-   Istruzioni per l'esecuzione di [Misurazioni delle prestazioni con il carico di lavoro dimostrativo](#PerformanceMeasurementsusingtheDemoWorkload): sono incluse le istruzioni per l'installazione e l'esecuzione di ostress, uno strumento usato per gestire il carico di lavoro nonché per eseguire il carico di lavoro dimostrativo stesso  
  
-   [Utilizzo di memoria e spazio su disco nell'esempio](#MemoryandDiskSpaceUtilizationintheSample)  
  
##  <a name="Prerequisites"></a>Prerequisiti  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]RTM-Evaluation, Developer o Enterprise Edition  
  
-   Per il test delle prestazioni, un server con specifiche simili all'ambiente di produzione. Per questo particolare esempio sono necessari almeno 16 GB di memoria disponibili per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per linee guida generali sull'hardware [!INCLUDE[hek_2](../includes/hek-2-md.md)]per, vedere il post di Blog seguente:[https://blogs.technet.com/b/dataplatforminsider/archive/2013/08/01/hardware-considerations-for-in-memory-oltp-in-sql-server-2014.aspx](https://blogs.technet.com/b/dataplatforminsider/archive/2013/08/01/hardware-considerations-for-in-memory-oltp-in-sql-server-2014.aspx)  
  
##  <a name="InstallingtheIn-MemoryOLTPsamplebasedonAdventureWorks"></a>Installazione dell' [!INCLUDE[hek_2](../includes/hek-2-md.md)] esempio basato su AdventureWorks  
 Per installare l'esempio, seguire i passaggi riportati di seguito.  
  
1.  Scaricare l'archivio per il backup completo del database AdventureWorks2014:  
  
    1.  Aprire il codice seguente [https://msftdbprodsamples.codeplex.com/downloads/get/880661](https://msftdbprodsamples.codeplex.com/downloads/get/880661):.  
  
    2.  Quando richiesto, salvare il file in una cartella locale.  
  
2.  Estrarre il file **AdventureWorks2014.bak** in una cartella locale, ad esempio 'c:\temp'.  
  
3.  Ripristinare il backup del database usando [!INCLUDE[tsql](../includes/tsql-md.md)] o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]:  
  
    1.  Identificare la cartella di destinazione e il nome del file di dati, ad esempio  
  
         'h:\DATA\AdventureWorks2014_Data.mdf'  
  
    2.  Identificare la cartella di destinazione e il nome del file di log, ad esempio  
  
         'i:\DATA\AdventureWorks2014_log.ldf'  
  
        1.  Il file di log deve essere posizionato in un'unità diversa dal file di dati, idealmente un'unità a bassa latenza, ad esempio l'archiviazione sull'unità SSD o PCIe, per prestazioni ottimali.  
  
     Script T-SQL di esempio:  
  
    ```  
    RESTORE DATABASE [AdventureWorks2014]   
      FROM DISK = N'C:\temp\AdventureWorks2014.bak'   
        WITH FILE = 1,    
      MOVE N'AdventureWorks2014_Data' TO N'h:\DATA\AdventureWorks2014_Data.mdf',    
      MOVE N'AdventureWorks2014_Log' TO N'i:\DATA\AdventureWorks2014_log.ldf'  
     GO  
    ```  
  
4.  Impostare il proprietario del database su un account di accesso nel server, eseguendo il comando riportato di seguito nella finestra Query di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]:  
  
    ```  
    ALTER AUTHORIZATION ON DATABASE::AdventureWorks2014 TO [<NewLogin>]  
    ```  
  
5.  Scaricare lo script di esempio[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] " [!INCLUDE[hek_2](../includes/hek-2-md.md)] RTM Sample. SQL" dall' [esempio di OLTP in memoria SQL Server 2014 RTM](https://go.microsoft.com/fwlink/?LinkID=396372) in una cartella locale.  
  
6.  Aggiornare il valore della variabile "checkpoint_files_location" nello script "[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] RTM [!INCLUDE[hek_2](../includes/hek-2-md.md)] Sample. SQL" per puntare al percorso di destinazione per i file del [!INCLUDE[hek_2](../includes/hek-2-md.md)] checkpoint. I file del checkpoint devono essere posizionati in un'unità con prestazioni di I/O sequenziali ottimali.  
  
     Aggiornare il valore della variabile 'database_name' in modo da puntare al database AdventureWorks2014.  
  
    1.  Assicurarsi di includere la barra rovesciata\' "come parte del nome del percorso  
  
    2.  Esempio:  
  
        ```  
        :setvar checkpoint_files_location "d:\DBData\"  
        ...  
        :setvar database_name "AdventureWorks2014"  
        ```  
  
7.  Eseguire lo script di esempio in una delle due modalità riportate di seguito.  
  
    1.  Utilizzando l'utilità della riga di comando sqlcmd. Ad esempio, eseguendo il comando riportato di seguito dal prompt della riga di comando nella cartella contenente lo script:  
  
        ```  
        sqlcmd -S . -E -i "ssSQL14 RTM hek_2 Sample.sql"  
        ```  
  
    2.  Utilizzando Management Studio:  
  
        1.  Aprire lo script "[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] RTM [!INCLUDE[hek_2](../includes/hek-2-md.md)] Sample. SQL" in una finestra di query  
  
        2.  Connettersi al server di destinazione contenente il database AdventureWorks2014  
  
        3.  Abilitare la modalità SQLCMD, facendo clic su "query-> modalità SQLCMD"  
  
        4.  Fare clic sul pulsante ' Esegui ' per eseguire lo script  
  
##  <a name="Descriptionofthesampletablesandprocedures"></a>Descrizione delle tabelle e delle procedure di esempio  
 Nell'esempio vengono create nuove tabelle per i prodotti e gli ordini vendita, basate sulle tabelle esistenti in AdventureWorks. Lo schema delle nuove tabelle è simile a quello delle tabelle esistenti, con alcune differenze, come illustrato di seguito.  
  
 Nelle nuove tabelle ottimizzate per la memoria è incluso il suffisso '_inmem'. Nell'esempio sono incluse anche tabelle corrispondenti con il suffisso "_ondisk". Queste tabelle possono essere usate per un confronto uno-a-uno tra le prestazioni delle tabelle ottimizzate per la memoria e quelle basate su disco nel sistema.  
  
 Si noti che le tabelle ottimizzate per la memoria utilizzate nel carico di lavoro per il confronto delle prestazioni sono completamente durevoli e con registrazione completa. Con queste tabelle non viene sacrificata la durabilità o l'affidabilità per ottenere un miglioramento delle prestazioni.  
  
 Il carico di lavoro di destinazione per questo esempio è rappresentato dall'elaborazione degli ordini vendita, in cui vengono prese in considerazione anche le informazioni sui prodotti e sugli sconti. A questo scopo, vengono utilizzate le tabelle SalesOrderHeader, SalesOrderDetail, Product, SpecialOffer e SpecialOfferProduct.  
  
 Per inserire gli ordini vendita e aggiornare le informazioni sulla spedizione di un determinato ordine vendita vengono utilizzate due nuove stored procedure: Sales.usp_InsertSalesOrder_inmem e Sales.usp_UpdateSalesOrderShipInfo_inmem.  
  
 Nel nuovo schema "Demo" sono incluse stored procedure e tabelle helper per eseguire un carico di lavoro dimostrativo.  
  
 In concreto, nell'esempio di [!INCLUDE[hek_2](../includes/hek-2-md.md)] vengono aggiunti ad AdventureWorks gli oggetti seguenti:  
  
### <a name="tables-added-by-the-sample"></a>Tabelle aggiunte con l'esempio  
  
#### <a name="the-new-tables"></a>Nuove tabelle  
 Sales.SalesOrderHeader_inmem  
  
-   Informazioni di intestazione sugli ordini vendita. Ogni ordine vendita è rappresentato da una riga nella tabella.  
  
 Sales.SalesOrderDetail_inmem  
  
-   Dettagli degli ordini vendita. Ogni voce di un ordine vendita è rappresentato da una riga nella tabella.  
  
 Sales.SpecialOffer_inmem  
  
-   Informazioni sulle offerte speciali, inclusa la percentuale di sconto associata a ogni offerta.  
  
 Sales.SpecialOfferProduct_inmem  
  
-   Tabella di riferimento tra offerte speciali e prodotti. Ogni offerta speciale può includere zero o più prodotti e ogni prodotto può essere caratterizzato da zero o più offerte speciali.  
  
 Production.Product_inmem  
  
-   Informazioni sui prodotti, tra cui il prezzo di listino.  
  
 Demo.DemoSalesOrderDetailSeed  
  
-   Utilizzata nel carico di lavoro dimostrativo per creare ordini vendita di esempio.  
  
 Varianti basate su disco delle tabelle:  
  
-   Sales.SalesOrderHeader_ondisk  
  
-   Sales.SalesOrderDetail_ondisk  
  
-   Sales.SpecialOffer_ondisk  
  
-   Sales.SpecialOfferProduct_ondisk  
  
-   Production.Product_ondisk  
  
#### <a name="differences-between-original-disk-based-and-the-and-new-memory-optimized-tables"></a>Differenze tra le tabelle basate su disco originali e le nuove tabelle ottimizzate per la memoria  
 In genere, nelle nuove tabelle introdotte con questo esempio vengono utilizzate le stesse colonne e gli stessi tipi di dati delle tabelle originali. Tuttavia, esistono alcune differenze elencate di seguito, insieme a una spiegazione logica delle modifiche.  
  
 Sales.SalesOrderHeader_inmem  
  
-   I *vincoli predefiniti* sono supportati per le tabelle ottimizzate per la memoria e la maggior parte dei vincoli predefiniti di cui è stata eseguita la migrazione. Tuttavia, nella tabella originale Sales.SalesOrderHeader sono contenuti due vincoli predefiniti tramite cui viene recuperata la data corrente per le colonne OrderDate e ModifiedDate. In un carico di lavoro di elaborazione dell'ordine a velocità effettiva elevata con molta concorrenza, qualsiasi risorsa globale può diventare un punto di contesa. L'ora di sistema è un esempio di risorsa globale e si è notato che può costituire un collo di bottiglia quando si esegue un carico di lavoro di [!INCLUDE[hek_2](../includes/hek-2-md.md)] con ordini vendita, in particolare se l'ora di sistema deve essere recuperata per più colonne nell'intestazione degli ordini vendita, nonché per i dettagli degli ordini vendita. In questo esempio il problema è stato risolto recuperando l'ora di sistema solo una volta per ogni ordine vendita inserito e il valore in questione viene utilizzato per le colonne di tipo datetime in SalesOrderHeader_inmem e in SalesOrderDetail_inmem, nella stored procedure Sales.usp_InsertSalesOrder_inmem.  
  
-   Tipi definiti dall'utente *alias* : la tabella originale usa due tipi di dati alias definiti dall'utente (UDT). OrderNumber e dbo. AccountNumber, rispettivamente per le colonne PurchaseOrderNumber e AccountNumber. 
  [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] non supporta il tipo di dati alias definito dall'utente per le tabelle ottimizzate per la memoria, pertanto le nuove tabelle usano rispettivamente i tipi di dati di sistema nvarchar(25) e nvarchar(15).  
  
-   *Colonne che ammettono i valori null nelle chiavi di indice* . nella tabella originale la colonna SalesPersonID ammette i valori null, mentre nelle nuove tabelle non ammette i valori null e ha un vincolo predefinito con valore (-1). Ciò è dovuto al fatto che gli indici nelle tabelle ottimizzate per la memoria non possono disporre di colonne che ammettono i valori Null nella chiave di indice; -1 è un surrogato di NULL in questo caso.  
  
-   *Colonne calcolate* : le colonne calcolate SalesOrderNumber e TotalDue vengono omesse, poiché [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] in non sono supportate le colonne calcolate nelle tabelle ottimizzate per la memoria. La nuova vista Sales.vSalesOrderHeader_extended_inmem riflette le colonne SalesOrderNumber e TotalDue. Pertanto, può essere utilizzata qualora queste colonne fossero necessarie.  
  
-   I *vincoli FOREIGN KEY* non sono supportati per le tabelle ottimizzate [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]per la memoria in. Inoltre, SalesOrderHeader_inmem è una tabella attiva nel carico di lavoro di esempio e i vincoli di chiavi esterne comportano un'ulteriore elaborazione per tutte le operazioni DML, in quanto sono necessarie ricerche in tutte le altre tabelle a cui viene fatto riferimento in questi vincoli. Pertanto, si presuppone che l'applicazione garantisca l'integrità referenziale e questa integrità non venga convalidata quando vengono inserite le righe. L'integrità referenziale per i dati di questa tabella può essere verificata utilizzando la stored procedure dbo.usp_ValidateIntegrity, tramite lo script seguente:  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SalesOrderHeader_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
-   I *vincoli check* non sono supportati per le tabelle ottimizzate per la memoria nel Server sq 2014. L'integrità di dominio viene convalidata insieme all'integrità referenziale tramite questo script:  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SalesOrderHeader_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
-   *Rowguid* : la colonna rowguid viene omessa. Anche se uniqueidentifier è il supporto per le tabelle ottimizzate per la memoria, l'opzione ROWGUIDCOL non è supportata in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. Le colonne di questo tipo vengono in genere utilizzate per la replica di tipo merge o per le tabelle con colonne FILESTREAM. Nell'esempio sono escluse entrambe.  
  
 Sales.SalesOrderDetail  
  
-   *Vincoli predefiniti* : Analogamente a SalesOrderHeader, non viene eseguita la migrazione del vincolo predefinito che richiede la data/ora di sistema, ma il stored procedure l'inserimento degli ordini di vendita si occupa dell'inserimento della data/ora di sistema corrente al primo inserimento.  
  
-   *Colonne calcolate* : la colonna calcolata LineTotal non è stata migrata perché le colonne calcolate non sono supportate con le tabelle ottimizzate per la memoria in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]. Per accedere a questa colonna, usare la vista Sales.vSalesOrderDetail_extended_inmem.  
  
-   *Rowguid* : la colonna rowguid viene omessa. Per informazioni dettagliate, vedere la descrizione della tabella SalesOrderHeader.  
  
-   Per i vincoli *CHECK* e di *chiave esterna* , vedere la descrizione di SalesOrderHeader. Lo script seguente può essere utilizzato per verificare le integrità di dominio e referenziale per la tabella:  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SalesOrderHeader_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
 Production.Product  
  
-   *Tipi definiti* dall'utente alias: la tabella originale usa il tipo di dati definito dall'utente dbo. Flag, equivalente al bit del tipo di dati di sistema. Nella tabella migrata viene utilizzato, in alternativa, il tipo di dati bit.  
  
-   *Regole di confronto di BIN2* : le colonne Name e ProductNumber sono incluse nelle chiavi di indice e devono quindi avere regole di [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]confronto di BIN2 in. In questo caso, si presuppone che l'applicazione non si basi sulle specifiche delle regole di confronto, quale l'esclusione della distinzione tra maiuscole e minuscole.  
  
-   *Rowguid* : la colonna rowguid viene omessa. Per informazioni dettagliate, vedere la descrizione della tabella SalesOrderHeader.  
  
-   I vincoli *Unique*, *Check* e *Foreign Key* sono rappresentati in due modi: le stored procedure product. usp_InsertProduct_inmem e Product. usp_DeleteProduct_inmem possono essere utilizzate per inserire ed eliminare i prodotti. Queste procedure convalidano l'integrità di dominio e referenziale e avranno esito negativo se l'integrità viene violata. Inoltre, lo script seguente può essere utilizzato per convalidare le integrità di dominio e referenziale senza apportarvi variazioni:  
  
    ```  
    DECLARE @o int = object_id(N'Production.Product')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
    -   Si noti che nelle stored procedure usp_InsertProduct_inmem e usp_DeleteProduct_inmem vengono prese in considerazione solo le chiavi esterne tra le tabelle migrate. I riferimenti ad altre tabelle quali ProductModel, ProductSubcategory e UnitMeasure non vengono presi in considerazione.  
  
 Sales.SpecialOffer  
  
-   I vincoli *Check* e *Foreign Key* sono rappresentati in due modi: le stored procedure Sales. usp_InsertSpecialOffer_inmem e Sales. usp_DeleteSpecialOffer_inmem possono essere utilizzate per inserire ed eliminare offerte speciali. Queste procedure convalidano l'integrità di dominio e referenziale e avranno esito negativo se l'integrità viene violata. Inoltre, lo script seguente può essere utilizzato per convalidare le integrità di dominio e referenziale senza apportarvi variazioni:  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SpecialOffer_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
-   *Rowguid* : la colonna rowguid viene omessa. Per informazioni dettagliate, vedere la descrizione della tabella SalesOrderHeader.  
  
 Sales.SpecialOfferProduct  
  
-   I *vincoli FOREIGN KEY* sono contabilizzati in due modi: il stored procedure Sales. usp_InsertSpecialOfferProduct_inmem può essere utilizzato per inserire relazioni tra offerte speciali e prodotti; Questa procedura convalida l'integrità referenziale e avrà esito negativo se l'integrità viene violata. Inoltre, lo script seguente può essere utilizzato per convalidare l'integrità referenziale senza apportarvi variazioni:  
  
    ```  
    DECLARE @o int = object_id(N'Sales.SpecialOfferProduct_inmem')  
    EXEC dbo.usp_ValidateIntegrity @o  
    ```  
  
-   *Rowguid* : la colonna rowguid viene omessa. Per informazioni dettagliate, vedere la descrizione della tabella SalesOrderHeader.  
  
#### <a name="considerations-for-indexes-on-memory-optimized-tables"></a>Considerazioni sugli indici nelle tabelle ottimizzate per la memoria  
 L'indice di base per le tabelle ottimizzate per la memoria è l'indice NONCLUSTERED, che supporta le ricerche di punti (ricerca nell'indice nel predicato di uguaglianza), le analisi dell'intervallo (ricerca nell'indice nel predicato di disuguaglianza), analisi di indici completi e analisi ordinate. Inoltre, gli indici NONCLUSTERED supportano la ricerca nelle colonne iniziali della chiave di indice. In realtà, gli indici NONCLUSTERED ottimizzati per la memoria supportano tutte le operazioni consentite dagli indici NONCLUSTERED basati su disco, con la sola eccezione che vengono eseguite analisi a ritroso. Pertanto, l'utilizzo di indici NONCLUSTERED è una scelta sicura.  
  
 Per ottimizzare ulteriormente il carico di lavoro, è possibile usare gli indici HASH. Vengono ottimizzati in particolare per le ricerche di punti e per gli inserimenti di righe. Tuttavia, è necessario considerare che non supportano le analisi dell'intervallo, le analisi ordinate o la ricerca nelle colonne iniziali della chiave di indice. Di conseguenza, prestare attenzione quando si utilizzano questi indici. Inoltre, è necessario specificare il bucket_count al momento della creazione. In genere deve essere impostato su un valore compreso tra una e due volte il numero di valori di chiave di indice; tuttavia, un valore superiore non rappresenta di solito un problema.  
  
 Vedere la documentazione online per altre informazioni sulle [linee guida relative agli indici](https://technet.microsoft.com/library/dn133166\(v=sql.120\).aspx) e sulle linee guida per [scegliere il bucket_count corretto](https://technet.microsoft.com/library/dn494956\(v=sql.120\).aspx).  
  
 Gli indici nelle tabelle migrate sono stati ottimizzati per il carico di lavoro dimostrativo dell'elaborazione degli ordini vendita. Il carico di lavoro si basa sugli inserimenti e sulle ricerche di punti nelle tabelle Sales.SalesOrderHeader_inmem e Sales.SalesOrderDetail_inmem, nonché sulle ricerche di punti nelle colonne chiavi primarie nelle tabelle Production.Product_inmem e Sales.SpecialOffer_inmem.  
  
 Sales.SalesOrderHeader_inmem prevede tre indici, che sono tutti di tipo HASH per motivi di prestazioni e perché per il carico di lavoro non sono necessarie analisi ordinate, né dell'intervallo.  
  
-   Indice HASH in (SalesOrderID): il bucket_count viene ridimensionato a 10 milioni (arrotondato fino a 16 milione), poiché il numero previsto di ordini vendita è pari a 10 milioni.  
  
-   Indice HASH in (SalesPersonID): il bucket_count è pari a 1 milione. Il set di dati fornito non include molti venditori, ma tiene conto della crescita futura, nonché delle mancate conseguenze in termini di riduzione delle prestazioni per le ricerche di punti in caso di ridimensionamento eccessivo del bucket_count.  
  
-   Indice HASH in (CustomerID): il bucket_count è pari a 1 milione. Il set di dati specificato non include molti clienti, ma tiene conto della crescita futura.  
  
 Sales.SalesOrderDetail_inmem prevede tre indici, che sono tutti di tipo HASH per motivi di prestazioni e perché per il carico di lavoro non sono necessarie analisi ordinate, né dell'intervallo.  
  
-   Indice HASH in (SalesOrderID, SalesOrderDetailID): si tratta dell'indice di chiave primaria e, anche se le ricerche in (SalesOrderID, SalesOrderDetailID) saranno rare, l'utilizzo di un indice hash per la chiave rende più veloce gli inserimenti di riga. Il bucket_count viene ridimensionato a 50 milioni (arrotondato fino a 67 milioni); il numero previsto di ordini vendita è 10 milioni che viene ridimensionato per ottenere una media di 5 articoli per ordine.  
  
-   Indice HASH in (SalesOrderID): le ricerche in base all'ordine vendita sono frequenti. È possibile individuare tutte le voci corrispondenti a un singolo ordine.  Il bucket_count viene ridimensionato a 10 milioni (arrotondato fino a 16 milione), poiché il numero previsto di ordini vendita è pari a 10 milioni.  
  
-   Indice HASH in (ProductID): il bucket_count è pari a 1 milione. Il set di dati specificato non include molti prodotti, ma tiene conto della crescita futura.  
  
 Production.Product_inmem prevede tre indici  
  
-   Indice HASH in (ProductID): le ricerche in ProductID si trovano in un percorso critico del carico di lavoro dimostrativo, pertanto si tratta di un indice hash  
  
-   Indice NONCLUSTERED in (Name): tramite esso saranno possibili analisi ordinate dei nomi dei prodotti  
  
-   Indice NONCLUSTERED in (ProductNumber): tramite esso saranno possibili analisi ordinate dei numeri dei prodotti  
  
 Sales.SpecialOffer_inmem con un indice HASH in (SpecialOfferID): le ricerche di punti delle offerte speciali si trovano nella parte essenziale del carico di lavoro dimostrativo. Il bucket_count viene ridimensionato a 1 milione per tener conto della crescita futura.  
  
 Nel carico di lavoro dimostrativo non viene fatto riferimento a Sales.SpecialOfferProduct_inmem, di conseguenza non vi sono esigenze apparenti di usare indici hash in questa tabella per ottimizzare il carico di lavoro; gli indici in (SpecialOfferID, ProductID) e (ProductID) sono NONCLUSTERED.  
  
 Si noti che nelle indicazioni sopra riportate, ad alcuni dei bucket_counts è stato applicato un ridimensionamento eccessivo, ma non ai bucket_counts per gli indici in SalesOrderHeader_inmem e SalesOrderDetail_inmem che vengono ridimensionati solo a 10 milioni di ordini vendita. Questa operazione viene eseguita per consentire l'installazione dell'esempio nei sistemi con disponibilità di memoria insufficiente, anche se in quei casi il carico di lavoro dimostrativo non può essere completato. Se si desidera scalare di oltre 10 milioni di ordini vendita, è possibile aumentare i numeri di bucket di conseguenza.  
  
#### <a name="considerations-for-memory-utilization"></a>Considerazioni sull'utilizzo della memoria  
 L'utilizzo della memoria nel database di esempio, sia prima che dopo l'esecuzione del carico di lavoro dimostrativo, è descritto nella sezione [Utilizzo della memoria per le tabelle ottimizzate per la memoria](#Memoryutilizationforthememory-optimizedtables).  
  
### <a name="stored-procedures-added-by-the-sample"></a>Stored procedure aggiunte nell'esempio  
 Di seguito sono riportate due stored procedure principali per l'inserimento dell'ordine vendita e l'aggiornamento dei dettagli sulla spedizione:  
  
-   Sales.usp_InsertSalesOrder_inmem  
  
    -   Inserisce un nuovo ordine vendita nel database e restituisce SalesOrderID per questi ordini vendita. Come parametri di input accetta i dettagli dell'intestazione dell'ordine vendita e le voci dell'ordine.  
  
    -   Parametro di output:  
  
        -   
  @SalesOrderID int: SalesOrderID per l'ordine vendita appena inserito  
  
    -   Parametri di input (obbligatori):  
  
        -   @DueDatedatetime2  
  
        -   @CustomerIDint  
  
        -   @BillToAddressIDint  
  
        -   @ShipToAddressIDint  
  
        -   @ShipMethodIDint  
  
        -   
  @SalesOrderDetails Sales.SalesOrderDetailType_inmem: TVP contenente voci dell'ordine  
  
    -   Parametri di input (facoltativi):  
  
        -   @Statustinyint  
  
        -   @OnlineOrderFlagpo'  
  
        -   
  @PurchaseOrderNumber [nvarchar](25\)  
  
        -   
  @AccountNumber [nvarchar](15\)  
  
        -   @SalesPersonIDint  
  
        -   @TerritoryIDint  
  
        -   @CreditCardIDint  
  
        -   
  @CreditCardApprovalCode [varchar](15\)  
  
        -   @CurrencyRateIDint  
  
        -   @Commentnvarchar (128)  
  
-   Sales.usp_UpdateSalesOrderShipInfo_inmem  
  
    -   Aggiornare le informazioni sulla spedizione per un ordine vendita specificato. Verranno aggiornate anche le informazioni sulla spedizione di tutte le voci dell'ordine vendita.  
  
    -   Si tratta di una stored procedure wrapper per le stored procedure compilate a livello nativo Sales.usp_UpdateSalesOrderShipInfo_native con logica di riesecuzione per gestire i potenziali (imprevisti) conflitti con transazioni simultanee con cui viene aggiornato lo stesso ordine. Per altre informazioni sulla logica di riesecuzione, vedere l'argomento nella documentazione online [qui](https://technet.microsoft.com/library/dn169141\(v=sql.120\).aspx).  
  
-   Sales.usp_UpdateSalesOrderShipInfo_native  
  
    -   Si tratta della stored procedure compilata a livello nativo tramite cui viene elaborato effettivamente l'aggiornamento delle informazioni sulla spedizione. Ciò significa che viene chiamata dalla stored procedure wrapper Sales.usp_UpdateSalesOrderShipInfo_inmem. Se tramite il client è possibile gestire gli errori e implementare la logica di riesecuzione, è possibile chiamare direttamente questa procedura, anziché usare quella wrapper.  
  
 La stored procedure seguente viene utilizzata per il carico di lavoro dimostrativo.  
  
-   Demo.usp_DemoReset  
  
    -   Reimposta la dimostrazione svuotando e reinizializzando le tabelle SalesOrderHeader e SalesOrderDetail.  
  
 Le stored procedure seguenti vengono utilizzate per l'inserimento nelle tabelle ottimizzate per la memoria ed eliminazione da queste ultime garantendo, nel contempo, le integrità di dominio e referenziale.  
  
-   Production.usp_InsertProduct_inmem  
  
-   Production.usp_DeleteProduct_inmem  
  
-   Sales.usp_InsertSpecialOffer_inmem  
  
-   Sales.usp_DeleteSpecialOffer_inmem  
  
-   Sales.usp_InsertSpecialOfferProduct_inmem  
  
 Infine, la stored procedure seguente viene utilizzata per verificare le integrità di dominio e referenziale.  
  
1.  dbo.usp_ValidateIntegrity  
  
    -   Parametro facoltativo: @object_id: ID dell'oggetto per cui convalidare l'integrità  
  
    -   Questa procedura si basa sulle tabelle dbo.DomainIntegrity, dbo.ReferentialIntegrity e dbo.UniqueIntegrity per le regole di integrità che devono essere verificate. Nell'esempio queste tabelle vengono popolate in base ai vincoli CHECK, di chiave esterna e univoci presenti per le tabelle originali nel database AdventureWorks.  
  
    -   Si basa sulle procedure helper dbo.usp_GenerateCKCheck, dbo.usp_GenerateFKCheck e dbo.GenerateUQCheck per generare il codice T-SQL necessario per eseguire i controlli di integrità.  
  
##  <a name="PerformanceMeasurementsusingtheDemoWorkload"></a>Misurazioni delle prestazioni con il carico di lavoro dimostrativo  
 Ostress è uno strumento da riga di comando sviluppato dal team di supporto [!INCLUDE[msCoName](../includes/msconame-md.md)] CSS [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Questo strumento può essere utilizzato per eseguire query o stored procedure in parallelo. È possibile configurare il numero di thread per eseguire un'istruzione T-SQL fornita in parallelo e specificare il numero di esecuzioni dell'istruzione in questo thread. Tramite ostress viene eseguita l'accelerazione dei thread e l'istruzione viene eseguita in tutti i thread in parallelo. Al termine dell'esecuzione di tutti i thread, tramite ostress verrà segnalato il tempo impiegato per il completamento dell'esecuzione di tutti i thread.  
  
### <a name="installing-ostress"></a>Installazione di ostress  
 Ostress viene installato come parte delle utilità RML. La relativa installazione non viene eseguita in modalità autonoma.  
  
 Passaggi per l'installazione:  
  
1.  Scaricare ed eseguire il pacchetto di installazione x64 per le utilità RML dalla pagina seguente:[https://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx](https://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx)  
  
2.  Se viene visualizzata una finestra di dialogo indicante l'utilizzo di determinati file, scegliere 'Continua'.  
  
### <a name="running-ostress"></a>Esecuzione di ostress  
 Ostress viene eseguito dal prompt della riga di comando. È più semplice eseguire lo strumento dal prompt dei comandi RML, installato come parte delle utilità RML.  
  
 Per aprire il prompt dei comandi RML, seguire queste istruzioni:  
  
 In Windows Server 2012 [R2] e in Windows 8 e 8.1 aprire il menu Start facendo clic sul pulsante Windows, quindi digitare 'rml'. Fare clic sul prompt dei comandi RML, che sarà disponibile nell'elenco dei risultati della ricerca.  
  
 Verificare che il prompt dei comandi si trovi nella cartella di installazione delle utilità RML. Ad esempio:  
  
 ![](../../2014/database-engine/media/SQLServer2014RTMIn-MemoryOLTP01.jpg)  
  
 Le opzioni della riga di comando per ostress possono essere visualizzate eseguendo semplicemente ostress.exe senza opzioni della riga di comando. Le opzioni principali da considerare per eseguire ostress con questo esempio sono:  
  
-   -S. Nome dell'istanza di [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] alla quale connettersi  
  
-   -E usa l'autenticazione di Windows per la connessione (impostazione predefinita); Se si utilizza [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] l'autenticazione di, utilizzare le opzioni-u e-P per specificare rispettivamente il nome utente e la password  
  
-   -d. Nome del database, per questo esempio AdventureWorks2014  
  
-   -Q. L'istruzione T-SQL da eseguire  
  
-   -n. Numero di connessioni tramite cui viene eseguita l'elaborazione di ogni query o file di input  
  
-   -r. Numero di iterazioni per ogni connessione per eseguire ogni query o file di input  
  
### <a name="demo-workload"></a>Carico di lavoro dimostrativo  
 La stored procedure principale utilizzata nel carico di lavoro dimostrativo è Sales.usp_InsertSalesOrder_inmem/ondisk. Tramite lo script riportato di seguito viene costruito un parametro con valori di tabella (TVP) con dati di esempio e viene chiamata la procedura per inserire un ordine vendita con 5 voci.  
  
 Lo strumento ostress viene utilizzato per eseguire le chiamate di stored procedure in parallelo, per simulare i client tramite cui vengono inseriti contemporaneamente gli ordini vendita.  
  
 Reimpostare la dimostrazione dopo ogni esecuzione di test di stress eseguendo Demo.usp_DemoReset. Tramite questa procedura vengono eliminate le righe nelle tabelle ottimizzate per la memoria, vengono troncate le tabelle basate su disco e viene eseguito un checkpoint del database.  
  
 Lo script seguente viene eseguito simultaneamente per simulare un carico di lavoro di elaborazione degli ordini vendita:  
  
```  
DECLARE   
      @i int = 0,   
      @od Sales.SalesOrderDetailType_inmem,   
      @SalesOrderID int,   
      @DueDate datetime2 = sysdatetime(),   
      @CustomerID int = rand() * 8000,   
      @BillToAddressID int = rand() * 10000,   
      @ShipToAddressID int = rand() * 10000,   
      @ShipMethodID int = (rand() * 5) + 1;   
  
INSERT INTO @od   
SELECT OrderQty, ProductID, SpecialOfferID   
FROM Demo.DemoSalesOrderDetailSeed   
WHERE OrderID= cast((rand()*106) + 1 as int);   
  
WHILE (@i < 20)   
BEGIN;   
      EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od;   
      SET @i += 1   
END  
  
```  
  
 Con questo script, ogni ordine di esempio creato viene inserito 20 volte, tramite 20 stored procedure eseguite in un ciclo WHILE. Il ciclo viene utilizzato per rappresentare il fatto che il database viene utilizzato per creare l'ordine di esempio. Negli ambienti di produzione tipici, tramite l'applicazione di livello intermedio verrà costruito l'ordine vendita da inserire.  
  
 Tramite lo script precedente gli ordini vendita vengono inseriti nelle tabelle ottimizzate per la memoria. Lo script per inserire gli ordini vendita nelle tabelle basate su disco deriva dalla sostituzione di due occorrenze di '_inmem' con '_ondisk'.  
  
 Si utilizzerà lo strumento ostress per eseguire gli script utilizzando diverse connessioni simultanee. Si utilizzerà il parametro '-n' per controllare il numero di connessioni e il parametro 'r' per controllare il numero di volte in cui lo script viene eseguito in ogni connessione.  
  
#### <a name="functional-validation-of-the-workload"></a>Convalida funzionale del carico di lavoro  
 Per verificare che tutto funzioni, si inizierà con un test di esempio, usando 10 connessioni simultanee e 5 iterazioni, inserendo un totale di 10 \* * 5 20 = 1000 di ordini di vendita.  
  
 Con il comando seguente si supponga di usare l'istanza predefinita nel computer locale. Se si utilizza un'istanza denominata o un server remoto, modificare il nome del server di conseguenza, utilizzando il parametro -S.  
  
 Inserire 1000 ordini vendita nelle tabelle ottimizzate per la memoria utilizzando il comando seguente nel prompt dei comandi RML:  
  
 Fare clic sul pulsante Copia per copiare il comando e incollarlo nel prompt dei comandi delle utilità RML.  
  
```  
ostress.exe -n10 -r5 -S. -E -dAdventureWorks2014 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 Se tutto funziona come previsto, la finestra di comando sarà simile a quanto riportato di seguito. I messaggi di errore non sono previsti.  
  
 ![](../../2014/database-engine/media/SQLServer2014RTMIn-MemoryOLTP02.jpg)  
  
 Verificare che anche il carico di lavoro funzioni come previsto per le tabelle basate su disco eseguendo il comando riportato di seguito nel prompt dei comandi RML:  
  
 Fare clic sul pulsante Copia per copiare il comando e incollarlo nel prompt dei comandi delle utilità RML.  
  
```  
ostress.exe -n10 -r5 -S. -E -dAdventureWorks2014 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_ondisk, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_ondisk @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
#### <a name="running-the-workload"></a>Esecuzione del carico di lavoro  
 Per testare una scala vengono inseriti 10 milioni di ordini vendita, utilizzando 100 connessioni. Questo test viene eseguito ragionevolmente in un server modesto, ad esempio con 8 core fisici e 16 logici, e un'archiviazione sull'unità SSD di base per il log. Se il test non viene eseguito correttamente nell'hardware, consultare la sezione [Risoluzione dei problemi relativi ai test con esecuzione prolungata](#Troubleshootingslow-runningtests). Se si vuole ridurre il livello di stress per questo test, ridurre il numero di connessioni modificando il parametro '-n'. Ad esempio, per abbassare il numero di connessioni a 40, impostare il parametro '-n100' su '-n40'.  
  
 Come misura delle prestazioni del carico di lavoro è possibile usare il tempo trascorso come riportato da ostress.exe dopo l'esecuzione del carico di lavoro.  
  
##### <a name="memory-optimized-tables"></a>Tabelle ottimizzate per la memoria  
 Si inizierà eseguendo il carico di lavoro nelle tabelle ottimizzate per la memoria. Tramite il comando seguente vengono aperti 100 thread, ognuno in esecuzione per 5.000 iterazioni.  Tramite ogni iterazione vengono inseriti 20 ordini vendita in transazioni separate. Vi sono 20 inserimenti per ogni iterazione per compensare il fatto che il database viene utilizzato per generare i dati da inserire. Ciò produce un totale pari a 20 * 5.000 \* 100 = 10.000.000 di inserimenti di ordini vendita.  
  
 Aprire il prompt dei comandi RML ed eseguire il comando riportato di seguito:  
  
 Fare clic sul pulsante Copia per copiare il comando e incollarlo nel prompt dei comandi delle utilità RML.  
  
```  
ostress.exe -n100 -r5000 -S. -E -dAdventureWorks2014 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 In un server di test con un numero totale di 8 core fisici (16 logici), l'operazione ha richiesto 2 minuti e 5 secondi. In un secondo server di prova con 24 core fisici (48 logici), l'operazione ha richiesto 1 minuto e 0 secondi.  
  
 Osservare l'utilizzo della CPU mentre il carico di lavoro è in esecuzione, ad esempio tramite Gestione attività. Si noterà che l'utilizzo della CPU è vicino al 100%. In caso contrario, si avrà un collo di bottiglia a livello di operazioni di I/O del log. Vedere anche [Risoluzione dei problemi relativi ai test con esecuzione prolungata](#Troubleshootingslow-runningtests).  
  
##### <a name="disk-based-tables"></a>Tabelle basate su disco  
 Tramite il comando riportato di seguito verrà eseguito il carico di lavoro nelle tabelle basate su disco. Si noti che l'esecuzione di questo carico di lavoro può richiedere del tempo, in gran parte a causa di una contesa di latch nel sistema. Le tabelle con ottimizzazione per la memoria sono prive di latch e pertanto prive di questo problema.  
  
 Aprire il prompt dei comandi RML ed eseguire il comando riportato di seguito:  
  
 Fare clic sul pulsante Copia per copiare il comando e incollarlo nel prompt dei comandi delle utilità RML.  
  
```  
ostress.exe -n100 -r5000 -S. -E -dAdventureWorks2014 -q -Q"DECLARE @i int = 0, @od Sales.SalesOrderDetailType_ondisk, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand() * 10000, @ShipMethodID int = (rand() * 5) + 1; INSERT INTO @od SELECT OrderQty, ProductID, SpecialOfferID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*106) + 1 as int); while (@i < 20) begin; EXEC Sales.usp_InsertSalesOrder_ondisk @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @ShipMethodID, @od; set @i += 1 end"  
```  
  
 In un server di prova con un numero totale di 8 core fisici (16 logici), l'operazione ha richiesto 41 minuti e 25 secondi. In un secondo server di prova con 24 core fisici (48 logici), l'operazione ha richiesto 52 minuti e 16 secondi.  
  
 Il fattore principale della differenza a livello di prestazioni tra le tabelle ottimizzate per la memoria e quelle basate su disco in questo test è che quando si utilizzano le tabelle basate su disco, tramite [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non è possibile usare completamente la CPU. Il motivo è la contesa di latch: tramite le transazioni simultanee si tenta di scrivere nella stessa pagina di dati; i latch vengono utilizzati per garantire che in una pagina venga scritta una sola transazione per volta. Il motore [!INCLUDE[hek_2](../includes/hek-2-md.md)] è privo di latch e le righe di dati non sono organizzate in pagine. Pertanto, le transazioni simultanee non bloccano gli inserimenti degli [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] altri, consentendo in tal modo di utilizzare completamente la CPU.  
  
 È possibile osservare l'utilizzo della CPU mentre il carico di lavoro è in esecuzione, ad esempio tramite Gestione attività. Si noterà che con le tabelle basate su disco l'utilizzo della CPU è lontano dal 100%. In una configurazione di prova con 16 processori logici, l'utilizzo si aggira intorno al 24%.  
  
 Facoltativamente, è possibile visualizzare il numero di attese latch al secondo tramite Performance Monitor, con il contatore delle prestazioni '\SQL Server:Latches\Latch Waits/sec'.  
  
#### <a name="resetting-the-demo"></a>Reimpostazione della dimostrazione  
 Per reimpostare la dimostrazione, aprire il prompt dei comandi RML ed eseguire il comando riportato di seguito:  
  
```  
ostress.exe -S. -E -dAdventureWorks2014 -Q"EXEC Demo.usp_DemoReset"  
```  
  
 A seconda dell'hardware, l'esecuzione può richiedere alcuni minuti.  
  
 Si consiglia una reimpostazione dopo ogni esecuzione della dimostrazione. Poiché questo carico di lavoro è caratterizzato solo da operazioni di inserimento, per ogni esecuzione verrà utilizzata più memoria e, pertanto, per impedire l'esaurimento di quest'ultima sarà necessario eseguire una reimpostazione. La quantità di memoria utilizzata dopo un'esecuzione è descritta nella sezione [Utilizzo della memoria dopo l'esecuzione del carico di lavoro](#Memoryutilizationafterrunningtheworkload).  
  
###  <a name="Troubleshootingslow-runningtests"></a>Risoluzione dei problemi relativi ai test con esecuzione rallentata  
 I risultati dei test variano in genere a seconda dell'hardware e del livello di concorrenza utilizzato durante l'esecuzione del test. Se i risultati non sono quelli previsti, è opportuno verificare alcune informazioni:  
  
-   Numero di transazioni simultanee. Quando si esegue il carico di lavoro in un solo thread, il miglioramento delle prestazioni con [!INCLUDE[hek_2](../includes/hek-2-md.md)] sarà probabilmente inferiore di 2 volte. La contesa di latch è un grande problema solo se vi è un livello elevato di concorrenza.  
  
-   Numero contenuto di core disponibili in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Ciò significa che vi sarà un livello basso di concorrenza nel sistema, dal momento che vi possono essere tante esecuzioni simultanee di transazioni quanti sono i core disponibili in SQL.  
  
    -   Sintomo: se l'utilizzo della CPU è elevato durante l'esecuzione del carico di lavoro nelle tabelle basate su disco, ciò significa che non vi sono molte contese, puntando a una mancanza di concorrenza.  
  
-   Velocità dell'unità dei log: se l'unità dei log non resta sincronizzata con il livello di velocità effettiva delle transazioni nel sistema, il carico di lavoro diventa un collo di bottiglia nelle operazioni di I/O del log. Sebbene la registrazione sia più efficiente con [!INCLUDE[hek_2](../includes/hek-2-md.md)], se le operazioni di I/O del log rappresentano un collo di bottiglia, il potenziale miglioramento delle prestazioni sarà limitato.  
  
    -   Sintomo: se l'utilizzo della CPU non è vicino al 100% o presenta molti problemi durante l'esecuzione del carico di lavoro nelle tabelle ottimizzate per la memoria, è possibile la presenza di un collo di bottiglia a livello di I/O del log. Questa situazione può essere verificata aprendo il monitoraggio risorse ed esaminando la lunghezza della coda per l'unità dei log.  
  
##  <a name="MemoryandDiskSpaceUtilizationintheSample"></a>Utilizzo di memoria e spazio su disco nell'esempio  
 Di seguito viene descritto cosa ci si aspetta in termini di utilizzo della memoria e dello spazio su disco per il database di esempio. Vengono inoltre illustrati i risultati ottenuti in un server di prova con 16 core logici.  
  
###  <a name="Memoryutilizationforthememory-optimizedtables"></a>Utilizzo della memoria per le tabelle ottimizzate per la memoria  
  
#### <a name="overall-utilization-of-the-database"></a>Utilizzo complessivo del database  
 La query seguente può essere utilizzata per ottenere l'utilizzo totale della memoria per [!INCLUDE[hek_2](../includes/hek-2-md.md)] nel sistema.  
  
```  
SELECT type  
   , name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
 Snapshot dopo aver appena creato il database:  
  
||||  
|-|-|-|  
|**tipo**|**nome**|**pages_MB**|  
|MEMORYCLERK_XTP|Default|94|  
|MEMORYCLERK_XTP|DB_ID_5|877|  
|MEMORYCLERK_XTP|Default|0|  
|MEMORYCLERK_XTP|Default|0|  
  
 I clerk di memoria predefiniti contengono strutture di memoria di sistema e sono relativamente ridotti. Il clerk di memoria per il database utente, in questo caso il database con ID 5, è pari a circa 900 MB.  
  
#### <a name="memory-utilization-per-table"></a>Utilizzo della memoria per ogni tabella  
 La query seguente può essere utilizzata per eseguire il drill-down nell'utilizzo della memoria delle singole tabelle e dei relativi indici:  
  
```  
SELECT object_name(t.object_id) AS [Table Name]  
     , memory_allocated_for_table_kb  
 , memory_allocated_for_indexes_kb  
FROM sys.dm_db_xtp_table_memory_stats dms JOIN sys.tables t   
ON dms.object_id=t.object_id  
WHERE t.type='U'  
```  
  
 Di seguito vengono mostrati i risultati di questa query per un'installazione aggiornata dell'esempio:  
  
||||  
|-|-|-|  
|**Nome tabella**|**memory_allocated_for_table_kb**|**memory_allocated_for_indexes_kb**|  
|SpecialOfferProduct_inmem|64|3840|  
|DemoSalesOrderHeaderSeed|1984|5504|  
|SalesOrderDetail_inmem|15316|663552|  
|DemoSalesOrderDetailSeed|64|10432|  
|SpecialOffer_inmem|3|8192|  
|SalesOrderHeader_inmem|7168|147456|  
|Product_inmem|124|12352|  
  
 Come si può notare, le dimensioni delle tabelle sono piuttosto piccole: SalesOrderHeader_inmem è di circa 7 MB e SalesOrderDetail_inmem di circa 15 MB.  
  
 Ciò che colpisce qui sono le dimensioni della memoria allocata per gli indici, rispetto alle dimensioni dei dati della tabella. Questa condizione è dovuta al fatto che gli indici hash nell'esempio vengono ridimensionati preventivamente per una dimensione più ampia dei dati. Si noti che gli indici hash hanno dimensioni fisse e pertanto non aumenteranno con le dimensioni dei dati nella tabella.  
  
####  <a name="Memoryutilizationafterrunningtheworkload"></a>Utilizzo della memoria dopo l'esecuzione del carico di lavoro  
 Dopo l'inserimento di 10 milioni di ordini vendita, l'aspetto dell'utilizzo di tutta la memoria è simile a quanto riportato di seguito:  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|**tipo**|**nome**|**pages_MB**|  
|MEMORYCLERK_XTP|Default|146|  
|MEMORYCLERK_XTP|DB_ID_5|7374|  
|MEMORYCLERK_XTP|Default|0|  
|MEMORYCLERK_XTP|Default|0|  
  
 Come si può notare, tramite [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] viene utilizzato un bit in 8 GB per gli indici e le tabelle ottimizzate per la memoria nel database di esempio.  
  
 Esaminare l'utilizzo dettagliato della memoria per tabella dopo un'esecuzione di esempio:  
  
```  
SELECT object_name(t.object_id) AS [Table Name]  
     , memory_allocated_for_table_kb  
 , memory_allocated_for_indexes_kb  
FROM sys.dm_db_xtp_table_memory_stats dms JOIN sys.tables t   
ON dms.object_id=t.object_id  
WHERE t.type='U'  
```  
  
||||  
|-|-|-|  
|**Nome tabella**|**memory_allocated_for_table_kb**|**memory_allocated_for_indexes_kb**|  
|SalesOrderDetail_inmem|5113761|663552|  
|DemoSalesOrderDetailSeed|64|10368|  
|SpecialOffer_inmem|2|8192|  
|SalesOrderHeader_inmem|1575679|147456|  
|Product_inmem|111|12032|  
|SpecialOfferProduct_inmem|64|3712|  
|DemoSalesOrderHeaderSeed|1984|5504|  
  
 Si può notare un totale pari a circa 6,5 GB di dati. Si noti che le dimensioni degli indici delle tabelle SalesOrderHeader_inmem e SalesOrderDetail_inmem equivalgono alle dimensioni degli indici prima dell'inserimento degli ordini vendita. Le dimensioni dell'indice non sono state modificate perché in entrambe le tabelle vengono utilizzati indici hash e questo tipo di indice è statico.  
  
#### <a name="after-demo-reset"></a>Dopo la reimpostazione della dimostrazione  
 La stored procedure Demo.usp_DemoReset può essere utilizzata per reimpostare la dimostrazione. Tramite essa vengono eliminati i dati nelle tabelle SalesOrderHeader_inmem e SalesOrderDetail_inmem e vengono reinizializzati i dati dalle tabelle originali SalesOrderHeader e SalesOrderDetail.  
  
 A questo punto, anche se le righe nelle tabelle sono state eliminate, questo non significa che la memoria venga recuperata immediatamente. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Recupera la memoria dalle righe eliminate nelle tabelle ottimizzate per la memoria in background, in base alle esigenze. Si noterà che subito dopo la reimpostazione della dimostrazione, senza il carico di lavoro transazionale nel sistema, la memoria non è ancora stata recuperata dalle righe eliminate:  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|**tipo**|**nome**|**pages_MB**|  
|MEMORYCLERK_XTP|Default|2261|  
|MEMORYCLERK_XTP|DB_ID_5|7396|  
|MEMORYCLERK_XTP|Default|0|  
|MEMORYCLERK_XTP|Default|0|  
  
 Si prevede che la memoria verrà recuperata quando il carico di lavoro transazionale è in esecuzione.  
  
 Se si avvia una seconda esecuzione del carico di lavoro dimostrativo, si noterà inizialmente una diminuzione dell'utilizzo della memoria, dal momento che le righe eliminate in precedenza vengono rimosse. A un certo punto le dimensioni della memoria aumenteranno di nuovo, finché il carico di lavoro non viene completato. Dopo l'inserimento di 10 milioni di righe al termine della reimpostazione della dimostrazione, l'utilizzo della memoria sarà molto simile all'utilizzo dopo la prima esecuzione. Ad esempio:  
  
```  
SELECT type  
, name  
, pages_kb/1024 AS pages_MB   
FROM sys.dm_os_memory_clerks WHERE type LIKE '%xtp%'  
```  
  
||||  
|-|-|-|  
|**tipo**|**nome**|**pages_MB**|  
|MEMORYCLERK_XTP|Default|1863|  
|MEMORYCLERK_XTP|DB_ID_5|7390|  
|MEMORYCLERK_XTP|Default|0|  
|MEMORYCLERK_XTP|Default|0|  
  
### <a name="disk-utilization-for-memory-optimized-tables"></a>Utilizzo del disco per tabelle ottimizzate per la memoria  
 Le dimensioni complessive su disco per i file del checkpoint di un database in un determinato momento possono essere recuperate tramite la query seguente:  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
  
```  
  
#### <a name="initial-state"></a>Stato iniziale  
 Quando vengono creati inizialmente il filegroup di esempio e le tabelle ottimizzate per la memoria di esempio, vengono creati preventivamente un numero di file del checkpoint e, tramite il sistema viene iniziata la compilazione di questi file. Il numero di file del checkpoint creati in precedenza dipende dal numero di processori logici nel sistema. Poiché l'esempio è inizialmente contenuto, i file creati in precedenza saranno per la maggior parte vuoti al termine della creazione iniziale.  
  
 Di seguito vengono mostrate le dimensioni iniziali su disco per l'esempio in un computer con 16 processori logici:  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**Dimensioni su disco in MB**|  
|2312|  
  
 Come si può notare, esiste una grande discrepanza tra le dimensioni su disco dei file del checkpoint, vale a dire 2,3 GB, e le dimensioni effettive dei dati, prossime a 30 MB.  
  
 Esaminando più da vicino la provenienza dell'utilizzo dello spazio su disco, è possibile usare la query indicata di seguito. La dimensione su disco restituita dalla query è approssimativa per i file con lo stato in 5 (REQUIRED FOR BACKUP/HA), 6 (IN TRANSITION TO TOMBSTONE) o 7 (TOMBSTONE).  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
 Per lo stato iniziale dell'esempio, il risultato sarà simile per un server con 16 processori logici:  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**conteggio**|**dimensioni su disco in MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|1|128|  
|UNDER CONSTRUCTION|DELTA|1|8|  
  
 Come si può notare, la maggior parte dello spazio è utilizzato dai file differenziali e di dati creati in precedenza. Tramite [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è stata creata preventivamente una coppia di file (differenziali e di dati) per processore logico. Inoltre, i file di dati vengono ridimensionati preventivamente a 128 MB mentre quelli differenziali a 8 MB, per poter consentire un inserimento di dati in questi file più efficiente.  
  
 I dati effettivi nelle tabelle ottimizzate per la memoria si trovano nel singolo file di dati.  
  
#### <a name="after-running-the-workload"></a>Dopo l'esecuzione del carico di lavoro  
 Dopo una singola esecuzione di test tramite cui vengono inseriti 10 milioni di ordini vendita, le dimensioni complessive su disco saranno simili alle seguenti (per un server di prova con 16 core):  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**Dimensioni su disco in MB**|  
|8828|  
  
 Le dimensioni su disco sono prossime ai 9 GB, che sono simili a quelle delle dimensioni in memoria dei dati.  
  
 Esaminando più da vicino le dimensioni dei file del checkpoint nei vari stati:  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**conteggio**|**dimensioni su disco in MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|1|128|  
|UNDER CONSTRUCTION|DELTA|1|8|  
  
 Si dispone ancora di 16 coppie di file creati in precedenza, pronti all'utilizzo alla chiusura dei checkpoint.  
  
 È disponibile una coppia in fase di costruzione, che viene utilizzata fino a quando il checkpoint corrente non viene chiuso. Insieme ai file del checkpoint attivi, questa coppia offre circa 6,5 GB di utilizzo su disco per 6,5 GB di dati in memoria. Si tenta presente che gli indici non vengono salvati in modo persistente su disco e pertanto, in questo caso, le dimensioni complessive su disco sono inferiori rispetto a quelle in memoria.  
  
#### <a name="after-demo-reset"></a>Dopo la reimpostazione della dimostrazione  
 Dopo la reimpostazione della dimostrazione, lo spazio su disco non viene recuperato immediatamente se non vi è un carico di lavoro transazionale nel sistema e non vi sono checkpoint del database. Per i file del checkpoint da spostare nelle varie fasi e infine da rimuovere, devono verificarsi diversi checkpoint ed eventi di troncamento del log, per avviare l'unione dei file del checkpoint, nonché il processo di Garbage Collection. Ciò si verifica automaticamente se si dispone di un carico di lavoro transazionale nel sistema, e vengono eseguiti backup regolari del log, qualora venga utilizzato il modello di recupero con registrazione completa, ma non quando il sistema è inattivo, come in uno scenario dimostrativo.  
  
 Nell'esempio, dopo la reimpostazione della dimostrazione, è possibile che si ottenga un risultato simile al seguente  
  
```  
SELECT SUM(df.size) * 8 / 1024 AS [On-disk size in MB]  
FROM sys.filegroups f JOIN sys.database_files df   
   ON f.data_space_id=df.data_space_id  
WHERE f.type=N'FX'  
```  
  
||  
|-|  
|**Dimensioni su disco in MB**|  
|11839|  
  
 Quasi 12 GB, che sono significativamente maggiori dei 9 GB disponibili prima della reimpostazione della dimostrazione. Ciò è dovuto al fatto che sono state avviate alcune operazioni di unione di file del checkpoint, ma alcune destinazioni delle unioni non sono ancora state installate e alcuni dei file di origine di unione non sono ancora stati rimossi, come si può notare da quanto riportato di seguito:  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**conteggio**|**dimensioni su disco in MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|ACTIVE|DATA|38|5152|  
|ACTIVE|DELTA|38|1331|  
|MERGE TARGET|DATA|7|896|  
|MERGE TARGET|DELTA|7|56|  
|MERGED SOURCE|DATA|13|1772|  
|MERGED SOURCE|DELTA|13|455|  
  
 Le destinazioni delle unioni vengono installate e le origini unite vengono rimosse quando viene eseguita l'attività transazionale nel sistema.  
  
 Al termine di una seconda esecuzione del carico di lavoro dimostrativo, inserendo 10 milioni di ordini vendita dopo la reimpostazione della dimostrazione, si noterà che i file creati durante la prima esecuzione del carico di lavoro sono stati rimossi. Se si esegue la query sopra indicata più volte durante l'esecuzione del carico di lavoro, si potranno visualizzare i file del checkpoint durante le varie fasi.  
  
 Dopo la seconda esecuzione del carico di lavoro con l'inserimento di 10 milioni di ordini vendita, si visualizzerà un utilizzo del disco molto simile a (ma non necessariamente lo stesso di quello dopo la prima esecuzione) quello del sistema dinamico in natura. Ad esempio:  
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(CASE  
   WHEN state = 5 AND file_type=0 THEN 128*1024*1024  
   WHEN state = 5 AND file_type=1 THEN 8*1024*1024  
   WHEN state IN (6,7) THEN 68*1024*1024  
   ELSE file_size_in_bytes  
    END) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  
|||||  
|-|-|-|-|  
|**state_desc**|**file_type_desc**|**conteggio**|**dimensioni su disco in MB**|  
|PRECREATED|DATA|16|2048|  
|PRECREATED|DELTA|16|128|  
|UNDER CONSTRUCTION|DATA|2|268|  
|UNDER CONSTRUCTION|DELTA|2|16|  
|ACTIVE|DATA|41|5608|  
|ACTIVE|DELTA|41|328|  
  
 In questo caso, sono disponibili due coppie di file di checkpoint nello stato 'in costruzione', il che significa che più coppie di file sono passate allo stato 'in costruzione' probabilmente a causa dell'elevato livello di concorrenza del carico di lavoro. Più thread simultanei hanno richiesto una nuova coppia di file contemporaneamente e di conseguenza una coppia è passata dallo stato di 'precreato' a quello di 'in costruzione'.  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;l'ottimizzazione in memoria&#41;](../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
