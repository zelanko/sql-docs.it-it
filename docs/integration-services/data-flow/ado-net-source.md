---
title: Origine ADO NET | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.adonetsource.f1
- sql13.dts.designer.adonetsource.connection.f1
- sql13.dts.designer.adonetsource.columns.f1
- sql13.dts.designer.adonetsource.erroroutput.f1
helpviewer_keywords:
- ADO.NET source
- sources [Integration Services], ADO.NET
- sources [Integration Services], DataReader
- .NET Framework [Integration Services]
- DataReader source
ms.assetid: 2a2f1750-2cda-4dda-9dca-623a96a6b3c0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 327585d0cdf0644a7beaddc83aba3d7451c812bd
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290577"
---
# <a name="ado-net-source"></a>Origine ADO NET
  L'origine ADO NET utilizza i dati di un provider .NET e li rende disponibili per il flusso di dati.  
  
 È possibile usare l'origine ADO NET per connettersi a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. La connessione a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] tramite OLE DB non è supportata. Per altre informazioni su [!INCLUDE[ssSDS](../../includes/sssds-md.md)], vedere [Limitazioni e linee guida generali per il database SQL di Azure](https://go.microsoft.com/fwlink/?LinkId=248228).  
  
## <a name="data-type-support"></a>Supporto dei tipi di dati  
 Tramite l'origine viene convertito qualsiasi tipo di dati di cui non è stato eseguito il mapping a un tipo di dati specifico di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel tipo di dati DT_NTEXT di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . La conversione viene eseguita anche se il tipo di dati è **System.Object**.  
  
 È possibile modificare il tipo di dati DT_NTEXT nel tipo di dati DT_WSTR e vice versa. È possibile modificare i tipi di dati configurando la proprietà **DataType** nella finestra di dialogo **Editor avanzato** dell'origine ADO NET. Per altre informazioni, vedere [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
 Il tipo di dati DT_NTEXT può anche essere convertito nel tipo di dati DT_BYTES o DT_STR utilizzando una trasformazione Conversione dati sull'origine ADO NET. Per altre informazioni, vedere [Trasformazione Conversione dati](../../integration-services/data-flow/transformations/data-conversion-transformation.md).  
  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]sui tipi di dati relativi alle date, DT_DBDATE, DT_DBTIME2, DT_DBTIMESTAMP2 e DT_DBTIMESTAMPOFFSET, viene eseguito il mapping a tipi di dati relativi alle date specifici in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile configurare l'origine ADO NET per convertire i tipi di dati relativi alle date usati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nei tipi usati in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per configurare l'origine ADO NET per convertire questi tipi di dati relativi alle date, impostare la proprietà **Type System Version** della gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] su **Ultima versione**. La proprietà **Type System Version** si trova nella pagina **Tutto** della finestra di dialogo **Gestione connessione** . Per aprire la finestra di dialogo **Gestione connessione** , fare clic con il pulsante destro del mouse sulla gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] e quindi su **Modifica**.  
  
> [!NOTE]  
>  Se la proprietà **Type System Version** della gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] è impostata su **SQL Server 2005**, i tipi di dati per le date di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono convertiti in dati DT_WSTR.  
  
 I tipi di dati definiti dall'utente (UDT, User-Defined Type) vengono convertiti negli oggetti binari di grandi dimensioni (Binary Large Object) di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] quando la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] specifica il provider come provider di dati .NET per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SqlClient). Durante la conversione del tipo di dati definito dall'utente (UDT), vengono applicate le regole seguenti:  
  
-   Se i dati sono di tipo definito dall'utente (UDT) di piccole dimensioni, vengono convertiti nel tipo di dati DT_BYTES.  
  
-   Se i dati sono di tipo definito dall'utente (UDT) non di grandi dimensioni e la proprietà **Length** della colonna nel database è impostata su -1 o su un valore maggiore di 8000 byte, i dati vengono convertiti nel tipo di dati DT_IMAGE.  
  
