---
title: Destinazione ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.odbcdest.f1
- sql13.ssis.designer.odbcdest.connection.f1
- sql13.ssis.designer.odbcdest.columns.f1
- sql13.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2914cdec402cee3be7ba92d74e0c8ff7db8fd41e
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726627"
---
# <a name="odbc-destination"></a>Destinazione ODBC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Tramite la destinazione ODBC viene eseguito il caricamento bulk di dati in tabelle di database supportate da ODBC. La destinazione ODBC utilizza una gestione connessione ODBC per la connessione all'origine dati.  
  
 Una destinazione ODBC include i mapping tra le colonne di input e le colonne presenti nell'origine dati di destinazione. Non è necessario eseguire il mapping delle colonne di input a tutte le colonne di destinazione ma, a seconda delle proprietà delle colonne di destinazione, possono verificarsi errori se non viene eseguito il mapping di alcuna colonna di input alle colonne di destinazione. Se, ad esempio, una colonna di destinazione non ammette valori Null, sarà necessario eseguire il mapping di una colonna di input a tale colonna. È inoltre possibile eseguire il mapping di colonne di tipi diversi, ma se i dati di input non sono compatibili per il tipo di colonna di destinazione, si verifica un errore in fase di esecuzione. A seconda dell'impostazione del comportamento in seguito all'errore, l'errore viene ignorato, provoca un problema o la riga viene inviata all'output degli errori.  
  
 La destinazione ODBC include un output regolare e un output degli errori.  
  
