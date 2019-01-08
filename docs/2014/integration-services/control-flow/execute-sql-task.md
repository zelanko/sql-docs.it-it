---
title: Attività Esegui SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executesqltask.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- batches [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 64e3a60d767c100ad66a293f1e588369a140d1e8
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367313"
---
# <a name="execute-sql-task"></a>Attività Esegui SQL
  L'attività Esegui SQL consente di eseguire istruzioni SQL o stored procedure da un pacchetto. L'attività può includere una o più istruzioni SQL che vengono eseguite in ordine sequenziale. È possibile utilizzare l'attività Esegui SQL per gli scopi seguenti:  
  
-   Troncare una tabella o una vista per prepararla per l'inserimento di dati.  
  
-   Creare, modificare ed eliminare oggetti di database come tabelle e viste.  
  
-   Ricreare tabelle dei fatti e delle dimensioni prima di caricarvi i dati.  
  
-   Eseguire stored procedure. Se l'istruzione SQL richiama una stored procedure che restituisce risultati da una tabella temporanea, utilizzare l'opzione WITH RESULT SETS per definire metadati per il set di risultati.  
  
-   Salvare in una variabile il set di righe restituito da una query.  
  
 L'attività Esegui SQL può essere usata in combinazione con i contenitori Ciclo Foreach e Ciclo For per eseguire più istruzioni SQL. Questi contenitori consentono di implementare flussi di controllo ripetuti in un pacchetto e possono eseguire più volte l'attività Esegui SQL. Utilizzando ad esempio il contenitore Ciclo Foreach, il pacchetto può enumerare i file in una cartella ed eseguire ripetutamente un'attività Esegui SQL per elaborare l'istruzione SQL archiviata in ogni file.  
  
## <a name="connecting-to-a-data-source"></a>Connessione a un'origine dei dati  
 Per connettersi all'origine dei dati su cui eseguire l'istruzione SQL o la stored procedure, l'attività Esegui SQL può utilizzare diversi tipi di gestione connessione, elencati nella tabella seguente.  
  
|Tipo di connessione|Gestione connessione|  
|---------------------|------------------------|  
|EXCEL|[Gestione connessione Excel](../connection-manager/excel-connection-manager.md)|  
|OLE DB|[Gestione connessione OLE DB](../connection-manager/ole-db-connection-manager.md)|  
|ODBC|[Gestione connessione ODBC](../connection-manager/odbc-connection-manager.md)|  
|ADO|[Gestione connessione ADO](../connection-manager/ado-connection-manager.md)|  
|ADO.NET|[Gestione connessione ADO.NET](../connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[Gestione connessione SQL Server Compact Edition](../connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## <a name="creating-sql-statements"></a>Creazione di istruzioni SQL  
 L'origine delle istruzioni SQL utilizzate da questa attività può essere una proprietà dell'attività che contiene un'istruzione, una connessione a un file che contiene una o più istruzioni oppure il nome di una variabile che contiene un'istruzione. Le istruzioni SQL devono essere scritte nel sottolinguaggio del sistema di gestione di database (DBMS) di origine. Per altre informazioni, vedere [Query di Integration Services &#40;SSIS&#41;](../integration-services-ssis-queries.md).  
  
 Se le istruzioni SQL sono memorizzate in un file, per connettersi al file l'attività utilizzerà una gestione connessione file. Per altre informazioni, vedere [File Connection Manager](../connection-manager/file-connection-manager.md).  
  
 In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] per creare query SQL è possibile digitare le istruzioni nella finestra di dialogo **Editor attività Esegui SQL** o utilizzare l'interfaccia utente grafica **Generatore di query**. Per altre informazioni, vedere [Editor attività Esegui SQL &#40;Pagina generale&#41;](../execute-sql-task-editor-general-page.md) e [Generatore di query](../query-builder.md).  
  
> [!NOTE]  
>  L'attività Esegui SQL non è in grado di elaborare correttamente le istruzioni SQL valide scritte al di fuori dell'attività stessa.  
  
> [!NOTE]  
>  L'attività Esegui SQL utilizza il valore di enumerazione ParseMode `RecognizeAll`. Per altre informazioni, vedere [Spazio dei nomi ManagedBatchParser](https://go.microsoft.com/fwlink/?LinkId=223617).  
  
## <a name="sending-multiple-statements-in-a-batch"></a>Invio di più istruzioni in un batch  
 Se un'attività Esegui SQL include più istruzioni, sarà possibile raggrupparle ed eseguirle come batch, utilizzando il comando GO per segnalare la fine del batch. Tutte le istruzioni SQL comprese tra due comandi GO vengono inviate in batch al provider OLE DB per l'esecuzione. Il comando SQL può includere più batch separati da comandi GO.  
  
 I tipi di istruzioni SQL che è possibile raggruppare in un batch sono soggetti a restrizioni. Per altre informazioni, vedere [Batch di istruzioni](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md).  
  
 Se l'attività Esegui SQL esegue un batch di istruzioni SQL, al batch verranno applicate le regole seguenti:  
  
-   Può restituire un set di risultati una sola istruzione, che deve essere la prima del batch.  
  
-   Se il set di risultati utilizza associazioni di risultati, le query dovranno restituire lo stesso numero di colonne. Se le query restituiscono numeri di colonne diversi, l'attività avrà esito negativo. Le query eseguite dall'attività, ad esempio DELETE o INSERT, possono tuttavia avere esito positivo anche se l'attività non viene eseguita correttamente.  
  
-   Se le associazioni di risultati utilizzano nomi di colonne, la query dovrà restituire colonne con nomi uguali a quelli del set di risultati dell'attività. Se le colonne non sono presenti, l'attività avrà esito negativo.  
  
-   Se l'attività utilizza un'associazione di parametri, tutte le query incluse nel batch dovranno avere lo stesso numero e gli stessi tipi di parametri.  
  
## <a name="running-parameterized-sql-commands"></a>Esecuzione di comandi SQL con parametri  
 Le istruzioni SQL e le stored procedure utilizzano spesso parametri di input, parametri di output e codici restituiti. L'attività Esegui SQL supporta parametri di tipo `Input`, `Output` e `ReturnValue`. Il tipo `Input` viene utilizzato per i parametri di input, il tipo `Output` per i parametri di output e il tipo `ReturnValue` per i codici restituiti.  
  
> [!NOTE]  
>  È possibile utilizzare parametri in un'attività Esegui SQL solo se il provider di dati li supporta.  
  
 Per informazioni sull'uso di parametri e codici restituiti nell'attività Esegui SQL, vedere [Parametri e codici restituiti nell’attività Esegui SQL](execute-sql-task.md).  
  
## <a name="specifying-a-result-set-type"></a>Impostazione del tipo di un set di risultati  
 A seconda del tipo di comando SQL, all'attività Esegui SQL può essere restituito o meno un set di risultati. Se si utilizzano ad esempio le istruzioni SELECT, viene in genere restituito un set di risultati, mentre questo non avviene per le istruzioni INSERT. Il set di risultati restituito da un'istruzione SELECT può contenere zero, una o più righe. Le stored procedure possono restituire anche un valore intero, detto codice restituito, che indica lo stato dell'esecuzione della procedura. In questo caso il set di risultati è costituito da una sola riga.  
  
 Per informazioni sul recupero di set di risultati dai comandi SQL nell'attività Esegui SQL, vedere [Set di risultati nell’attività Esegui SQL](../result-sets-in-the-execute-sql-task.md).  
  
## <a name="troubleshooting-the-execute-sql-task"></a>Risoluzione dei problemi relativi all'attività Esegui SQL  
 È possibile registrare le chiamate eseguite dall'attività Esegui SQL a provider di dati esterni. Questa funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi ai comandi SQL eseguiti dall'attività Esegui SQL. Per registrare le chiamate eseguite dall'attività Esegui SQL a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello del pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Talvolta un comando SQL o una stored procedure restituiscono più set di risultati. Tali set di risultati non solo includono i set di righe che sono il risultato di query `SELECT`, ma anche valori singoli che sono il risultato di errori di istruzioni `RAISERROR` o `PRINT`. L'attività ignora gli errori nei set di risultati che si verificano dopo il primo set di risultati in base al tipo di gestione connessione utilizzata:  
  
-   Se si utilizzano le gestioni connessioni OLE DB e ADO, l'attività ignora i set di risultati che si verificano dopo il primo set di risultati. Pertanto, con tali gestioni connessioni, l'attività ignora un errore restituito da un comando SQL o da una stored procedure quando l'errore non fa parte del primo set di risultati.  
  
-   Se si utilizzano le gestioni connessioni ODBC e ADO.NET, l'attività non ignora i set di risultati che si verificano dopo il primo set di risultati. Con queste gestioni connessioni, l'attività non riesce e viene restituito un errore qualora un set di risultati diverso dal primo set di risultati contiene un errore.  
  
### <a name="custom-log-entries"></a>Voci di log personalizzate  
 Nella tabella seguente è indicata la voce di log personalizzata disponibile per l'attività Esegui SQL. Per altre informazioni, vedere [Registrazione di Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) e [Messaggi personalizzati per la registrazione](../custom-messages-for-logging.md).  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|`ExecuteSQLExecutingQuery`|Fornisce informazioni sulle fasi di esecuzione dell'istruzione SQL. Vengono scritte voci di log quando l'attività acquisisce la connessione al database, quando inizia a preparare l'istruzione SQL e al termine dell'esecuzione dell'istruzione SQL. La voce di log per la fase di preparazione include l'istruzione SQL utilizzata dall'attività.|  
  
## <a name="configuring-the-execute-sql-task"></a>Configurazione dell'attività Esegui SQL  
 Per configurare l'attività Esegui SQL, procedere nel modo seguente:  
  
-   Specificare il tipo di gestione connessione da utilizzare per la connessione a un database.  
  
-   Specificare il tipo di set di risultati restituito dall'istruzione SQL.  
  
-   Specificare un timeout per l'istruzione SQL.  
  
-   Specificare l'origine dell'istruzione SQL.  
  
-   Indicare se l'attività salta la fase di preparazione per l'istruzione SQL.  
  
-   Se si utilizza il tipo di connessione ADO, è necessario indicare se l'istruzione SQL è una stored procedure. Per altri tipi di connessione questa proprietà è di sola lettura e ha sempre valore `false`.  
  
 È possibile impostare le proprietà a livello di programmazione o tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Esegui SQL &#40;pagina Generale&#41;](../execute-sql-task-editor-general-page.md)  
  
-   [Editor attività Esegui SQL &#40;pagina Mapping parametri&#41;](../execute-sql-task-editor-parameter-mapping-page.md)  
  
-   [Editor attività Esegui SQL &#40;pagina Set dei risultati&#41;](../execute-sql-task-editor-result-set-page.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="configuring-the-execute-sql-task-programmatically"></a>Configurazione dell'attività Esegui SQL a livello di codice  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask>  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Mapping di parametri di query a variabili in un'attività Esegui SQL](../map-query-parameters-to-variables-in-an-execute-sql-task.md)  
  
-   [Mapping di set di risultati a variabili in un'attività Esegui SQL](../map-result-sets-to-variables-in-an-execute-sql-task.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   [Parametri e codici restituiti nell'attività Esegui SQL](execute-sql-task.md)  
  
-   [Set di risultati nell'attività Esegui SQL](../result-sets-in-the-execute-sql-task.md)  
  
-   [Guida di riferimento a Transact-SQL &#40;Motore di database&#41;](/sql/t-sql/language-reference)  
  
-   Intervento nel blog relativo alle [nuove funzioni di data e ora in SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=239783)sul sito Web mssqltips.com  
  
  
