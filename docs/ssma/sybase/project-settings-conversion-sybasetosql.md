---
title: Impostazioni progetto (conversione) (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: eeb80fa5-f530-4f21-beee-25f5a4b8ace6
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 5d4936638fc9e283caafffc2f2a7cfdbed396920
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028760"
---
# <a name="project-settings-conversion-sybasetosql"></a>Impostazioni del progetto (conversione) (SybaseToSQL)
La pagina conversione della finestra di dialogo **Impostazioni progetto** contiene impostazioni che consentono di personalizzare il modo in cui SSMA converte la sintassi di Sybase Adaptive [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Server Enterprise (ASE) in o SQL Azure la sintassi.  
  
Il riquadro conversione è disponibile nelle finestre di dialogo **Impostazioni** progetto e **Impostazioni progetto predefinite** :  
  
-   Se si desidera specificare le impostazioni per tutti i progetti SSMA, nel menu **strumenti** selezionare **Impostazioni progetto predefinite**, fare clic su **generale** nella parte inferiore del riquadro sinistro, quindi fare clic su **conversione**.  
  
-   Per specificare le impostazioni per il progetto corrente, scegliere **Impostazioni progetto**dal menu **strumenti** , fare clic su **generale** nella parte inferiore del riquadro sinistro, quindi fare clic su **conversione**.  
  
## <a name="miscellaneous-options"></a>Opzioni varie  
**@@ERROR**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure e ASE utilizzano codici di errore diversi.  
  
Usare questa impostazione per specificare il tipo di messaggio (avviso o errore) visualizzato da SSMA nel riquadro Output o elenco errori quando viene rilevato un riferimento a **@@ERROR ** nel codice dell'ambiente del servizio app.  
  
-   Se si seleziona **Convert e Mark con Warning**, SSMA convertirà le istruzioni e le contrassegnerà con i commenti di avviso.  
  
-   Se si seleziona **contrassegna con errore**, SSMA ignorerà la conversione e contrassegnerà le istruzioni con commenti di errore.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Converti e contrassegno con avviso  
  
**Modalità completa:** Contrassegno con errore  
  
**Conversione dell'operatore LIKE**  
Specifica se convertire gli operandi LIKE in modo che corrispondano al comportamento di Sybase ASE. Il punto è che Sybase rimuove gli spazi vuoti finali in un modello like. La soluzione alternativa consiste nel creare un cast di espressione a destra in un tipo di dati a lunghezza fissa con una precisione massima.  
  
-   Selezionare **conversione semplice** per convertire le espressioni senza alcuna correzione.  
  
-   Per usare il comportamento dell'ambiente del servizio app **, selezionare cast a lunghezza fissa.**  
  
Quando si seleziona una modalità di conversione nella casella modalità, SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica**: conversione semplice  
  
**Modalità completa**: eseguire il cast alla lunghezza fissa  
  
**CONVERTE O ESEGUE IL CAST DI STRINGHE VUOTE IN TIPI NUMERICI**  
Specifica come gestire stringhe vuote o vuote all'interno di espressioni CONVERT o CAST con tipo numerico come argomento DataType. Per questa impostazione sono disponibili le opzioni seguenti:  
  
-   Selezionare **conversione semplice** per convertire le espressioni senza alcuna correzione.  
  
-   Se è selezionata una **stringa vuota, il** parametro di stringa {s} verrà sostituito con il case LTRIM (RTRIM ({s})) quando "", quindi 0 else {s} End Expression  
  
Quando si seleziona una modalità di conversione nella casella modalità, SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica**: conversione semplice  
  
**Modalità completa**: stringa vuota come valore numerico zero  
  
**Concatenazione di valori NULL**  
Questa impostazione specifica come convertire la concatenazione di stringhe con NULL. Per questa particolare impostazione è possibile impostare le opzioni seguenti:  
  
-   **Wrapping con la funzione IsNull:** Se questa opzione è impostata, verrà eseguito il wrapper di ogni ' string_expression ' non costante nella concatenazione con ISNULL (string_expression) e i valori NULL verranno sostituiti con una stringa vuota.  
  
-   **Mantieni sintassi corrente**  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Mantieni sintassi corrente  
  
**Modalità completa:** Wrapping con la funzione ISNULL  
  
**Conversione di stringhe vuote**  
Questa impostazione specifica come convertire le stringhe vuote. Per questa particolare impostazione è possibile impostare le opzioni seguenti:  
  
-   **Sostituisci tutte le espressioni stringa con lo spazio**  
  
-   **Sostituisci costanti stringa vuote con spazio**  
  
-   Per usare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]comportamento/SQL Azure, selezionare **Mantieni sintassi corrente**.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Mantieni sintassi corrente  
  
**Modalità completa:** Sostituisci tutte le espressioni stringa con lo spazio  
  
**CONVERTIRE e eseguire il CAST della conversione di stringhe binarie**  
La conversione di valori binari in numeri può restituire valori diversi su piattaforme diverse. Ad esempio, nei processori x86, CONVERT (Integer, 0x00000100) restituisce 65536 in ASE e 256 in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ambiente del servizio app restituisce anche valori diversi a seconda dell'ordine dei byte.  
  
Usare questa impostazione per controllare il modo in cui SSMA converte le espressioni di conversione e maiuscole e minuscole contenenti valori binari:  
  
-   Selezionare **conversione semplice** per convertire le espressioni senza avvisi o correzioni. Usare questa impostazione se si è certi che il server dell'ambiente del servizio app ha un ordine dei byte che non richiede alcuna modifica del valore binario.  
  
-   Selezionare **Converti e Correggi** affinché SSMA converta e corregga le espressioni da utilizzare in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'ordine dei byte nelle costanti letterali verrà invertito. Tutti gli altri valori binari (ad esempio, le variabili e le colonne binarie) verranno contrassegnati con errori. Usare questo valore se si è certi che il server dell'ambiente del servizio app ha un ordine dei byte che richiede modifiche ai valori binari.  
  
-   Selezionare **Converti e contrassegna con avviso** per fare in modo che SSMA converta e corregga le espressioni e contrassegna tutte le espressioni convertite con commenti di avviso.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita:** Converti e contrassegno con avviso  
  
**Modalità ottimistica:** Conversione semplice  
  
**Modalità completa:** Converti e Correggi  
  
**SQL dinamica**  
Usare questa impostazione per specificare il tipo di messaggio (avviso o errore) visualizzato da SSMA nel riquadro Output o Elenco errori quando rileva SQL dinamico nel codice dell'ambiente del servizio app.  
  
-   Se si seleziona **Convert e Mark con Warning**, SSMA convertirà il SQL dinamico e contrassegnerà le istruzioni con commenti di avviso.  
  
-   Se si seleziona **contrassegna con errore**, SSMA ignorerà la conversione e contrassegnerà le istruzioni con commenti di errore.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Converti e contrassegno con avviso  
  
**Modalità completa:** Contrassegno con errore  
  
**Conversione controllo di uguaglianza**  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure se l'impostazione ANSI_NULLS è on, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure restituisce Unknown quando un confronto di uguaglianza contiene un valore null. Se ANSI_NULLS è impostata su off, i confronti di uguaglianza che contengono valori Null restituiscono true se la colonna e l'espressione confrontate o due espressioni sono entrambe null. Per impostazione predefinita (ANSINULL OFF) i confronti di uguaglianza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di Sybase ASE si comportano come/SQL Azure con ANSI_NULLS disattivato.  
  
-   Se si seleziona **conversione semplice**, SSMA convertirà il codice dell'ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]del servizio app in/SQL Azure la sintassi senza ulteriori controlli per i valori null. Usare questa impostazione se ANSI_NULLS è disattivata in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure o se si vuole rivedere i confronti di uguaglianza per ogni singolo caso.  
  
-   Se si seleziona **considera i valori null**, SSMA aggiungerà i controlli per i valori null usando le clausole is null e is not null.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Conversione semplice  
  
**Modalità completa:** Considera valori NULL  
  
**Stringhe di formato**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure non supporta più l'argomento *FORMAT_STRING* nelle istruzioni Print e RAISERROR. La variabile *FORMAT_STRING* supportava l'inserimento di parametri sostituibili direttamente nella stringa e quindi la sostituzione dei parametri in fase di esecuzione. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Richiede invece la stringa completa usando un valore letterale stringa o una stringa compilata usando una variabile. Per ulteriori informazioni, vedere l'argomento "PRINT [!INCLUDE[tsql](../../includes/tsql-md.md)]()" nella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione online di.  
  
Quando SSMA rileva un argomento di *FORMAT_STRING* , può compilare un valore letterale stringa usando le variabili o creare una nuova variabile e compilare una stringa usando tale variabile.  
  
-   Per utilizzare un valore letterale stringa per le funzioni PRINT e RAISERROR, selezionare **Crea nuova stringa**.  
  
    In questa modalità, se un'istruzione PRINT o RAISERROR non utilizza segnaposti e variabili locali, l'istruzione è invariata. Doppio carattere percentuale (%%) vengono modificati in un singolo carattere di percentuale% nei valori letterali stringa di stampa.  
  
    Se un'istruzione PRINT o RAISERROR utilizza segnaposti e una o più variabili locali, ad esempio nell'esempio seguente:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA lo convertirà nella sintassi seguente:  
  
    ```  
    PRINT 'Total: '+ CAST(@percent AS varchar(max)) + '%'  
    ```  
    Se *FORMAT_STRING* è una variabile, ad esempio nell'istruzione seguente:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA non è in grado di eseguire una conversione di stringa semplice e deve creare una nuova variabile:  
  
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
    Quando usa la modalità di creazione di una **nuova stringa** , SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] presuppone che l'opzione CONCAT_NULL_YIELDS_NULL sia disattivata. SSMA non verifica quindi gli argomenti null.  
  
