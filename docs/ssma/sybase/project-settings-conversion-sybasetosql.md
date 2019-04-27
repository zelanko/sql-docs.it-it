---
title: Impostazioni (conversione) (SybaseToSQL) del progetto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 4d7f290459e1da736605acad941602399ec3ea53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62664663"
---
# <a name="project-settings-conversion-sybasetosql"></a>Impostazioni del progetto (conversione) (SybaseToSQL)
La pagina di conversione del **impostazioni del progetto** finestra di dialogo contiene impostazioni che consentono di personalizzare la modalità SSMA Converte la sintassi di Sybase Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la sintassi SQL Azure.  
  
Nel riquadro di conversione è disponibile nel **impostazioni del progetto** e **impostazioni di progetto predefinite** finestre di dialogo:  
  
-   Se si desidera specificare le impostazioni per tutti i progetti SSMA, il **strumenti** dal menu **impostazioni di progetto predefinite**, fare clic su **generali** nella parte inferiore del riquadro a sinistra e quindi fare clic su **Conversione**.  
  
-   Per specificare le impostazioni per il progetto corrente, il **strumenti** dal menu **le impostazioni del progetto**, fare clic su **generale** nella parte inferiore del riquadro di sinistra e quindi fare clic su **Conversione**.  
  
## <a name="miscellaneous-options"></a>Opzioni varie  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure e ambiente del servizio App Usa i codici di errore diversi.  
  
Usare questa impostazione per specificare il tipo di messaggio (avviso o errore) indicante SSMA nel riquadro di Output o un elenco di errore quando rileva un riferimento a **@@ERROR**  nel codice di ambiente del servizio app.  
  
-   Se si seleziona **convertire e contrassegnare con avviso**, SSMA convertirà le istruzioni e contrassegnarli con commenti di avviso.  
  
-   Se si seleziona **contrassegnare con l'errore**, SSMA. Always ignorerà la conversione e contrassegnare le istruzioni con commenti di errore.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Convertire e contrassegnare con avviso  
  
**Modalità completa:** Contrassegno con l'errore  
  
**Conversione dell'operatore LIKE**  
Specifica se convertire, ad esempio gli operandi in modo che corrisponda il comportamento di Sybase ASE. Il punto è che Sybase Taglia gli spazi vuoti finali in un modello like. La soluzione alternativa consiste nel rendere un cast dell'espressione a destra di un tipo di dati di lunghezza fissa con una precisione massima.  
  
-   Selezionare **conversione semplice** per convertire le espressioni senza alcuna correzione.  
  
-   Usare l'istruzione select comportamento ASE **eseguire il Cast a lunghezza fissa.**  
  
Quando si seleziona una modalità di conversione nella finestra di modalità, SSMA si applica l'impostazione seguente:  
  
**La modalità predefinita/ottimistico**: Conversione semplice  
  
**Modalità intero**: Eseguire il cast a lunghezza fissa  
  
**CONVERTIRE O ESEGUIRE IL CAST DI STRINGHE VUOTE PER I TIPI NUMERICI**  
Specifica come gestire le stringhe vuote o null all'interno di espressioni di CONVERT o CAST con un tipo numerico come argomento di tipo di dati. Le opzioni seguenti sono disponibili per questa impostazione:  
  
-   Selezionare **conversione semplice** per convertire le espressioni senza alcuna correzione.  
  
-   Se **stringa vuota come zero numerico** è selezionata, il parametro di stringa {s} verrà sostituito con maiuscole ltrim(rtrim({s})) quando "" quindi 0 else {s} espressione finale  
  
Quando si seleziona una modalità di conversione nella finestra di modalità, SSMA si applica l'impostazione seguente:  
  
**La modalità predefinita/ottimistico**: Conversione semplice  
  
**Modalità intero**: Stringa vuota come zero numerico  
  
**Concatenazione Null**  
Questa impostazione specifica come convertire la concatenazione di stringhe con valori NULL. Per questa particolare impostazione, è possono impostare le opzioni seguenti:  
  
