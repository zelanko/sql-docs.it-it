---
title: 'Appendice B: Tabelle della transizione di stato ODBC | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 82c19931073aa96eb045f574e8670068f3d3c659
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026940"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>Appendice B: Tabelle della transizione di stato ODBC
Le tabelle in questa appendice mostrano come funzioni ODBC causano le transizioni di ambiente, connessione, istruzione e gli stati del descrittore. Lo stato dell'ambiente, connessione, istruzione o descrittore determina in genere quando le funzioni che usano il corrispondente tipo di handle (ambiente, connessione, istruzione o descrittore) possono essere chiamate. Gli stati di ambiente, connessione, istruzione e descrittore si sovrappongono all'incirca, come illustrato nelle figure seguenti. Ad esempio, la sovrapposizione esatta della connessione stati C5 e C6 e istruzione dichiara che s1 tramite S12 sono dati dipende dall'origine, poiché le transazioni iniziano in momenti diversi in origini dati diverse e lo stato di descrittore D1i (allocato in modo implicito descrittore) dipende dal sullo stato dell'istruzione a cui il descrittore è associato, mentre state D1e (allocato in modo esplicito descrittore) è indipendenti dallo stato di qualsiasi istruzione. Per una descrizione di ogni stato, vedere [transizioni di ambiente](../../../odbc/reference/appendixes/environment-transitions.md), [transizioni di connessione](../../../odbc/reference/appendixes/connection-transitions.md), [transizioni di istruzione](../../../odbc/reference/appendixes/statement-transitions.md), e [transizioni dei descrittori ](../../../odbc/reference/appendixes/descriptor-transitions.md), più avanti in questa appendice.  
  
 Gli stati di connessione e dell'ambiente si sovrappongono nel modo seguente:  
  
 ![Sovrapposizione degli stati di connessione e dell'ambiente](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 Gli stati di connessione e l'informativa si sovrappongono nel modo seguente:  
  
 ![Sovrapposizione degli stati di connessione e l'informativa](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 Gli stati di istruzione e descrittore si sovrappongono nel modo seguente:  
  
 ![Sovrapposizione degli stati di istruzione e descrittore](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 Gli stati di connessione e descrittore si sovrappongono nel modo seguente:  
  
 ![Sovrapposizione degli stati di connessione e descrittore](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 Ogni voce in una tabella di transizione può essere uno dei valori seguenti:  
  
-   **--** -Lo stato rimane invariato dopo l'esecuzione della funzione.  
  
-   **E**  

     **_n_**  , **C_n_** , **S_n_** , oppure **D_n_** -lo stato di ambiente, connessione, istruzione o descrittore passa allo stato specificato.  
 
-   **(IH)**  -È stato passato un handle non valido alla funzione. Ad esempio, se l'handle è un handle null oppure un handle valido del tipo errato - è stato passato un handle di connessione quando un handle di istruzione è stata necessario: la funzione non restituisca SQL_INVALID_HANDLE; in caso contrario, il comportamento è indefinito e probabilmente irreversibile. Questo errore viene visualizzato solo quando è il risultato della chiamata alla funzione nello stato specificato solo possibile. Questo errore non modifica lo stato e viene sempre rilevato da Gestione Driver, come indicato dalla parentesi.  
  
-   **NS** -lo stato successivo. La transizione di istruzione è lo stesso come se l'istruzione non ha esaminato gli stati asincroni. Ad esempio, si supponga che un'istruzione che crea un set di risultati entra nello stato S11 dallo stato S1, poiché **SQLExecDirect** restituito SQL_STILL_EXECUTING. La notazione NS nello stato S11 significa che le transizioni per l'istruzione sono identici a quelli per un'istruzione nello stato S1 che viene creato un set di risultati. Se **SQLExecDirect** restituisce un errore, l'istruzione rimane nello stato S1; se ha esito positivo, l'istruzione passa allo stato S5; se necessita di dati, l'istruzione passa allo stato S8; e se è ancora in esecuzione, rimane nello stato S11.  

-   **_XXXXX_**  oppure **(*XXXXX*)** : un valore SQLSTATE è correlata alla tabella delle transizioni; SQLSTATE rilevati da Gestione Driver sono racchiusi tra parentesi. La funzione ha restituito SQL_ERROR e il valore SQLSTATE specificato, ma non modifica lo stato. Ad esempio, se **SQLExecute** viene chiamato prima **SQLPrepare**, restituisce SQLSTATE HY010 (funzione di errore nella sequenza).  

> [!NOTE]  
>  Le tabelle non vengono visualizzati gli errori non correlati alle tabelle che non modificano lo stato di transizione. Ad esempio, quando **SQLAllocHandle** viene chiamato nello stato di ambiente E1 e restituisce SQLSTATE HY001 (errore di allocazione della memoria), l'ambiente rimane nello stato E1; ciò non è indicato nella tabella delle transizioni di ambiente per  **SQLAllocHandle**.  
  
 Se l'ambiente, connessione, istruzione o descrittore possa spostare in più di uno stato, viene visualizzato ogni possibile stato e uno o più piè di pagina illustrano le condizioni in cui ogni transizione ha luogo. Le note seguenti possono essere in qualsiasi tabella.  
  
|Piè di pagina|Significato|  
|--------------|-------------|  
|b|Prima o dopo. Il cursore era posizionato prima dell'inizio del set di risultati o dopo la fine del set di risultati.|  
|c|Funzione corrente. L'esecuzione della funzione corrente in modo asincrono.|  
|d|Dati necessari. La funzione ha restituito SQL_NEED_DATA.|  
|e|Errore. La funzione ha restituito SQL_ERROR.|  
|i|Riga non valida. È stato posizionato il cursore su una riga nel risultato del set e la riga è stati eliminati o si è verificato un errore in un'operazione sulla riga. Se la matrice di stato di riga esistente, il valore della matrice di stato di riga per la riga è SQL_ROW_DELETED o SQL_ROW_ERROR. (La matrice di stato di riga a cui punta l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR.)|  
|nf|Non è stato trovato. La funzione ha restituito SQL_NO_DATA. Questo non è applicabile quando **SQLExecDirect**, **SQLExecute**, o **SQLParamData** restituisce SQL_NO_DATA dopo l'esecuzione di una ricerca istruzione update o delete.|  
|np|Non è pronto. L'istruzione non è stato preparato.|  
|nr|Nessun risultato. L'istruzione non fornirà o non è stato creato un set di risultati.|  
|o|Altra funzione. Un'altra funzione era in esecuzione in modo asincrono.|  
|p|Preparati. L'istruzione è stata preparata.|  
|r|Risultati. L'istruzione verrà o è stato creato un set di risultati (eventualmente vuota).|  
|s|Esito positivo. La funzione ha restituito SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.|  
|v|Riga valida. Il cursore è posizionato in una riga nel set di risultati e la riga era stata inserita correttamente, è stato aggiornato, o un'altra operazione sulla riga era stata completata correttamente. Se la matrice di stato di riga esistente, il valore della matrice di stato di riga per la riga è stata SQL_ROW_ADDED, SQL_ROW_SUCCESS o SQL_ROW_UPDATED. (La matrice di stato di riga a cui punta l'attributo di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR.)|  
|x|In esecuzione. La funzione restituita SQL_STILL_EXECUTING.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 In questo esempio, la riga di transizione ambiente table per **SQLFreeHandle** quando *HandleType* SQL_HANDLE_ENV è come indicato di seguito.  
  
|E0<br /><br /> Non allocato|E1<br /><br /> allocato|E2<br /><br /> Connessione|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|(HY010)|  
  
 Se **SQLFreeHandle** viene chiamato con stato ambiente E0 *HandleType* impostato su SQL_HANDLE_ENV, gestione Driver non restituisca SQL_INVALID_HANDLE. Se viene chiamato con stato E1 *HandleType* impostato su SQL_HANDLE_ENV, l'ambiente passa allo stato E0 se la funzione ha esito positivo e rimane nello stato E1 se la funzione ha esito negativo. Se viene chiamato con stato E2 *HandleType* impostato su SQL_HANDLE_ENV, gestione Driver sempre restituisce SQL_ERROR e SQLSTATE HY010 (funzione di errore nella sequenza) e l'ambiente rimane nello stato E2.  
  
 Per comprendere le tabelle della transizione di stato, è necessario comprendere quale elemento (ambiente, connessione, istruzione o descrittore) fanno riferimento. Si supponga che una funzione accetta l'handle di un elemento di tipo X. Tabella delle transizioni di stato X per tale funzione viene descritta la funzione, con l'handle di un elemento di tipo X, influisce su tale elemento come chiamante. Ad esempio, **SQLDisconnect** accetta un handle di connessione. La tabella di transizione dello stato di connessione per **SQLDisconnect** viene descritto come **SQLDisconnect** influisce sullo stato della connessione per il quale viene chiamato.  
  
 Si supponga che una funzione accetta l'handle di un elemento di tipo Y, in cui non è uguale a X Y. Tabella delle transizioni di stato X per tale funzione viene descritto come chiamata di funzione, con un handle di tipo X che è associato l'elemento di tipo Y, interessa l'elemento di tipo Y. Ad esempio, l'istruzione transizione tabella di stato per **SQLDisconnect** viene descritto come **SQLDisconnect** influisce sullo stato di un'istruzione quando viene chiamato con l'handle della connessione con il quale il l'istruzione è associato.  
  
 In questa appendice contiene gli argomenti seguenti.  
  
-   [Transizioni di ambiente](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [Transizioni di connessione](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [Transizioni di istruzione](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [Transizioni dei descrittori](../../../odbc/reference/appendixes/descriptor-transitions.md)
