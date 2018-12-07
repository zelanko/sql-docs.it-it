---
title: DECLARE CURSOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECLARE_CURSOR_TSQL
- CURSOR_TSQL
- DECLARE CURSOR
- CURSOR
dev_langs:
- TSQL
helpviewer_keywords:
- DECLARE CURSOR statement
- cursors [SQL Server], attributes
- local cursors [SQL Server]
- nesting cursors
- Transact-SQL cursors, attributes
- global cursors [SQL Server]
ms.assetid: 5a3a27aa-03e8-4c98-a27e-809282379b21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e085aff8a426a748e49c450e1bbb6258881583e5
ms.sourcegitcommit: f1cf91e679d1121d7f1ef66717b173c22430cb42
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/29/2018
ms.locfileid: "52586304"
---
# <a name="declare-cursor-transact-sql"></a>DECLARE CURSOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Definisce gli attributi di un cursore del server [!INCLUDE[tsql](../../includes/tsql-md.md)], ad esempio lo scorrimento e la query utilizzata per compilare il set di risultati su cui agisce il cursore. L'istruzione `DECLARE CURSOR` supporta sia la sintassi basata sullo standard ISO che una sintassi che usi un set di estensioni [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```  
ISO Syntax  
DECLARE cursor_name [ INSENSITIVE ] [ SCROLL ] CURSOR   
     FOR select_statement   
     [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]  
