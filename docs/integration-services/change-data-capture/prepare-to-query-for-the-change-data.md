---
description: Preparazione dell'esecuzione di una query per i dati delle modifiche
title: Preparare l'esecuzione di una query per i dati delle modifiche | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],preparing query
ms.assetid: 9ea2db7a-3dca-4bbf-9903-cccd2d494b5f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b0b2f12bf0ad4b5166e7a206b30264782992f144
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457693"
---
# <a name="prepare-to-query-for-the-change-data"></a>Preparazione dell'esecuzione di una query per i dati delle modifiche

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Nel flusso di controllo di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per l'esecuzione di un caricamento incrementale dei dati delle modifiche, la terza e ultima attività consiste nel preparare l'esecuzione di una query per i dati delle modifiche e nell'aggiungere un'attività Flusso di dati.  
  
> [!NOTE]  
>  La seconda attività per il flusso di controllo consiste nel verificare che i dati delle modifiche per l'intervallo selezionato siano pronti. Per altre informazioni su questa attività, vedere [Determinare se i dati delle modifiche sono pronti](../../integration-services/change-data-capture/determine-whether-the-change-data-is-ready.md). Per una descrizione del processo complessivo di progettazione del flusso di controllo, vedere [Change Data Capture &#40;SSIS&#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md).  
  