-   **Eseguire il wrapping con la funzione ISNULL:** Se questa opzione è impostata, verrà incluso ogni valore non costante 'string_expression' nella concatenazione ISNULL(string_expression) e i valori null verranno sostituite con una stringa vuota.  
  
-   **Mantenere la sintassi corrente**  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Mantenere la sintassi corrente  
  
**Modalità completa:** Eseguire il wrapping con la funzione ISNULL  
  
**Conversione delle stringhe vuote**  
Questa impostazione specifica come convertire le stringhe vuote. Per questa particolare impostazione, è possono impostare le opzioni seguenti:  
  
-   **Sostituire tutte le espressioni stringa con spazi**  
  
-   **Sostituire le costanti di stringa vuoto con lo spazio**  
  
-   Usare la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ comportamento di SQL Azure, seleziona **mantenere sintassi corrente**.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Mantenere la sintassi corrente  
  
**Modalità completa:** Sostituire tutte le espressioni stringa con spazi  
  
**Conversione di stringa binaria di CAST e CONVERT**  
La conversione di valori binari in numeri può restituire valori diversi su piattaforme diverse. Ad esempio, su x86 processori, CONVERT (integer, 0x00000100) restituisce 65536 nell'ambiente del servizio App e 256 in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ambiente del servizio App restituisce inoltre valori diversi a seconda dell'ordine dei byte.  
  
Usare questa impostazione per controllare come la conversione converte SSMA e le espressioni CASE che contengono valori binari:  
  
-   Selezionare **conversione semplice** per convertire le espressioni senza eventuali avvisi o correzione. Usare questa impostazione se si sa che il server dell'ambiente del servizio App ha un ordine di byte che non richiede modifiche del valore binario.  
  
-   Selezionare **convertire e correggere** affinché SSMA convertire e in modo corretto le espressioni per l'uso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verrà invertito l'ordine dei byte in valori letterali costanti. Tutti gli altri valori binari (ad esempio binarie variabili e colonne) verranno contrassegnate con errori. Utilizzare questo valore se si sa che il server dell'ambiente del servizio App ha un ordine di byte che richiede modifiche a valori binari.  
  
-   Selezionare **convertire e contrassegnare con avviso** avere SSMA convertire e correggere le espressioni e contrassegnare tutti convertiti espressioni con i commenti di avviso.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita:** Convertire e contrassegnare con avviso  
  
**Ottimistica modalità:** Conversione semplice  
  
**Modalità completa:** Convertire e correggere  
  
**SQL dinamico**  
Usare questa impostazione per specificare il tipo di messaggio (avviso o errore) indicante SSMA nel riquadro di Output o elenco errori in presenza di istruzioni SQL dinamiche in codice l'ambiente del servizio app.  
  
-   Se si seleziona **convertire e contrassegnare con avviso**, SSMA convertirà le istruzioni SQL dinamiche e contrassegnare le istruzioni con commenti di avviso.  
  
-   Se si seleziona **contrassegnare con l'errore**, SSMA. Always ignorerà la conversione e contrassegnare le istruzioni con commenti di errore.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Convertire e contrassegnare con avviso  
  
**Modalità completa:** Contrassegno con l'errore  
  
**Conversione di controllo di uguaglianza**  
Nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure, se l'impostazione di ANSI_NULLS è on, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure returns SCONOSCIUTI quando qualsiasi confronto delle uguaglianze contiene un valore null. Se ANSI_NULLS è impostata su, i confronti di uguaglianza che contengono valori null restituiscono true se due espressioni ed espressioni o la colonna confrontata sono entrambi null. Di uguaglianza predefinito (ANSINULL OFF) Sybase ASE confronti si comportano come [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure con ANSI_NULLS OFF.  
  
-   Se si seleziona **conversione semplice**, SSMA convertirà il codice di ambiente del servizio App a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ sintassi SQL Azure senza controlli aggiuntivi per i valori null. Usare questa impostazione se ANSI_NULLS è impostata su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure o se si desidera rivedere i confronti di uguaglianza in base al case.  
  
-   Se si seleziona **i valori NULL è consigliabile**, SSMA aggiungerà controlli per i valori null con la clausola IS NULL e IS NOT NULL.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Conversione semplice  
  