-   Per fare in modo che SSMA crei una nuova variabile per ogni istruzione PRINT e RAISERROR, quindi usare tale variabile per il valore stringa, selezionare **Crea nuova variabile**.  
  
    In questa modalità, se un'istruzione PRINT o RAISERROR non utilizza segnaposti e variabili locali, SSMA sostituisce tutti i caratteri di percentuale doppia (%%) con un singolo carattere di percentuale per conformarsi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]alla sintassi/SQL Azure.  
  
    Se un'istruzione PRINT o RAISERROR utilizza segnaposti e una o più variabili locali, ad esempio nell'esempio seguente:  
  
    ```  
    PRINT 'Total: %1!%%', @percent  
    ```  
    SSMA lo convertirà nella sintassi seguente:  
  
    ```  
    DECLARE @print_format_1 varchar(max)  
    SET @print_format_1 = 'Total: %1!%'  
    SET @print_format_1  =   
        REPLACE (@print_format_1, '%1!',   
        ISNULL(CAST (@percent AS VARCHAR(max)), ''))  
    PRINT @print_format_1  
    ```  
    Se *FORMAT_STRING* è una variabile, ad esempio nell'istruzione seguente:  
  
    ```  
    PRINT @fmt, @arg1, @arg2  
    ```  
    SSMA crea una nuova variabile come indicato di seguito, verificando la presenza di valori null in ogni argomento:  
  
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
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Crea nuova stringa  
  
