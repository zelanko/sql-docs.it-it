---
title: Creare la funzione per il recupero dei dati delle modifiche | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],creating function
ms.assetid: 55dd0946-bd67-4490-9971-12dfb5b9de94
author: janinezhang
ms.author: janinez
ms.openlocfilehash: e4da506162bc50e4089c0077b4b2e94854282c3b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060828"
---
# <a name="create-the-function-to-retrieve-the-change-data"></a>Creazione della funzione per il recupero dei dati delle modifiche

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Dopo avere completato il flusso di controllo per un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che esegue un caricamento incrementale dei dati delle modifiche, l'attività successiva consiste nella creazione di una funzione con valori di tabella per il recupero di tali dati. Questa funzione deve essere creata solo una volta, prima del primo caricamento incrementale.  
  
> [!NOTE]  
>  La creazione di una funzione per il recupero dei dati delle modifiche rappresenta il secondo passaggio del processo di creazione di un pacchetto che esegue il caricamento incrementale di tali dati. Per una descrizione del processo completo di creazione del pacchetto, vedere [Change Data Capture &#40;SSIS &#41;](../../integration-services/change-data-capture/change-data-capture-ssis.md) (Modificare i dati di acquisizione &#40;SSIS &#41;).  
  
## <a name="design-considerations-for-change-data-capture-functions"></a>Considerazioni sulla progettazione per le funzioni Change Data Capture  
 Per recuperare i dati delle modifiche, un componente di origine nel flusso di dati del pacchetto chiama una delle funzioni Change Data Capture seguenti:  
  
-   **cdc.fn_cdc_get_net_changes_<capture_instance>** Per questa query, la singola riga restituita per ogni aggiornamento contiene lo stato finale di ogni riga modificata. Nella maggior parte dei casi i dati restituiti da una query sono necessari solo per modifiche totali. Per altre informazioni, vedere [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md).  
  
-   **cdc.fn_cdc_get_all_changes_<capture_instance>** Questa query restituisce tutte le modifiche apportate in ogni riga durante l'intervallo di acquisizione. Per altre informazioni, vedere [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md).  
  
 Il componente di origine passa quindi i risultati restituiti dalla funzione a destinazioni e trasformazioni a valle, che applicano i dati delle modifiche alla destinazione finale.  
  
 Un componente di origine di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , tuttavia, non è in grado di chiamare direttamente le funzioni di acquisizioni dei dati delle modifiche. Un componente di origine di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] richiede i metadati sulle colonne restituite dalla query. Le funzioni Change Data Capture non definiscono le colonne della relativa tabella di output. Di conseguenza, le funzioni non restituiscono metadati sufficienti per un componente di origine di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Viene utilizzata invece una funzione wrapper con valori di tabella perché questo tipo di funzione definisce in modo esplicito le colonne della relativa tabella di output nella clausola RETURNS. Questa definizione esplicita di colonne fornisce i metadati necessari per un componente di origine di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . È necessario creare questa funzione per ogni tabella per cui si desidera recuperare dati delle modifiche.  
  
 Sono disponibili due opzioni per la creazione della funzione wrapper con valori di tabella che chiama la funzione di query Change Data Capture:  
  
-   È possibile chiamare la stored procedure di sistema **sys.sp_cdc_generate_wrapper_function** per creare automaticamente le funzioni con valori di tabella.  
  
-   È possibile scrivere una funzione con valori di tabella personalizzata tramite le linee guida e l'esempio presenti in questo argomento.  
  
## <a name="calling-a-stored-procedure-to-create-the-table-valued-function"></a>Chiamata di una stored procedure per la creazione della funzione con valori di tabella  
 Il modo più semplice e rapido per creare le funzioni con valori di tabella necessarie consiste nel chiamare la stored procedure di sistema **sys.sp_cdc_generate_wrapper_function** . Questa stored procedure genera gli script per creare le funzioni wrapper specificamente progettate per soddisfare le esigenze di un componente di origine di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  La stored procedure di sistema **sys.sp_cdc_generate_wrapper_function** non crea direttamente le funzioni wrapper, ma genera gli script CREATE per le funzioni wrapper. Lo sviluppatore deve eseguire gli script CREATE generati dalla stored procedure affinché le funzioni wrapper possano essere chiamate da un pacchetto del caricamento incrementale.  
  
 Per comprendere il modo in cui utilizzare questa stored procedure di sistema è necessario capire le operazioni eseguite dalla procedura, gli script generati dalla procedura e le funzioni wrapper create dagli script.  
  
