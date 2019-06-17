---
title: Origine ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d125a725a9e1c0cab34c7066fd9554ef0099d6e6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62901106"
---
# <a name="odbc-source"></a>Origine ODBC
  Tramite l'origine ODBC vengono estratti dati da un database supportato da ODBC mediante una tabella di database, una vista o un'istruzione SQL.  
  
 Per l'origine ODBC sono disponibili le modalità di accesso ai dati seguenti per l'estrazione dei dati:  
  
-   Vista o tabella.  
  
-   Risultato di un'istruzione SQL.  
  
 L'origine utilizza una gestione connessione ODBC che specifica il provider da utilizzare.  
  
 Un'origine ODBC include le colonne di output dei dati di origine. Durante il mapping delle colonne di output nella destinazione ODBC alle colonne di destinazione, possono verificarsi errori se non viene eseguito il mapping di alcuna colonna di output alle colonne di destinazione. È possibile eseguire il mapping di colonne di tipi diversi, ma se i dati di output non sono compatibili per la destinazione, si verifica un errore in fase di esecuzione. A seconda del comportamento in seguito all'errore, l'impostazione dell'errore verrà ignorata, provocherà un problema o la riga verrà inviata all'output degli errori.  
  
 L'origine ODBC include un output regolare e un output degli errori.  
  
## <a name="error-handling"></a>Gestione degli errori  
 L'origine ODBC include un output degli errori. L'output degli errori del componente include le colonne di output seguenti:  
  
-   **Error Code** (Codice errore): numero che corrisponde all'errore corrente. Per un elenco degli errori, vedere la documentazione per il database supportato da ODBC in uso. Per un elenco dei codici di errore SSIS, vedere la Guida di riferimento ai messaggi e ai codici di errore SSIS.  
  
-   **Error Column**(Colonna errore): colonna di origine che causa l'errore (per gli errori di conversione).  
  
-   Colonne dei dati di output standard.  
  
 A seconda dell'impostazione del comportamento in seguito all'errore, l'origine ODBC supporta la restituzione degli errori (conversione dei dati, troncamento) che si verificano durante il processo di estrazione nell'output degli errori. Per altre informazioni, vedere [Editor destinazione ODBC &#40;pagina Gestione connessione&#41;](../odbc-destination-editor-connection-manager-page.md).  
  
## <a name="data-type-support"></a>Supporto dei tipi di dati  
 Per informazioni sui tipi di dati supportati dall'origine ODBC, vedere Connettore per ODBC (Open Database Connectivity) di Attunity.  
  
## <a name="extract-options"></a>Opzioni di estrazione  
 L'origine ODBC usa la modalità **Batch** o **Row-by-Row** . La modalità utilizzata è determinata dalla proprietà **FetchMethod** . Nell'elenco seguente vengono descritte le diverse modalità.  
  
-   **Batch**: il componente tenta di usare il metodo di recupero più efficiente in base alle funzionalità del provider ODBC rilevate. Per la maggior parte degli attuali provider ODBC, tale metodo è SQLFetchScroll con associazione di matrici (in cui le dimensioni delle matrici sono determinate dalla proprietà **BatchSize** ). Se si seleziona **Batch** e il provider non supporta questo metodo, la destinazione ODBC passa automaticamente alla modalità **Riga per riga** .  
  
-   **Row-by Row** (Riga per riga): il componente usa SQLFetch per recuperare le righe una per volta.  
  
 Per altre informazioni sulla proprietà **FetchMethod** , vedere [Proprietà personalizzate dell'origine ODBC](odbc-source-custom-properties.md).  
  
## <a name="parallelism"></a>Parallelism  
 Non sussiste alcuna limitazione al numero di componenti dell'origine ODBC che possono essere eseguiti in parallelo rispetto alla stessa tabella o a tabelle diverse, nello stesso computer o in computer diversi, ad eccezione dei normali limiti di sessione globali.  
  
 Alcune limitazioni del provider ODBC utilizzato possono tuttavia ridurre il numero di connessioni simultanee tramite il provider. Queste limitazioni riducono il numero di possibili istanze parallele supportate per l'origine ODBC. Lo sviluppatore di SSIS deve essere a conoscenza delle limitazioni di qualsiasi provider ODBC utilizzato e tenerne conto in caso di compilazione di pacchetti SSIS.  
  
## <a name="troubleshooting-the-odbc-source"></a>Risoluzione dei problemi relativi all'origine ODBC  
 È possibile registrare le chiamate eseguite dall'origine ODBC a provider di dati esterni. Questa funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi al caricamento di dati da origini dati esterne eseguito dall'origine ODBC. Per registrare le chiamate eseguite dall'origine ODBC a provider di dati esterni, abilitare la traccia di Gestione driver ODBC. Per altre informazioni, vedere la documentazione di Microsoft su *come generare una traccia ODBC con l'amministratore dell'origine dati ODBC*.  
  
## <a name="configuring-the-odbc-source"></a>Configurazione dell'origine ODBC  
 È possibile configurare l'origine ODBC a livello di codice o tramite Progettazione SSIS.  
  
 Per ulteriori informazioni, vedere uno degli argomenti seguenti:  
  
-   [Editor origine ODBC &#40;pagina Gestione connessione&#41;](../odbc-source-editor-connection-manager-page.md)  
  
-   [Editor origine ODBC &#40;pagina Colonne&#41;](../odbc-source-editor-columns-page.md)  
  
-   [Editor origine ODBC &#40;pagina Output degli errori&#41;](../odbc-source-editor-error-output-page.md)  
  
 La finestra di dialogo **Editor avanzato** contiene le proprietà che è possibile impostare a livello di codice.  
  
 Per aprire la finestra di dialogo **Editor avanzato** :  
  
-   Nella schermata **Flusso di dati** del progetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] fare clic con il pulsante destro del mouse sull'origine ODBC e scegliere **Visualizza editor avanzato**.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo Editor avanzato, vedere [Proprietà personalizzate dell'origine ODBC](odbc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Editor origine ODBC &#40;pagina Output degli errori&#41;](../odbc-source-editor-error-output-page.md)  
  
-   [Editor origine ODBC &#40;pagina Colonne&#41;](../odbc-source-editor-columns-page.md)  
  
-   [Editor origine ODBC &#40;pagina Gestione connessione&#41;](../odbc-source-editor-connection-manager-page.md)  
  
-   [Estrarre dati tramite l'origine ODBC](odbc-source.md)  
  
-   [Proprietà personalizzate dell'origine ODBC](odbc-source-custom-properties.md)  
  
  