**Modalità completa:** Crea nuova variabile  
  
**Inserire un valore esplicito in una colonna timestamp**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure non supporta l'inserimento di valori espliciti in una colonna timestamp.  
  
-   Per escludere le colonne timestamp dalle istruzioni INSERT, selezionare **Escludi colonna**.  
  
-   Per stampare un messaggio di errore ogni volta che una colonna timestamp si trova in un'istruzione INSERT, selezionare **contrassegna con errore**. In questa modalità, le istruzioni INSERT non verranno convertite e verranno contrassegnate con i commenti degli errori.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Escludi colonna  
  
**Modalità completa:** Contrassegno con errore  
  
**Archiviare oggetti temporanei definiti nelle procedure**  
Questa impostazione specifica se le definizioni degli oggetti temporanei visualizzate nelle procedure devono essere archiviate nei metadati di origine durante la conversione.  
  
-   Selezionare **Sì** per archiviare i metadati.  
  
-   Selezionare **No** se gli oggetti non devono essere archiviati.  
  
**Modalità predefinita/ottimistica:** Sì  
  
**Modalità completa:** No  
  
**Conversione di tabelle proxy**  
Specifica se le tabelle proxy dell'ambiente del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]servizio app vengono convertite in/SQL Azure tabelle oppure non vengono convertite e il codice è contrassegnato con commenti di errore.  
  