### <a name="understanding-and-using-the-stored-procedure"></a>Informazioni sulla stored procedure e relativo utilizzo  
 La stored procedure di sistema **sys.sp_cdc_generate_wrapper_function** genera gli script per creare le funzioni wrapper da usare con i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Di seguito vengono riportate le prime righe della definizione della stored procedure:  
  
 `CREATE PROCEDURE sys.sp_cdc_generate_wrapper_function`  
  
 `(`  
  
 `@capture_instance sysname = null`  
  
 `@closed_high_end_point bit = 1,`  
  
 `@column_list = null,`  
  
 `@update_flag_list = null`  
  
 `)`  
  
 Tutti i parametri per la stored procedure sono facoltativi. Se si chiama la stored procedure senza fornire alcun valore per i parametri, la stored procedure crea funzioni wrapper per tutte le istanze di acquisizione a cui si ha accesso.  
  
> [!NOTE]  
>  Per altre informazioni sulla sintassi di questa stored procedure e sui relativi parametri, vedere [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md).  
  
 La stored procedure genera sempre una funzione wrapper per restituire tutte le modifiche da ogni istanza di acquisizione. Se durante la creazione dell'istanza di acquisizione è stato impostato il parametro *@supports_net_changes* , la stored procedure genera anche una funzione wrapper per restituire le modifiche totali da ogni istanza di acquisizione applicabile.  
  
 La stored procedure restituisce un set di risultati con due colonne:  
  
-   Il nome della funzione wrapper generata dalla stored procedure. La stored procedure deduce il nome della funzione dal nome dell'istanza di acquisizione. Il nome della funzione è 'fn_all_changes_' seguito dal nome dell'istanza di acquisizione. Il prefisso utilizzato per la funzione di rilevamento delle modifiche delta, se creato, è 'fn_net_changes_'.  
  
-   L'istruzione CREATE per la funzione wrapper.  
  
### <a name="understanding-and-using-the-scripts-created-by-the-stored-procedure"></a>Informazioni sugli script creati dalla stored procedure e relativo utilizzo  
 Uno sviluppatore usa in genere un'istruzione INSERT...EXEC per chiamare la stored procedure **sys.sp_cdc_generate_wrapper_function** e salvare gli script creati dalla stored procedure in una tabella temporanea. Ogni script può quindi essere selezionato singolarmente ed eseguito per creare la funzione wrapper corrispondente. Uno sviluppatore può tuttavia utilizzare anche un set di comandi SQL per eseguire tutti gli script CREATE, come illustrato nel codice di esempio seguente:  
  
```  
create table #wrapper_functions  
      (function_name sysname, create_stmt nvarchar(max))  
insert into #wrapper_functions  
exec sys.sp_cdc_generate_wrapper_function  
  
declare @stmt nvarchar(max)  
declare #hfunctions cursor local fast_forward for   
      select create_stmt from #wrapper_functions  
open #hfunctions  
fetch #hfunctions into @stmt  
while (@@fetch_status <> -1)  
begin  
      exec sp_executesql @stmt  
      fetch #hfunctions into @stmt  
end  
close #hfunctions  
deallocate #hfunctions  
```  
  
### <a name="understanding-and-using-the-functions-created-by-the-stored-procedure"></a>Informazioni sulle funzioni create dalla stored procedure e relativo utilizzo  
 Per ripercorrere sistematicamente la cronologia dei dati modificati acquisiti, le funzioni wrapper generate richiedono che il parametro *@end_time* di un intervallo sia il parametro *@start_time* dell'intervallo successivo. Quando viene rispettata questa convenzione, le funzioni wrapper generate possono effettuare le attività seguenti:  
  
-   Eseguire il mapping dei valori di data e ora ai valori LSN utilizzati internamente.  
  