-   Se i dati sono di tipo definito dall'utente (UDT) di grandi dimensioni, vengono convertiti nel tipo di dati DT_IMAGE.  
  
    > [!NOTE]  
    >  Se l'origine ADO NET non è configurata per l'utilizzo dell'output degli errori, i dati vengono trasmessi alla colonna DT_IMAGE in blocchi da 8.000 byte. Se l'origine ADO NET è configurata per l'utilizzo dell'output degli errori, l'intera matrice di byte viene trasmessa alla colonna DT_IMAGE. Per altre informazioni sulla configurazione dei componenti per l'uso dell'output degli errori, vedere [Gestione degli errori nei dati](../../integration-services/data-flow/error-handling-in-data.md).  
  
 Per altre informazioni sui tipi di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , sulle conversioni dei tipi di dati supportate e sul mapping dei tipi di dati in alcuni database, tra cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Per altre informazioni sul mapping di tipi di dati di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a tipi di dati gestiti, vedere [Utilizzo di tipi di dati nel flusso di dati](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md).  
  
## <a name="ado-net-source-troubleshooting"></a>Risoluzione dei problemi relativi all'origine ADO NET  
 È possibile registrare le chiamate eseguite dall'origine ADO NET a provider di dati esterni. Questa funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi al caricamento di dati da origini esterne da parte dell'origine ADO NET. Per registrare le chiamate eseguite dall'origine ADO NET a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** al livello di pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="ado-net-source-configuration"></a>Configurazione dell'origine ADO NET  
 Per configurare l'origine ADO NET, è necessario specificare l'istruzione SQL che definisce il set di risultati. Un'origine ADO NET che si connette ad esempio al database [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] e usa l'istruzione SQL `SELECT * FROM Production.Product` estrae tutte le righe della tabella **Production.Product** e fornisce il set di dati a un componente a valle.  
  
> [!NOTE]  
>  Quando si utilizza un'istruzione SQL per richiamare una stored procedure che restituisce risultati da una tabella temporanea, utilizzare l'opzione WITH RESULT SETS per definire metadati per il set di risultati.  
  
> [!NOTE]  
>  Se si usa un'istruzione SQL per eseguire una stored procedure e l'esecuzione del pacchetto ha esito negativo con l'errore seguente, è possibile risolvere il problema aggiungendo l'istruzione **SET FMTONLY OFF** prima dell'istruzione exec.  
>   
>  **Impossibile trovare la colonna <nome_colonna> nell'origine dati.**  
  
 Nell'origine ADO NET viene usata una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] in cui è specificato il provider .NET per connettersi a un'origine dati. Per altre informazioni, vedere [Gestione connessione ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md).  
  
 L'origine ADO NET include un output regolare e un output degli errori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate ADO NET](../../integration-services/data-flow/ado-net-custom-properties.md)  
  
 Per altre informazioni su come impostare le proprietà, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="ado-net-source-editor-connection-manager-page"></a>Editor origine ADO NET (pagina Gestione connessione)
  Usare la pagina **Gestione connessione** della finestra di dialogo **Editor origine ADO.NET** per selezionare la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] per l'origine. Tramite questa pagina è inoltre possibile selezionare una tabella o una vista del database.  
  
 Per ulteriori informazioni sull'origine ADO NET, vedere [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Per aprire la pagina Gestione connessione**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con l'origine ADO NET.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine ADO NET.  
  
3.  In **Editor origine ADO.NET**, fare clic su **Gestione connessione**.  
  
### <a name="static-options"></a>Opzioni statiche  
 **Gestione connessione ADO.NET**  
 Selezionare una gestione connessione esistente nell'elenco o crearne una nuova facendo clic su **Nuova**.  
  
 **Nuova**  
 Consente di creare una nuova gestione connessione usando la finestra di dialogo **Configura gestione connessione ADO.NET** .  
  
 **Modalità di accesso ai dati**  
 Consente di specificare il metodo per la selezione dei dati dall'origine.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Tabella o vista|Consente di recuperare dati da una tabella o da una vista nell'origine dei dati [!INCLUDE[vstecado](../../includes/vstecado-md.md)] .|  
|Comando SQL|Consente di recuperare dati dall'origine dei dati [!INCLUDE[vstecado](../../includes/vstecado-md.md)] usando una query SQL.|  
  
 **Anteprima**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Vista dati** . L'**anteprima** supporta la visualizzazione di un massimo di 200 righe.  
  