-   Selezionare **Converti** per convertire le tabelle proxy in tabelle normali.  
  
-   Selezionare **contrassegno con errore** per contrassegnare semplicemente il codice della tabella proxy con i commenti degli errori.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/completa:** Contrassegno con errore  
  
**Numero del messaggio di base RAISERROR**  
I messaggi utente dell'ambiente del servizio app vengono archiviati in ogni database. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]i messaggi utente vengono archiviati centralmente e resi disponibili tramite la vista del catalogo **sys. messages** . Inoltre, i messaggi utente dell'ambiente del servizio app [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] iniziano da 20000, ma i messaggi di errore iniziano con 50001.  
  
Questa impostazione specifica il numero da aggiungere al numero del messaggio utente dell'ambiente del servizio app per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convertirlo in un messaggio utente. Se il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone di messaggi utente nella vista del catalogo **sys. messages** , potrebbe essere necessario modificare questo numero in un valore superiore. In questo modo i numeri di messaggio convertiti non sono in conflitto con i numeri dei messaggi esistenti.  
  
Tenere presente quanto segue:  
  
-   I messaggi dell'ambiente del servizio app compresi nell'intervallo 17000-19999 provengono dalla tabella di sistema sysmessages e non vengono convertiti.  
  
-   Se il numero del messaggio a cui viene fatto riferimento nell'istruzione RAISERROR è una costante, SSMA aggiungerà il numero del messaggio di base alla costante per determinare il numero del nuovo messaggio utente.  
  
-   Se il numero del messaggio a cui viene fatto riferimento è una variabile o un'espressione, SSMA creerà una variabile locale intermedia.  
  
-   In modalità ottimistica, SSMA presuppone che l' [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opzione CONCAT_NULL_YIELDS_NULL sia disattivata e non esegue alcun controllo per gli argomenti null.  
  
-   In modalità completa, SSMA controlla gli argomenti null.  
  
-   RAISERROR con l' *elenco* ERRORDATA non viene convertito.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/completa:** 30001  
  
**Oggetti di sistema**  
Usare questa impostazione per specificare il tipo di messaggio (avviso o errore) visualizzato da SSMA nel riquadro Output o Elenco errori quando rileva l'uso degli oggetti di sistema dell'ambiente del servizio app.  
  
-   Se si seleziona **Convert e Mark con Warning**, SSMA convertirà i riferimenti in oggetti di sistema e contrassegnerà le istruzioni con commenti di avviso.  
  
-   Se si seleziona **contrassegna con errore**, SSMA non convertirà i riferimenti in oggetti di sistema e contrassegnerà le istruzioni con commenti di errore.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Converti e contrassegno con avviso  
  
**Modalità completa:** Contrassegno con errore  
  
**Identificatori non risolti**  
Usare questa impostazione per specificare il tipo di messaggio (avviso o errore) visualizzato da SSMA nel riquadro Output o Elenco errori quando non è possibile risolvere un identificatore.  
  
-   Se si seleziona **Convert e Mark con Warning**, SSMA tenterà di convertire i riferimenti in identificatori non risolti e contrassegnerà le istruzioni con commenti di avviso.  
  
-   Se si seleziona **contrassegno con errore**, SSMA non convertirà i riferimenti in identificatori non risolti e contrassegnerà le istruzioni con commenti di errore.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Converti e contrassegno con avviso  
  
**Modalità completa:** Contrassegno con errore  
  
## <a name="system-function-options"></a>Opzioni funzione di sistema  
**CHARINDEX, funzione**  
In ASE, CHARINDEX restituisce NULL solo se tutte le espressioni di input sono NULL. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure restituirà NULL se un'espressione di input è NULL.  
  