**Modalità completa:** Prendere in considerazione i valori NULL  
  
**Stringhe di formato**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure non supporta più il *format_string* argomento nelle istruzioni PRINT e RAISERROR. Il *format_string* variabile supportati l'inserimento di parametri sostituibili direttamente nella stringa e quindi sostituendo i parametri in fase di esecuzione. Al contrario, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede la stringa completa con un valore letterale stringa o una stringa compilata usando una variabile. Per altre informazioni, vedere la "PRINT ( [!INCLUDE[tsql](../../includes/tsql-md.md)])" argomento nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
Quando viene rilevata SSMA una *format_string* argomento, è possibile compilare una stringa letterale usando le variabili o creare una nuova variabile e compilare una stringa usando tale variabile.  
  
-   Per usare un valore letterale stringa per le funzioni PRINT e RAISERROR, selezionare **creare una nuova stringa**.  
  
    In questa modalità, se un'istruzione PRINT o RAISERROR non usa i segnaposto e le variabili locali, l'istruzione viene modificato. Caratteri di percentuale doppio (%) vengono modificati in un singolo carattere di percentuale % nei valori letterali stringa di stampa.  
  
    Se un'istruzione PRINT o RAISERROR Usa i segnaposto e uno o più variabili locali, come illustrato nell'esempio seguente:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA lo convertirà la sintassi seguente:  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    Se *format_string* è una variabile, ad esempio l'istruzione seguente:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA non è possibile eseguire una conversione di stringa semplice e deve creare una nuova variabile:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        CAST (@arg1 AS varchar(max)))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        CAST (@arg2 AS varchar(max)))  
    PRINT @print_format_1  
    ```  
    Quando Usa **creare una nuova stringa** modalità SSMA presuppone che il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opzione CONCAT_NULL_YIELDS_NULL è impostata su OFF. Pertanto, SSMA non verifica per gli argomenti null.  
  
-   Per creare una nuova variabile per ogni istruzione PRINT e RAISERROR e quindi usare tale variabile per il valore stringa SSMA, selezionare **Crea nuova variabile**.  
  
    In questa modalità, se un'istruzione PRINT o RAISERROR non usa i segnaposto e le variabili locali, SSMA sostituisce tutti i caratteri di percentuale doppio (%) con i caratteri di percentuale singoli per assicurare la conformità con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ sintassi SQL Azure.  
  
    Se un'istruzione PRINT o RAISERROR Usa i segnaposto e uno o più variabili locali, come illustrato nell'esempio seguente:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA lo convertirà la sintassi seguente:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1 = 'Total: %1!%'  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))  
    PRINT @print_format_1  
    ```  
    Se *format_string* è una variabile, ad esempio l'istruzione seguente:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA consente di creare una nuova variabile come indicato di seguito, verifica dei valori null in ogni argomento:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1  =   
        REPLACE (@fmt, '%%', '%')  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@arg1 AS varchar(max)),''))  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%2!',   
        ISNULL(CAST (@arg2 AS varchar(max)),''))  
    PRINT @print_format_1  
    ```  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Creare una nuova stringa  
  
**Modalità completa:** Creare una nuova variabile  
  
**Inserire un valore esplicito in una colonna timestamp**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure non supporta l'inserimento di valori espliciti in una colonna timestamp.  
  
-   Per escludere colonne timestamp dalle istruzioni INSERT, selezionare **Exclude colonna**.  
  
-   Per stampare un messaggio di errore ogni volta che è una colonna timestamp in un'istruzione INSERT, selezionare **contrassegnare con l'errore**. In questa modalità, le istruzioni INSERT non verranno convertite e verranno contrassegnate con commenti di errore.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Escludere la colonna  
  
**Modalità completa:** Contrassegno con l'errore  
  
**Oggetti temporanei Store definiti nelle procedure**  
Questa impostazione specifica se le definizioni di oggetti temporanei che vengono visualizzati nelle procedure devono essere archiviate nei metadati di origine durante la conversione.  
  
-   Selezionare **Sì** archiviare nei metadati.  
  
-   Selezionare **No** se gli oggetti non devono essere archiviati.  
  
**Modalità predefinita/ottimistico:** Yes  
  
**Modalità completa:** No  
  
**Conversione della tabella per proxy**  
Specifica se le tabelle di proxy di ambiente del servizio App vengono convertite in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ tabelle di SQL Azure o sei non convertito e il codice è contrassegnato con commenti di errore.  
  
-   Selezionare **convertire** per convertire le tabelle di proxy per le tabelle regolari.  
  
-   Selezionare **contrassegnare con l'errore** semplicemente contrassegnare il codice con commenti di errore nella tabella del proxy.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Contrassegno con l'errore  
  
**Numero di messaggi di base di RAISERROR**  
I messaggi utente ambiente del servizio App vengono archiviati in ogni database. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i messaggi utente vengono archiviati in modo centralizzato e resi disponibili tramite il **Sys. Messages** vista del catalogo. Inoltre i messaggi dell'ambiente del servizio App utente partono da 20000, ma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 50001 partono da messaggi di errore.  
  
Questa impostazione specifica il numero da aggiungere al numero di messaggi di ambiente del servizio App utente per convertirlo in un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] messaggio utente. Se il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presenta messaggi utente nella **Sys. Messages** vista del catalogo, potrebbe essere necessario modificare questo numero su un valore superiore. Si tratta in modo che i numeri di messaggio convertito non siano in conflitto con i numeri dei messaggi esistente.  
  
Tenere presente quanto segue:  
  
-   Messaggi ambiente del servizio App nell'intervallo 17000 19999 sono compresi tra la tabella di sistema sysmessages e non vengono convertiti.  
  
-   Se il numero di messaggi a cui fa riferimento l'istruzione RAISERROR è una costante, SSMA aggiungeranno il numero di messaggi di base per la costante per determinare il nuovo numero di messaggi utente.  
  
-   Se il numero di messaggi a cui viene fatto riferimento è una variabile o espressione, SSMA creerà una variabile locale intermedia.  
  
-   Nella modalità ottimistica SSMA si presuppone che il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opzione CONCAT_NULL_YIELDS_NULL è e non rende verifica se gli argomenti null.  
  
-   In modalità estesa, SSMA Cerca argomenti null.  
  
-   RAISERROR con ERRORDATA *elenco* non viene convertito.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** 30001  
  
**Oggetti di sistema**  
Usare questa impostazione per specificare il tipo di messaggio (avviso o errore) indicante SSMA nel riquadro di Output o un elenco di errore quando rileva l'uso di oggetti di sistema di ambiente del servizio app.  
  
-   Se si seleziona **convertire e contrassegnare con avviso**, SSMA convertirà i riferimenti agli oggetti di sistema e verranno contrassegnate come istruzioni e i commenti di avviso.  
  
-   Se si seleziona **contrassegnare con l'errore**, SSMA non converte i riferimenti agli oggetti di sistemi e verranno contrassegnate come istruzioni e i commenti di errore.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Convertire e contrassegnare con avviso  
  
**Modalità completa:** Contrassegno con l'errore  
  
**Identificatori non risolti**  
Usare questa impostazione per specificare il tipo di messaggio (avviso o errore) indicante SSMA nel riquadro di Output o un elenco di errore quando è in grado di risolvere un identificatore.  
  
-   Se si seleziona **convertire e contrassegnare con avviso**, SSMA tenterà di convertire i riferimenti a identificatori non risolti e verranno contrassegnate come istruzioni e i commenti di avviso.  
  
-   Se si seleziona **contrassegnare con l'errore**, SSMA non converte i riferimenti a identificatori non risolti e verranno contrassegnate come istruzioni e i commenti di errore.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Convertire e contrassegnare con avviso  
  
**Modalità completa:** Contrassegno con l'errore  
  
## <a name="system-function-options"></a>Opzioni di sistema (funzione)  
**Funzione CHARINDEX**  
Nell'ambiente del servizio App, CHARINDEX restituisce NULL solo se tutte le espressioni di input sono NULL. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure restituirà NULL se qualsiasi espressione di input è NULL.  
  
-   Per utilizzare il comportamento di ambiente del servizio App, selezionare **funzione Replace**. Tutte le chiamate alla funzione CHARINDEX viene sostituito con una chiamata a CHARINDEX_VARCHAR o CHARINDEX_NVARCHAR funzione definita dall'utente in base al tipo dei parametri passati (creato nel database utente con il nome dello schema 's2ss') per emulare il comportamento di Sybase ASE.  
  
-   Usare la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ comportamento di SQL Azure, seleziona **mantenere sintassi corrente**.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Mantenere la sintassi corrente  
  
**Modalità completa:** Sostituire (funzione)  
  
**Funzione DATALENGTH**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] / SQL Azure e ambiente del servizio App si differenziano per il valore restituito dalla funzione DATALENGTH quando il valore è uno spazio singolo. In questo caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure restituisce 0 e ambiente del servizio App 1.  
  
-   Per utilizzare il comportamento di ambiente del servizio App, selezionare **funzione Replace**. Tutte le chiamate alla funzione DATALENGTH vengono sostituite con espressione CASE per emulare il comportamento di Sybase ASE.  
  
-   Usare il valore predefinito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] / comportamento di SQL Azure, seleziona **mantenere sintassi corrente**.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Mantenere la sintassi corrente  
  
**Modalità completa:** Sostituire (funzione)  
  
**Index_col-funzione**  
Ambiente del servizio App supporta facoltativo *user_id* argomento della funzione INDEX_COL; tuttavia, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure non supporta questo argomento. Se si usa la *user_id* argomento, questa funzione non può essere convertita in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ sintassi SQL Azure.  
  
-   Per utilizzare il comportamento di ambiente del servizio App, selezionare **Converti la funzione**. Se il codice contiene il *user_id* argomento, SSMA verrà visualizzato un errore.  
  
-   Per visualizzare un messaggio di errore ogni volta che viene rilevato che INDEX_COL, selezionare **contrassegnare con l'errore**. SSMA non converte i riferimenti alla funzione e contrassegna l'istruzione con commenti di errore.  
  
**Modalità predefinita/ottimistica/Full:** Contrassegno con l'errore  
  
**Funzione INDEX_COLORDER**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure non è una funzione di sistema INDEX_COLORDER.  
  
-   Per utilizzare il comportamento di ambiente del servizio App, selezionare **Converti la funzione**. Tutte le chiamate alla funzione INDEX_COLORDER viene sostituito con una chiamata a una funzione definita dall'utente con lo stesso nome INDEX_COLORDER (creata nel database utente con il nome dello schema 's2ss') che emula il comportamento di Sybase ASE.  
  
-   Per stampare un messaggio di errore ogni volta che viene rilevato che INDEX_COLORDER, selezionare **contrassegnare con l'errore**. SSMA non converte i riferimenti alla funzione e contrassegna l'istruzione con commenti di errore.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Contrassegno con l'errore  
  
**Le funzioni LEFT e RIGHT**  
A sinistra e destra funzioni in Sybase si comportano in modo diverso per il parametro di lunghezza negativa.  
  
-   Per utilizzare il comportamento di ambiente del servizio App, selezionare **funzione Replace**. Il parametro della lunghezza verrà quindi sostituito con espressione CASE che restituirà null per il valore negativo.  
  
-   Per utilizzare il comportamento di SQL Server, selezionare **mantenere sintassi corrente**  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Mantenere la sintassi corrente  
  
**Modalità completa:** Sostituire (funzione)  
  
> [!NOTE]  
> Se il parametro della lunghezza è un valore letterale e non un'espressione complessa, il valore di lunghezza viene sostituito sempre con null indipendentemente dall'impostazione di progetto.  
  
**Funzione NEXT_IDENTITY**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure non è una funzione di sistema NEXT_IDENTITY.  
  
-   Per utilizzare il comportamento di ambiente del servizio App, selezionare **convertire funzione**. Tutte le chiamate alla funzione NEXT_IDENTITY viene sostituito con espressione (IDENT_CURRENT(parameter Value) + IDENT_INCR(parameter Value) che emula il comportamento di Sybase ASE.  
  
-   Per stampare un messaggio di errore ogni volta che viene rilevato che NEXT_IDENTITY, selezionare **contrassegnare con l'errore**. SSMA non converte i riferimenti alla funzione e contrassegna l'istruzione con commenti di errore.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/Full:** Contrassegno con l'errore  
  
**Funzione PATINDEX**  
Specifica se Converti la funzione PATINDEX per corrispondenza con il comportamento di Sybase ASE. Il punto è che Sybase Taglia gli spazi vuoti finali in un criterio di ricerca. Per risolvere il problema è eseguire un cast dell'espressione di valore a un tipo con precisione massima di dati e applicano la funzione rtrim per cercare pattern a lunghezza fissa.  
  
-   Usare l'istruzione select comportamento ASE **usare**.  
  
-   Usare il valore predefinito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ comportamento di SQL Azure, seleziona **non usare**.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Non utilizzare  
  
**Modalità completa:** Utilizzare  
  
**Funzione REPLICATE**  
La funzione REPLICATE viene ripetuto il numero specificato di volte in cui una stringa. Nell'ambiente del servizio App, se si specifica per ripetere la stringa di zero volte, il risultato è null. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure, il risultato è una stringa vuota.  
  
-   Per utilizzare il comportamento di ambiente del servizio App, selezionare **funzione Replace**. Tutte le chiamate alla funzione di eseguire la replica viene sostituito con una chiamata a REPLICATE_VARCHAR o REPLICATE_NVARCHAR funzione definita dall'utente in base al tipo dei parametri passati (creato nel database utente con il nome dello schema 's2ss') per emulare il comportamento di Sybase ASE.  
  
-   Usare il valore predefinito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ comportamento di SQL Azure, seleziona **funzione Replace**.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità di Full/modalità predefinita/ottimistico:** Sostituire (funzione)  
  
**Funzione TRIM (LTRIM, RTRIM)**  
Questa impostazione specifica se per sostituire le chiamate alle funzioni Trim (LTRIM, RTRIM) con le funzioni di sintassi di Sybase ASE-equivalente o mantenere la sintassi corrente. Sono presenti per questa impostazione specifica le opzioni seguenti:  
  
-   **Sostituire (funzione)**  
  
-   **Mantenere la sintassi corrente**  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità di Full/modalità predefinita/ottimistico:** Sostituire (funzione)  
  
**SUBSTRING-funzione**  
Nell'ambiente del servizio App, la funzione `SUBSTRING(expression, start, length)` restituisce NULL se viene specificato un valore di inizio maggiore del numero di caratteri nell'espressione o se lunghezza è uguale a zero. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/ SQL Azure, l'espressione equivalente restituisce una stringa vuota.  
  
-   Per utilizzare il comportamento di ambiente del servizio App, selezionare **funzione Replace**. Tutte le chiamate alla funzione SUBSTRING viene sostituito con una chiamata a SUBSTRING_VARCHAR o SUBSTRING_NVARCHAR o SUBSTRING_VARBINARY funzione definita dall'utente in base al tipo dei parametri passati (creata nel database utente con il nome dello schema 's2ss') per emulare il Comportamento di Sybase ASE.  
  
-   Usare la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] / comportamento di SQL Azure, seleziona **mantenere sintassi corrente**.  
  
Quando si seleziona una modalità di conversione di **modalità** SSMA finestra viene applicata l'impostazione seguente:  
  
**Modalità predefinita/ottimistico:** Mantenere la sintassi corrente  
  
**Modalità completa:** Sostituire (funzione)  
  
## <a name="tables"></a>TABLES  
**Aggiungere la chiave primaria**  
Crea una nuova chiave primaria nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o se una tabella di Access non ha alcuna chiave primaria o un indice univoco nella tabella di SQL Azure.  
  
-   **Modalità predefinita**: False  
  
-   **La modalità ottimistico**: False  
  
-   **Modalità intero**: True  
  
> [!NOTE]  
> Quando si è connessi a SQL Azure, è per impostazione predefinita True.  
  
## <a name="see-also"></a>Vedere anche  
[Riferimento all'interfaccia utente &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
