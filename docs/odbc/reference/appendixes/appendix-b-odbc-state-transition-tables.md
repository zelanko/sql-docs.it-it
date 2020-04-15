---
title: 'Appendice B: Tabelle di transizione dello stato ODBC Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db20c492ababbe6bf8f065fce88067c643f2694d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302885"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>Appendice B: Tabelle della transizione di stato ODBC
Le tabelle in questa appendice mostrano come le funzioni ODBC causano le transizioni dell'ambiente, connessione, istruzione e stati descrittore. Lo stato dell'ambiente, della connessione, dell'istruzione o del descrittore determina in genere quando è possibile chiamare funzioni che utilizzano il tipo corrispondente di handle (ambiente, connessione, istruzione o descrittore). Gli stati di ambiente, connessione, istruzione e descrittore si sovrappongono approssimativamente come illustrato nelle figure seguenti. Ad esempio, l'esatta sovrapposizione degli stati di connessione C5 e C6 e degli stati di istruzione da S1 a S12 dipende dall'origine dati, poiché le transazioni iniziano in momenti diversi su origini dati diverse e lo stato del descrittore D1i (descrittore allocato in modo implicito) dipende dallo stato dell'istruzione a cui è associato il descrittore, mentre lo stato D1e (descrittore allocato in modo esplicito) è indipendente dallo stato di qualsiasi istruzione. Per una descrizione di ogni stato, vedere [Transizioni di ambiente](../../../odbc/reference/appendixes/environment-transitions.md), [Transizioni di connessione](../../../odbc/reference/appendixes/connection-transitions.md), Transizioni di istruzioni e [Transizioni](../../../odbc/reference/appendixes/statement-transitions.md) [descrittore](../../../odbc/reference/appendixes/descriptor-transitions.md), più avanti in questa appendice.  
  
 Gli stati dell'ambiente e della connessione si sovrappongono come segue:  
  
 ![Sovrapposizione degli stati della connessione e dell'ambiente](../../../odbc/reference/appendixes/media/app01.gif "app01 (app)")  
  
 Gli stati di connessione e istruzione si sovrappongono come segue:  
  
 ![Sovrapposizione degli stati della connessione e dell'istruzione](../../../odbc/reference/appendixes/media/app02.gif "app02 (app)")  
  
 Gli stati dell'istruzione e del descrittore si sovrappongono come segue:  
  
 ![Sovrapposizione degli stati del descrittore e dell'istruzione](../../../odbc/reference/appendixes/media/app03.gif "app03 (app)")  
  
 Gli stati di connessione e descrittore si sovrappongono come segue:  
  
 ![Sovrapposizione degli stati del descrittore e della connessione](../../../odbc/reference/appendixes/media/app04.gif "app04 (app)")  
  
 Ogni voce di una tabella di transizione può essere uno dei seguenti valori:  
  
-   **--**-Lo stato non viene modificato dopo l'esecuzione della funzione.  
  
-   **E (in questo modo**  

     **_n_** , **C_n_**, **S_n_ o** **D_n_** - Lo stato dell'ambiente, della connessione, dell'istruzione o del descrittore passa allo stato specificato.  
 
-   **(IH)** - Alla funzione è stato passato un handle non valido. Se l'handle è un handle null o un handle valido del tipo errato, ad esempio un handle di connessione è stato superato quando è stato richiesto un handle di istruzione, la funzione restituisce SQL_INVALID_HANDLE; in caso contrario, il comportamento non è definito e probabilmente fatale. Questo errore viene visualizzato solo quando è l'unico risultato possibile della chiamata della funzione nello stato specificato. Questo errore non modifica lo stato e viene sempre rilevato da Gestione Driver, come indicato dalle parentesi.  
  
-   **NS** - Stato successivo. La transizione dell'istruzione è la stessa come se l'istruzione non fosse passata attraverso gli stati asincroni. Si supponga, ad esempio, che un'istruzione che crea un set di risultati entri nello stato S11 dallo stato S1 perché **SQLExecDirect** ha restituito SQL_STILL_EXECUTING. La notazione NS nello stato S11 significa che le transizioni per l'istruzione sono le stesse di quelle per un'istruzione nello stato S1 che crea un set di risultati. Se **SQLExecDirect** restituisce un errore, l'istruzione rimane nello stato S1; se ha esito positivo, l'istruzione passa allo stato S5; se sono necessari dati, l'istruzione passa allo stato S8; e se è ancora in esecuzione, rimane nello stato S11.  

-   **_XXXXX_** o **(*XXXXX*)** - UN SQLSTATE correlato alla tabella di transizione; SQLSTATEs rilevati da Gestione Driver sono racchiusi tra parentesi. La funzione ha restituito SQL_ERROR e il sqlSTATE specificato, ma lo stato non cambia. Ad esempio, se **SQLExecute** viene chiamato prima di **SQLPrepare**, restituisce SQLSTATE HY010 (errore di sequenza di funzioni).  

> [!NOTE]  
>  Le tabelle non mostrano errori non correlati alle tabelle di transizione che non modificano lo stato. Ad esempio, quando **SQLAllocHandle** viene chiamato nello stato di ambiente E1 e restituisce SQLSTATE HY001 (errore di allocazione della memoria), l'ambiente rimane nello stato E1; ciò non viene visualizzato nella tabella di transizione dell'ambiente per **SQLAllocHandle**.  
  
 Se l'ambiente, la connessione, l'istruzione o il descrittore possono passare a più di uno stato, viene visualizzato ogni stato possibile e una o più note a piè di pagina spiegano le condizioni in cui avviene ogni transizione. Le seguenti note a piè di pagina possono essere visualizzate in qualsiasi tabella.  
  
|Nota|Significato|  
|--------------|-------------|  
|b|Prima o dopo. Il cursore è stato posizionato prima dell'inizio del set di risultati o dopo la fine del set di risultati.|  
|c|Funzione corrente. La funzione corrente era in esecuzione in modo asincrono.|  
|d|Hai bisogno di dati. La funzione ha restituito SQL_NEED_DATA.|  
|e|Errore. La funzione ha restituito SQL_ERROR.|  
|i|Riga non valida. Il cursore è stato posizionato su una riga nel set di risultati e la riga è stata eliminata o si è verificato un errore in un'operazione sulla riga. Se la matrice di stato della riga esisteva, il valore nella matrice di stato della riga è stato SQL_ROW_DELETED o SQL_ROW_ERROR. La matrice di stato della riga fa riferimento all'attributo statement SQL_ATTR_ROW_STATUS_PTR.|  
|nf|Non trovato. La funzione ha restituito SQL_NO_DATA. Ciò non si applica quando **SQLExecDirect**, **SQLExecute**o **SQLParamData** restituisce SQL_NO_DATA dopo l'esecuzione di un'istruzione searched update o delete .|  
|np|Non preparato. La dichiarazione non è stata preparata.|  
|nr|Nessun risultato. L'istruzione non creerà o non creerà un set di risultati.|  
|o|Altra funzione. Un'altra funzione era l'esecuzione in modo asincrono.|  
|p|Preparato. La dichiarazione è stata preparata.|  
|r|Risultati. L'istruzione creerà o ha creato un set di risultati (eventualmente vuoto).|  
|s|Esito positivo. La funzione ha restituito SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.|  
|v|Riga valida. Il cursore è stato posizionato su una riga nel set di risultati e la riga è stata inserita, aggiornata correttamente o un'altra operazione sulla riga è stata completata correttamente. Se la matrice di stato della riga esisteva, il valore nella matrice di stato della riga è stato SQL_ROW_ADDED, SQL_ROW_SUCCESS o SQL_ROW_UPDATED. La matrice di stato della riga fa riferimento all'attributo statement SQL_ATTR_ROW_STATUS_PTR.|  
|x|In esecuzione. La funzione ha restituito SQL_STILL_EXECUTING.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 In questo esempio, la riga nella tabella di transizione dello stato dell'ambiente per **SQLFreeHandle** quando *HandleType* è SQL_HANDLE_ENV è la seguente.  
  
|E0 (in questo stato del sistema<br /><br /> Non allocato|E1<br /><br /> Allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0 (in questo stato del sistema|(HY010)|  
  
 Se **SQLFreeHandle** viene chiamato nello stato dell'ambiente E0 con *HandleType* impostato su SQL_HANDLE_ENV, Gestione Driver restituisce SQL_INVALID_HANDLE. Se viene chiamato nello stato E1 con *HandleType* impostato su SQL_HANDLE_ENV, l'ambiente passa allo stato E0 se la funzione ha esito positivo e rimane nello stato E1 se la funzione ha esito negativo. Se viene chiamato nello stato E2 con *HandleType* impostato su SQL_HANDLE_ENV, Gestione Driver restituisce sempre SQL_ERROR e SQLSTATE HY010 (errore di sequenza di funzione) e l'ambiente rimane nello stato E2.  
  
 Per comprendere le tabelle di transizione dello stato, è necessario comprendere a quale elemento (ambiente, connessione, istruzione o descrittore) fanno riferimento. Si supponga che una funzione accetti l'handle di un elemento di tipo X. La tabella di transizione dello stato X per tale funzione descrive come la chiamata della funzione, con l'handle di un elemento di tipo X, influisce su tale elemento. Ad esempio, **SQLDisconnect** accetta un handle di connessione. La tabella di transizione dello stato della connessione per **SQLDisconnect** descrive come **SQLDisconnect** influisce sullo stato della connessione per cui viene chiamato.  
  
 Si supponga che una funzione accetti l'handle di un elemento di tipo Y, dove Y non è uguale a X. La tabella di transizione dello stato X per tale funzione descrive come la chiamata della funzione, con un handle di tipo X associato all'elemento di tipo Y, influisce sull'elemento di tipo Y. Ad esempio, la tabella di transizione dello stato dell'istruzione per **SQLDisconnect** descrive come **SQLDisconnect** influisce sullo stato di un'istruzione quando viene chiamato con l'handle della connessione a cui è associata l'istruzione.  
  
 Questa appendice contiene i seguenti argomenti.  
  
-   [Transizioni di ambiente](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [Transizioni di connessione](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [Transizioni di istruzione](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [Transizioni dei descrittori](../../../odbc/reference/appendixes/descriptor-transitions.md)
