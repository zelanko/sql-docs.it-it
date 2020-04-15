---
title: SELECT - Comando SQL Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 640189a5a31d0c21642b037e906bd6361690a9a5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300941"
---
# <a name="select---sql-command"></a>SELECT (comando SQL)
Recupera i dati da una o più tabelle.  
  
 Il driver ODBC di Visual FoxPro supporta la sintassi nativa del linguaggio Visual FoxPro per questo comando. Per informazioni specifiche del driver, vedere **Osservazioni del driver**.  
  
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
>  Una *sottoquery,* a cui si fa riferimento negli argomenti seguenti, è un'istruzione SELECT all'interno di un'istruzione SELECT e deve essere racchiusa tra parentesi. È possibile avere fino a due sottoquery allo stesso livello (non annidate) nella clausola WHERE. (Vedere quella sezione degli argomenti.) Le sottoquery possono contenere più condizioni di join.  
  
 [ALL &#124; DISTINCT]   [*Alias*.] *Select_Item* *[Column_Name*AS ] [,*[Alias*.] *Select_Item* *[Column_Name*AS ] ...]  
 La clausola SELECT specifica i campi, le costanti e le espressioni visualizzate nei risultati della query.  
  
 Per impostazione predefinita, ALL visualizza tutte le righe nei risultati della query.  
  
 DISTINCT esclude i duplicati di tutte le righe dai risultati della query.  
  
> [!NOTE]  
>  È possibile utilizzare DISTINCT una sola volta per ogni clausola SELECT.  
  
 *Alias*. qualifica i nomi degli articoli corrispondenti. Ogni elemento specificato con *Select_Item* genera una colonna dei risultati della query. Se due o più elementi hanno lo stesso nome, includere l'alias della tabella e un punto prima del nome dell'elemento per impedire la duplicazione delle colonne.  
  
 *Select_Item* specifica un elemento da includere nei risultati della query. Un elemento può essere uno dei seguenti:  
  
-   Nome di un campo di una tabella nella clausola FROM.  
  
-   Costante che specifica che lo stesso valore costante deve essere visualizzato in ogni riga dei risultati della query.  
  
-   Espressione che può essere il nome di una funzione definita dall'utente.  
  
 **Funzioni definite dall'utente con SELECTUser-Defined Functions with SELECT**  
  
 Sebbene l'utilizzo di funzioni definite dall'utente nella clausola SELECT presenti vantaggi evidenti, è necessario considerare anche le restrizioni seguenti:  
  
-   La velocità delle operazioni eseguite con SELECT potrebbe essere limitata dalla velocità di esecuzione di tali funzioni definite dall'utente. Le manipolazioni di volumi elevati che coinvolgono funzioni definite dall'utente potrebbero essere eseguite meglio utilizzando API e funzioni definite dall'utente scritte in linguaggio C o assembly.  
  
-   L'unico modo affidabile per passare valori alle funzioni definite dall'utente richiamate da SELECT è tramite l'elenco di argomenti passato alla funzione quando viene richiamata.  
  
-   Anche se si sperimenta e scoprire una manipolazione apparentemente proibita che funziona correttamente in una certa versione di FoxPro, non vi è alcuna garanzia che continuerà a funzionare nelle versioni successive.  
  
 Oltre a queste restrizioni, le funzioni definite dall'utente sono accettabili nella clausola SELECT. Tuttavia, tenere presente che l'utilizzo di SELECT potrebbe rallentare le prestazioni.  
  
 Le seguenti funzioni di campo sono disponibili per l'utilizzo con un elemento selezionato che sia un campo o un'espressione che coinvolge un campo:  
  
-   AVG(*Select_Item*)-Medie una colonna di dati numerici.  
  
-   COUNT(*Select_Item*)-Conta il numero di elementi selezionati in una colonna. CONTA.  
  
-   MIN(*Select_Item*)-Determina il valore più piccolo di *Select_Item* in una colonna.  
  
-   MAX(*Select_Item*)-Determina il valore più grande di *Select_Item* in una colonna.  
  
-   *SOMMA(Select_Item*)-Totalisce una colonna di dati numerici.  
  
 Non è possibile nidificare funzioni di campo.  
  
 COLUMN_NAME *Column_Name* AS  
 Specifica l'intestazione di una colonna nell'output della query. Ciò è utile quando *Select_Item* è un'espressione o contiene una funzione di campo e si desidera assegnare alla colonna un nome significativo. *Column_Name* può essere un'espressione ma non può contenere caratteri (ad esempio, spazi) non consentiti nei nomi dei campi di tabella.  
  
 FROM [*NomeDatabase*!] *Tabella* [*Local_Alias*] [, [*NomeDatabase*!] *Tabella* [*Local_Alias*] ...]  
 Elenca le tabelle che contengono i dati recuperati dalla query. Se non è aperta alcuna tabella, In Visual FoxPro viene visualizzata la finestra di dialogo **Apri** in modo che sia possibile specificare il percorso del file. Dopo l'apertura, la tabella rimane aperta al termine della query.  
  
 *DatabaseName*! specifica il nome di un database diverso da quello specificato con l'origine dati. È necessario includere il nome del database che contiene la tabella se il database non è specificato con l'origine dati. Includere il delimitatore punto esclamativo (!) dopo il nome del database e prima del nome della tabella.  
  
 *Local_Alias* specifica un nome temporaneo per la tabella denominata in *Tabella*. Se si specifica un alias locale, è necessario utilizzare l'alias locale anziché il nome della tabella in tutta l'istruzione SELECT. L'alias locale non influisce sull'ambiente Visual FoxPro.  
  
 WHERE *JoinCondition* [And *JoinCondition* ...]    [E &#124; OR *FilterCondition* [E &#124; OR *FilterCondition* ...]]  
 Indica a Visual FoxPro di includere solo determinati record nei risultati della query. WHERE è necessario per recuperare i dati da più tabelle.  
  
 *JoinCondition* specifica i campi che collegano le tabelle nella clausola FROM. Se si include più di una tabella in una query, è necessario specificare una condizione di join per ogni tabella dopo la prima.  
  
> [!IMPORTANT]  
>  Quando si creano condizioni di join, tenere presenti le informazioni seguenti:Consider the following information when you create join conditions:  
  
-   Se si includono due tabelle in una query e non si specifica una condizione di join, ogni record nella prima tabella viene unito in join a ogni record della seconda tabella, purché vengano soddisfatte le condizioni di filtro. Una query di questo tipo può produrre risultati lunghi.  
  
-   Prestare attenzione quando si uniscono tabelle con campi vuoti perché Visual FoxPro corrisponde a campi vuoti. Ad esempio, se si partecipa a CUSTOMER. CAP e INVOICE. CAP e se CUSTOMER contiene 100 codici postali vuoti e INVOICE contiene 400 codici postali vuoti, l'output della query contiene 40.000 record aggiuntivi risultanti dai campi vuoti. Utilizzare la funzione **EMPTY( )** per eliminare i record vuoti dall'output della query.  
  
-   È necessario utilizzare l'operatore AND per connettere più condizioni di join. Ogni condizione di join ha il seguente formato:  
  
     *NomeCampo1 Confronto NomeCampo2*  
  
     *NomeCampo1* è il nome di un campo di una tabella, *NomeCampo2* è il nome di un campo di un'altra tabella e *Confronto* è uno degli operatori descritti nella tabella seguente.  
  
|Operatore|Confronto|  
|--------------|----------------|  
|=|Uguale|  
|==|Esattamente uguale|  
|LIKE|SQL LIKE|  
|<>, ! #|Diverso da|  
|>|Più di|  
|>=|Più o uguale a|  
|<|Minore di|  
|<=|Minore o uguale a|  
  
 Quando si utilizza l'operatore s con le stringhe, agisce in modo diverso, a seconda dell'impostazione di SET ANSI. Quando set ANSI è impostato su OFF, Visual FoxPro considera i confronti tra stringhe in modo familiare agli utenti Xbase. Quando SET ANSI è impostato su ON, Visual FoxPro segue gli standard ANSI per i confronti tra stringhe. Vedere [SET ANSI](../../odbc/microsoft/set-ansi-command.md) e [SET EXACT](../../odbc/microsoft/set-exact-command.md) per ulteriori informazioni su come Visual FoxPro esegue confronti tra stringhe.  
  
 *FilterCondition* specifica i criteri che i record devono soddisfare per essere inclusi nei risultati della query. È possibile includere in una query tutte le condizioni di filtro desiderate, connettendole con l'operatore AND o OR. È inoltre possibile utilizzare l'operatore NOT per invertire il valore di un'espressione logica oppure **EMPTY( )** per verificare la presenza di un campo vuoto. *FilterCondition* può assumere uno qualsiasi dei form negli esempi seguenti:  
  
 **Esempio 1** *NomeCampo1 Confronto NomeCampo2*  
  
 `customer.cust_id = orders.cust_id`  
  
 **Esempio 2** *Espressione di confronto NomeCampoExample* 2 FieldName Comparison Expression  
  
 `payments.amount >= 1000`  
  
 **Esempio 3** *Confronto nome campo* ALL (*Sottoquery*)  
  
 `company < ALL ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Quando la condizione di filtro include TUTTI, il campo deve soddisfare la condizione di confronto per tutti i valori generati dalla sottoquery prima che il relativo record venga incluso nei risultati della query.  
  
 **Esempio 4** *Confronto dei nomi dei* campi QUALSIASI &#124; SOME (*Sottoquery*)  
  
 `company < ANY ;`  
  
 `(SELECT company FROM customer WHERE country = "USA")`  
  
 Quando la condizione di filtro include ANY o SOME, il campo deve soddisfare la condizione di confronto per almeno uno dei valori generati dalla sottoquery.  
  
 L'esempio seguente verifica se i valori nel campo sono compresi in un intervallo di valori specificato:  
  
 **Esempio 5** *NomeCampo* [NOT] BETWEEN *Start_Range* E *End_Range*  
  
 `customer.postalcode BETWEEN 90000 AND 99999`  
  
 Nell'esempio seguente viene verificato se almeno una riga soddisfa i criteri nella sottoquery. Quando la condizione di filtro include EXISTS, la condizione di filtro restituisce True (. T.) a meno che la sottoquery non restituisca il set vuoto.  
  
 **Esempio 6** [NOT] EXISTS (*Sottoquery*)  
  
 `EXISTS ;`  
  
 `(SELECT * FROM orders WHERE customer.postalcode =`  
  
 `orders.postalcode)`  
  
 **Esempio 7** *NomeCampo* [NOT] IN *Value_Set*  
  
 `customer.postalcode NOT IN ("98052","98072","98034")`  
  
 Quando la condizione di filtro include IN, il campo deve contenere uno dei valori prima che il relativo record venga incluso nei risultati della query.  
  
 **Esempio 8** *NomeCampo* [NOT] IN (*Sottoquery*)  
  
 `customer.cust_id IN ;`  
  
 `(SELECT orders.cust_id FROM orders WHERE orders.city="Seattle")`  
  
 In questo caso il campo deve contenere uno dei valori restituiti dalla sottoquery prima che il relativo record venga incluso nei risultati della query.  
  
 **Esempio 9** *NomeCampo* [NOT] LIKE *cExpression*  
  
 `customer.country NOT LIKE "USA"`  
  
 Questa condizione di filtro cerca ogni campo che corrisponde a *cExpression*. È possibile utilizzare il segno di percentuale (%) e caratteri jolly di sottolineatura ( _ ) come parte di *cExpression*. Il carattere di sottolineatura rappresenta un singolo carattere sconosciuto nella stringa.  
  
 GROUP BY *GroupColumn* [, *ColonnaGruppo* ...]  
 Raggruppa le righe della query in base ai valori di una o più colonne. *GroupColumn* può essere uno dei seguenti:  
  
-   Nome di un campo tabella normale.  
  
-   Campo che include una funzione di campo SQL.  
  
-   Espressione numerica che indica la posizione della colonna nella tabella dei risultati. (Il numero di colonna più a sinistra è 1.)  
  
 HAVING *FilterCondition*  
 Specifica una condizione di filtro che i gruppi devono soddisfare per essere inclusi nei risultati della query. HAVING deve essere utilizzato con GROUP BY e può includere tutte le condizioni di filtro desiderate, collegate dall'operatore AND o OR. È inoltre possibile utilizzare NOT per invertire il valore di un'espressione logica.  
  
 *FilterCondition* non può contenere una sottoquery.  
  
 Una clausola HAVING senza una clausola GROUP BY si comporta come una clausola WHERE. È possibile utilizzare alias locali e funzioni di campo nella clausola HAVING. Utilizzare una clausola WHERE per prestazioni più veloci se la clausola HAVING non contiene funzioni di campo.  
  
 [UNION [ALL] *SELECTCommand*]  
 Combina i risultati finali di un'istruzione SELECT con i risultati finali di un'altra istruzione SELECT. Per impostazione predefinita, UNION controlla i risultati combinati ed elimina le righe duplicate. Utilizzare le parentesi per combinare più clausole UNION.  
  
 ALL impedisce a UNION di eliminare le righe duplicate dai risultati combinati.  
  
 Le clausole UNION seguono queste regole:  
  
-   Non è possibile utilizzare UNION per combinare sottoquery.  
  
-   Entrambi i comandi SELECT devono avere lo stesso numero di colonne nell'output della query.  
  
-   Ogni colonna nei risultati della query di un'istruzione SELECT deve avere lo stesso tipo di dati e la stessa larghezza della colonna corrispondente nell'altra istruzione SELECT.  
  
-   Solo l'istruzione SELECT finale può avere una clausola ORDER BY, che deve fare riferimento alle colonne di output per numero. Se viene inclusa una clausola ORDER BY, influisce sul risultato completo.  
  
 È inoltre possibile utilizzare la clausola UNION per simulare un outer join.  
  
 Quando si uniscono due tabelle in una query, nell'output vengono inclusi solo i record con valori corrispondenti nei campi di join. Se un record nella tabella padre non dispone di un record corrispondente nella tabella figlio, il record nella tabella padre non viene incluso nell'output. Un outer join consente di includere tutti i record nella tabella padre nell'output, insieme ai record corrispondenti nella tabella figlio. Per creare un outer join in Visual FoxPro, è necessario utilizzare un comando SELECT annidato, come nell'esempio seguente:  
  
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
  
 La sezione del comando prima della clausola UNION seleziona i record da entrambe le tabelle con valori corrispondenti. Le società cliente a cui non sono associate fatture non sono incluse. La sezione del comando dopo la clausola UNION seleziona i record nella tabella customer che non dispongono di record corrispondenti nella tabella orders.  
  
 Per quanto riguarda la seconda sezione del comando, notare quanto segue:  
  
-   L'istruzione SELECT all'interno delle parentesi viene elaborata per prima. Questa istruzione crea una selezione di tutti i numeri cliente nella tabella orders.  
  
-   La clausola WHERE trova tutti i numeri cliente nella tabella customer che non sono presenti nella tabella orders. Poiché la prima sezione del comando ha fornito tutte le società che avevano un numero cliente nella tabella orders, tutte le società nella tabella customer sono ora incluse nei risultati della query.  
  
-   Poiché le strutture delle tabelle incluse in un'UNIONE devono essere identiche, nella seconda istruzione SELECT sono presenti due segnaposto per rappresentare *orders.order_id* e *orders.emp_id* dalla prima istruzione SELECT.  
  
    > [!NOTE]  
    >  I segnaposto devono essere dello stesso tipo dei campi che rappresentano. Se il campo è un tipo di data, il segnaposto deve essere . Se il campo è un campo di caratteri, il segnaposto deve essere la stringa vuota ("").  
  
 ORDER BY *Order_Item* [ASC &#124; DESC] [, *Order_Item* [ASC &#124; DESC] ...]  
 Ordina i risultati della query in base ai dati di una o più colonne. Ogni *Order_Item* deve corrispondere a una colonna nei risultati della query e può essere una delle seguenti:  
  
-   Un campo in una tabella FROM che è anche un elemento selezionato nella clausola SELECT principale (non in una sottoquery).  
  
-   Espressione numerica che indica la posizione della colonna nella tabella dei risultati. (La colonna più a sinistra è il numero 1.)  
  
 ASC specifica un ordine crescente per i risultati della query, in base all'elemento o agli elementi dell'ordine, ed è l'impostazione predefinita per ORDER BY.  
  
 DESC specifica un ordine decrescente per i risultati della query.  
  
 I risultati della query vengono visualizzati non ordinati se non si specifica un ordine con ORDER BY.  
  
## <a name="remarks"></a>Osservazioni  
 SELECT è un comando SQL integrato in Visual FoxPro come qualsiasi altro comando di Visual FoxPro. Quando si utilizza SELECT per eseguire una query, Visual FoxPro interpreta la query e recupera i dati specificati dalle tabelle. È possibile creare una query SELECT dalla finestra del prompt dei comandi o da un programma Visual FoxPro (come con qualsiasi altro comando Visual FoxPro).  
  
> [!NOTE]  
>  SELECT non rispetta la condizione di filtro corrente specificata con SET FILTER.  
  
## <a name="driver-remarks"></a>Osservazioni del conducente  
 Quando l'applicazione invia l'istruzione SQL ODBC SELECT all'origine dati, il driver ODBC di Visual FoxPro converte il comando nel comando Select di Visual FoxPro senza conversione, a meno che il comando non contenga una sequenza di escape ODBC. Gli elementi racchiusi in una sequenza di escape ODBC vengono convertiti nella sintassi di Visual FoxPro. Per ulteriori informazioni sull'utilizzo delle sequenze di escape ODBC, vedere [Funzioni di data e ora e data](../../odbc/microsoft/time-and-date-functions-visual-foxpro-odbc-driver.md) e in Microsoft ODBC *Programmer's Reference*, vedere [Sequenze](../../odbc/reference/develop-app/escape-sequences-in-odbc.md)di escape in ODBC .  
  
## <a name="see-also"></a>Vedere anche  
 [CREA TABELLA - SQLCREATE TABLE - SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT - SQL](../../odbc/microsoft/insert-sql-command.md)   
 [IMPOSTARE ANSI](../../odbc/microsoft/set-ansi-command.md)   
 [IMPOSTA ESATTO](../../odbc/microsoft/set-exact-command.md)