## <a name="design-considerations"></a>Considerazioni sulla progettazione  
 Per recuperare i dati delle modifiche, è necessario chiamare una funzione Transact-SQL con valori di tabella che accetti gli endpoint dell'intervallo come parametri di input e restituisca i dati delle modifiche per l'intervallo specificato. Un componente di origine nel flusso di dati chiama questa funzione. Per informazioni su questo componente di origine, vedere [Recuperare e comprendere i dati delle modifiche](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md).  
  
 I componenti di origine [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usati più di frequente, incluse l'origine OLE DB, l'origine ADO e l'origine ADO NET, non possono derivare informazioni sui parametri per una funzione valutata a livello di tabella. La maggior parte delle origini, pertanto, non può chiamare una funzione con parametri direttamente.  
  
 Per passare i parametri di input alla funzione, sono disponibili due opzioni di progettazione:  
  
-   **Assemblare la query con parametri come stringa**. È possibile utilizzare un'attività Script o un'attività Esegui SQL per assemblare una stringa SQL dinamica con valori di parametro specificati a livello di codice nella stringa. È quindi possibile archiviare tale stringa in una variabile del pacchetto e utilizzarla per impostare la proprietà SqlCommand di un componente di origine. Questo approccio ha esito positivo perché il componente di origine non richiede più informazioni sui parametri.  
  
    > [!NOTE]  
    >  Uno script precompilato è soggetto a un overhead minore rispetto a un'attività Esegui SQL.  
  
-   **Usare un wrapper con parametri**. In alternativa, è possibile creare una stored procedure con parametri come wrapper che chiama la funzione valutata a livello di tabella con parametri. Questo approccio ha esito positivo perché un componente di origine è in grado di derivare correttamente le informazioni sui parametri per una stored procedure.  
  
 In questo argomento viene utilizzata la prima opzione di progettazione, assemblando una query con parametri come stringa.  
  
## <a name="preparing-the-query"></a>Preparazione della query  
 Prima che sia possibile concatenare i valori dei parametri di input in una singola stringa di query, è necessario configurare le variabili del pacchetto necessarie per la query.  
  
#### <a name="to-set-up-package-variables"></a>Per configurare le variabili del pacchetto  
  
-   Nella finestra [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Variabili **in** creare una variabile con un tipo di dati stringa per memorizzare la stringa di query restituita dall'attività Esegui SQL.  
  
     In questo esempio viene utilizzato il nome di variabile SqlDataQuery.  
  
 Dopo avere creato la variabile del pacchetto, è possibile utilizzare un'attività Script o un'attività Esegui SQL per concatenare i valori dei parametri di input. Nelle due procedure seguenti viene descritto come configurare tali componenti.  
  
#### <a name="to-use-a-script-task-to-concatenate-the-query-string"></a>Per utilizzare un'attività Script per concatenare la stringa di query  
  
1.  Nella scheda **Flusso di controllo** aggiungere un'attività Script al pacchetto dopo il contenitore Ciclo For e connettere tale contenitore all'attività.  
  
    > [!NOTE]  
    >  In questa procedura si presuppone che il pacchetto esegua un caricamento incrementale da una singola tabella. Se il pacchetto esegue il caricamento da più tabelle e ha un pacchetto padre con più pacchetti figlio, questa attività viene aggiunta come primo componente a ciascun pacchetto figlio. Per altre informazioni, vedere [Eseguire un caricamento incrementale di più tabelle](../../integration-services/change-data-capture/perform-an-incremental-load-of-multiple-tables.md).  
  
2.  Nella pagina **Script**in **Editor attività Script** selezionare le opzioni seguenti:  
  
    1.  Per **ReadOnlyVariables**selezionare **User::DataReady**, **User::ExtractStartTime**e **User::ExtractEndTime** .  
  
    2.  Per **ReadWriteVariables**selezionare User::SqlDataQuery nell'elenco.  
  
3.  Nella pagina **Script**in **Editor attività Script** fare clic su **Modifica script** per aprire l'ambiente di sviluppo dello script.  
  
4.  Nella routine Main immettere uno dei segmenti di codice seguenti:  
  
    -   Se si utilizza il linguaggio di programmazione C#, immettere le righe di codice seguenti:  
  
        ```csharp 
        int dataReady;  
        System.DateTime extractStartTime;  
        System.DateTime extractEndTime;  
        string sqlDataQuery;  
  
        dataReady = (int)Dts.Variables["DataReady"].Value;  
        extractStartTime = (System.DateTime)Dts.Variables["ExtractStartTime"].Value;  
        extractEndTime = (System.DateTime)Dts.Variables["ExtractEndTime"].Value;  
  
        if (dataReady == 2)  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) + "', '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
        else  
          {  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" + ", '" + string.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) + "')";  
          }  
  
        Dts.Variables["SqlDataQuery"].Value = sqlDataQuery;  
        ```  
  
         \- - oppure -  
  
    -   Se si usa il linguaggio di programmazione [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], immettere le righe di codice seguenti:  
  
        ```vb  
        Dim dataReady As Integer  
        Dim extractStartTime As Date  
        Dim extractEndTime As Date  
        Dim sqlDataQuery As String  
  
        dataReady = CType(Dts.Variables("DataReady").Value, Integer)  
        extractStartTime = CType(Dts.Variables("ExtractStartTime").Value, Date)  
        extractEndTime = CType(Dts.Variables("ExtractEndTime").Value, Date)  
  
        If dataReady = 2 Then  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer('" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractStartTime) & _  
              "', '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        Else  
          sqlDataQuery = "SELECT * FROM CDCSample.uf_Customer(null" & _  
              ", '" & _  
              String.Format("{0:yyyy-MM-dd hh:mm:ss}", extractEndTime) & _  
              "')"  
        End If  
  
        Dts.Variables("SqlDataQuery").Value = sqlDataQuery  
  
        ```  
  
5.  Lasciare la riga di codice predefinita, che restituisce **DtsExecResult.Success** dall'esecuzione dello script.  
  
6.  Chiudere l'ambiente di sviluppo dello script ed **Editor attività Script**.  
  
#### <a name="to-use-an-execute-sql-task-to-concatenate-the-query-string"></a>Per utilizzare un'attività Esegui SQL per concatenare la stringa di query  
  
1.  Nella scheda **Flusso di controllo** aggiungere un'attività Esegui SQL al pacchetto dopo il contenitore Ciclo For e connettere tale contenitore all'attività.  
  
    > [!NOTE]  
    >  In questa procedura si presuppone che il pacchetto esegua un caricamento incrementale da una singola tabella. Se il pacchetto esegue il caricamento da più tabelle e ha un pacchetto padre con più pacchetti figlio, questa attività viene aggiunta come primo componente a ciascun pacchetto figlio. Per altre informazioni, vedere [Eseguire un caricamento incrementale di più tabelle](../../integration-services/change-data-capture/perform-an-incremental-load-of-multiple-tables.md).  
  
2.  Nella pagina **Generale**in **Editor attività Esegui SQL** selezionare le opzioni seguenti:  
  
    1.  Per **ResultSet**, selezionare **Riga singola**.  
  
    2.  Configurare una connessione valida al database di origine.  
  
    3.  Per **SQLSourceType**, selezionare **Input diretto**.  
  
    4.  Per **SQLStatement**immettere l'istruzione SQL seguente:  
  
        ```sql
        declare @ExtractStartTime datetime,  
        @ExtractEndTime datetime,   
        @DataReady int  
  
        select @DataReady = ?,   
        @ExtractStartTime = ?,   
        @ExtractEndTime = ?  
  
        if @DataReady = 2  
        select N'select * from CDCSample.uf_Customer'  
        + N'('''+ convert(nvarchar(30),@ExtractStartTime,120)  
        + ''', '''  
        + convert(nvarchar(30),@ExtractEndTime,120) + ''') '   
        as SqlDataQuery  
        else  
        select N'select * from CDCSample.uf_Customer'  
        + N'(null, '''  
        + convert(nvarchar(30),@ExtractEndTime,120)  
        + ''') '  
        as SqlDataQuery  
  
        ```  
  
        > [!NOTE]  
        >  In questo esempio la clausola **else** genera una query per il caricamento iniziale dei dati delle modifiche passando un valore Null per la data e l'ora di inizio. Questo esempio non si applica a uno scenario in cui le modifiche apportate prima dell'attivazione di Change Data Capture devono essere caricate anche nel data warehouse.  
  
3.  Nella pagina **Mapping parametri** di **Editor attività Esegui SQL**creare i mapping seguenti:  
  
    1.  Eseguire il mapping tra la variabile DataReady e il parametro 0.  
  
    2.  Eseguire il mapping tra la variabile ExtractStartTime e il parametro 1.  
  
    3.  Eseguire il mapping tra la variabile ExtractEndTime e il parametro 2.  
  
4.  Nella pagina **Set di risultati** di **Editor attività Esegui SQL**eseguire il mapping tra il nome del risultato e la variabile SqlDataQuery.  
  
     Il nome del risultato è il nome della singola colonna restituita, ovvero SqlDataQuery.  
  
 Nelle procedure precedenti è stata configurata un'attività per la preparazione di una stringa di query con valori stringa specificati a livello di codice per i parametri di input. Il codice seguente rappresenta un esempio di tale stringa di query:  
  
 `select * from CDCSample. uf_Customer('2007-06-11 14:21:58', '2007-06-12 14:21:58')`  
  
## <a name="adding-a-data-flow-task"></a>Aggiunta di un'attività Flusso di dati  
 L'ultimo passaggio nella progettazione del flusso di controllo per il pacchetto consiste nell'aggiungere un'attività Flusso di dati.  
  
#### <a name="to-add-a-data-flow-task-and-complete-the-control-flow"></a>Per aggiungere un'attività Flusso di dati e completare il flusso di controllo  
  
-   Nella scheda **Flusso di controllo** aggiungere un'attività Flusso di dati e connettere l'attività che ha concatenato la stringa di query.  
  
## <a name="next-step"></a>passaggio successivo  
 Dopo avere preparato la stringa di query e avere configurato l'attività Flusso di dati, il passaggio successivo consiste nel creare la funzione valutata a livello di tabella per il recupero dei dati delle modifiche dal database.  
  
 **Argomento successivo:** [Creare la funzione per il recupero dei dati delle modifiche](../../integration-services/change-data-capture/create-the-function-to-retrieve-the-change-data.md)  
  
  