-   Per usare il comportamento dell'ambiente del servizio app, selezionare **Sostituisci funzione**. Tutte le chiamate alla funzione CHARINDEX vengono sostituite con una chiamata a CHARINDEX_VARCHAR o CHARINDEX_NVARCHAR funzione definita dall'utente in base al tipo di parametri passati (creati nel database utente sotto il 2SS ' del nome dello schema) per emulare il comportamento dell'ambiente del servizio app Sybase.  
  
-   Per usare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]comportamento/SQL Azure, selezionare **Mantieni sintassi corrente**.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Mantieni sintassi corrente  
  
**Modalità completa:** Replace (funzione)  
  
**DATALENGTH - funzione**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure e l'ambiente del servizio app differiscono nel valore restituito dalla funzione DATALENGTH quando il valore è uno spazio singolo. In questo caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure restituisce 0 e ASE restituisce 1.  
  
-   Per usare il comportamento dell'ambiente del servizio app, selezionare **Sostituisci funzione**. Tutte le chiamate alla funzione DATALENGTH vengono sostituite con l'espressione CASE per emulare il comportamento di Sybase ASE.  
  
-   Per usare il comportamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinito/SQL Azure, selezionare **Mantieni sintassi corrente**.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Mantieni sintassi corrente  
  
**Modalità completa:** Replace (funzione)  
  
**INDEX_COL - funzione**  
Ambiente del servizio app supporta un argomento di *user_id* facoltativo per la funzione di INDEX_COL; Tuttavia, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure non supporta questo argomento. Se si usa l'argomento *user_id* , questa funzione non può essere convertita in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure sintassi.  
  
-   Per usare il comportamento dell'ambiente del servizio app, selezionare **Converti funzione**. Se il codice contiene l'argomento *user_id* , SSMA visualizzerà un errore.  
  
-   Per visualizzare un messaggio di errore ogni volta che viene rilevata INDEX_COL, selezionare **contrassegna con errore**. SSMA non convertirà i riferimenti alla funzione e contrassegnerà l'istruzione con i commenti degli errori.  
  
**Modalità predefinita/ottimistica/completa:** Contrassegno con errore  
  
**Funzione INDEX_COLORDER**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure non dispone di una funzione di sistema INDEX_COLORDER.  
  
-   Per usare il comportamento dell'ambiente del servizio app, selezionare **Converti funzione**. Tutte le chiamate a INDEX_COLORDER funzione vengono sostituite con una chiamata a una funzione definita dall'utente con lo stesso nome INDEX_COLORDER, creato nel database utente con il nome dello schema 2SS ', che emula il comportamento dell'ambiente del servizio app Sybase.  
  
-   Per stampare un messaggio di errore ogni volta che viene rilevata INDEX_COLORDER, selezionare **contrassegna con errore**. SSMA non convertirà i riferimenti alla funzione e contrassegnerà l'istruzione con i commenti degli errori.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/completa:** Contrassegno con errore  
  
**Funzioni LEFT e RIGHT**  
Le funzioni Left e right in Sybase si comportano in modo diverso per il parametro di lunghezza negativa.  
  
-   Per usare il comportamento dell'ambiente del servizio app, selezionare **Sostituisci funzione**. Il parametro length viene quindi sostituito con un'espressione CASE che restituirà null per un valore negativo.  
  
-   Per usare il comportamento di SQL Server, selezionare **Mantieni sintassi corrente**  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Mantieni sintassi corrente  
  
**Modalità completa:** Replace (funzione)  
  
> [!NOTE]  
> Se il parametro length è un valore letterale e non un'espressione complessa, il valore length viene sempre sostituito con null indipendentemente dall'impostazione del progetto.  
  
**Funzione NEXT_IDENTITY**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure non dispone di una funzione di sistema NEXT_IDENTITY.  
  
-   Per usare il comportamento dell'ambiente del servizio app, selezionare **Converti funzione**. Tutte le chiamate a NEXT_IDENTITY funzione vengono sostituite con Expression (IDENT_CURRENT (valore del parametro) + IDENT_INCR (valore del parametro) che emula il comportamento dell'ambiente del servizio app Sybase.  
  
