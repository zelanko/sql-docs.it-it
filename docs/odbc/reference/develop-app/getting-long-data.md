---
title: Recupero di dati long Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: da901c22eb26af063397b4af184179ebe5c75924
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298991"
---
# <a name="getting-long-data"></a>Recupero di dati Long
I DBS definiscono i *dati long* come qualsiasi carattere o dati binari di una determinata dimensione, ad esempio 255 caratteri. Questi dati possono essere sufficientemente piccoli da essere archiviati in un singolo buffer, ad esempio una descrizione di parte di diverse migliaia di caratteri. Tuttavia, potrebbe essere troppo lungo per essere archiviato in memoria, ad esempio documenti di testo lunghi o bitmap. Poiché tali dati non possono essere archiviati in un singolo buffer, vengono recuperati dal driver in parti con **SQLGetData** dopo il recupero degli altri dati nella riga.  
  
> [!NOTE]  
>  Un'applicazione può effettivamente recuperare qualsiasi tipo di dati con **SQLGetData**, non solo dati lunghi, anche se solo i dati di tipo carattere e binario possono essere recuperati in parti. Tuttavia, se i dati sono sufficientemente piccoli da essere contenuti in un singolo buffer, non vi è in genere alcun motivo per utilizzare **SQLGetData**. È molto più semplice associare un buffer alla colonna e lasciare che il driver restituisca i dati nel buffer.  
  
 Per recuperare dati lunghi da una colonna, un'applicazione chiama innanzitutto **SQLFetchScroll** o **SQLFetch** per spostarsi in una riga e recuperare i dati per le colonne associate. L'applicazione chiama quindi **SQLGetData**. **SQLGetData** ha gli stessi argomenti di **SQLBindCol:** un handle di istruzione; un numero di colonna; il tipo di dati C, l'indirizzo e la lunghezza in byte di una variabile di applicazione; e l'indirizzo di un buffer di lunghezza/indicatore. Entrambe le funzioni hanno gli stessi argomenti perché eseguono essenzialmente la stessa attività: descrivono entrambe una variabile di applicazione al driver e specificano che i dati per una determinata colonna devono essere restituiti in tale variabile. Le differenze principali sono che **SQLGetData** viene chiamato dopo il recupero di una riga (e viene talvolta indicato come *associazione tardiva* per questo motivo) e che l'associazione specificata da **SQLGetData** dura solo per la durata della chiamata.  
  
 Per quanto riguarda una singola colonna, **SQLGetData** si comporta come **SQLFetch**: recupera i dati per la colonna, li converte nel tipo della variabile di applicazione e lo restituisce in tale variabile. Restituisce anche la lunghezza in byte dei dati nel buffer di lunghezza/indicatore. Per ulteriori informazioni su come **SQLFetch** restituisce i dati, vedere [Recupero di una riga di dati](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 **SQLGetData** differisce da **SQLFetch** per un aspetto importante. Se viene chiamato più di una volta in successione per la stessa colonna, ogni chiamata restituisce una parte successiva dei dati. Ogni chiamata tranne l'ultima chiamata restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dati stringa, troncati a destra); l'ultima chiamata restituisce SQL_SUCCESS. Questo è il modo in cui **SQLGetData** viene utilizzato per recuperare dati lunghi in parti. Quando non sono presenti altri dati da restituire, **SQLGetData** restituisce SQL_NO_DATA. L'applicazione è responsabile per l'unione dei dati lunghi, che potrebbe significare la concatenazione delle parti dei dati. Ogni parte è con terminazione null; l'applicazione deve rimuovere il carattere di terminazione null se si concatenano le parti. Il recupero dei dati nelle parti può essere eseguito per i segnalibri di lunghezza variabile e per altri dati lunghi. Il valore restituito nel buffer di lunghezza/indicatore diminuisce in ogni chiamata per il numero di byte restituiti nella chiamata precedente, anche se è comune per il driver non essere in grado di individuare la quantità di dati disponibili e restituire una lunghezza in byte di SQL_NO_TOTAL. Ad esempio:  
  
```  
// Declare a binary buffer to retrieve 5000 bytes of data at a time.  
SQLCHAR       BinaryPtr[5000];  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd, BinaryLenOrInd, NumBytes;  
SQLRETURN     rc;   
SQLHSTMT      hstmt;  
  
// Create a result set containing the ID and picture of each part.  
SQLExecDirect(hstmt, "SELECT PartID, Picture FROM Pictures", SQL_NTS);  
  
// Bind PartID to the PartID column.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &PartID, 0, &PartIDInd);  
  
// Retrieve and display each row of data.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // Display the part ID and initialize the picture.  
   DisplayID(PartID, PartIDInd);  
   InitPicture();  
  
   // Retrieve the picture data in parts. Send each part and the number   
   // of bytes in each part to a function that displays it. The number   
   // of bytes is always 5000 if there were more than 5000 bytes   
   // available to return (cbBinaryBuffer > 5000). Code to check if   
   // rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLGetData(hstmt, 2, SQL_C_BINARY, BinaryPtr, sizeof(BinaryPtr),  
                           &BinaryLenOrInd)) != SQL_NO_DATA) {  
      NumBytes = (BinaryLenOrInd > 5000) || (BinaryLenOrInd == SQL_NO_TOTAL) ?  
                  5000 : BinaryLenOrInd;  
      DisplayNextPictPart(BinaryPtr, NumBytes);  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 Esistono diverse restrizioni sull'utilizzo di **SQLGetData**. In genere, le colonne a cui si accede con **SQLGetData:**  
  
-   È necessario accedere in ordine di numero di colonna crescente (a causa del modo in cui le colonne di un set di risultati vengono lette dall'origine dati). Ad esempio, è un errore chiamare SQLGetData per la colonna 5 e quindi chiamarlo per la colonna 4.For example, it is an error to call **SQLGetData** for column 5 and then call it for column 4.  
  
-   Non può essere associato.  
  
-   Deve avere un numero di colonna superiore rispetto all'ultima colonna associata. Ad esempio, se l'ultima colonna associata è la colonna 3, è un errore chiamare SQLGetData per la colonna 2.For example, if the last bound column is column 3, it is an error to call **SQLGetData** for column 2. Per questo motivo, le applicazioni devono assicurarsi di inserire colonne di dati lunghe alla fine dell'elenco di selezione.  
  
-   Non può essere utilizzato se **SQLFetch** o **SQLFetchScroll** è stato chiamato per recuperare più di una riga. Per ulteriori informazioni, consultate [Utilizzo dei cursori](../../../odbc/reference/develop-app/using-block-cursors.md)a blocchi.  
  
 Alcuni driver non applicano queste restrizioni. Le applicazioni interoperabili devono presupporre che esistano o determinare quali restrizioni non vengono applicate chiamando **SQLGetInfo** con l'opzione SQL_GETDATA_EXTENSIONS.  
  
 Se l'applicazione non necessita di tutti i dati in una colonna di dati binari o di tipo carattere, può ridurre il traffico di rete nei driver basati su DBMS impostando l'attributo dell'istruzione SQL_ATTR_MAX_LENGTH prima di eseguire l'istruzione. In questo modo si limita il numero di byte di dati che verranno restituiti per qualsiasi carattere o colonna binaria. Si supponga, ad esempio, che una colonna contenga documenti di testo lunghi. Un'applicazione che esplora la tabella contenente questa colonna potrebbe essere necessario visualizzare solo la prima pagina di ogni documento. Anche se questo attributo di istruzione può essere simulato nel driver, non vi è alcun motivo per eseguire questa operazione. In particolare, se un'applicazione desidera troncare i dati di tipo carattere o binario, deve associare un piccolo buffer alla colonna con **SQLBindCol** e lasciare che il driver tronca i dati.