[;]  
Transact-SQL Extended Syntax  
DECLARE cursor_name CURSOR [ LOCAL | GLOBAL ]   
     [ FORWARD_ONLY | SCROLL ]   
     [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
     [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
     [ TYPE_WARNING ]   
     FOR select_statement   
     [ FOR UPDATE [ OF column_name [ ,...n ] ] ]  
[;]  
```  
  
## <a name="arguments"></a>Argomenti  
 *cursor_name*  
 Nome del cursore server [!INCLUDE[tsql](../../includes/tsql-md.md)] definito. *cursor_name* deve essere conforme alle regole per gli identificatori.  
  
 INSENSITIVE  
 Definisce un cursore che crea una copia temporanea dei dati utilizzati dal cursore. La risposta alle richieste indirizzate al cursore viene formulata tramite questa tabella temporanea in **tempdb**. Le modifiche alle tabelle di base non vengono pertanto riportate nei dati restituiti dalle operazioni di recupero eseguite in questo cursore, in cui non è consentito apportare modifiche. Nella sintassi ISO, se viene omessa la parola chiave `INSENSITIVE`, le operazioni di eliminazione e aggiornamento di cui è stato eseguito il commit nelle tabelle sottostanti da parte di qualsiasi utente si riflettono nelle operazioni di recupero successive.  
  
 SCROLL  
 Specifica che tutte le opzioni di recupero (`FIRST`, `LAST`, `PRIOR`, `NEXT`, `RELATIVE`, `ABSOLUTE`) sono disponibili. Se l'opzione `SCROLL` non viene specificata in un'istruzione `DECLARE CURSOR` ISO, l'unica opzione di recupero supportata è `NEXT`. Non è possibile specificare l'opzione `SCROLL` se è specificata l'opzione `FAST_FORWARD`.  
  
 *select_statement*  
 Istruzione `SELECT` standard che definisce il set di risultati del cursore. Le parole chiave `FOR BROWSE` e `INTO` non sono consentite all'interno dell'argomento *select_statement* della dichiarazione di un cursore.  
  
 Se le clausole nell'argomento *select_statement* sono in conflitto con la funzionalità del tipo di cursore richiesto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte il cursore in modo implicito in un altro tipo.  
  
 READ ONLY  
 Impedisce gli aggiornamenti eseguiti tramite il cursore. Non è possibile fare riferimento al cursore in una clausola `WHERE CURRENT OF` di un'istruzione `UPDATE` o `DELETE`. Questa opzione è prioritaria rispetto alla funzionalità di aggiornamento predefinita di un cursore.  
  
 UPDATE [OF *column_name* [**,**...*n*]]  
 Definisce le colonne aggiornabili nel cursore. Se è specificato l'argomento OF <column_name> [, <... n>], è possibile apportare modifiche solo nelle colonne elencate. Se si specifica `UPDATE` senza un elenco di colonne, è possibile aggiornare tutte le colonne.  
  
 *cursor_name*  
 Nome del cursore server [!INCLUDE[tsql](../../includes/tsql-md.md)] definito. *cursor_name* deve essere conforme alle regole per gli identificatori.  
  
 LOCAL  
 Specifica che l'ambito del cursore è locale rispetto al batch, alla stored procedure o al trigger in cui il cursore è stato creato. Il nome del cursore è valido solo in tale ambito. È possibile fare riferimento al cursore tramite variabili di cursore locali nel batch, nella stored procedure o nel trigger oppure tramite un parametro `OUTPUT` di stored procedure. Un parametro `OUTPUT` consente di passare il cursore locale al batch, alla stored procedure o al trigger chiamante, che può quindi assegnare il parametro a una variabile cursore per fare riferimento al cursore dopo l'esecuzione della stored procedure. Il cursore viene deallocato in modo implicito al termine del batch, della stored procedure o del trigger, a meno che non venga passato a un parametro `OUTPUT`. In tal caso, il cursore viene deallocato quando l'ultima variabile che vi fa riferimento viene deallocata o risulta esterna all'ambito di validità.  
  
 GLOBAL  
 Specifica che l'ambito del cursore è globale rispetto alla connessione. È possibile fare riferimento al nome del cursore in qualsiasi stored procedure o batch eseguiti tramite la connessione. Il cursore viene deallocato solo in modo implicito in fase di disconnessione.  
  
> [!NOTE]  
>  Se gli argomenti `GLOBAL` e `LOCAL` vengono entrambi omessi, il valore predefinito dipende dall'impostazione dell'opzione di database **default to local cursor**.  
  
 FORWARD_ONLY  
 Specifica che è possibile scorrere il cursore solo dalla prima all'ultima riga. `FETCH NEXT` è l'unica opzione di recupero supportata. Se si specifica l'opzione `FORWARD_ONLY` senza la parola chiave `STATIC`, `KEYSET` o `DYNAMIC`, il cursore fungerà da cursore DYNAMIC. Se si omettono sia `FORWARD_ONLY` che `SCROLL`, l'impostazione predefinita è `FORWARD_ONLY`, a meno che non sia specificata la parola chiave `STATIC`, `KEYSET` o `DYNAMIC`. L'impostazione predefinita dei cursori `STATIC`, `KEYSET` e `DYNAMIC` è `SCROLL`. A differenza delle API di database, ad esempio ODBC e ADO, l'opzione `FORWARD_ONLY` è supportata con i cursori `STATIC`, `KEYSET` e `DYNAMIC` [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 STATIC  
 Definisce un cursore che crea una copia temporanea dei dati utilizzati dal cursore. La risposta alle richieste indirizzate al cursore viene formulata tramite questa tabella temporanea in **tempdb**. Le modifiche alle tabelle di base non vengono pertanto riportate nei dati restituiti dalle operazioni di recupero eseguite in questo cursore, in cui non è consentito apportare modifiche.  
  
 KEYSET  
 Specifica che all'apertura del cursore l'appartenenza e l'ordine delle righe nel cursore sono fissi. Il set di chiavi che identifica le righe in modo univoco è incluso in una tabella di **tempdb** denominata **keyset**.  
  
> [!NOTE]  
> Se la query fa riferimento ad almeno una tabella priva di indice univoco, il cursore keyset viene convertito in cursore statico.  
  
 Le modifiche a valori non chiave apportate nelle tabelle di base dal proprietario del cursore o confermate tramite commit da altri utenti sono visibili quando il proprietario scorre il cursore. Gli inserimenti eseguiti da altri utenti non sono visibili (tali inserimenti non possono essere eseguiti tramite un cursore [!INCLUDE[tsql](../../includes/tsql-md.md)] del server). Se una riga viene eliminata, il tentativo di recuperarla restituirà un valore -2 per la funzione `@@FETCH_STATUS`. Le operazioni di aggiornamento di valori di chiave dall'esterno del cursore sono simili a un'operazione di eliminazione della riga precedente seguita da un'operazione di inserimento della nuova riga. La riga con i nuovi valori non è visibile e i tentativi di recuperare la riga con i valori precedenti restituiranno il valore -2 per la funzione `@@FETCH_STATUS`. I nuovi valori sono visibili se l'aggiornamento viene effettuato tramite il cursore con l'aggiunta della clausola `WHERE CURRENT OF`.  
  
 DYNAMIC  
 Definisce un cursore in cui, durante lo scorrimento, vengono riportate tutte le modifiche ai dati apportate alle righe nel set di risultati. I valori dei dati, l'ordine e l'appartenenza delle righe possono cambiare a ogni operazione di recupero. L'opzione ABSOLUTE dell'istruzione FETCH non è supportata con cursori dinamici.  
  
 FAST_FORWARD  
 Specifica un cursore `FORWARD_ONLY`, `READ_ONLY` con le ottimizzazioni delle prestazioni abilitate. Non è possibile specificare l'opzione `FAST_FORWARD` se è specificata l'opzione `SCROLL` o `FOR_UPDATE`.  
  
> [!NOTE]  
>  Le opzioni `FAST_FORWARD` e `FORWARD_ONLY` possono essere usate nella stessa istruzione `DECLARE CURSOR`.  
  
 READ_ONLY  
 Impedisce gli aggiornamenti eseguiti tramite il cursore. Non è possibile fare riferimento al cursore in una clausola `WHERE CURRENT OF` di un'istruzione `UPDATE` o `DELETE`. Questa opzione è prioritaria rispetto alla funzionalità di aggiornamento predefinita di un cursore.  
  
 SCROLL_LOCKS  
 Specifica che gli aggiornamenti o le eliminazioni posizionate eseguite tramite il cursore avranno esito positivo. Durante la lettura nel cursore [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] blocca le righe in modo che siano disponibili per modifiche successive. Non è possibile specificare l'opzione `SCROLL_LOCKS` se è specificata l'opzione `FAST_FORWARD` o `STATIC`.  
  
 OPTIMISTIC  
 Specifica che gli aggiornamenti o le eliminazioni posizionate eseguite tramite il cursore non avranno esito positivo se la riga ha subito un aggiornamento dopo la lettura nel cursore. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non blocca le righe man mano che vengono lette nel cursore. Per determinare se la riga è stata modificata dopo la lettura nel cursore, vengono usati confronti tra i valori della colonna **timestamp** oppure un valore di checksum se la tabella non include una colonna **timestamp**. Se la riga è stata modificata, i tentativi di eseguire un aggiornamento o un'eliminazione posizionata hanno esito negativo. Non è possibile specificare l'opzione `OPTIMISTIC` se è specificata l'opzione `FAST_FORWARD`.  
  
 TYPE_WARNING  
 Specifica che deve essere inviato un messaggio di avviso al client quando il cursore viene convertito in modo implicito dal tipo richiesto in un altro tipo.  
  
 *select_statement*  
 Istruzione SELECT standard che definisce il set di risultati del cursore. Le parole chiave `COMPUTE`, `COMPUTE BY`, `FOR BROWSE` e `INTO` non sono consentite all'interno dell'argomento *select_statement* della dichiarazione di un cursore.  
  
> [!NOTE]  
>  Nella dichiarazione di un cursore è possibile usare un hint per la query. Se tuttavia si usa anche la clausola `FOR UPDATE OF`, specificare `OPTION (<query_hint>)` subito dopo.  
  
 Se le clausole nell'argomento *select_statement* sono in conflitto con la funzionalità del tipo di cursore richiesto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] converte il cursore in modo implicito in un altro tipo. Per ulteriori informazioni, vedere l'argomento relativo alla conversione implicita dei cursori.  
  
 FOR UPDATE [OF *column_name* [**,**...*n*]]  
 Definisce le colonne aggiornabili nel cursore. Se si specifica `OF <column_name> [, <... n>]`, è possibile apportare modifiche solo nelle colonne elencate. Se l'istruzione `UPDATE` viene specificata senza un elenco di colonne, è possibile aggiornare tutte le colonne, a meno che non sia stata specificata l'opzione di concorrenza `READ_ONLY`.  
  
## <a name="remarks"></a>Remarks  
`DECLARE CURSOR` definisce gli attributi di un cursore server [!INCLUDE[tsql](../../includes/tsql-md.md)], ad esempio il comportamento dello scorrimento e la query usata per compilare il set di risultati su cui il cursore opera. L'istruzione `OPEN` popola il set di risultati e l'istruzione `FETCH` restituisce una riga di questo set. L'istruzione `CLOSE` rilascia il set di risultati corrente associato al cursore. L'istruzione `DEALLOCATE` rilascia le risorse usate dal cursore.  
  
 La prima forma dell'istruzione `DECLARE CURSOR` dichiara il funzionamento del cursore tramite la sintassi ISO. La seconda forma dell'istruzione `DECLARE CURSOR` usa estensioni di [!INCLUDE[tsql](../../includes/tsql-md.md)] che consentono di definire cursori in base allo stesso tipo di cursore usato nelle funzioni di cursore delle API di database ODBC o ADO.  
  
 Non è possibile combinare le due forme dell'istruzione. Se si specifica la parola chiave `SCROLL` o `INSENSITIVE` prima della parola chiave `CURSOR`, non è possibile specificare parole chiave tra le parole chiave `CURSOR` e `FOR <select_statement>`. Se si specifica una parola chiave tra le parole chiave `CURSOR` e `FOR <select_statement>`, non è possibile specificare `SCROLL` o `INSENSITIVE` prima della parola chiave `CURSOR`.  
  
 Se un'istruzione `DECLARE CURSOR` che usa la sintassi [!INCLUDE[tsql](../../includes/tsql-md.md)] non specifica `READ_ONLY`, `OPTIMISTIC` o `SCROLL_LOCKS`, il valore predefinito viene stabilito come segue:  
  
-   Se l'istruzione `SELECT` non supporta aggiornamenti (autorizzazioni insufficienti, accesso a tabelle remote che non supportano aggiornamenti e così via), il cursore viene impostato come `READ_ONLY`.  
  
-   L'impostazione predefinita dei cursori `STATIC` e `FAST_FORWARD` è `READ_ONLY`.  
  
-   L'impostazione predefinita dei cursori `DYNAMIC` e `KEYSET` è `OPTIMISTIC`.  
  
 È possibile fare riferimento a nomi di cursore solo tramite altre istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)]. Non è possibile fare riferimento ai nomi di cursore con funzioni API del database. Dopo la dichiarazione del cursore, ad esempio, non è possibile fare riferimento al nome del cursore tramite le funzioni o i metodi di OLE DB, ODBC o ADO. Le righe del cursore non possono essere recuperate tramite le funzioni o i metodi di recupero API, ma solo utilizzando istruzioni FETCH [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Dopo la dichiarazione di un cursore è possibile eseguire le stored procedure di sistema seguenti per determinare le caratteristiche del cursore.  
  
|Stored procedure di sistema|Descrizione|  
|------------------------------|-----------------|  
|**sp_cursor_list**|Restituisce l'elenco dei cursori visibili nella connessione e gli attributi corrispondenti.|  
|**sp_describe_cursor**|Descrive gli attributi di un cursore, ad esempio se si tratta di un cursore forward-only o scorrevole.|  
|**sp_describe_cursor_columns**|Descrive gli attributi delle colonne nel set di risultati del cursore.|  
|**sp_describe_cursor_tables**|Descrive le tabelle di base a cui ha avuto accesso il cursore.|  
  
 È possibile usare variabili come parte dell'istruzione *select_statement* che dichiara un cursore. Dopo la dichiarazione di un cursore i valori delle variabili di cursore non cambiano.  
  
## <a name="permissions"></a>Permissions  
 Le autorizzazioni per l'istruzione `DECLARE CURSOR` vengono assegnate per impostazione predefinita a qualsiasi utente che disponga delle autorizzazioni per l'istruzione `SELECT` nelle viste, nelle tabelle e nelle colonne usate nel cursore.
 
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni

Non è possibile usare cursori o trigger in una tabella con un indice columnstore cluster. Questa restrizione non si applica agli indici columnstore non cluster. In una tabella con un indice columnstore non cluster è possibile usare cursori e trigger. 
  
## <a name="examples"></a>Esempi  
  
### <a name="a-using-simple-cursor-and-syntax"></a>A. Utilizzo di una semplice sintassi per la definizione di un cursore  

Il set di risultati generato all'apertura del cursore include tutte le righe e le colonne della tabella. Questo cursore può essere aggiornato e tutti gli aggiornamenti e le eliminazioni sono rappresentati nei recuperi eseguiti su questo cursore. `FETCH NEXT` è l'unica operazione di recupero disponibile perché l'opzione `SCROLL` non è stata specificata.  
 
```sql  
DECLARE vend_cursor CURSOR  
    FOR SELECT * FROM Purchasing.Vendor  
OPEN vend_cursor  
FETCH NEXT FROM vend_cursor;  
```  
  
### <a name="b-using-nested-cursors-to-produce-report-output"></a>B. Utilizzo di cursori annidati per la generazione di report  
 Nell'esempio seguente viene illustrato in che modo è possibile nidificare i cursori per generare report complessi. Il cursore interno viene dichiarato per ogni fornitore.  
  
```sql  
SET NOCOUNT ON;  
  
DECLARE @vendor_id int, @vendor_name nvarchar(50),  
    @message varchar(80), @product nvarchar(50);  
  
PRINT '-------- Vendor Products Report --------';  
  
DECLARE vendor_cursor CURSOR FOR   
SELECT VendorID, Name  
FROM Purchasing.Vendor  
WHERE PreferredVendorStatus = 1  
ORDER BY VendorID;  
  
OPEN vendor_cursor  
  
FETCH NEXT FROM vendor_cursor   
INTO @vendor_id, @vendor_name  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    PRINT ' '  
    SELECT @message = '----- Products From Vendor: ' +   
        @vendor_name  
  
    PRINT @message  
  
    -- Declare an inner cursor based     
    -- on vendor_id from the outer cursor.  
  
    DECLARE product_cursor CURSOR FOR   
    SELECT v.Name  
    FROM Purchasing.ProductVendor pv, Production.Product v  
    WHERE pv.ProductID = v.ProductID AND  
    pv.VendorID = @vendor_id  -- Variable value from the outer cursor  
  
    OPEN product_cursor  
    FETCH NEXT FROM product_cursor INTO @product  
  
    IF @@FETCH_STATUS <> 0   
        PRINT '         <<None>>'       
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
  
        SELECT @message = '         ' + @product  
        PRINT @message  
        FETCH NEXT FROM product_cursor INTO @product  
        END  
  
    CLOSE product_cursor  
    DEALLOCATE product_cursor  
        -- Get the next vendor.  
    FETCH NEXT FROM vendor_cursor   
    INTO @vendor_id, @vendor_name  
END   
CLOSE vendor_cursor;  
DEALLOCATE vendor_cursor;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursori &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
