---
title: Contenitore Ciclo Foreach | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.f1
helpviewer_keywords:
- repeating control flow
- Foreach Loop containers
- foreach enumerators [Integration Services]
- containers [Integration Services], Foreach Loop
ms.assetid: dd6cc2ba-631f-4adf-89dc-29ef449c6933
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: bb50b4000397ca3dd51be58867e45135d1d587f1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62831582"
---
# <a name="foreach-loop-container"></a>Contenitore Ciclo Foreach
  Il contenitore Ciclo Foreach definisce un flusso di controllo ripetuto all'interno di un pacchetto. L'implementazione del ciclo è simile alla struttura del ciclo **Foreach** nei linguaggi di programmazione. In un pacchetto per l'esecuzione del ciclo viene utilizzato un enumeratore Foreach.  Il contenitore Ciclo Foreach ripete il flusso di controllo per ogni membro di un enumeratore specificato.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] in sono disponibili i tipi di enumeratori seguenti:  
  
-   Foreach ADO Enumerator, per enumerare righe nelle tabelle. Consente ad esempio di ottenere le righe in un recordset ADO.  
  
     Con la destinazione recordset è possibile salvare i dati in memoria in un recordset archiviato in una variabile del pacchetto il cui tipo di dati è `Object`. In genere si utilizza un contenitore Ciclo Foreach con l'enumeratore Foreach ADO per elaborare una riga del recordset alla volta. Il tipo di dati della variabile specificata per l'enumeratore Foreach ADO deve essere Object. Per ulteriori informazioni sulla destinazione recordset, vedere [Use a Recordset Destination](../data-flow/recordset-destination.md).  
  
-   Foreach ADO.NET Schema Rowset Enumerator, per enumerare le informazioni dello schema relative a un'origine dei dati. È possibile, ad esempio, enumerare e ottenere un elenco delle tabelle nel [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] database.  
  
-   Foreach File Enumerator, per enumerare i file contenuti in una cartella. È possibile includere nell'enumerazione anche le sottocartelle. È ad esempio possibile leggere tutti i file con estensione log presenti nella cartella di Windows e nelle relative sottocartelle.  
  
-   Foreach From Variable Enumerator, per enumerare gli oggetti enumerabili contenuti in una variabile specificata. L'oggetto enumerabile può essere costituito da una matrice, da un oggetto `DataTable` ADO.NET, da un enumeratore di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] e così via. È ad esempio possibile enumerare i valori di una matrice che contiene i nomi dei server.  
  
-   Foreach Item Enumerator, per enumerare elementi costituiti da raccolte. È ad esempio possibile enumerare i nomi degli eseguibili e delle directory di lavoro utilizzate dall'attività Esegui processo.  
  
-   Foreach Nodelist Enumerator, per enumerare il set di risultati di un'espressione XPath (XML Path Language). L'espressione seguente consente ad esempio di enumerare e ottenere un elenco di tutti gli autori del periodo classico: `/authors/author[@period='classical']`.  
  
-   Foreach SMO Enumerator, per enumerare oggetti SMO ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects). Consente ad esempio di enumerare e ottenere un elenco delle viste presenti in un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Enumeratore BLOB di Azure Foreach per enumerare i BLOB in un contenitore BLOB di Archiviazione di Azure.  
  
