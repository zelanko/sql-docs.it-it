---
title: Finestra di dialogo Modifica avanzata (Condizione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.condition.advancededit.f1
ms.assetid: a0bbe501-78c5-45ad-9087-965d04855663
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 50c6c92c6145c6ac148c8fe5f1b753151e5e3dc1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85069010"
---
# <a name="advanced-edit-condition-dialog-box"></a>Finestra di dialogo Modifica avanzata (Condizione)
  Usare la finestra di dialogo **Modifica avanzata** per creare espressioni complesse per le condizioni della gestione basata su criteri.  
  
## <a name="options"></a>Opzioni  
 **Valore cella**  
 Visualizza la funzione o l'espressione che verrà utilizzata per il valore della cella quando viene creata. Quando si fa clic su **OK**il valore della cella verrà visualizzato nella cella **Campo** o **Valore** della casella dell'espressione della condizione nella finestra di dialogo **Crea nuova condizione** o **Apri condizione** della pagina **Generale** .  
  
 **Funzioni e proprietà**  
 Visualizza le funzioni e le proprietà disponibili.  
  
 **Dettagli**  
 Visualizza informazioni sulle funzioni e sulle proprietà nel formato seguente: firma funzione, descrizione funzione, valore restituito ed esempio.  
  
## <a name="syntax"></a>Sintassi  
 Le espressioni valide devono avere il formato seguente:  
  
 `{property | function | constant}`  
  
 `{operator}`  
  
 `{property | function | constant}`  
  
## <a name="examples"></a>Esempi  
 Di seguito sono riportati alcuni esempi di espressioni valide:  
  
-   *Property1*> 5  
  
-   *Property1*=*Property2*  
  
-   Add(5, Multiply(.2,*Property1*))<*Property2*  
  
-   *Sometext* IN *Property1*  
  
-   *Property1* \< FN (*Property2*)  
  
-   BitwiseAnd(*Property1*,*Property2*)= 0  
  
## <a name="additional-function-information"></a>Ulteriori informazioni sulle funzioni  
 Nelle sezioni seguenti vengono fornite ulteriori informazioni sulle funzioni che è possibile utilizzare per creare espressioni complesse per le condizioni della gestione basata su criteri.  
  
> [!IMPORTANT]  
>  Le funzioni che è possibile utilizzare per creare le condizioni della gestione basata su criteri non utilizzano sempre la sintassi [!INCLUDE[tsql](../../includes/tsql-md.md)] . Verificare di seguire la sintassi di esempio. Ad esempio, quando si utilizzano le `DateAdd` `DatePart` funzioni o, è necessario racchiudere l'argomento *DatePart* tra virgolette singole.  
  
|Funzione|Descrizione|Argomenti|Valore restituito|Esempio|  
|--------------|-----------------|---------------|------------------|-------------|  
|`Add()`|Numeric Add (Numeric *expression1*, Numeric *expression2*)<br /><br /> Esegue la somma di due numeri.|*expression1* e *expression2* : qualsiasi espressione valida di uno dei tipi di dati della categoria numerica, ad eccezione del `bit` tipo di dati. Può essere una costante, una proprietà o una funzione che restituisce un tipo numerico.|**Valore restituito:** Restituisce il tipo di dati dell'argomento con precedenza maggiore.|**Esempio:** `Add(Property1, 5)`|  
|`Array()`|Array Array (VarArgs *expression*)<br /><br /> Crea una matrice da un elenco di valori. Può essere utilizzata con funzioni di aggregazione, ad esempio Sum() e Count().|*expression* : espressione che verrà convertita in matrice.|Matrice.|`Array(2,3,4,5,6)`|  
|`Avg()`|Numeric Avg (*VarArgs*)<br /><br /> Restituisce la media dei valori nell'elenco di argomenti.|*Varargs* -elenco di espressioni Variant della categoria di tipi di dati numerici esatti o numerici approssimati, ad eccezione del `bit` tipo di dati.|Il tipo restituito dipende dal tipo del risultato dell'espressione.<br /><br /> Se il risultato dell'espressione appartiene alle categorie `integer`, `decimal`, `money` e `smallmoney`, `float` e `real`, i tipi restituiti sono rispettivamente `int`, `decimal`, `money` e `float`.|`Avg(1.0, 2.0, 3.0, 4.0, 5.0)` restituisce `3.0` in questo esempio.|  
|`BitwiseAnd()`|Numeric BitwiseAnd (Numeric *expression 1*, Numeric *expression2*)<br /><br /> Esegue un'operazione con AND logico bit per bit tra due valori integer.|*expression1* ed *expression2* : qualsiasi espressione valida di un qualsiasi tipo di dati della categoria dei tipi di dati integer.|Restituisce un valore della categoria di tipi di dati integer.|`BitwiseAnd(Property1, Property2)`|  
|`BitwiseOr()`|Numeric BitwiseOr (Numeric *expression1*, Numeric *expression2*)<br /><br /> Esegue un'operazione con OR logico bit per bit su due valori integer specificati.|*expression1* ed *expression2* : qualsiasi espressione valida di un qualsiasi tipo di dati della categoria dei tipi di dati integer.|Restituisce un valore della categoria di tipi di dati integer.|`BitwiseOr(Property1, Property2)`|  
|`Concatenate()`|String Concatenate (String *string1*, String *string2*)<br /><br /> Concatena due stringhe.|*string1* e *string2* : le due stringhe da concatenare. che possono essere costituite da qualsiasi stringa non Null valida.|La stringa concatenata, con *string1* seguito da *string2*.|`Concatenate("Hello", " World``")`restituisce " `Hello World` ".|  
|`Count()`|Numeric Count (*VarArgs*)<br /><br /> Restituisce il numero di elementi nell'elenco di argomenti.|*Varargs* -espressione di qualsiasi tipo, ad eccezione di `text` , `image` e `ntext` .|Restituisce un valore della categoria di tipi di dati integer.|`Count(1.0, 2.0, 3.0, 4.0, 5.0)` restituisce `5` in questo esempio.|  
|`DateAdd()`|DateTime DateAdd (String *datepart*, Numeric *number*, DateTime *date*)<br /><br /> Restituisce un nuovo valore `datetime`, basato sull'aggiunta di un intervallo alla data specificata.|*datepart* : parametro che specifica in quale parte della data restituire un nuovo valore. I tipi supportati includono year(yy, yyyy), month(mm, m) e dayofyear(dy, y). Per altre informazioni, vedere [DATEADD &#40;Transact-SQL&#41;](/sql/t-sql/functions/dateadd-transact-sql).<br /><br /> *number*: valore usato per incrementare *datepart*.<br /><br /> *date* : espressione che restituisce un `datetime` valore o una stringa di caratteri in un formato di data.|Nuovo valore `datetime`, basato sull'aggiunta di un intervallo alla data specificata.|`DateAdd('day', 21, DateTime('2007-08-06 14:21:50'))` restituisce `'2007-08-27 14:21:50'` in questo esempio.<br /><br /> Di seguito sono elencate le coppie *dateParts* e abbreviazione supportate da questa funzione:<br /><br /> **year**: yy, yyyy<br /><br /> **mese**: mm, m<br /><br /> **DayOfYear**: DY, y<br /><br /> **giorno**: DD, d<br /><br /> **settimana**: WK, WW<br /><br /> **weekday**: dw, w<br /><br /> **ora**: HH<br /><br /> **minute**: mi, n<br /><br /> **secondo**: SS, s<br /><br /> **millisecondi**: ms|  
|`DatePart()`|Numeric DatePart (String *datepart*, DateTime *date*)<br /><br /> Restituisce un intero che rappresenta la *DatePart* specificata della data specificata.|*datepart* : parametro che specifica la parte della data da restituire. I tipi supportati includono year(yy, yyyy), month(mm, m) e dayofyear(dy, y). Per altre informazioni, vedere [DATEPART &#40;Transact-SQL&#41;](/sql/t-sql/functions/datepart-transact-sql).<br /><br /> *date* : espressione che restituisce un `datetime` valore o una stringa di caratteri in un formato di data.|Restituisce un valore di una categoria dei tipi di dati integer che rappresenta il valore *datepart* specificato della data indicata.|`DatePart('month', DateTime('2007-08-06 14:21:50.620'))` restituisce `8` in questo esempio.|  
|`DateTime()`|DateTime DateTime (String *dateString*)<br /><br /> Crea un valore datetime da una stringa.|*dateString* : valore datetime come stringa.|Restituisce un valore datetime creato dalla stringa di input.|`DateTime('3/12/2006')`|  
|`Divide()`|Numeric Divide (Numeric *expression_dividend*, Numeric *expression_divisor*)<br /><br /> Divide un numero per un altro.|*expression_dividend* : espressione numerica da dividere. Il dividendo può essere qualsiasi espressione valida di un qualsiasi tipo di dati della categoria di tipi di dati numerici, ad eccezione del tipo di dati `datetime`.<br /><br /> *expression_divisor* : espressione numerica per cui dividere il dividendo. Il divisore può essere qualsiasi espressione valida di un qualsiasi tipo di dati della categoria di tipi di dati numerici, ad eccezione del tipo di dati `datetime`.|Restituisce il tipo di dati dell'argomento con precedenza maggiore.|`Divide(Property1, 2)`<br /><br /> Nota: si tratta di una doppia operazione. Per eseguire un confronto tra integer, è necessario combinare i risultati con `Round()`, Ad esempio: `Round(Divide(10, 3), 0) = 3`.|  
|`Enum()`|Numeric Enum (String *enumTypeName*, String *enumValueName*)<br /><br /> Crea un valore enum da una stringa.|*enumTypeName* : nome del tipo di enumerazione.<br /><br /> *enumValueName* : valore dell'enumerazione.|Restituisce il valore enum come valore numerico.|`Enum('CompatibilityLevel','Version100')`|  
|`Escape()`|String Escape (String *replaceString*, String *stringToEscape*, String *escapeString*)<br /><br /> Applica una stringa di escape specificata a una sottostringa della stringa di input.|*replaceString*: stringa di input.<br /><br /> *stringToEscape*: sottostringa di *replaceString*. Si tratta della stringa davanti alla quale si desidera aggiungere una stringa di escape.<br /><br /> *escapeString*: stringa di escape da aggiungere prima di ogni istanza di *stringToEscape*.|Restituisce un valore *replaceString* modificato in cui ogni istanza di *stringToEscape* è preceduta da *escapeString*.|`Escape("Hello", "l", "[")` restituisce "`He[l[lo`".|  
|`ExecuteSQL()`|Variant ExecuteSQL (String *returnType*, String *sqlQuery*)<br /><br /> Esegue la query [!INCLUDE[tsql](../../includes/tsql-md.md)] nel server di destinazione.<br /><br /> Per altre informazioni su ExecuteSql(), vedere [Funzione ExecuteSql()](https://blogs.msdn.com/b/sqlpbm/archive/2008/07/03/executesql.aspx).|*returnType* : specifica il tipo restituito dei dati restituiti dall'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] . I valori letterali validi per *returnType* sono i seguenti: `Numeric` ,, `String` `Bool` , `DateTime` , `Array` e `Guid` .<br /><br /> *sqlQuery* : stringa che contiene la query da eseguire.||`ExecuteSQL ('Numeric', 'SELECT COUNT(*) FROM msdb.dbo.sysjobs') <> 0`<br /><br /> Esegue una query Transact-SQL con valori scalari su un'istanza di destinazione di SQL Server. È possibile specificare una sola colonna in un'istruzione `SELECT` . Le colonne aggiuntive oltre la prima vengono ignorate. La query risultante deve restituire una sola riga. Le righe aggiuntive oltre la prima vengono ignorate. Se la query restituisce un set vuoto, l'espressione della condizione compilata in base a `ExecuteSQL` restituirà false. `ExecuteSql` supporta le modalità di valutazione **Su richiesta** e **Su pianificazione** .<br /><br /> `@@ObjectName`-Corrisponde al campo del nome in [sys. Objects](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql). La variabile verrà sostituita con il nome dell'oggetto corrente.<br /><br /> `@@SchemaName`-Corrisponde al campo del nome in [sys. schemas](/sql/relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas). La variabile verrà sostituita con il nome dello schema per l'oggetto corrente, se applicabile.<br /><br /> <br /><br /> Nota: per includere una virgoletta singola in un'istruzione ExecuteSQL, trasformarla in una sequenza di escape con una seconda virgoletta singola. Ad esempio, per includere un riferimento a un utente di nome O'Brian, digitare O"Brian.|  
|`ExecuteWQL()`|Variant ExecuteWQL (string *returnType* , string *namespace*, string *wql*)<br /><br /> Esegue lo script WQL sullo spazio dei nomi specificato. L'istruzione Select può contenere solo una singola colonna restituita. Se vengono specificate più colonne, verrà generato un errore.|*returnType* : specifica il tipo restituito dei dati restituiti da WQL. I valori letterali validi sono `Numeric`, `String`, `Bool`, `DateTime`, `Array` e `Guid`.<br /><br /> *namespace* : spazio dei nomi WMI su cui eseguire la funzione.<br /><br /> *wql* : stringa che contiene la funzione WQL da eseguire.||`ExecuteWQL('Numeric', 'root\CIMV2', 'select NumberOfProcessors from win32_ComputerSystem') <> 0`|  
|`False()`|Bool False()<br /><br /> Restituisce il valore booleano FALSE.||Restituisce il valore booleano FALSE.|`IsDatabaseMailEnabled = False()`|  
|`GetDate()`|DateTime GetDate()<br /><br /> Restituisce la data di sistema.||Restituisce la data di sistema come valore DateTime.|`@DateLastModified = GetDate()`|  
|`Guid()`|Guid Guid(String *guidString*)<br /><br /> Restituisce un GUID da una stringa.|*guidString* : rappresentazione stringa del GUID da creare.|Restituisce il GUID creato dalla stringa.|`Guid('12340000-0000-3455-0000-000000000454')`|  
|`IsNull()`|Variant IsNull (Variant *check_expression*, Variant *replacement_value*)<br /><br /> Il valore di *check_expression* viene restituito se non è NULL. In caso contrario, viene restituito *replacement_value* . Se i tipi sono diversi, *replacement_value* viene convertito in modo implicito nel tipo *check_expression*.|*check_expression* : l'espressione da verificare per determinare se è NULL. *check_expression* può essere uno dei tipi supportati dalla gestione basata su criteri: Numeric, String, Bool, DateTime, Array e Guid.<br /><br /> *replacement_value* : espressione da restituire se *check_expression* è NULL. *replacement_value* deve essere di un tipo che viene convertito in modo implicito nel tipo *check_expression*.|Il tipo restituito è il tipo di *check_expression* se *check_expression* non è NULL. In caso contrario, viene restituito il tipo di *replacement_value* .||  
|`Len()`|Numeric Len (*string_expression*)<br /><br /> Restituisce il numero dei caratteri contenuti nell'espressione stringa specificata, esclusi gli spazi vuoti finali.|*string_expression* : espressione stringa da valutare.|Restituisce un valore della categoria di tipi di dati integer.|`Len('Hello')` restituisce `5` in questo esempio.|  
|`Lower()`|String Lower (String *_expression*)<br /><br /> Restituisce la stringa dopo aver convertito in minuscolo tutti i caratteri in maiuscolo.|*expression* : espressione stringa di origine.|Restituisce una stringa che rappresenta l'espressione stringa di origine dopo che tutti i caratteri in maiuscolo sono stati convertiti in minuscolo.|`Len('HeLlO')` restituisce `'hello'` in questo esempio.|  
|`Mod()`|Numeric Mod (Numeric *expression_dividend*, Numeric *expression_divisor*)<br /><br /> Viene restituito il resto intero dopo aver diviso la prima espressione numerica per la seconda espressione numerica.|*expression_dividend* : espressione numerica da dividere. *expression_dividend* deve essere un'espressione valida di uno dei tipi di dati nelle categorie di dati Integer o Numeric.<br /><br /> *expression_divisor* : espressione numerica per cui dividere il dividendo. *expression_dividend* deve essere un'espressione valida di uno dei tipi di dati nelle categorie di tipi di dati Integer o Numeric.|Restituisce un valore della categoria di tipi di dati integer.|`Mod(Property1, 3)`|  
|`Multiply()`|Numeric Multiply (Numeric *expression1*, Numeric *expression2*)<br /><br /> Moltiplica due espressioni.|*expression1* e *expression2* : qualsiasi espressione valida di uno dei tipi di dati della categoria numerica, ad eccezione del `datetime` tipo di dati.|Restituisce il tipo di dati dell'argomento con precedenza maggiore.|`Multiply(Property1, .20)`|  
|`Power()`|Numeric Power (Numeric *numeric_expression*, Numeric *expression_power*)<br /><br /> Restituisce il valore dell'espressione specificata alla potenza specificata.|*numeric_expression* : espressione della categoria dei tipi di dati numerici esatti o numerici approssimativi, ad eccezione del tipo di dati bit.<br /><br /> *expression_power* : potenza a cui elevare *numeric_expression*. *expression_power* può essere un'espressione della categoria di tipi di dati numerici esatti o numerici approssimati, ad eccezione del `bit` tipo di dati.|Il tipo restituito è identico a *numeric_expression*.|`Power(Property1, 3)`|  
|`Round()`|Numeric Round (Numeric *expression*, Numeric *expression_precision*)<br /><br /> Restituisce un'espressione numerica arrotondata alla lunghezza o alla precisione specificata.|*Expression* : espressione della categoria di tipi di dati numerici esatti o numerici approssimativi, ad eccezione del `bit` tipo di dati.<br /><br /> *expression_precision* : precisione a cui arrotondare l'espressione. Quando *expression_precision* è un numero positivo, *numeric_expression* viene arrotondato al numero di posizioni decimali specificato da length. Quando *expression_precision* è un numero negativo, *numeric_expression* viene arrotondato a sinistra del punto decimale, come specificato da *expression_precision*.|Restituisce lo stesso tipo di *numeric_expression*.|`Round(5.333, 0)`|  
|`String()`|String String (Variant *_expression*)<br /><br /> Converte un'espressione Variant in una stringa.|*expression* : espressione Variant da convertire in stringa.|Restituisce il valore stringa dell'espressione Variant.|`String(4)`|  
|`Sum()`|Numeric Sum (*VarArgs*)<br /><br /> Restituisce la somma di tutti i valori nell'elenco di argomenti. È possibile utilizzare Sum con valori numerici.|*Varargs*: elenco di espressioni Variant della categoria di tipi di dati numerici esatti o numerici approssimati, ad eccezione del `bit` tipo di dati.|Restituisce la somma di tutti i valori dell'espressione nel tipo di dati di espressione più preciso.<br /><br /> Se il risultato dell'espressione appartiene alle categorie `integer`, `numeric`, `money` e `small money`, `float` e `real`, i tipi restituiti sono rispettivamente `int`, `numeric`, `money` e `float`.|`Sum(1.0, 2.0, 3.0, 4.0, 5.0)` restituisce `15` in questo esempio.|  
|`True()`|Bool TRUE()<br /><br /> Restituisce il valore booleano TRUE.||Restituisce il valore booleano TRUE.|`IsDatabaseMailEnabled = True()`|  
|`Upper()`|String Upper (String *_expression*)<br /><br /> Restituisce la stringa dopo aver convertito in maiuscolo tutti i caratteri in minuscolo.|*expression* : espressione stringa di origine.|Restituisce una stringa che rappresenta l'espressione stringa di origine dopo che tutti i caratteri in minuscolo sono stati convertiti in maiuscolo.|`Len('HeLlO')` restituisce `'HELLO'` in questo esempio.|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Crea nuova condizione o Apri condizione, pagina generale](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [Amministrazione di server tramite la gestione basata su criteri](administer-servers-by-using-policy-based-management.md)  
  
  