##  <a name="BKMK_odbcdestination_loadoptions"></a> Opzioni di caricamento  
 La destinazione ODBC può utilizzare uno tra due moduli di caricamento di accesso. Impostare la modalità in [Editor origine ODBC &#40;pagina Gestione connessione #41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md). Le due modalità sono:  
  
-   **Batch**: in questa modalità la destinazione ODBC tenta di usare il metodo di inserimento più efficiente in base alle funzionalità del provider ODBC rilevate. Per la maggior parte degli attuali provider ODBC, ciò significa preparare un'istruzione INSERT con parametri e quindi usare un'associazione di parametri di matrice a livello di riga, in cui le dimensioni della matrice sono determinate dalla proprietà **BatchSize** . Se si seleziona **Batch** e il provider non supporta questo metodo, la destinazione ODBC passa automaticamente alla modalità **Riga per riga** .  
  
-   **Riga per riga**: in questa modalità, la destinazione ODBC prepara un'istruzione INSERT con parametri e usa **SQL Execute** per inserire le righe una per volta.  
  
## <a name="error-handling"></a>Gestione degli errori  
 La destinazione ODBC include un output degli errori. L'output degli errori del componente include le colonne di output seguenti:  
  
-   **Error Code** (Codice errore): numero che corrisponde all'errore corrente. Per un elenco degli errori, vedere la documentazione per il database di origine. Per un elenco dei codici di errore SSIS, vedere la Guida di riferimento ai messaggi e ai codici di errore SSIS.  
  
-   **Error Column**(Colonna errore): colonna di origine che causa l'errore (per gli errori di conversione).  
  
-   Colonne dei dati di output standard.  
  
 A seconda dell'impostazione del comportamento in seguito all'errore, la destinazione ODBC supporta la restituzione degli errori (conversione dei dati, troncamento) che si verificano durante il processo di estrazione nell'output degli errori. Per altre informazioni, vedere [Editor origine ODBC &#40;pagina Output degli errori&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md).  
  
## <a name="parallelism"></a>Parallelismo  
 Non sussiste alcuna limitazione al numero di componenti della destinazione ODBC che possono essere eseguiti in parallelo rispetto alla stessa tabella o a tabelle diverse, nello stesso computer o in computer diversi, ad eccezione dei normali limiti di sessione globali.  
  
 Alcune limitazioni del provider ODBC utilizzato possono tuttavia ridurre il numero di connessioni simultanee tramite il provider. Queste limitazioni riducono il numero di possibili istanze parallele supportate per la destinazione ODBC. Lo sviluppatore di SSIS deve essere a conoscenza delle limitazioni di qualsiasi provider ODBC utilizzato e tenerne conto in caso di compilazione di pacchetti SSIS.  
  
 È necessario tenere anche presente che il caricamento simultaneo nella stessa tabella può ridurre le prestazioni a causa del blocco del record standard. Ciò dipende dai dati caricati e dall'organizzazione della tabella.  
  
## <a name="troubleshooting-the-odbc-destination"></a>Risoluzione dei problemi relativi alla destinazione ODBC  
 È possibile registrare le chiamate eseguite dall'origine ODBC a provider di dati esterni. Questa nuova funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi al salvataggio di dati in origini dati esterne eseguito dalla destinazione ODBC. Per registrare le chiamate eseguite dalla destinazione ODBC a provider di dati esterni, abilitare la traccia di Gestione driver ODBC. Per altre informazioni, vedere la documentazione di Microsoft *Come generare un'analisi ODBC con l'amministratore origine dati ODBC*.  
  
## <a name="configuring-the-odbc-destination"></a>Configurazione della destinazione ODBC  
 È possibile configurare la destinazione ODBC a livello di codice o tramite Progettazione SSIS.  
  
 Per ulteriori informazioni, vedere uno degli argomenti seguenti:  
  
-   [Editor destinazione ODBC &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)  
  
-   [ODBC Destination Editor &#40;pagina Mapping&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
-   [Editor destinazione ODBC &#40;pagina Output degli errori&#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
 La finestra di dialogo **Editor avanzato** contiene le proprietà che è possibile impostare a livello di codice.  
  
 Per aprire la finestra di dialogo **Editor avanzato** :  
  
-   Nella schermata **Flusso di dati** del progetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] fare clic con il pulsante destro del mouse sulla destinazione ODBC e scegliere **Visualizza editor avanzato**.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo Editor avanzato, vedere [Proprietà personalizzate della destinazione ODBC](../../integration-services/data-flow/odbc-destination-custom-properties.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Caricare dati tramite la destinazione ODBC](../../integration-services/data-flow/load-data-by-using-the-odbc-destination.md)  
  
-   [Proprietà personalizzate della destinazione ODBC](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
## <a name="odbc-destination-editor-connection-manager-page"></a>Editor destinazione ODBC (pagina Gestione connessione)
  Utilizzare la pagina **Gestione connessione** della finestra di dialogo **ODBC Destination Editor** per selezionare la gestione connessione ODBC per la destinazione. Tramite questa pagina è inoltre possibile selezionare una tabella o una vista del database  
  
 **Per aprire ODBC Destination Editor (pagina Gestione connessione)**  
  
### <a name="task-list"></a>Elenco attività  
  
-   In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], aprire il pacchetto [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] con la destinazione ODBC.  
  
-   Nella scheda **Flusso di dati** fare doppio clic sulla destinazione ODBC.  
  
-   In **ODBC Destination Editor**, fare clic su **Gestione connessione**.  
  
### <a name="options"></a>Opzioni  
  
#### <a name="connection-manager"></a>Gestione connessione  
 Consente di selezionare una gestione connessione ODBC esistente nell'elenco o di creare una nuova connessione facendo clic su Nuova. La connessione può essere a qualsiasi database supportato da ODBC.  
  
#### <a name="new"></a>Nuovo  
 Fare clic su **Nuovo**. Viene visualizzata la finestra di dialogo **Configura gestione connessione ODBC** in cui è possibile creare una nuova gestione connessione.  
  
#### <a name="data-access-mode"></a>Modalità di accesso ai dati  
 Consente di selezionare il metodo di caricamento dei dati nella destinazione. Le opzioni disponibili vengono visualizzate nella tabella seguente.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Nome tabella - Batch|Selezionare questa opzione per configurare la destinazione ODBC per l'utilizzo della modalità batch. Se si seleziona questa opzione, sono disponibili le opzioni seguenti.|  
||**Nome tabella o vista**: selezionare una tabella o vista disponibile nell'elenco.<br /><br /> Questo elenco contiene solo le prime 1000 tabelle. Se il database contiene più di 1000 tabelle, è possibile digitare l'inizio di un nome di tabella o usare il carattere jolly (\*) per immettere qualsiasi parte del nome e visualizzare la tabella o le tabelle che si vuole usare.<br /><br /> **Dimensioni batch**: tipo di dimensioni del batch per il caricamento bulk. Si tratta del numero di righe caricato come un batch|  
|Nome tabella - Riga per riga|Selezionare questa opzione per configurare la destinazione ODBC per l'inserimento di una riga per volta nella tabella di destinazione. Se si seleziona questa opzione, è disponibile l'opzione seguente.|  
||**Nome tabella o vista**: selezionare una tabella o vista disponibile dal database nell'elenco.<br /><br /> Questo elenco contiene solo le prime 1000 tabelle. Se il database contiene più di 1000 tabelle, è possibile digitare l'inizio di un nome di tabella o utilizzare il carattere jolly (*) per immettere qualsiasi parte del nome e visualizzare la tabella o le tabelle che si desidera utilizzare.|  
  
#### <a name="preview"></a>Anteprima  
 Fare clic su **Anteprima** per visualizzare fino a 200 dati per la tabella selezionata.  
  
## <a name="odbc-destination-editor-mappings-page"></a>ODBC Destination Editor (pagina Mapping)
  Utilizzare la pagina **Mapping** della finestra di dialogo **ODBC Destination Editor** per eseguire il mapping tra colonne di input e colonne di destinazione.  
  
### <a name="options"></a>Opzioni  
  
#### <a name="available-input-columns"></a>Colonne di input disponibili  
 Elenco delle colonne di input disponibili. Trascinare un colonna di input in una colonna di destinazione disponibile per eseguire il mapping tra le colonne.  
  
#### <a name="available-destination-columns"></a>Colonne di destinazione disponibili  
 Elenco delle colonne di destinazione disponibili. Trascinare un colonna di destinazione in una colonna di input disponibile per eseguire il mapping tra le colonne.  
  
#### <a name="input-column"></a>Colonna di input  
 Consente di visualizzare le colonne di input selezionate dall'utente. È possibile rimuovere i mapping selezionando **\<ignora>** per escludere colonne dall'output.  
  
#### <a name="destination-column"></a>Colonna di destinazione  
 Consente di visualizzare tutte le colonne di destinazione disponibili, con o senza mapping eseguito.  
  
## <a name="odbc-destination-editor-error-output-page"></a>Editor destinazione ODBC (pagina Output errori)
  Utilizzare la pagina **Output degli errori** della finestra di dialogo **ODBC Destination Editor** per selezionare le opzioni di gestione degli errori.  
  
 **Per aprire ODBC Destination Editor (pagina Output degli errori)**  
  
### <a name="task-list"></a>Elenco attività  
  
-   In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], aprire il pacchetto [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] con la destinazione ODBC.  
  
-   Nella scheda **Flusso di dati** fare doppio clic sulla destinazione ODBC.  
  
-   In **ODBC Destination Editor**, fare clic su **Output degli errori**.  
  
### <a name="options"></a>Opzioni  
  
#### <a name="inputoutput"></a>Input/Output  
 Consente di visualizzare il nome dell'origine dei dati.  
  
#### <a name="column"></a>colonna  
 Non usato.  
  
#### <a name="error"></a>Errore  
 Consente di selezionare il modo in cui la destinazione ODBC deve gestire gli errori in un flusso: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
#### <a name="truncation"></a>Troncamento  
 Consente di selezionare il modo in cui la destinazione ODBC deve gestire il troncamento in un flusso: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
#### <a name="description"></a>Descrizione  
 Consente di visualizzare una descrizione dell'errore.  
  
#### <a name="set-this-value-to-selected-cells"></a>Imposta questo valore nelle celle selezionate  
 Consente di selezionare il modo in cui la destinazione ODBC gestisce tutte le celle selezionate in caso di errore o troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
#### <a name="apply"></a>Applica  
 Consente di applicare le opzioni di gestione degli errori alle celle selezionate.  
  
### <a name="error-handling-options"></a>Opzioni di gestione degli errori  
 Utilizzare le opzioni seguenti per configurare il modo in cui la destinazione ODBC gestisce errori e troncamenti.  
  
#### <a name="fail-component"></a>Interrompi componente  
 Quando si verifica un errore o un troncamento l'attività Flusso di dati viene interrotta. Questo è il comportamento predefinito.  
  
#### <a name="ignore-failure"></a>Ignora errore  
 L'errore o il troncamento vengono ignorati.  
  
#### <a name="redirect-flow"></a>Reindirizza flusso  
 La riga che determina l'errore o il troncamento viene inviata all'output degli errori della destinazione ODBC. Per ulteriori informazioni, vedere Destinazione ODBC.  
  