-   Foreach ADLS File Enumerator per enumerare i file in una directory ADLS.
  
 Nella figura seguente viene illustrato un contenitore Ciclo Foreach che include un'attività File system. Il ciclo Foreach utilizza Foreach File Enumerator e l'attività File system è configurata per la copia di un file. Se la cartella specificata dall'enumeratore contiene quattro file, il ciclo si ripeterà quattro volte e copierà quattro file.  
  
 ![Contenitore Foreach Loop per l'enumerazione di una cartella](../media/ssis-foreachloop.gif "Contenitore Foreach Loop per l'enumerazione di una cartella")  
  
 È possibile utilizzare una combinazione di variabili ed espressioni di proprietà per aggiornare la proprietà dell'oggetto pacchetto con il valore della raccolta dell'enumeratore. È innanzitutto necessario eseguire il mapping del valore della raccolta a una variabile definita dall'utente e quindi implementare un'espressione di proprietà sulla proprietà che utilizza la variabile. Ad esempio, il valore della raccolta dell'enumeratore Foreach file viene mappato a una `MyFile` variabile denominata e la variabile viene quindi utilizzata nell'espressione di proprietà per la proprietà Subject di un'attività Invia messaggi. Quando il pacchetto viene eseguito, la proprietà Oggetto viene aggiornata con il nome di un file ogni volta che il ciclo si ripete. Per altre informazioni, vedere [Utilizzo delle espressioni di proprietà nei pacchetti](../expressions/use-property-expressions-in-packages.md).  
  
 Le variabili sulle quali viene eseguito il mapping al valore della raccolta dell'enumeratore possono essere utilizzate anche in espressioni e script.  
  
 Un contenitore Ciclo Foreach può includere più attività e contenitori, ma può utilizzare un solo tipo di enumeratore. Se il contenitore Ciclo Foreach include più attività, sarà possibile eseguire il mapping il valore della raccolta dell'enumeratore a più proprietà di ogni attività.  
  
 È possibile impostare un attributo di transazione per ogni contenitore Ciclo Foreach per definire una transazione per un subset del flusso di controllo del pacchetto. In questo modo è possibile gestire le transazioni a livello di ciclo Foreach, anziché a livello di pacchetto. Se ad esempio un contenitore Ciclo Foreach ripete un flusso di controllo che aggiorna le tabelle delle dimensioni e dei fatti in uno schema star, sarà possibile configurare una transazione per garantire che vengano aggiornate tutte le tabelle dei fatti oppure nessuna. Per altre informazioni, vedere [Transazioni di Integration Services](../integration-services-transactions.md).  
  
## <a name="enumerator-types"></a>Tipi di enumeratori  
 Gli enumeratori sono configurabili ed è necessario specificare informazioni diverse a seconda dell'enumeratore.  
  
 Nella tabella seguente vengono riepilogate le informazioni richieste da ogni tipo di enumeratore.  
  
|Enumeratore|Requisiti di configurazione|  
|----------------|--------------------------------|  
|Foreach ADO|Specificare la variabile di origine dell'oggetto ADO e la modalità dell'enumeratore. Il tipo di dati della variabile deve essere Object.|  
|Foreach ADO.NET Schema Rowset|Specificare la connessione a un database e lo schema da enumerare.|  
|Foreach File|Specificare una cartella, i file da enumerare e il formato del nome dei file recuperati e indicare se includere le sottocartelle nell'enumerazione.|  
|Foreach From Variable|Specificare la variabile che contiene gli oggetti da enumerare.|  
|Foreach Item|Definire gli elementi nella raccolta di Foreach Item Enumerator, comprese le colonne e i tipi di dati delle colonne.|  
|Foreach Nodelist|Specificare l'origine del documento XML e configurare l'operazione XPath.|  
|Foreach SMO|Specificare una connessione a un database e gli oggetti SMO da enumerare.|  
|Blob di Azure Foreach|Specificare il contenitore BLOB di Azure che contiene i BLOB da enumerare.|  
|Foreach file di ADLS|Specificare la directory ADLS che contiene i file da enumerare, insieme ad alcuni filtri.|
  
## <a name="property-expressions-in-foreach-loop-containers"></a>Espressioni di proprietà nei contenitori Ciclo Foreach  
 Un pacchetto può essere configurato in modo da eseguire più eseguibili contemporaneamente. Questo tipo di configurazione deve essere tuttavia utilizzato con cautela, se il pacchetto include un contenitore Ciclo Foreach che implementa espressioni di proprietà.  
  
 È spesso utile implementare un'espressione di proprietà per impostare il valore della proprietà ConnectionString delle gestioni connessioni usate dagli enumeratori del ciclo Foreach. L'espressione di proprietà di ConnectionString viene impostata da una variabile della quale viene eseguito il mapping al valore della raccolta dell'enumeratore e che viene aggiornata a ogni iterazione del ciclo.  
  
 Per evitare le conseguenze negative della temporizzazione non deterministica dell'esecuzione parallela delle attività nel ciclo, è possibile configurare il pacchetto in modo da eseguire un solo eseguibile alla volta. Se ad esempio un pacchetto che può eseguire più attività contemporaneamente include un contenitore Ciclo Foreach che enumera i file in una cartella, recupera i nomi dei file e quindi utilizza un'attività Esegui SQL per inserire i nomi dei file in una tabella, quando due istanze dell'attività Esegui SQL tentano di scrivere contemporaneamente nella tabella potrebbero verificarsi conflitti di scrittura. Per altre informazioni, vedere [Utilizzo delle espressioni di proprietà nei pacchetti](../expressions/use-property-expressions-in-packages.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per informazioni dettagliate sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Configurare un contenitore Ciclo Foreach](foreach-loop-container.md)  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
 Per informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>  
  
## <a name="related-content"></a>Contenuto correlato  
 Intervento nel blog relativo all' [enumeratore Foreach Nodelist in SSIS](https://go.microsoft.com/fwlink/?LinkId=220671)sul sito Web bidn.com.  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di controllo](control-flow.md)   
 [Contenitori in Integration Services](integration-services-containers.md)  
  
  