-   Verificare che i dati non vengano persi o ripetuti.  
  
 Per semplificare l'esecuzione di query su tutte le righe di una tabella delle modifiche, le funzioni wrapper generate supportano inoltre le convenzioni seguenti:  
  
-   Se il parametro @start_time è null, le funzioni wrapper usano il valore LSN minimo nell'istanza di acquisizione come limite inferiore della query.  
  
-   Se il parametro @end_time è null, le funzioni wrapper usano il valore LSN massimo nell'istanza di acquisizione come limite superiore della query.  
  
 La maggior parte degli utenti dovrebbe essere in grado di usare le funzioni wrapper create dalla stored procedure di sistema **sys.sp_cdc_generate_wrapper_function** senza apportare modifiche. Tuttavia, per personalizzare le funzioni wrapper, è necessario personalizzare gli script CREATE prima di eseguire gli script.  
  
 Quando il pacchetto chiama le funzioni wrapper, il pacchetto deve fornire i valori per tre parametri. Questi tre parametri sono analoghi ai tre parametri utilizzati dalle funzioni Change Data Capture. I tre parametri sono:  
  
-   Il valore data/ora di inizio e il valore data/ora di fine per l'intervallo. Mentre le funzioni wrapper utilizzano i valori di data e ora come endpoint per l'intervallo di query, le funzioni Change Data Capture utilizzano due valori LSN come endpoint.  
  
-   Il filtro di riga. Il parametro *@row_filter_option* è uguale sia per le funzioni wrapper che per le funzioni di Change Data Capture. Per altre informazioni, vedere [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) e [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md).  
  
 Il set di risultati restituito dalle funzioni wrapper include i dati seguenti:  
  
-   Tutte le colonne di dati di modifica richieste.  
  
-   Una colonna denominata __CDC_OPERATION che utilizza un campo di uno o due caratteri per identificare l'operazione associata alla riga. I valori validi per questo campo sono i seguenti: 'I' per inserimento, 'D' per eliminazione, 'UO' per aggiornamento di valori vecchi e 'UN' per aggiornamento di valori nuovi.  
  
-   Flag di aggiornamento, quando necessari, visualizzati come colonne bit dopo il codice dell'operazione e nell'ordine specificato nel parametro *@update_flag_list* . Per creare il nome di queste colonne, si aggiunge '_uflag' al nome della colonna associato.  
  
 Se il pacchetto chiama una funzione wrapper che esegue una query su tutte le modifiche, la funzione wrapper restituisce anche le colonne __CDC_STARTLSN e \__CDC_SEQVAL. Queste due colonne diventano rispettivamente la prima e la seconda colonna del set di risultati. La funzione wrapper ordina inoltre il set di risultati in base a queste due colonne.  
  
## <a name="writing-your-own-table-value-function"></a>Scrittura della funzione con valori di tabella personalizzata  
 È anche possibile usare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per scrivere una funzione wrapper con valori di tabella personalizzata che chiama la funzione di query Change Data Capture e archiviare la funzione wrapper con valori di tabella in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni sulla creazione di una funzione Transact-SQL, vedere [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md).  
  
 Nell'esempio seguente viene definita una funzione con valori di tabella per il recupero delle modifiche da una tabella Customer per l'intervallo di modifiche specificato. La funzione usa le funzioni di Change Data Capture per eseguire il mapping tra i valori **datetime** e i valori dei numeri di sequenza del file di log (LSN) binario usati dalle tabelle delle modifiche. Questa funzione gestisce inoltre diverse condizioni speciali:  
  
-   Quando viene passato un valore Null per l'ora di inizio, questa funzione utilizza il valore disponibile per primo.  
  
-   Quando viene passato un valore Null per l'ora di fine, questa funzione utilizza il valore disponibile per ultimo.  
  
-   Quando il numero LSN iniziale è uguale al numero LSN finale, a indicare in genere che non è presente alcun record per l'intervallo selezionato, la funzione viene chiusa.  
  
### <a name="example-of-a-table-value-function-that-queries-for-change-data"></a>Esempio di una funzione con valori di tabella che esegue query per i dati delle modifiche  
  