-   Per stampare un messaggio di errore ogni volta che viene rilevata NEXT_IDENTITY, selezionare **contrassegna con errore**. SSMA non convertirà i riferimenti alla funzione e contrassegnerà l'istruzione con i commenti degli errori.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/completa:** Contrassegno con errore  
  
**PATINDEX - funzione**  
Specifica se convertire la funzione PATINDEX in modo che corrisponda al comportamento di Sybase ASE. Il punto è che Sybase rimuove gli spazi vuoti finali in un criterio di ricerca. La soluzione alternativa consiste nell'eseguire un cast dell'espressione valore a un tipo di dati a lunghezza fissa con una precisione massima e applicare la funzione RTRIM ai criteri di ricerca.  
  
-   Per usare il comportamento dell'ambiente del servizio app, selezionare **use**.  
  
-   Per usare il comportamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]predefinito/SQL Azure, selezionare **non usare**.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Non usare  
  
**Modalità completa:** Usare  
  
**REPLICATE - funzione**  
La funzione REPLICAte ripete una stringa per il numero di volte specificato. Nell'ambiente del servizio app, se si specifica di ripetere la stringa zero volte, il risultato è null. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure il risultato è una stringa vuota.  
  
-   Per usare il comportamento dell'ambiente del servizio app, selezionare **Sostituisci funzione**. Tutte le chiamate alla funzione REPLICAte vengono sostituite con una chiamata a REPLICATE_VARCHAR o REPLICATE_NVARCHAR funzione definita dall'utente in base al tipo di parametri passati (creati nel database utente sotto il nome dello schema 2SS ') per emulare il comportamento di Sybase ASE.  
  
-   Per usare il comportamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]predefinito/SQL Azure, selezionare **Sostituisci funzione**.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/modalità completa:** Replace (funzione)  
  
**Funzione TRIM (LTRIM, RTRIM)**  
Questa impostazione specifica se sostituire le chiamate alle funzioni Trim (LTRIM, RTRIM) con le funzioni di sintassi equivalenti di Sybase ASE o per mantenete la sintassi corrente. Per questa particolare impostazione sono presenti le opzioni seguenti:  
  
-   **Replace (funzione)**  
  
-   **Mantieni sintassi corrente**  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica/modalità completa:** Replace (funzione)  
  
**SUBSTRING - funzione**  
Nell'ambiente del servizio app `SUBSTRING(expression, start, length)` la funzione restituisce null se viene specificato un valore iniziale maggiore del numero di caratteri nell'espressione o se la lunghezza è uguale a zero. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/SQL Azure l'espressione equivalente restituisce una stringa vuota.  
  
-   Per usare il comportamento dell'ambiente del servizio app, selezionare **Sostituisci funzione**. Tutte le chiamate alla funzione SUBSTRING vengono sostituite con una chiamata a SUBSTRING_VARCHAR o SUBSTRING_NVARCHAR o SUBSTRING_VARBINARY funzione definita dall'utente in base al tipo di parametri passati (creati nel database utente sotto il nome dello schema 2SS ') per emulare il comportamento di Sybase ASE.  
  
-   Per usare il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comportamento/SQL Azure, selezionare **Mantieni sintassi corrente**.  
  
Quando si seleziona una modalità di conversione nella casella **modalità** , SSMA applica l'impostazione seguente:  
  
**Modalità predefinita/ottimistica:** Mantieni sintassi corrente  
  
**Modalità completa:** Replace (funzione)  
  
## <a name="tables"></a>TABLES  
**Aggiungi chiave primaria**  
Crea una nuova chiave primaria nella tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure se una tabella di accesso non dispone di una chiave primaria o di un indice univoco.  
  
-   **Modalità predefinita**: false  
  
-   **Modalità ottimistica**: false  
  
-   **Modalità completa**: true  
  
> [!NOTE]  
> Quando si è connessi a SQL Azure, per impostazione predefinita è true.  
  
## <a name="see-also"></a>Vedere anche  
[Informazioni di riferimento sull'interfaccia utente &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
  