> [!NOTE]  
>  Quando vengono visualizzati i dati in anteprima, le colonne con tipo definito dall'utente CLR (UDT) non contengono dati. Vengono invece visualizzati i valori \<dimensione valore eccessiva per la visualizzazione> o System.Byte[]. Il primo viene visualizzato se si accede all'origine dei dati mediante il [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , il secondo se si utilizza il provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
### <a name="data-access-mode-dynamic-options"></a>Opzioni dinamiche relative alla modalità di accesso ai dati  
  
#### <a name="data-access-mode--table-or-view"></a>Modalità di accesso ai dati = Tabella o vista  
 **Nome tabella o vista**  
 Consente di selezionare il nome della tabella o della vista nell'elenco dei nomi disponibili nell'origine dei dati.  
  
#### <a name="data-access-mode--sql-command"></a>Modalità di accesso ai dati = Comando SQL  
 **Testo comando SQL**  
 Immettere il testo di una query SQL, fare clic su **Compila query**per compilare la query o fare clic su **Sfoglia**per individuare il file che contiene il testo della query.  
  
 **Compila query**  
 Usare la finestra di dialogo **Generatore query** per creare la query SQL con strumenti grafici.  
  
 **Sfoglia**  
 Usare la finestra di dialogo **Apri** per individuare il file contenente il testo della query SQL.  
  
## <a name="ado-net-source-editor-columns-page"></a>Editor origine ADO NET (pagina Colonne)
  Usare la pagina **Colonne** della finestra di dialogo **Editor origine ADO NET** per eseguire il mapping tra una colonna di output e ogni colonna esterna (di origine).  
  
 Per ulteriori informazioni sull'origine ADO NET, vedere [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Per aprire la pagina Colonne**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con l'origine ADO NET.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine ADO NET.  
  
3.  In **Editor origine ADO NET**, fare clic su **Colonne**.  
  
### <a name="options"></a>Opzioni  
 **Colonne esterne disponibili**  
 Consente di visualizzare l'elenco delle colonne esterne disponibili nell'origine dei dati. Non è possibile utilizzare questa tabella per l'aggiunta o l'eliminazione di colonne.  
  
 **Colonna esterna**  
 Consente di visualizzare le colonne esterne (di origine) nell'ordine in cui verranno presentate durante la configurazione di componenti che utilizzano i dati dell'origine.  
  
 **Colonna di output**  
 Consente di specificare un nome univoco per ogni colonna di output. Per impostazione predefinita viene suggerito il nome della colonna esterna (di origine) selezionata. È comunque possibile scegliere qualsiasi nome descrittivo univoco. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
## <a name="ado-net-source-editor-error-output-page"></a>Editor origine ADO NET (pagina Output errori)
  Usare la pagina **Output errori** della finestra di dialogo **Editor origine ADO NET** per selezionare le opzioni di gestione degli errori e impostare le proprietà delle colonne di output degli errori.  
  
 Per ulteriori informazioni sull'origine ADO NET, vedere [ADO NET Source](../../integration-services/data-flow/ado-net-source.md).  
  
 **Per aprire la pagina Output errori**  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], aprire il pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con l'origine ADO NET.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine ADO NET.  
  
3.  In **Editor origine ADO NET**, fare clic su **Output errori**.  
  
### <a name="options"></a>Opzioni  
 **Input/Output**  
 Consente di visualizzare il nome dell'origine dei dati.  
  
 **Colonna**  
 Consente di visualizzare le colonne esterne (di origine) selezionate nella pagina **Gestione connessione** della finestra di dialogo **Editor origine ADO NET** .  
  
 **Errore**  
 Consente di specificare l'azione da eseguire in caso di errori, ovvero ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Argomenti correlati:** [Gestione degli errori nei dati](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Troncamento**  
 Consente di specificare l'azione da eseguire in caso di troncamenti, ovvero ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Descrizione**  
 Consente di visualizzare la descrizione dell'errore.  
  
 **Imposta questo valore nelle celle selezionate**  
 Consente di specificare l'azione che dovrà interessare tutte le celle selezionate in caso di errore o troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Applica**  
 Consente di applicare l'opzione di gestione degli errori alle celle selezionate.  
  
## <a name="see-also"></a>Vedere anche  
 [Destinazione DataReader](../../integration-services/data-flow/datareader-destination.md)   
 [Destinazione ADO NET](../../integration-services/data-flow/ado-net-destination.md)   
 [Flusso di dati](../../integration-services/data-flow/data-flow.md)  
  
  