```  
CREATE function CDCSample.uf_Customer (  
     @start_time datetime  
    ,@end_time datetime  
)  
returns @Customer table (  
     CustomerID int  
    ,TerritoryID int  
    ,CustomerType nchar(1)  
    ,rowguid uniqueidentifier  
    ,ModifiedDate datetime  
    ,CDC_OPERATION varchar(1)  
) as  
begin  
    declare @from_lsn binary(10), @to_lsn binary(10)  
  
    if (@start_time is null)  
        select @from_lsn = sys.fn_cdc_get_min_lsn('Customer')  
    else  
        select @from_lsn = sys.fn_cdc_increment_lsn(sys.fn_cdc_map_time_to_lsn('largest less than or equal',@start_time))  
  
    if (@end_time is null)  
        select @to_lsn = sys.fn_cdc_get_max_lsn()  
    else  
        select @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal',@end_time)  
  
    if (@from_lsn = sys.fn_cdc_increment_lsn(@to_lsn))  
        return  
  
    -- Query for change data  
    insert into @Customer  
    select   
        CustomerID,      
        TerritoryID,   
        CustomerType,   
        rowguid,   
        ModifiedDate,   
        case __$operation  
                when 1 then 'D'  
                when 2 then 'I'  
                when 4 then 'U'  
                else null  
         end as CDC_OPERATION  
    from   
        cdc.fn_cdc_get_net_changes_Customer(@from_lsn, @to_lsn, 'all')  
  
    return  
end   
go  
  
```  
  
### <a name="retrieving-additional-metadata-with-the-change-data"></a>Recupero di metadati aggiuntivi con i dati di modifica  
 Anche se la funzione con valori di tabella creata dall'utente illustrata in precedenza usa solo la colonna **__$operation**, la funzione **cdc.fn_cdc_get_net_changes_<capture_instance>** restituisce quattro colonne di metadati per ogni riga di modifica. Se si desidera utilizzare questi valori nel flusso di dati, è possibile restituirli come colonne aggiuntive dalla funzione wrapper con valori di tabella.  
  
|Nome colonna|Tipo di dati|Descrizione|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|Valore LSN associato al commit della transazione per la modifica.<br /><br /> Tutte le modifiche di cui è stato eseguito il commit nella stessa transazione condividono lo stesso valore LSN di commit. Se, ad esempio, un'operazione di aggiornamento nella tabella di origine modifica due diverse righe, la tabella delle modifiche conterrà quattro righe, due con i valori precedenti e due con i nuovi valori, ognuna delle quali con lo stesso valore **__$start_lsn** .|  
|**__$seqval**|**binary(10)**|Valore di sequenza utilizzato per ordinare le modifiche alle righe in una transazione.|  
|**__$operation**|**int**|Operazione DML (Data Manipulation Language) associata alla modifica. I possibili valori sono i seguenti:<br /><br /> 1 = eliminazione<br /><br /> 2 = inserimento<br /><br /> 3 = aggiornamento (valori precedenti all'operazione di aggiornamento)<br /><br /> 4 = aggiornamento (valori successivi all'operazione di aggiornamento)|  
|**__$update_mask**|**varbinary(128)**|Maschera di bit basata su numeri ordinali di colonna della tabella delle modifiche che identifica le colonne modificate. È possibile esaminare questo valore se è necessario determinare le colonne modificate.|  
|**\<colonne della tabella di origine acquisite>**|variabile|Le colonne rimanenti restituite dalla funzione sono le colonne della tabella di origine identificate come colonne acquisite durante la creazione dell'istanza di acquisizione. Se in origine non è stata specificata alcuna colonna nell'elenco delle colonne acquisite, verranno restituite tutte le colonne della tabella di origine.|  
  
 Per altre informazioni, vedere [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md).  
  
## <a name="next-step"></a>Passaggio successivo  
 Dopo avere creato la funzione con valori di tabella per l'esecuzione di query per i dati delle modifiche, il passaggio successivo consiste nell'iniziare a progettare il flusso di dati nel pacchetto.  
  
 **Argomento successivo:** [Recuperare e interpretare i dati delle modifiche](../../integration-services/change-data-capture/retrieve-and-understand-the-change-data.md)  
  
  
