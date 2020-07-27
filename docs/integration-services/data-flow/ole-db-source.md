---
title: Origine OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbsource.f1
- sql13.dts.designer.oledbsourceadapter.connection.f1
- sql13.dts.designer.oledbsourceadapter.columns.f1
- sql13.dts.designer.oledbsourceadapter.errorhandling.f1
helpviewer_keywords:
- sources [Integration Services], OLE DB
- OLE DB source [Integration Services]
ms.assetid: f87cc5f6-b078-40f3-9d87-7a65e13e4c86
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3a19cee0b650c82c513bd6f4d9d0b7afd11184b3
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913809"
---
# <a name="ole-db-source"></a>Origine OLE DB

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  L'origine OLE DB consente di estrarre dati da un'ampia gamma di database relazionali conformi con OLE DB, tramite una tabella o vista di database oppure un comando SQL. L'origine OLE DB consente ad esempio di estrarre dati dalle tabelle nei database di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Se l'origine dati è [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, è richiesta una gestione connessione diversa rispetto alle versioni precedenti di Excel. Per altre informazioni, vedere [Connessione a una cartella di lavoro di Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
 Sono disponibili quattro diverse modalità di accesso ai dati per l'estrazione dei dati:  
  
-   Vista o tabella.  
  
-   Vista o tabella specificata in una variabile.  
  
-   Risultato di un'istruzione SQL. La query può essere con parametri.  
  
-   Risultato di un'istruzione SQL archiviata in una variabile.  
  
> [!NOTE]  
>  Quando si utilizza un'istruzione SQL per richiamare una stored procedure che restituisce risultati da una tabella temporanea, utilizzare l'opzione WITH RESULT SETS per definire metadati per il set di risultati.  
  
 Se si utilizza una query con parametri, sarà possibile eseguire il mapping delle variabili ai parametri per specificare i valori dei singoli parametri nelle istruzioni SQL.  
  
 Per connettersi a un'origine dei dati questa origine utilizza una gestione connessione OLE DB, che specifica il provider OLE DB da utilizzare. Per altre informazioni, vedere [Gestione connessione OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 In un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene inoltre fornito l'oggetto di origine dati da cui è possibile creare una gestione connessione OLE DB, rendendo disponibili origini dati e relative viste all'origine OLE DB.  
  
 A seconda del provider OLE DB, l'origine OLE DB può presentare le limitazioni seguenti:  
  
-   Il provider OLE DB [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Oracle non supporta i tipi di dati Oracle BLOB, CLOB, NCLOB, BFILE e UROWID e l'origine OLE DB non è in grado di estrarre dati da tabelle che contengono colonne con tali tipi di dati.  
  
-   I provider IBM OLE DB per DB2 e [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per DB2 non supportano l'utilizzo di comandi SQL che chiamano stored procedure. Quando viene utilizzato un comando di questo tipo l'origine OLE DB non è in grado di creare i metadati delle colonne e, di conseguenza, i dati delle colonne non sono disponibili per i componenti del flusso di dati che seguono l'origine OLE DB nel flusso di dati. Questo impedisce di completare l'esecuzione del flusso di dati.  
  
 L'origine OLE DB include un output regolare e un output degli errori.  
  
## <a name="using-parameterized-sql-statements"></a>Utilizzo di istruzioni SQL con parametri  
 Per l'estrazione dei dati l'origine OLE DB può utilizzare un'istruzione SQL, che può essere costituita da un'istruzione SELECT o EXEC.  
  
 L'origine OLE DB utilizza una gestione connessione OLE DB per connettersi all'origine dei dati da cui estrae i dati. A seconda del provider utilizzato dalla gestione connessione OLE DB e del sistema di gestione di database relazionali (RDBMS) a cui si connette la gestione connessione, verranno applicate regole diverse per la denominazione e l'elencazione dei parametri. Se i nomi dei parametri vengono restituiti dal sistema RDBMS, sarà possibile utilizzare nomi di parametro per eseguire il mapping dei parametri di un elenco di parametri a quelli inclusi in un'istruzione SQL. In caso contrario, sui parametri viene eseguito il mapping a quelli dell'istruzione SQL in base alla posizione ordinale nell'elenco dei parametri. I tipi di nomi di parametro supportati variano a seconda del provider. Alcuni provider richiedono ad esempio che vengano utilizzati i nomi delle variabili o delle colonne, mentre altri richiedono l'utilizzo di nomi simbolici, quali 0 o Param0. Per informazioni sui nomi di parametro da utilizzare nelle istruzioni SQL, vedere la documentazione specifica del provider.  
  
 Quando si utilizza una gestione connessione OLE DB, non è possibile utilizzare sottoquery con parametri, perché l'origine OLE DB non può derivare le informazioni sui parametri tramite il provider OLE DB. Tuttavia, è possibile usare un'espressione per concatenare i valori dei parametri nella stringa di query e impostare la proprietà SqlCommand dell'origine. In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , è possibile configurare un'origine OLE DB usando la finestra di dialogo **Editor origine OLE DB** ed eseguire il mapping dei parametri alle variabili nella finestra di dialogo **Imposta parametri query** .  
  
### <a name="specifying-parameters-by-using-ordinal-positions"></a>Indicazione dei parametri tramite la posizione ordinale  
 Se non viene restituito alcun nome di parametro, gli indicatori di parametro a cui viene eseguito il mapping dei parametri in fase di esecuzione sono determinati dall'ordine in cui compaiono i parametri nell'elenco **Parametri** della finestra di dialogo **Imposta parametri query** . Viene eseguito il mapping del primo parametro dell'elenco al primo ? nell'istruzione SQL, il secondo al secondo? e così via.  
  
 L'istruzione SQL seguente seleziona righe dalla tabella **Product[!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] del database** . Sul primo parametro nell'elenco **Mapping** viene eseguito il mapping al primo parametro nella colonna **Color** , mentre sul secondo parametro viene eseguito il mapping alla colonna **Size** .  
  
 `SELECT * FROM Production.Product WHERE Color = ? AND Size = ?`  
  
 I nomi di parametro sono ininfluenti. Se ad esempio un determinato parametro ha lo stesso nome della colonna a cui si riferisce, ma non compare nella posizione ordinale corretta nell'elenco **Parameters** , per il mapping dei parametri eseguito in fase di esecuzione verrà comunque usata la posizione ordinale del parametro e non il suo nome.  
  
 Per il comando EXEC, come nomi di parametro è in genere necessario utilizzare i nomi delle variabili che specificano i valori dei parametri nella procedura.  
  
### <a name="specifying-parameters-by-using-names"></a>Indicazione dei parametri tramite i nomi  
 Se il sistema RDBMS restituisce i nomi effettivi dei parametri, sui parametri utilizzati dalle istruzioni SELECT ed EXEC verrà eseguito il mapping in base al nome. I nomi dei parametri devono essere quelli previsti dalla stored procedure eseguita dall'istruzione SELECT o EXEC.  
  
 L'istruzione SQL seguente esegue la stored procedure **uspGetWhereUsedProductID** disponibile nel database [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] .  
  
 `EXEC uspGetWhereUsedProductID ?, ?`  
  
 La stored procedure prevede che i valori dei parametri vengano specificati dalle variabili `@StartProductID` e `@CheckDate`. L'ordine in cui i parametri sono visualizzati nell'elenco **Mapping** è irrilevante. L'unico requisito consiste nel fatto che i nomi dei parametri devono coincidere con quelli delle variabili nella stored procedure, incluso il simbolo \@.  
  
### <a name="mapping-parameters-to-variables"></a>Mapping di parametri a variabili  
 Il mapping dei parametri alle variabili che ne specificano i valori avviene in fase di esecuzione. Sebbene in genere vengano usate variabili definite dall'utente, è possibile usare anche le variabili di sistema disponibili in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se si utilizzano variabili definite dall'utente, verificare che il tipo di dati impostato sia compatibile con quello della colonna a cui fa riferimento il parametro di cui viene eseguito il mapping. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md).  
  
## <a name="troubleshooting-the-ole-db-source"></a>Risoluzione dei problemi relativi all'origine OLE DB  
 È possibile registrare le chiamate eseguite dall'origine OLE DB a provider di dati esterni. Questa funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi al caricamento di dati da origini esterne da parte dell'origine OLE DB. Per registrare le chiamate eseguite dall'origine OLE DB a provider di dati esterni, attivare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello del pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ole-db-source"></a>Configurazione dell'origine OLE DB  
 È possibile impostare le proprietà a livello di programmazione o tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Estrarre dati tramite l'origine OLE DB](../../integration-services/data-flow/extract-data-by-using-the-ole-db-source.md)  
  
-   [Mapping dei parametri di query a variabili in un componente flusso di dati](../../integration-services/data-flow/map-query-parameters-to-variables-in-a-data-flow-component.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordinare i dati per le trasformazioni Unione e Merge Join](../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 Articolo di Wiki sui [connettori SSIS con Oracle](https://go.microsoft.com/fwlink/?LinkId=220670)sul sito Web social.technet.microsoft.com.  
  
## <a name="ole-db-source-editor-connection-manager-page"></a>Editor origine OLE DB (pagina Gestione connessione)
  Usare la pagina **Gestione connessione** della finestra di dialogo **Editor origine OLE DB** per selezionare la gestione connessione OLE DB per l'origine. Tramite questa pagina è inoltre possibile selezionare una tabella o una vista del database.  
  
> [!NOTE]  
>  Per caricare dati da un'origine dati basata su [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, usare un'origine OLE DB. Non è possibile utilizzare un'origine Excel per caricare dati da un'origine dei dati Excel 2007. Per altre informazioni, vedere [Configura gestione connessione OLE DB](../../integration-services/connection-manager/configure-ole-db-connection-manager.md).  
>   
>  Per caricare dati da un'origine dei dati che utilizza [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2003 o versione precedente, utilizzare un'origine Excel. Per altre informazioni, vedere [Editor origine Excel &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/excel-source-editor-connection-manager-page.md).  
  
> [!NOTE]  
>  La proprietà **CommandTimeout** dell'origine OLE DB non è disponibile nell' **Editor origine OLE DB**, tuttavia può essere impostata usando l' **Editor avanzato**. Per ulteriori informazioni su questa proprietà, vedere la sezione relativa all'origine Excel in [Proprietà personalizzate OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
### <a name="open-the-ole-db-source-editor-connection-manager-page"></a>Aprire Editor origine OLE DB (pagina Gestione connessione)  
  
1.  Aggiungere l'origine OLE DB al pacchetto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse sul componente di origine, quindi scegliere **Modifica**.  
  
3.  Fare clic su **Gestione connessione**.  
  
### <a name="static-options"></a>Opzioni statiche  
 **Gestione connessione OLE DB**  
 Selezionare una gestione connessione esistente nell'elenco o crearne una nuova facendo clic su **Nuova**.  
  
 **Nuovo**  
 Consente di creare una nuova gestione connessione usando la finestra di dialogo **Configura gestione connessione OLE DB** .  
  
 **Modalità di accesso ai dati**  
 Consente di specificare il metodo per la selezione dei dati dall'origine.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Tabella o vista|Consente di recuperare dati da una tabella o da una vista nell'origine dei dati OLE DB.|  
|Variabile nome vista o nome tabella|Consente di specificare il nome della vista o della tabella in una variabile.<br /><br /> **Informazioni correlate:** [Uso di variabili nei pacchetti](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Comando SQL|Consente di recuperare dati dall'origine dei dati OLE DB utilizzando una query SQL.|  
|Comando SQL da variabile|Consente di specificare il testo della query SQL in una variabile.|  
  
 **Anteprima**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Vista dati** . L'**anteprima** supporta la visualizzazione di un massimo di 200 righe.  
  
> [!NOTE]  
>  Quando vengono visualizzati i dati in anteprima, le colonne con tipo definito dall'utente CLR (UDT) non contengono dati. Contengono invece i valori \<value too big to display> o System.Byte[] display. Il primo viene visualizzato se si accede all'origine dati mediante il provider SQL OLE DB, il secondo se si usa il provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
### <a name="data-access-mode-dynamic-options"></a>Opzioni dinamiche relative alla modalità di accesso ai dati  
  
#### <a name="data-access-mode--table-or-view"></a>Modalità di accesso ai dati = Tabella o vista  
 **Nome tabella o vista**  
 Consente di selezionare il nome della tabella o della vista nell'elenco dei nomi disponibili nell'origine dei dati.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modalità di accesso ai dati = Variabile nome vista o nome tabella  
 **Nome variabile**  
 Consente di selezionare la variabile che contiene il nome della tabella o vista.  
  
#### <a name="data-access-mode--sql-command"></a>Modalità di accesso ai dati = Comando SQL  
 **Testo comando SQL**  
 Immettere il testo di una query SQL, fare clic su **Compila query**per compilare la query o fare clic su **Sfoglia**per individuare il file che contiene il testo della query.  
  
 **Parameters**  
 Se è stata immessa una query con parametri utilizzando ? come segnaposto per il parametro nel testo della query, usare la finestra di dialogo **Imposta parametri query** per eseguire il mapping tra i parametri di input della query e le variabili del pacchetto.  
  
 **Compila query**  
 Usare la finestra di dialogo **Generatore query** per creare la query SQL con strumenti grafici visuali.  
  
 **Sfoglia**  
 Usare la finestra di dialogo **Apri** per individuare il file contenente il testo della query SQL.  
  
 **Analizza query**  
 Consente di verificare la sintassi del testo della query.  
  
#### <a name="data-access-mode--sql-command-from-variable"></a>Modalità di accesso ai dati = Comando SQL da variabile  
 **Nome variabile**  
 Consente di selezionare la variabile contenente il testo della query SQL.  
  
## <a name="ole-db-source-editor-columns-page"></a>Editor origine OLE DB (pagina Colonne)
  Usare la pagina **Colonne** della finestra di dialogo **Editor origine OLE DB** per eseguire il mapping tra una colonna di output e ogni colonna esterna (di origine).  
  
### <a name="options"></a>Opzioni  
 **Colonne esterne disponibili**  
 Consente di visualizzare l'elenco delle colonne esterne disponibili nell'origine dei dati. Non è possibile utilizzare questa tabella per l'aggiunta o l'eliminazione di colonne.  
  
 **Colonna esterna**  
 Consente di visualizzare le colonne esterne (di origine) nell'ordine in cui verranno presentate durante la configurazione di componenti che utilizzano i dati dell'origine. È possibile modificare l'ordine deselezionando innanzitutto le colonne della tabella selezionate e quindi selezionando dall'elenco le colonne esterne in un ordine diverso.  
  
 **Colonna di output**  
 Consente di specificare un nome univoco per ogni colonna di output. Per impostazione predefinita viene suggerito il nome della colonna esterna (di origine) selezionata. È comunque possibile scegliere qualsiasi nome descrittivo univoco. Il nome specificato verrà visualizzato in Progettazione SSIS.  
  
## <a name="ole-db-source-editor-error-output-page"></a>Editor origine OLE DB (pagina Output degli errori)
  Usare la pagina **Output degli errori** della finestra di dialogo **Editor origine OLE DB** per selezionare le opzioni di gestione degli errori e impostare le proprietà delle colonne di output degli errori.  
  
### <a name="options"></a>Opzioni  
 **Input/Output**  
 Consente di visualizzare il nome dell'origine dei dati.  
  
 **Colonna**  
 Consente di visualizzare le colonne esterne (origine) selezionate nella pagina **Gestione connessione** della finestra di dialogo **Editor origine OLE DB**.  
  
 **Error (Errore) (Error (Errore)e)**  
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
 [Destinazione OLE DB](../../integration-services/data-flow/ole-db-destination.md)   
 [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)   
 [Flusso di dati](../../integration-services/data-flow/data-flow.md)  
  
  
