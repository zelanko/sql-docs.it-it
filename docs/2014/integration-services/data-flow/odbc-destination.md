---
title: Destinazione ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcdest.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9de91ba98533e82fbf63376ed6d9c56ad73a000c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62771027"
---
# <a name="odbc-destination"></a>Destinazione ODBC
  Tramite la destinazione ODBC viene eseguito il caricamento bulk di dati in tabelle di database supportate da ODBC. La destinazione ODBC utilizza una gestione connessione ODBC per la connessione all'origine dati.  
  
 Una destinazione ODBC include i mapping tra le colonne di input e le colonne presenti nell'origine dati di destinazione. Non è necessario eseguire il mapping delle colonne di input a tutte le colonne di destinazione ma, a seconda delle proprietà delle colonne di destinazione, possono verificarsi errori se non viene eseguito il mapping di alcuna colonna di input alle colonne di destinazione. Se, ad esempio, una colonna di destinazione non ammette valori Null, sarà necessario eseguire il mapping di una colonna di input a tale colonna. È inoltre possibile eseguire il mapping di colonne di tipi diversi, ma se i dati di input non sono compatibili per il tipo di colonna di destinazione, si verifica un errore in fase di esecuzione. A seconda dell'impostazione del comportamento in seguito all'errore, l'errore viene ignorato, provoca un problema o la riga viene inviata all'output degli errori.  
  
 La destinazione ODBC include un output regolare e un output degli errori.  
  
##  <a name="BKMK_odbcdestination_loadoptions"></a> Opzioni di caricamento  
 La destinazione ODBC può utilizzare uno tra due moduli di caricamento di accesso. Impostare la modalità in [Editor origine ODBC &#40;pagina Gestione connessione #41;](../odbc-source-editor-connection-manager-page.md). Le due modalità sono:  
  
-   **Batch**: in questa modalità il componente tenta di usare il metodo di inserimento più efficiente in base alle funzionalità del provider ODBC rilevate. Per la maggior parte degli attuali provider ODBC, ciò significa preparare un'istruzione INSERT con parametri e quindi usare un'associazione di parametri di matrice a livello di riga, in cui le dimensioni della matrice sono determinate dalla proprietà **BatchSize** . Se si seleziona **Batch** e il provider non supporta questo metodo, la destinazione ODBC passa automaticamente alla modalità **Riga per riga** .  
  
-   **Riga per riga**: in questa modalità, tramite la destinazione ODBC viene preparata un'istruzione INSERT con parametri e viene usato **SQL Execute** per inserire le righe una per volta.  
  
## <a name="error-handling"></a>Gestione degli errori  
 La destinazione ODBC include un output degli errori. L'output degli errori del componente include le colonne di output seguenti:  
  
-   **Error Code**: numero che corrisponde all'errore corrente. Per un elenco degli errori, vedere la documentazione per il database di origine. Per un elenco dei codici di errore SSIS, vedere la Guida di riferimento ai messaggi e ai codici di errore SSIS.  
  
-   **Error Column**(Colonna errore): colonna di origine che provoca l'errore (per gli errori di conversione).  
  
-   Colonne dei dati di output standard.  
  
 A seconda dell'impostazione del comportamento in seguito all'errore, la destinazione ODBC supporta la restituzione degli errori (conversione dei dati, troncamento) che si verificano durante il processo di estrazione nell'output degli errori. Per altre informazioni, vedere [Editor origine ODBC &#40;pagina Output degli errori&#41;](../odbc-source-editor-error-output-page.md).  
  
## <a name="parallelism"></a>Parallelismo  
 Non sussiste alcuna limitazione al numero di componenti della destinazione ODBC che possono essere eseguiti in parallelo rispetto alla stessa tabella o a tabelle diverse, nello stesso computer o in computer diversi, ad eccezione dei normali limiti di sessione globali.  
  
 Alcune limitazioni del provider ODBC utilizzato possono tuttavia ridurre il numero di connessioni simultanee tramite il provider. Queste limitazioni riducono il numero di possibili istanze parallele supportate per la destinazione ODBC. Lo sviluppatore di SSIS deve essere a conoscenza delle limitazioni di qualsiasi provider ODBC utilizzato e tenerne conto in caso di compilazione di pacchetti SSIS.  
  
 È necessario tenere anche presente che il caricamento simultaneo nella stessa tabella può ridurre le prestazioni a causa del blocco del record standard. Ciò dipende dai dati caricati e dall'organizzazione della tabella.  
  
## <a name="troubleshooting-the-odbc-destination"></a>Risoluzione dei problemi relativi alla destinazione ODBC  
 È possibile registrare le chiamate eseguite dall'origine ODBC a provider di dati esterni. Questa nuova funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi al salvataggio di dati in origini dati esterne eseguito dalla destinazione ODBC. Per registrare le chiamate eseguite dalla destinazione ODBC a provider di dati esterni, abilitare la traccia di Gestione driver ODBC. Per altre informazioni, vedere la documentazione di Microsoft *Come generare un'analisi ODBC con l'amministratore origine dati ODBC*.  
  
## <a name="configuring-the-odbc-destination"></a>Configurazione della destinazione ODBC  
 È possibile configurare la destinazione ODBC a livello di codice o tramite Progettazione SSIS.  
  
 Per ulteriori informazioni, vedere uno degli argomenti seguenti:  
  
-   [Editor destinazione ODBC &#40;pagina Gestione connessione&#41;](../odbc-destination-editor-connection-manager-page.md)  
  
-   [ODBC Destination Editor &#40;pagina Mapping&#41;](../odbc-destination-editor-mappings-page.md)  
  
-   [Editor destinazione ODBC &#40;pagina Output degli errori&#41;](../odbc-destination-editor-error-output-page.md)  
  
 La finestra di dialogo **Editor avanzato** contiene le proprietà che è possibile impostare a livello di codice.  
  
 Per aprire la finestra di dialogo **Editor avanzato** :  
  
-   Nella schermata **Flusso di dati** del progetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] fare clic con il pulsante destro del mouse sulla destinazione ODBC e scegliere **Visualizza editor avanzato**.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo Editor avanzato, vedere [Proprietà personalizzate della destinazione ODBC](odbc-destination-custom-properties.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Editor destinazione ODBC &#40;pagina Output degli errori&#41;](../odbc-destination-editor-error-output-page.md)  
  
-   [ODBC Destination Editor &#40;pagina Mapping&#41;](../odbc-destination-editor-mappings-page.md)  
  
-   [Editor destinazione ODBC &#40;pagina Gestione connessione&#41;](../odbc-destination-editor-connection-manager-page.md)  
  
-   [Caricare dati tramite la destinazione ODBC](odbc-destination.md)  
  
-   [Proprietà personalizzate della destinazione ODBC](odbc-destination-custom-properties.md)  
  
  
