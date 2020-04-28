---
title: Recupero di dati lunghi | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298991"
---
# <a name="getting-long-data"></a>Recupero di dati Long
I DBMS definiscono *dati* di tipo long come dati di tipo carattere o binario su una determinata dimensione, ad esempio 255 caratteri. Questi dati possono essere sufficientemente piccoli da essere archiviati in un singolo buffer, ad esempio una descrizione di una parte di più migliaia di caratteri. Tuttavia, potrebbe essere troppo lungo per l'archiviazione in memoria, ad esempio documenti di testo lunghi o bitmap. Poiché tali dati non possono essere archiviati in un singolo buffer, vengono recuperati dal driver in parti con **SQLGetData** dopo che sono stati recuperati gli altri dati della riga.  
  
> [!NOTE]  
>  Un'applicazione può effettivamente recuperare qualsiasi tipo di dati con **SQLGetData**, non solo dati di tipo Long, sebbene sia possibile recuperare solo i dati di tipo carattere e binario in parti. Tuttavia, se i dati sono sufficientemente piccoli da adattarsi a un singolo buffer, in genere non esiste alcun motivo per utilizzare **SQLGetData**. È molto più semplice associare un buffer alla colonna e consentire al driver di restituire i dati nel buffer.  
  
 Per recuperare dati Long da una colonna, un'applicazione chiama prima **SQLFetchScroll** o **SQLFetch** per spostarsi in una riga e recuperare i dati per le colonne con binding. L'applicazione chiama quindi **SQLGetData**. **SQLGetData** presenta gli stessi argomenti di **SQLBindCol**: un handle di istruzione. numero di colonna; il tipo di dati C, l'indirizzo e la lunghezza in byte di una variabile di applicazione. e l'indirizzo di un buffer di lunghezza/indicatore. Entrambe le funzioni hanno gli stessi argomenti perché eseguono essenzialmente la stessa attività, ovvero descrivono una variabile di applicazione nel driver e specificano che i dati per una determinata colonna devono essere restituiti in tale variabile. Le differenze principali sono che **SQLGetData** viene chiamato dopo il recupero di una riga (e viene talvolta definito *associazione tardiva* per questo motivo) e che l'associazione specificata da **SQLGetData** dura solo per la durata della chiamata.  
  
 Per quanto concerne una singola colonna, **SQLGetData** si comporta come **SQLFetch**: recupera i dati per la colonna, li converte nel tipo della variabile dell'applicazione e li restituisce in tale variabile. Restituisce anche la lunghezza in byte dei dati nel buffer di lunghezza/indicatore. Per ulteriori informazioni su come **SQLFetch** restituisce i dati, vedere [recupero di una riga di dati](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 **SQLGetData** differisce da **SQLFetch** in un aspetto importante. Se viene chiamato più di una volta in successione per la stessa colonna, ogni chiamata restituisce una parte successiva dei dati. Ogni chiamata tranne l'ultima chiamata restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dati stringa, troncati a destra); L'ultima chiamata restituisce SQL_SUCCESS. Questo è il modo in cui viene usato **SQLGetData** per recuperare dati lunghi in parti. Quando non sono disponibili altri dati da restituire, **SQLGetData** restituisce SQL_NO_DATA. L'applicazione è responsabile dell'inserimento dei dati Long, che potrebbero significare la concatenazione delle parti dei dati. Ogni parte è con terminazione null. Se si concatenano le parti, l'applicazione deve rimuovere il carattere di terminazione null. Il recupero dei dati in parti può essere eseguito per i segnalibri a lunghezza variabile e per altri dati di lunga durata. Il valore restituito nel buffer di lunghezza/indicatore diminuisce in ogni chiamata dal numero di byte restituiti nella chiamata precedente, sebbene sia comune per il driver non essere in grado di individuare la quantità di dati disponibili e restituire una lunghezza in byte di SQL_NO_TOTAL. Ad esempio:  
  
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
  
 L'utilizzo di **SQLGetData**presenta diverse limitazioni. Generalmente, le colonne a cui si accede con **SQLGetData**:  
  
-   È necessario accedere a per aumentare il numero di colonna, a causa del modo in cui le colonne di un set di risultati vengono lette dall'origine dati. Ad esempio, è un errore chiamare **SQLGetData** per la colonna 5 e quindi chiamarlo per la colonna 4.  
  
-   Non può essere associato.  
  
-   Deve avere un numero di colonna maggiore dell'ultima colonna associata. Se, ad esempio, l'ultima colonna associata è la colonna 3, è un errore chiamare **SQLGetData** per la colonna 2. Per questo motivo, le applicazioni devono assicurarsi di inserire colonne di dati lunghe alla fine dell'elenco di selezione.  
  
-   Non può essere utilizzato se è stato chiamato **SQLFetch** o **SQLFetchScroll** per recuperare più di una riga. Per ulteriori informazioni, vedere [utilizzo dei cursori a blocchi](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 Alcuni driver non applicano queste restrizioni. Le applicazioni interoperative devono presupporre che esistano o determinare quali restrizioni non vengono applicate chiamando **SQLGetInfo** con l'opzione SQL_GETDATA_EXTENSIONS.  
  
 Se l'applicazione non necessita di tutti i dati in una colonna di dati di tipo carattere o binaria, può ridurre il traffico di rete nei driver basati su DBMS impostando l'attributo dell'istruzione SQL_ATTR_MAX_LENGTH prima di eseguire l'istruzione. Questo limita il numero di byte di dati che verranno restituiti per qualsiasi colonna di tipo carattere o binario. Si supponga, ad esempio, che una colonna contenga documenti di testo lunghi. Un'applicazione che Esplora la tabella contenente questa colonna potrebbe dover visualizzare solo la prima pagina di ogni documento. Sebbene questo attributo di istruzione possa essere simulato nel driver, non esiste alcun motivo per eseguire questa operazione. In particolare, se un'applicazione desidera troncare dati di tipo carattere o binario, deve associare un buffer di piccole dimensioni alla colonna con **SQLBindCol** e consentire al driver di troncare i dati.
