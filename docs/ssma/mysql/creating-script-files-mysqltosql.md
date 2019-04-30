---
title: Creazione di file di Script (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Creating script files, configuring console settings
- Creating script files, Script commands
- Creating script files, script file validation
- Creating script files, server connection parameters
ms.assetid: b4608fe7-c777-4ba5-b853-4402f02109e3
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: da5b708c4dbf80a1faa7fa74f237b1cc750ea975
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63132322"
---
# <a name="creating-script-files-mysqltosql"></a>Creazione di file di script (MySQLToSQL)
Il primo passaggio prima di avviare l'applicazione console SSMA consiste nel creare il file di script e, se è necessario creare il file di valore della variabile e il file di connessione del server.  
  
Il file di script può essere suddivisi in tre sezioni, una visualizzazione dei..,:  
  
1.  **config:** Consente all'utente di impostare i parametri di configurazione per l'applicazione console.  
  
2.  **Server:** Consente all'utente di impostare le definizioni del server di origine/destinazione. Può essere anche in un file di connessione server separato.  
  
3.  **script-commands:** Consente all'utente di eseguire i comandi del flusso di lavoro SSMA.  
  
Ogni sezione viene descritto in dettaglio di seguito:  
  
## <a name="configuring-mysql-console-settings"></a>Configurazione delle impostazioni di Console MySQL  
Le configurazioni di uno script vengono visualizzate nel file di script della console.  
  
Se viene specificato uno degli elementi nel nodo di configurazione, sono configurate come l'impostazione globale, ovvero sono applicabili per tutti i comandi di script. Questi elementi di configurazione anche possono essere impostati all'interno di ogni comando nella sezione del comando script se l'utente desidera eseguire l'override dell'impostazione globale.  
  
Le opzioni configurabili dall'utente includono:  
  
1.  **Provider di finestra di output:** Se-Elimina messaggi attributo è impostato su 'true', la specifica del comando messaggi non visualizzati nella console. Di seguito è riportata la descrizione degli attributi:  
  
    -   Destinazione: Specifica se l'output deve ottenere stampato in un file o stdout. Questo è false per impostazione predefinita.  
  
    -   nome del file: Il percorso del file (facoltativo).  
  
    -   eliminare-messages: Elimina i messaggi nella console. Ciò è 'false' per impostazione predefinita.  
  
    **Esempio:**  
  
    ```xml  
    <output-providers>  
  
      <output-window  
  
        suppress-messages="<true/false>"   (optional)  
  
        destination="<file/stdout>"        (optional)  
  
        file-name="<file-name>"            (optional)  
  
       />  
  
    </output-providers>  
    ```  
    *o Gestione configurazione*  
  
    ```xml  
    <...All commands...>  
  
      <output-window  
  
         suppress-messages="<true/false>"   (optional)  
  
         destination="<file/stdout>"        (optional)  
  
         file-name="<file-name>"            (optional)  
  
       />  
  
    </...All commands...>  
    ```  
  
2.  **Provider di connessione dati della migrazione:** Specifica che il server di origine/destinazione è da considerare per la migrazione dei dati.  Origine-usare-last-used indica che viene utilizzato l'ultimo server di origine usati per la migrazione dei dati. Allo stesso modo destinazione Usa-ultimo usato indica che viene utilizzato l'ultimo server di destinazione usata per la migrazione dei dati. L'utente può anche specificare il server (origine o destinazione) con il server di origine degli attributi o server di destinazione.  
  
    Solo uno o l'altro attributo specificato può essere utilizzato, ad esempio:  
  
    - origine utilizzare-ultimo usato = "true" (impostazione predefinita) o server di origine = "source_servername"  
  
    - target-use-last-used="true" (default) or target-server="target_servername"  
  
    **Esempio:**  
  
    ```xml  
    <output-providers>  
  
      <data-migration-connection  source-use-last-used="true"  
  
                                  target-server="<target-server-unique-name>"/>  
  
    </output-providers>  
    ```  
    *o Gestione configurazione*  
  
    ```xml  
    <migrate-data>  
  
      <data-migration-connection   source-server="<source-server-unique-name>"  
  
                                   target-use-last-used="true"/>  
  
    </migrate-data>  
    ```  
  
3.  **Popup di Input utente:** In questo modo la gestione degli errori, quando gli oggetti vengono caricati dal database. L'utente fornisce le modalità di input e in caso di errore, la console prosegue come se l'utente specifica.  
  
    Le modalità comprendono:  
  
    -   **chiedere-utente -** chiede all'utente continue('yes') o generato un errore ('no').  
  
    -   **errore -** la console viene visualizzato un errore e arresta l'esecuzione.  
  
    -   **continuare-** console procede con l'esecuzione.  
  
    La modalità predefinita è **errore**.  
  
    **Esempio:**  
  
    ```xml  
    <output-providers>  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </output-providers>  
    ```  
    *o Gestione configurazione*  
  
    ```xml  
    <!-- Connect to target database -->  
  
    <connect-target-database server="<target-server-unique-name>">  
  
      <user-input-popup mode="<ask-user/continue/error>"/>  
  
    </connect-target-database>  
    ```  
  
4.  **Ristabilire la connessione del Provider:** Ciò consente all'utente di impostare la riconnessione ignori le impostazioni degli errori di connessione. Può essere impostato per i server di origine e di destinazione.  
  
    Le modalità di riconnessione sono:  
  
    -   ristabilire la connessione-last-utilizzato-server: Se la connessione non è attiva, tenta di riconnettersi all'ultimo server utilizzato al massimo 5 volte.  
  
    -   generare un-errore: Se la connessione non è attiva, viene generato un errore.  
  
    La modalità predefinita è **generare un errore**.  
  
    **Esempio:**  
  
    ```xml  
    <output-providers>  
  
    <reconnect-manager  on-source-reconnect="<reconnect-to-last-used-server/generate-an-error>"  
  
                        on-target-reconnect="<reconnect-to-last-used-server/generate-an-error>"/>  
  
    </output-providers>  
    ```  
    *o Gestione configurazione*  
  
    ```xml  
    <!--synchronization-->  
  
    <synchronize-target>  
  
      <reconnect-manager on-target-reconnect="reconnect-to-last-used-server"/>  
  
    </synchronize-target>  
    ```  
    *o Gestione configurazione*  
  
    ```xml  
    <!--data migration-->  
  
    <migrate-data server="target-server-unique-name">  
  
      <reconnect-manager  
  
        on-source-reconnect="reconnect-to-last-used-server"  
  
        on-target-reconnect="generate-an-error"/>  
  
    </migrate-data>  
    ```  
  
5.  **Convertitore di sovrascrittura del Provider:** Ciò consente all'utente di gestire gli oggetti che sono già presenti nella destinazione della metabase. Le possibili azioni includono:  
  
    -   Errore: La console viene visualizzato un errore e arresta l'esecuzione.  
  
    -   sovrascrittura: Sovrascrive i valori di oggetto esistente. Questa azione viene eseguita per impostazione predefinita.  
  
    -   Skip: La console ignora gli oggetti che esistono già nel database  
  
    -   ask-user: Richiede l'input dell'utente ('Sì' / 'no')  
  
    **Esempio:**  
  
    ```xml  
    <output-providers>  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </output-providers>  
    ```  
    *o Gestione configurazione*  
  
    ```xml  
    <convert-schema object-name="<object-name>">  
  
      <object-overwrite action="<error/skip/overwrite/ask-user>"/>  
  
    </convert-schema>  
    ```  
  
6.  **Provider di prerequisiti con errori:** Ciò consente all'utente di gestire tutti i prerequisiti necessari per l'elaborazione di un comando. Per impostazione predefinita, la modalità strict è 'false'. Se è impostata su 'true', eccezione generato per la mancata soddisfino i prerequisiti.  
  
    **Esempio:**  
  
    ```xml  
    <output-providers>  
  
      <prerequisites strict-mode="<true/false>"/>  
  
    </output-providers>  
    ```  
  
7.  **Arrestare l'operazione:** Durante l'operazione a metà, se l'utente desidera arrestare l'operazione, quindi **'Ctrl + C'** tasti di scelta rapida può essere utilizzato. SSMA per la MySQL Console attenderà il completamento dell'operazione e termina l'esecuzione della console.  
  
    Se l'utente desidera arrestare l'esecuzione immediatamente, quindi **'Ctrl + C'** tasti di scelta rapida è possibile premere nuovamente per la chiusura improvvisa di applicazione Console SSMA  
  
8.  **Provider di stato di avanzamento:** Indica lo stato di avanzamento di ogni comando della console. Questo è disabilitato per impostazione predefinita. Gli attributi di report di stato includono quanto segue:  
  
    -   off  
  
    -   ogni 1%  
  
    -   ogni 2%  
  
    -   ogni 5%  
  
    -   ogni 10%  
  
    -   ogni 20%  
  
    **Esempio:**  
  
    ```xml  
    <output-providers>  
  
      <progress-reporting enable="<true/false>"          (optional)  
  
                         report-messages="<true/false>"  (optional)  
  
                         report-progress="<every-1%/every-2%/every-5%/every-10%/every-20%/off>" (optional)/>  
  
    </output-providers>  
    ```  
    *o Gestione configurazione*  
  
    ```xml  
    <...All commands...>  
  
      <progress-reporting  
  
        enable="<true/false>"              (optional)  
  
        report-messages="<true/false>"     (optional)  
  
        report-progress="<every-1%/every-2%/every-5%/every-10%/every-20%/off>"     (optional)/>  
  
    </...All commands...>  
    ```  
  
9. **Livello di dettaglio del logger:** Set di log a livello di dettaglio. Questo corrisponde all'opzione di tutte le categorie nell'interfaccia utente. Per impostazione predefinita, il livello di dettaglio del log è "error".  
  
    Le opzioni a livello di logger includono:  
  
    -   Errore irreversibile: Vengono registrati solo i messaggi di errore irreversibile.  
  
    -   Errore: Vengono registrati solo i messaggi di errore ed errore irreversibile.  
  
    -   Avviso: Tutti i livelli ad eccezione dei messaggi di debug e le informazioni vengono registrati.  
  
    -   Info: Tutti i livelli ad eccezione del fatto che vengono registrati i messaggi di debug.  
  
    -   debug: Tutti i livelli di messaggi registrati.  
  
    > [!NOTE]  
    > Obbligatori vengono registrati a qualsiasi livello.  
  
    **Esempio:**  
  
    ```xml  
    <output-providers>  
  
      <log-verbosity level="<fatal-error/error/warning/info/debug>"/>  
  
    </output-providers>  
    ```  
    *o Gestione configurazione*  
  
    ```xml  
    <...All commands...>  
  
      <log-verbosity level="<fatal-error/error/warning/info/debug>"/>  
  
    </...All commands...>  
    ```  
  
10. **Eseguire l'override Password crittografate:** Se 'true', la password come testo non crittografato specificato nella sezione Definizione server dei file di connessione del server o nel file di script, gli override la password crittografata archiviata nell'archivio protetto, se presente. Se non viene specificata alcuna password in testo non crittografato, l'utente viene richiesto di immettere la password.  
  
    Qui si verificano due casi:  
  
    1.  Se ignorare l'opzione viene **false**, l'ordine della ricerca sarà protetto archiviazione -&gt;Script di File -&gt;File Server di connessione -&gt; Chiedi conferma all'utente.  
  
    2.  Se l'opzione di override è **true**, l'ordine della ricerca sarà File di Script -&gt;File Server di connessione -&gt;Chiedi conferma all'utente.  
  
    **Esempio:**  
  
    ```xml  
    <output-providers>  
  
      <encrypted-password override="<true/false>"/>  
  
    </output-providers>  
    ```  
  
L'opzione non configurabile è:  
  
-   **Numero massimo di tentativi di riconnessione:** Quando una connessione stabilita scade o viene interrotta a causa di errori di rete, il server è necessario la riconnessione. I tentativi di riconnessione sono consentiti al massimo **5** tentativi dopo questa operazione, la console esegue automaticamente la riconnessione. La funzionalità di riconnessione automatica riduce l'impegno nell'eseguire nuovamente lo script.  
  
## <a name="server-connection-parameters"></a>Parametri di connessione server  
Parametri di connessione server possono essere definiti nel file di script o nel file di connessione del server. Consultare il [creazione di file di connessione del Server &#40;MySQLToSQL&#41; ](../../ssma/mysql/creating-the-server-connection-files-mysqltosql.md) sezione per altri dettagli.  
  
## <a name="script-commands"></a>Comandi script  
Il file script contiene una sequenza di comandi del flusso di lavoro migrazione in formato XML. L'applicazione console SSMA elabora la migrazione nell'ordine i comandi visualizzati nel file di script.  
  
Ad esempio, una migrazione tipica dei dati di una tabella specifica in un database MySQL segue la gerarchia di: Database -&gt; tabella.  
  
Quando tutti i comandi nel file di script vengono eseguiti correttamente, l'applicazione console SSMA viene chiusa e restituisce il controllo all'utente. Il contenuto di un file script è più o meno statico con informazioni sulle variabili contenute in un [file con valori di variabile](creating-variable-value-files-mysqltosql.md) o, in una sezione separata all'interno del file di script per i valori delle variabili.  
  
**Esempio:**  
  
```xml  
<!--Sample of script file commands -->  
  
<ssma-script-file>  
  
  <script-commands>  
  
    <create-new-project project-folder="<project-folder>"  
  
                        project-name="<project-name>"  
  
                        overwrite-if-exists="<true/false>"/>  
  
    <connect-source-database server="<source-server-unique-name>"/>  
  
    <save-project/>  
  
    <close-project/>  
  
  </script-commands>  
  
</ssma-script-file>  
```  
Modelli costituito da 3 file script (per l'esecuzione di diversi scenari di), file di valore della variabile e un file di connessione del server sono disponibili nella cartella Scripts Console di esempio di directory del prodotto:  
  
-   AssessmentReportGenerationSample.xml  
  
-   ConversionAndDataMigrationSample.xml  
  
-   SqlStatementConversionSample.xml  
  
-   VariableValueFileSample.xml  
  
-   ServersConnectionFileSample.xml  
  
È possibile eseguire i modelli (file) dopo la modifica dei parametri visualizzati al suo interno per pertinenza.  
  
Elenco completo dei comandi di script è reperibile nel [esecuzione della Console SSMA &#40;MySQLToSQL&#41;](../../ssma/mysql/executing-the-ssma-console-mysqltosql.md)  
  
## <a name="script-file-validation"></a>Convalida del File script  
L'utente può facilmente convalidare il file di script in base al file di definizione dello schema **'M2SSConsoleScriptSchema.xsd'** disponibile nella cartella "Schemi".  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo in costi operativi console consiste [creazione di file di valore variabile &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md).  
  
## <a name="see-also"></a>Vedere anche  
[Creazione di file di valore della variabile &#40;MySQLToSQL&#41;](../../ssma/mysql/creating-variable-value-files-mysqltosql.md)  
  
