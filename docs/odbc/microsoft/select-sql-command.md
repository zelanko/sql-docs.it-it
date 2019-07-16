---
title: SELECT - comando SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- select [ODBC]
ms.assetid: 2149c3ca-3a71-446d-8d53-3d056e2f301a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85f281aefe79a09806c42e13cd771f976362d053
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943780"
---
# <a name="select---sql-command"></a>SELECT (comando SQL)
Recupera i dati da una o più tabelle.  
  
 Il Driver ODBC Visual FoxPro supporta la sintassi del linguaggio Visual FoxPro nativa per questo comando. Per informazioni specifiche del driver, vedere **osservazioni Driver**.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SELECT [ALL | DISTINCT]  
   [Alias.] Select_Item [AS Column_Name]  
   [, [Alias.] Select_Item [AS Column_Name] ...]   
FROM [DatabaseName!]Table [Local_Alias]  
   [, [DatabaseName!]Table [Local_Alias] ...]   
[WHERE JoinCondition [AND JoinCondition  
...]  
   [AND | OR FilterCondition [AND | OR FilterCondition ...]]]  
[GROUP BY GroupColumn [, GroupColumn ...]]  
[HAVING FilterCondition]  
[UNION [ALL] SELECTCommand]  
[ORDER BY Order_Item [ASC | DESC] [, Order_Item [ASC | DESC] ...]]  
```  
  
## <a name="arguments"></a>Argomenti  
  
> [!NOTE]  
>  Oggetto *sottoquery*, a cui gli argomenti seguenti, è un'istruzione SELECT all'interno di un'istruzione SELECT e deve essere racchiuso tra parentesi. È possibile avere fino a due sottoquery allo stesso livello (non annidato) nella clausola WHERE. (Vedere la sezione degli argomenti). Le sottoquery possono contenere più condizioni di join.  
  
 [Tutte le &#124; DISTINCT]   [*Alias*.] *Select_Item* [AS *Column_Name*] [, [*Alias*.] *Select_Item* [AS *Column_Name*]...]  
 La clausola SELECT specifica i campi, le costanti e le espressioni che vengono visualizzate nei risultati della query.  
  
 Per impostazione predefinita, tutti vengono visualizzate tutte le righe nei risultati della query.  
  
 DISTINCT sono esclusi i duplicati di tutte le righe dai risultati della query.  
  
> [!NOTE]  
>  È possibile usare DISTINCT una sola volta per ogni clausola SELECT.  
  
 *Alias*. qualifica i nomi di elemento corrispondente. Ogni elemento specificato con *Select_Item* genera una colonna dei risultati della query. Se due o più elementi hanno lo stesso nome, includere l'alias di tabella e un punto prima del nome di elemento per impedire che le colonne da duplicare.  
  
 *Select_Item* specifica un elemento da includere nei risultati della query. Un elemento può essere uno dei seguenti:  
  
-   Il nome di un campo da una tabella nella clausola FROM.  
  
-   Costante che specifica che lo stesso valore di costante deve essere visualizzato in ogni riga dei risultati della query.  
  
-   Espressione che può essere il nome di una funzione definita dall'utente.  
  
 **Funzioni definite dall'utente con l'istruzione SELECT**  
  
 Sebbene l'utilizzo di funzioni definite dall'utente nella clausola SELECT presenta evidenti vantaggi, si consiglia inoltre le restrizioni seguenti:  
  
-   La velocità delle operazioni eseguite con l'istruzione SELECT potrà essere limitata dalla velocità con cui vengono eseguite tali funzioni definite dall'utente. Manipolazioni di volumi elevati che includono funzioni definite dall'utente potrebbero essere effettuate migliore usando API e funzioni definite dall'utente scritte in C o in linguaggio assembly.  
  
-   L'unica modalità affidabile per passare valori a funzioni definite dall'utente richiamate da selezionare è dall'elenco degli argomenti passato alla funzione quando viene richiamato.  
  
-   Anche se sperimentare e si rileva una modifica apparentemente non consentita che funziona correttamente in una determinata versione di FoxPro, non c'è garanzia che continueranno a funzionare nelle versioni successive.  
  
 Oltre a queste limitazioni, funzioni definite dall'utente sono accettabili nella clausola SELECT. Tuttavia, tenere presente che l'utilizzo dell'istruzione SELECT può rallentare le prestazioni.  
  
 Le funzioni di campo seguenti sono disponibili per l'uso con un elemento selezionato è un campo o un'espressione che include un campo:  
  
-   AVG (*Select_Item*): calcola la media di una colonna di dati numerici.  
  
-   CONTEGGIO (*Select_Item*)-conta il numero di selezionare gli elementi in una colonna. Count conta il numero di righe nell'output della query.  
  
-   MIN (*Select_Item*)-determina il valore più piccolo della *Select_Item* in una colonna.  
  
-   MAX (*Select_Item*)-determina il valore più grande della *Select_Item* in una colonna.  
  
-   SUM (*Select_Item*)-totali di una colonna di dati numerici.  
  
 È possibile nidificare le funzioni di campo.  
  
 AS *Column_Name*  
 Specifica l'intestazione per una colonna nell'output della query. Ciò è utile nei casi *Select_Item* è un'espressione o contiene un campo (funzione) e si desidera assegnare un nome significativo alla colonna. *Column_Name* può essere un'espressione non può contenere caratteri (ad esempio, spazi) che non sono consentiti nei nomi di campo di tabella.  
  
 DA [*DatabaseName*!] *Tabella* [*Local_Alias*] [, [*NomeDatabase*!] *Tabella* [*Local_Alias*]...]  
 Elenca le tabelle che contengono i dati recuperati dalla query. Se nessuna tabella è aperta, Visual FoxPro consente di visualizzare il **aprire** finestra di dialogo, in modo che sia possibile specificare il percorso del file. Dopo che è stato aperto, la tabella rimane aperta dopo la query è stata completata.  
  
 *DatabaseName*! Specifica il nome di un database diverso da quello specificato con l'origine dati. È necessario includere il nome del database contenente la tabella se il database non è specificato con l'origine dati. Includere il delimitatore punto esclamativo (!) dopo il nome del database e prima del nome di tabella.  
  
 *Local_Alias* specifica un nome temporaneo per la tabella denominata nella *tabella*. Se si specifica un alias locale, è necessario usare l'alias locale anziché il nome della tabella in tutto l'istruzione SELECT. L'alias locale non influenza l'ambiente di Visual FoxPro.  
  
 In cui *JoinCondition* [AND *JoinCondition* ...]    [AND &#124; oppure *FilterCondition* [AND &#124; oppure *FilterCondition* ...]]  
 Indica a Visual FoxPro da includere solo alcuni record nei risultati della query. Quando viene richiesto per recuperare i dati da più tabelle.  
  
 *JoinCondition* specifica i campi che si collegano tabelle nella clausola FROM. Se si include più di una tabella in una query, è necessario specificare una condizione di join per ogni tabella dopo il primo.  
  
> [!IMPORTANT]  
>  Quando si crea le condizioni di join, considerare le informazioni seguenti:  
  
-   Se si includono due tabelle in una query e non si specifica una condizione di join, ogni record nella prima tabella fa parte di ogni record nella seconda tabella fino a quando vengono soddisfatte le condizioni di filtro. Una query di questo tipo può produrre risultati di lunga durati.  
  
-   Prestare attenzione quando si uniscono le tabelle con i campi vuoti, poiché Visual FoxPro corrispondono ai campi vuoti. Ad esempio, se si partecipa su CUSTOMER. Codice postale e di fatturazione. COMPRIMERE e se cliente contiene 100 i codici postali zip vuoti e della fattura contiene 400 i codici postali zip vuoti, l'output della query contiene 40.000 extra record risultanti dai campi vuoti. Usare la **(vuoto)** funzione per eliminare record vuoti dall'output della query.  
  
-   È necessario utilizzare l'operatore AND per connettere più condizioni di join. Ogni condizione join ha il formato seguente:  
  
     *Confronto FieldName1 FieldName2*  
  
     *FieldName1* è il nome di un campo da una tabella, *FieldName2* è il nome di un campo da un'altra tabella, e *confronto* è uno degli operatori descritti nella tabella seguente.  
  
|Operator|Confronto|  
|--------------|----------------|  
|=|Uguale|  
|==|Esattamente uguale a|  
|LIKE|SIMILE A SQL|  
|<>, !=, #|Non uguaglianza|  
|>|Più di|  
|>=|Maggiore o uguale a|  
|<|Minore di|  
|<=|Minore o uguale a|  
  
 Quando si usa l'operatore = con stringhe, che viene elaborata in modo diverso, a seconda dell'impostazione di SET ANSI. Quando SET ANSI è impostata su OFF, Visual FoxPro considera i confronti di stringhe in modo familiare agli utenti di Xbase. Quando SET ANSI è impostata su ON, Visual FoxPro conforme agli standard ANSI per confronti tra stringhe. Visualizzare [SET ANSI](../../odbc/microsoft/set-ansi-command.md) e [SET EXACT](../../odbc/microsoft/set-exact-command.md) per altre informazioni sul modo in cui Visual FoxPro esegue confronti di stringhe.  
  
 *FilterCondition* specifica i criteri che i record devono soddisfare per essere inclusi nei risultati della query. È possibile includere le condizioni in una query di filtro desiderati, connetterle con l'operatore AND o l'operatore OR. È anche possibile usare l'operatore NOT per invertire il valore di un'espressione logica oppure è possibile usare **(vuoto)** per verificare la presenza di un campo vuoto. *FilterCondition* può accettare uno qualsiasi dei formati negli esempi seguenti:  
  
 **Esempio 1** *FieldName1 FieldName2 confronto*  
  
 `customer.cust_id = orders.cust_id`  
  
 **Esempio 2** *espressione di confronto FieldName*  
  
 `payments.amount >= 1000`  
  
 **Esempio 3** *confronto FieldName* tutte (*sottoquery*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Quando la condizione di filtro include tutti, il campo deve soddisfare la condizione di confronto per tutti i valori generati dalla sottoquery, prima di inclusa il proprio record nei risultati della query.  
  
 **Esempio 4** *confronto FieldName* ANY &#124; SOME (*sottoquery*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Quando la condizione di filtro include una o più, il campo deve soddisfare la condizione di confronto per almeno uno dei valori generati dalla sottoquery.  
  
 L'esempio seguente controlla se i valori nel campo sono all'interno di un determinato intervallo di valori:  
  
 **Esempio 5** *FieldName* [NOT] tra *Start_Range* AND *End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 Nell'esempio seguente verifica se almeno una riga soddisfa i criteri nella sottoquery. Quando la condizione di filtro include EXISTS, la condizione di filtro restituisce True (. T.), a meno che la sottoquery restituisce un set vuoto.  
  
 **Esempio 6** [NOT] esiste (*sottoquery*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **Esempio 7** *FieldName* [NOT] IN *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 Quando la condizione di filtro include IN, il campo deve contenere uno dei valori prima di inclusa il proprio record nei risultati della query.  
  
 **Esempio 8** *FieldName* [NOT] IN (*sottoquery*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 In questo caso il campo deve contenere uno dei valori restituiti dalla sottoquery, prima di inclusa il proprio record nei risultati della query.  
  
 **Esempio 9** *FieldName* [] operatore NOTLIKE *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 Questa condizione di filtro ricerca di ogni campo corrispondente *cExpression*. È possibile utilizzare il segno di percentuale (%) e caratteri jolly di sottolineatura (_) come parte della *cExpression*. Il carattere di sottolineatura rappresenta un singolo carattere sconosciuto nella stringa.  
  
 Clausola GROUP BY *GroupColumn* [, *GroupColumn* ...]  
 Raggruppa le righe nella query in base ai valori in una o più colonne. *GroupColumn* può essere uno dei seguenti:  
  
-   Il nome di un campo di tabella normale.  
  
-   Un campo che include una funzione di campo SQL.  
  
-   Un'espressione numerica che indica la posizione della colonna nella tabella dei risultati. (Il numero di colonna più a sinistra è 1).  
  
 VISTO *FilterCondition*  
 Specifica una condizione di filtro che i gruppi devono soddisfare per essere inclusi nei risultati della query. HAVING deve essere utilizzata con GROUP BY e può includere le condizioni di filtro desiderati, connessi tramite l'operatore AND o l'operatore OR. È anche possibile usare non per invertire il valore di un'espressione logica.  
  
 *FilterCondition* non può contenere una sottoquery.  
  
 Una clausola HAVING senza una clausola GROUP BY si comporta come una clausola WHERE. È possibile usare gli alias locali e funzioni di campi nella clausola HAVING. Usare una clausola WHERE per migliorare le prestazioni se la clausola HAVING non contiene funzioni alcun campo.  
  
 [[Totale] unione *SELECTCommand*]  
 Combina i risultati finali di uno selezionare con i risultati finali di selezionare un altro. Per impostazione predefinita, un'unione controlla i risultati combinati ed Elimina le righe duplicate. Usare le parentesi per combinare più clausole di unione.  
  
 UNIONE tutti impedisce eliminando le righe duplicate dai risultati combinati.  
  
 Le clausole UNION rispettare queste regole:  
  
-   È possibile usare UNION per combinare le sottoquery.  
  
-   Entrambi i comandi SELECT devono avere lo stesso numero di colonne nell'output query.  
  
-   Ogni colonna nei risultati della query SELECT uno deve avere lo stesso tipo di dati e la stessa larghezza della colonna corrispondente in altro selezionare.  
  
-   Solo l'istruzione SELECT finale può avere una clausola ORDER BY, che deve fare riferimento alle colonne di output tramite un numero. Se è inclusa una clausola ORDER BY, influisce sul risultato completo.  
  
 È anche possibile usare la clausola UNION per simulare un outer join.  
  
 Quando si crea un join due tabelle in una query, solo i record con valori corrispondenti nei campi unita tramite join sono inclusi nell'output. Se un record nella tabella padre non dispone di un record corrispondente della tabella figlio, il record nella tabella padre non è incluso nell'output. Un outer join consente di includere tutti i record nella tabella padre nell'output, insieme ai record corrispondenti nella tabella figlio. Per creare un outer join in Visual FoxPro, è necessario usare un comando SELECT annidato, come nell'esempio seguente:  
  
```  
SELECT customer.company, orders.order_id, orders.emp_id ;  
FROM customer, orders ;  
WHERE customer.cust_id = orders.cust_id ;  
UNION ;  
SELECT customer.company, 0, 0 ;  
FROM customer ;  
WHERE customer.cust_id NOT IN ;  
(SELECT orders.cust_id FROM orders)  
```  
  
> [!NOTE]  
>  Assicurarsi di includere lo spazio che precede immediatamente ogni punto e virgola. In caso contrario, si riceverà un errore.  
  
 La sezione del comando prima che la clausola UNION consente di selezionare i record da entrambe le tabelle che dispongono di valori corrispondenti. Le società dei clienti che non dispongono delle fatture associate non sono incluse. La sezione del comando dopo la clausola UNION consente di selezionare i record nella tabella customer che non dispongono dei record nella tabella orders corrispondenti.  
  
 Riguardanti la seconda sezione del comando, tenere presente quanto segue:  
  
-   L'istruzione SELECT tra parentesi viene elaborata per prima. Questa istruzione crea una selezione di tutti i numeri di cliente nella tabella orders.  
  
-   La clausola WHERE consente di trovare tutti i numeri di cliente nella tabella customer che non sono presenti nella tabella orders. Poiché la prima sezione del comando fornito tutte le società che ha un numero cliente nella tabella orders, tutte le società nella tabella customer sono ora inclusi nei risultati della query.  
  
-   Poiché le strutture delle tabelle incluse in un'unione devono essere identiche, esistono due segnaposto nella seconda istruzione SELECT per rappresentare *orders.order_id* e *orders.emp_id* dalla prima istruzione SELECT affermazione.  
  
    > [!NOTE]  
    >  I segnaposto devono essere dello stesso tipo di campi che rappresentano. Se il campo è un tipo date, deve essere il segnaposto {/ /}. Se il campo è un carattere, il segnaposto deve essere una stringa vuota ("").  
  
 ORDER BY *Order_Item* [ASC &#124; DESC] [, *Order_Item* [ASC &#124; DESC] ...]  
 Ordina i risultati della query in base ai dati in una o più colonne. Ciascuna *Order_Item* deve corrispondere a una colonna nei risultati della query e può essere uno dei seguenti:  
  
-   Campo in una tabella da cui è anche un elemento selezionato nella clausola SELECT principale (non in una sottoquery).  
  
-   Un'espressione numerica che indica la posizione della colonna nella tabella dei risultati. (La colonna più a sinistra è il numerica 1.)  
  
 Centro sicurezza di AZURE consente di specificare un ordine crescente per risultati di query, in base a ordine degli elementi ed è il valore predefinito per ORDER BY.  
  
 DESC specifica un ordine decrescente per i risultati della query.  
  
 Vengono visualizzati i risultati della query non ordinati se non si specifica un ordine con ORDER BY.  
  
## <a name="remarks"></a>Note  
 Selezionare è un comando SQL compilato in Visual FoxPro come qualsiasi altro comando di Visual FoxPro. Quando si utilizzano selezionare questa opzione per rappresentare una query, Visual FoxPro interpreta la query e recupera i dati specificati dalle tabelle. È possibile creare una query di selezione dalla finestra del prompt dei comandi o da un programma Visual FoxPro (come con qualsiasi altro comando di Visual FoxPro).  
  
> [!NOTE]  
>  Selezionare non rispetta la condizione di filtro corrente specificata con il filtro impostato.  
  
## <a name="driver-remarks"></a>Sezione Osservazioni di driver  
 Quando l'applicazione invia l'istruzione ODBC SQL SELECT per l'origine dati, il Driver ODBC Visual FoxPro converte il comando al comando selezionare Visual FoxPro senza conversione, a meno che il comando contiene una sequenza di escape ODBC. Gli elementi racchiusi tra parentesi una sequenza di escape ODBC vengono convertiti alla sintassi di Visual FoxPro. Per altre informazioni sull'utilizzo di ODBC sequenze di escape, vedere [funzioni data e ora](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md) e nella *riferimento per programmatori ODBC Microsoft*, vedere [sequenze di Escape in ODBC](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) .  
  
## <a name="see-also"></a>Vedere anche  
 [CREA TABELLA - SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL](../../odbc/microsoft/insert-sql-command.md)   
 [SET ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [SET ESATTO](../../odbc/microsoft/set-exact-command.md)
