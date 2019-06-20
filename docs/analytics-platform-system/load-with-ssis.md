---
title: Caricare i dati con Integration Services - Data Warehouse parallelo | Microsoft Docs
description: Fornisce informazioni di riferimento e la distribuzione per il caricamento dei dati in Parallel Data Warehouse (PDW) con i pacchetti di SQL Server Integration Services (SSIS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b8a1ca0ec3662dddb2baa5fbac5fe01ed4d4f2e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213379"
---
# <a name="load-data-with-integration-services-to-parallel-data-warehouse"></a>Caricare dati con Integration Services per Parallel Data Warehouse
Fornisce informazioni di riferimento e la distribuzione per il caricamento di dati in SQL Server Parallel Data Warehouse usando i pacchetti di SQL Server Integration Services (SSIS).  
  
<!-- MISSING LINKS

## <a name="BeforeBegin"></a>Before You Begin  
Before you can start loading data, use the following topics to install the Integration Services Destination Adapters and to create an Integration Services package that connects SQL Server PDW:  


-   [Install Integration Services destination adapters](install-integration-services-destination-adapters.md)  
  
-   [Connect With Integration Services for loading](connect-with-ssis-for-loading.md)  
  
For general information about developing Integration Services packages, see [Designing and Implementing Packages (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx) on MSDN.  

-->
  
## <a name="Basics"></a>Nozioni di base  
Integration Services è il componente di SQL Server per ad alte prestazioni estrazione, trasformazione e caricamento (ETL) dei dati e viene comunemente usato per popolare e aggiornare un data warehouse.  
  
L'adattatore di destinazione PDW è un componente di Integration Services che consente di caricare i dati in PDW utilizzando pacchetti dtsx di Integration Services. In un pacchetto del flusso di lavoro per ServerPDW SQL, è possibile caricare e unire dati da più origini e caricare i dati a più destinazioni. I caricamenti avvengono in parallelo, sia all'interno di un pacchetto sia tra più pacchetti in esecuzione contemporaneamente, fino a un massimo di 10 caricamenti paralleli sullo stesso strumento.  
  
Oltre alle attività descritte in questo argomento, è possibile usare altre funzionalità di Integration Services per filtrare, trasformare, analizzare e pulire i dati prima di caricarli nel data warehouse. È inoltre possibile migliorare il flusso di lavoro del pacchetto eseguendo istruzioni SQL e pacchetti figlio o inviando messaggi di posta elettronica.  
  
Per una documentazione completa di Integration Services, vedere [SQL Server Integration Services](../integration-services/sql-server-integration-services.md).  
  
## <a name="HowToDeployPackage"></a>Metodi per l'esecuzione di un pacchetto di Integration Services  
Usare uno di questi metodi per eseguire un pacchetto di Integration Services.  
  
### <a name="run-from-sql-server-2008-r2-business-intelligence-development-studio-bids"></a>Eseguire da SQL Server 2008 R2 Business Intelligence Development Studio (BIDS)  
Per eseguire il pacchetto da all'interno di BIDS, fare clic sul pacchetto e scegliere **Esegui pacchetto**.  
  
Per impostazione predefinita, le offerte esegue i pacchetti utilizzando i file binari a 64 bit. Ciò è determinato dal **Run64BitRuntime** proprietà del pacchetto. Per impostare questa proprietà, passare a **Esplora soluzioni**, fare clic sul progetto e scegliere **proprietà**. Nel **pagine delle proprietà di Integration Services**passare alla **le proprietà di configurazione** e selezionare **debug**. Verrà visualizzato il **Run64BitRuntime** proprietà sotto il **opzioni di Debug**. Per usare i Runtime a 32 bit, impostare questa opzione su **False**. Per usare i Runtime a 64 bit, impostare questa opzione su **True**.  
  
### <a name="run-from-sql-server-2012-sql-server-data-tools"></a>Eseguire da SQL Server 2012 SQL Server Data Tools  
Per eseguire il pacchetto da all'interno di SQL Server Data Tools, fare clic sul pacchetto e scegliere **Esegui pacchetto**.  
  
### <a name="run-from-powershell"></a>Eseguire da PowerShell  
Per eseguire il pacchetto da Windows PowerShell, usando il **dtexec** utilità: `dtexec /FILE <packagePath>`  
  
Ad esempio, usare `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
### <a name="run-from-a-windows-command-prompt"></a>Eseguire Windows da un prompt dei comandi 
Per eseguire il pacchetto da un prompt dei comandi di Windows, utilizzando il **dtexec** utilità: `dtexec /FILE <packagePath>`  
  
Ad esempio: `dtexec /FILE "C:\Users\User1\Desktop\Package.dtsx"`  
  
## <a name="DataTypes"></a>Tipi di dati  
Quando si usa servizi di integrazione per caricare i dati da un'origine dati a un database di SQL Server PDW, i dati viene prima eseguito il mapping dai dati di origine ai tipi di dati di Integration Services. In questo modo è possibile eseguire il mapping dei dati di più origini a un set comune di tipi di dati.  
  
Quindi i dati viene eseguito il mapping da Integration Services ai tipi di dati di SQL Server PDW. Per ogni tipo di dati di SQL Server PDW, la tabella seguente elenca i tipi di dati di Integration Services che possono essere convertiti nel tipo di dati di SQL Server PDW.  
  
|Tipo di dati PDW|Dati tipi di Integration Services (s) che eseguono il mapping al tipo di dati PDW|  
|---------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|  
|BIT|DT_BOOL|  
|bigint|DT_I1, DT_I2, DT_I4, DT_I8, DT_UI1, DT_UI2, DT_UI4|  
|CHAR|DT_STR|  
|DATE|DT_DBDATE|  
|DATETIME|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIME2|DT_DATE, DT_DBDATE, DT_DBTIMESTAMP, DT_DBTIMESTAMP2|  
|DATETIMEOFFSET|DT_WSTR|  
|Decimal|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|FLOAT|DT_R4, DT_R8|  
|INT|DT_I1, DTI2, DT_I4, DT_UI1, DT_UI2|  
|MONEY|DT_CY|  
|NCHAR|DT_WSTR|  
|NUMERIC|DT_DECIMAL, DT_I1, DT_I2, DT_I4, DT_I8, DT_NUMERIC, DT_UI1, DT_UI2, DT_UI4, DT_UI8|  
|NVARCHAR|DT_WSTR, DT_STR|  
|real|DT_R4|  
|SMALLDATETIME|DT_DBTIMESTAMP2|  
|SMALLINT|DT_I1, DT_I2, DT_UI1|  
|SMALLMONEY|DT_R4|  
|TIME|DT_WSTR|  
|TINYINT|DT_I1|  
|VARBINARY|DT_BYTES|  
|VARCHAR|DT_STR|  
  
**Supporto limitato per la precisione del tipo di dati**  
  
PDW genera un errore di convalida se il mapping di una colonna di input DT_NUMERIC o DT_DECIMAL contenente un valore con una precisione maggiore di 28.  
  
**Tipi di dati non supportato**  
  
SQL Server PDW non supporta i tipi di dati di Integration Services seguenti:  
  
-   DT_DBTIMESTAMPOFFSET  
  
-   DT_DBTIME2  
  
-   DT_GUID  
  
-   DT_IMAGE  
  
-   DT_NTEXT  
  
-   DT_TEXT  
  
Per caricare le colonne che contengono questi tipi di dati in SQL Server PDW, è necessario aggiungere una trasformazione conversione dati a monte nel flusso di dati per convertire i dati in un tipo di dati compatibile.  
  
## <a name="permissions"></a>Permissions  
Per eseguire un pacchetto di caricamento di Integration Services, è necessario:  
  
-   CARICARE l'autorizzazione per il database.  
  
-   Applicabile INSERT, UPDATE, le autorizzazioni di eliminazione nella tabella di destinazione.  
  
-   Se viene usato un database di gestione temporanea, l'autorizzazione per creare il database di gestione temporanea. Si tratta di creare una tabella temporanea.  
  
-   Se non viene usato alcun database di gestione temporanea, l'autorizzazione per creare il database di destinazione. Si tratta di creare una tabella temporanea.  
  
## <a name="GenRemarks"></a>Osservazioni generale  
Quando un pacchetto di Integration Services dispone di più destinazioni di SQL Server PDW in esecuzione e una delle connessioni viene terminata, Integration Services interrompe il push dei dati per tutte le destinazioni di SQL Server PDW.  
  
## <a name="Limits"></a>Limitazioni e restrizioni  
Per un pacchetto di Integration Services, il numero di destinazioni di SQL Server PDW per la stessa origine dati è limitato dal numero massimo di caricamenti attivi. Il numero massimo è preconfigurato e non è configurabile dall'utente. 

<!-- MISSING LINKS
For the maximum number of loads and queued loads per appliance, see [Minimum and maximum values](minimum-and-maximum-values.md).  
-->
  
Ogni destinazione del pacchetto Integration Services per la stessa origine dati viene considerato uno carico durante l'esecuzione del pacchetto. Si supponga ad esempio che il numero massimo di caricamenti attivi sia 10. Il pacchetto non viene eseguito se tenta di aprire 11 o più destinazioni per la stessa origine dati.  
  
È possibile eseguire contemporaneamente più pacchetti purché ogni pacchetto non utilizzi un numero di caricamenti attivi superiore al limite massimo consentito. Ad esempio, se il numero massimo di caricamenti attivi è 10, è possibile eseguire contemporaneamente due pacchetti che utilizzino entrambi 10 destinazioni. Mentre un pacchetto viene eseguito, l'altro rimane in attesa nella coda di caricamento.  
  
Se il numero di caricamenti in coda supera il numero massimo consentito di caricamenti in coda, il pacchetto non verrà eseguito. Ad esempio, se il numero massimo di caricamenti è 10 per strumento e il numero massimo di caricamenti in coda è 40 per strumento, è possibile eseguire contemporaneamente cinque pacchetti di Integration Services che 10 destinazioni aperte ciascuno. L'eventuale tentativo di eseguire un sesto pacchetto avrà esito negativo.  

> [!IMPORTANT]
> Utilizza un'origine dati OLE DB in SSIS con l'adattatore di destinazione PDW, può causare il danneggiamento dei dati se la tabella di origine contiene colonne char e varchar con regole di confronto SQL. È consigliabile usare un'origine ADO.NET se la tabella di origine contiene colonne char o varchar con regole di confronto SQL. 

  
## <a name="Locks"></a>Comportamento di blocco  
Quando si caricano dati con Integration Services, SQL ServerPDW Usa i blocchi a livello di riga per aggiornare i dati nella tabella di destinazione. Ciò significa che durante l'aggiornamento ogni riga viene bloccata per la lettura e la scrittura. Le righe della tabella di destinazione non sono bloccate mentre i dati vengono caricati nella tabella di staging.  
  
## <a name="Examples"></a>Esempi  
  
### <a name="Walkthrough"></a>A. Caricamento semplice file flat  
La procedura riportata di seguito viene illustrato un carico di dati semplice utilizzando Integration Services per caricare i dati di file flat a un'appliance di SQL Server PDW.  Questo esempio si presuppone che i servizi di integrazione è già stato installato nel computer client e la destinazione di SQL Server PDW è stata installata, come descritto in precedenza.  
  
In questo esempio si caricherà nel `Orders` tabella che include l'istruzione DDL seguente. Il `Orders` tabella è inclusa la `LoadExampleDB` database.  
  
```sql  
CREATE TABLE LoadExampleDB.dbo.Orders (  
   id INT,  
   city varchar(25),  
   lastUpdateDate DATE,  
   orderDate DATE)  
;  
```  
  
Ecco il caricamento dei dati:  
  
```  
id        city           lastUpdateDate     orderdate  
--------- -------------- ------------------ ----------  
1         Seattle        2010-05-01         2010-01-01  
2         Denver         2002-06-25         1999-01-02  
```  
  
In preparazione per il carico, creare il file flat `exampleLoad.txt`, che contiene i dati del carico:  
  
```  
id,city,lastUpdateDate,orderDate  
1,Seattle,2010-05-01,2010-01-01  
2,Denver,2002-06-25,1999-01-02  
```  
  
In primo luogo, creare un pacchetto di Integration Services eseguendo questi passaggi:  
  
1.  In SQL Server Data Tools \(SSDT\), selezionare **File**, **New**e quindi **progetto**. Selezionare **progetto di Integration Services** le opzioni desiderate. Denominare il progetto `ExampleLoad`, fare clic su **OK**.  
  
2.  Fare clic sui **flusso di controllo** scheda e quindi trascinare il **Data Flow Task** dal **della casella degli strumenti** per il **flusso di controllo** riquadro.  
  
3.  Fare clic sui **flusso di dati** scheda e quindi trascinare **origine File Flat** dal **della casella degli strumenti** per il **del flusso di dati** riquadro. Fare doppio clic sulla casella appena creata per aprire la **Editor origine File Flat**.  
  
4.  Fare clic su **gestione connessione** e quindi fare clic su **New**.  
  
5.  Nel **nome della gestione connessione** immettere un nome descrittivo per la connessione. In questo esempio `Example Load Flat File CM`.  
  
6.  Fare clic su **esplorare** e selezionare il `ExampleLoad.txt` file dal computer locale.  
  
7.  Poiché il file flat contiene una riga con i nomi delle colonne, fare clic sui **nomi di colonna nella prima riga di dati** casella.  
  
8.  Fare clic su **colonne** nella colonna a sinistra e nell'anteprima i dati che verranno caricati per assicurarsi che i nomi delle colonne e dati sono stati interpretati correttamente.  
  
9. Fare clic su **avanzate** nella colonna sinistra. Fare clic su ogni nome di colonna per esaminare il tipo di dati che è stato associato a dati. Digitare le modifiche nella casella in modo che i tipi di dati dei dati caricati saranno compatibili con i tipi di colonna di destinazione.  
  
10. Fare clic su **OK** per salvare la gestione connessione.  
  
11. Fare clic su **OK** per chiudere la **Editor origine File Flat**.  
  
Specificare la destinazione del flusso di dati.  
  
1.  Trascinare il **destinazione SQL Server PDW** dalle **della casella degli strumenti** per il **del flusso di dati** riquadro.  
  
2.  Fare doppio clic sulla casella appena creata per caricare il **Editor destinazione SQL Server PDW**.  
  
3.  Fare clic sulla freccia in giù accanto a **gestione connessione**.  
  
4.  Selezionare **creare una nuova connessione**.  
  
5.  Immettere le informazioni per il database del server, utente, password e destinazione con informazioni specifiche per l'appliance. (Di seguito sono riportati alcuni esempi.) Fare clic su **OK**.  
  
    Per le connessioni InfiniBand **nome Server**: Immettere < appliance-name >-SQLCTL01, 17001.  
  
    Per le connessioni Ethernet **nome Server**: Immettere l'indirizzo IP del cluster di nodi di controllo, virgole, porta 17001. Ad esempio, 10.192.63.134,17001.  
  
    **Utente:** `user1`  
  
    **Password:** `password1`  
  
    **Database di destinazione:** `LoadExampleDB`  
  
6.  Selezionare la tabella di destinazione: `Orders`.  
  
7.  Selezionare **Append** come modalità di caricamento e fare clic su **OK**.  
  
Specificare il flusso di dati dall'origine alla destinazione.  
  
1.  Nel **del flusso di dati** riquadro, trascinare la freccia verde dal **origine File Flat** casella per il **destinazione SQL Server PDW** casella.  
  
2.  Fare doppio clic sui **destinazione SQL Server PDW** casella che consente di visualizzare i **Editor destinazione SQL Server PDW** nuovamente. Verranno visualizzati i nomi delle colonne del file flat a sinistra, in **colonne Input senza mapping**. Verranno visualizzati i nomi delle colonne dalla tabella di destinazione a destra, in **colonne di destinazione senza mapping**. Il mapping delle colonne trascinando o facendo doppio clic su nomi di colonna corrispondente nel **colonne Input senza mapping** e **colonne di destinazione senza mapping** vengono elencati per il **colonne con mapping**finestra. Fare clic su **OK** per salvare le impostazioni.  
  
3.  Salvare il pacchetto facendo clic **salvare** nel **File** menu.  
  
Eseguire il pacchetto nel computer Integration Services.  
  
1.  I servizi di integrazione**Esplora soluzioni** (colonna destra), fare doppio clic su `Package.dtsx` e selezionare **Execute**.  
  
2.  Il pacchetto verrà eseguito e verranno visualizzati lo stato di avanzamento e gli eventuali errori nel **lo stato di avanzamento** riquadro. Usare un client SQL per confermare il carico o monitorare il carico tramite la Console di amministrazione di SQL Server PDW.  
  
## <a name="see-also"></a>Vedere anche  
[Creare un'attività script che utilizza l'adattatore di destinazione PDW SSIS](create-ssis-script-task-using-pdw-destination-adapter.md)  
[SQL Server Integration Services](../integration-services/sql-server-integration-services.md)  
[Progettazione e implementazione di pacchetti (Integration Services)](https://msdn.microsoft.com/library/ms141091\(v=sql11\).aspx)  
[Esercitazione: Creazione di un pacchetto di base utilizzando una procedura guidata](https://technet.microsoft.com/library/ms365330\(v=sql11\).aspx)  
[Introduzione (Integration Services)](https://go.microsoft.com/fwlink/?LinkId=202412)  
[Esempio di generazione dinamica dei pacchetti](https://go.microsoft.com/fwlink/?LinkId=202413)  
[Progettazione di pacchetti SSIS per parallelismo (Video di SQL Server)](https://msdn.microsoft.com/library/dd795221.aspx)  
[Esempi della Community di Microsoft SQL Server: Integration Services](https://go.microsoft.com/fwlink/?LinkId=202415)  
[Miglioramento dei caricamenti incrementali con Change Data Capture](../integration-services/change-data-capture/change-data-capture-ssis.md)  
[Trasformazione Dimensione a modifica lenta](../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md)  
[Attività Inserimento bulk](../integration-services/control-flow/bulk-insert-task.md)  
  
<!-- MISSING LINKS
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examples](metadata-query-examples.md)
-->
