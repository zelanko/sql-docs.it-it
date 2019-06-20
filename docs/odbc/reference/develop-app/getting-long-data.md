---
title: Recupero di dati Long | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d61f6e2d5c2999a1ff7cea86d497eb4f0fb13244
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061599"
---
# <a name="getting-long-data"></a>Recupero di dati Long
Definiscono DBMS *dati di tipo long* come qualsiasi carattere o dati binari in una determinata dimensione, ad esempio i 255 caratteri. Questi dati possono essere sufficientemente piccoli da archiviare in un singolo buffer, ad esempio una descrizione di parte di diverse migliaia di caratteri. Tuttavia, potrebbe essere troppo lungo per l'archiviazione in memoria, ad esempio documenti di testo lungo o bitmap. Perché questo tipo di dati non può essere archiviati in un singolo buffer, viene recuperato dal driver nelle parti con **SQLGetData** dopo gli altri dati nella riga sono stati recuperati.  
  
> [!NOTE]  
>  Un'applicazione può effettivamente di recuperare qualsiasi tipo di dati con **SQLGetData**, non solo lunga data, anche se solo i caratteri e dati binari possono essere recuperati in parti. Tuttavia, se i dati sono sufficientemente piccoli da rientrare in un singolo buffer, non è in genere necessario usare **SQLGetData**. È molto più semplice associare un buffer per la colonna e consentire il driver di restituire i dati nel buffer.  
  
 Per recuperare dati long da una colonna, un'applicazione chiama innanzitutto **SQLFetchScroll** oppure **SQLFetch** per spostarsi in una riga e recuperare i dati per le colonne associate. L'applicazione chiama quindi **SQLGetData**. **SQLGetData** ha gli stessi argomenti **SQLBindCol**: un handle di istruzione, un numero di colonna, il C lunghezza dei dati tipo, indirizzo e byte di una variabile di applicazione; e l'indirizzo di un buffer di lunghezza/indicatore. Entrambe le funzioni hanno gli stessi argomenti poiché eseguono essenzialmente la stessa attività: Entrambi descrivono una variabile di applicazione al driver e specificare che i dati per una determinata colonna devono essere restituiti nella variabile stessa. Le principali differenze sono che **SQLGetData** viene chiamato dopo che viene recuperata una riga (e talvolta si intende *associazione tardiva* per questo motivo) e che l'associazione specificata dal **SQLGetData**  viene mantenuta solo per la durata della chiamata.  
  
 Per quanto riguarda una singola colonna, **SQLGetData** si comporta come **SQLFetch**: Recupera i dati per la colonna, lo converte nel tipo della variabile di applicazione e lo restituisce in tale variabile. Restituisce anche la lunghezza in byte dei dati nel buffer di lunghezza/indicatore. Per altre informazioni su come **SQLFetch** restituisce dati, vedere [il recupero di una riga di dati](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 **SQLGetData** è diverso da **SQLFetch** un aspetto importante. Se viene chiamato più volte in successione per la stessa colonna, ogni chiamata restituisca una parte successiva dei dati. Ogni chiamata, ad eccezione dell'ultima chiamata restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dati String, a destra troncati); l'ultima chiamata restituisce SQL_SUCCESS. Questa è la modalità **SQLGetData** viene usato per recuperare dati long in parti. Quando non sono presenti dati da restituire, ulteriori **SQLGetData** restituisce SQL_NO_DATA. L'applicazione è responsabile per la creazione di dati long, che potrebbe significare concatenando le parti dei dati. Ogni parte è con terminazione null; l'applicazione è necessario rimuovere il carattere di terminazione null se il concatenamento le parti. Il recupero dei dati in parti può essere eseguita per a lunghezza variabile segnalibri oltre a quella di altri dati di tipo long. Il valore restituito in una riduzione delle buffer di lunghezza/indicatore ogni chiamata per il numero di byte restituiti nella chiamata al precedente, anche se è comune per il driver a non essere in grado di individuare la quantità di dati disponibili e restituire una lunghezza in byte dei SQL_NO_TOTAL. Ad esempio:  
  
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
  
 Esistono diverse restrizioni sull'uso **SQLGetData**. In generale, di accedere alle colonne con **SQLGetData**:  
  
-   È necessario accedere in ordine crescente numero di colonne (a causa del modo che le colonne di un set di risultati vengono letti dall'origine dati). Ad esempio, è possibile chiamare **SQLGetData** per colonna 5 e chiamarlo successivamente per la colonna 4.  
  
-   non è possibile associare.  
  
-   Deve avere un numero di colonne superiore rispetto l'ultima colonna associata. Ad esempio, se l'ultima colonna associata viene colonna 3, è un errore chiamare **SQLGetData** per la colonna 2. Per questo motivo, le applicazioni devono assicurarsi di inserire le colonne di dati long alla fine dell'elenco di selezione.  
  
-   Non può essere utilizzato se **SQLFetch** oppure **SQLFetchScroll** è stato chiamato per recuperare più righe. Per altre informazioni, vedere [cursori a blocchi usando](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 Alcuni driver non applicano queste restrizioni. Applicazioni interoperative devono supporre che esiste o determinare le restrizioni che non vengono applicate chiamando **SQLGetInfo** con l'opzione SQL_GETDATA_EXTENSIONS.  
  
 Se l'applicazione non è necessario che tutti i dati in un carattere o una colonna di dati binari, è possibile ridurre il traffico di rete nel driver basati su DBMS impostando l'attributo di istruzione SQL_ATTR_MAX_LENGTH prima di eseguire l'istruzione. Ciò limita il numero di byte di dati che verranno restituiti per qualsiasi colonna di tipo binario o carattere. Si supponga, ad esempio, che una colonna contiene documenti di testo lungo. Un'applicazione che visualizza la tabella contenente questa colonna potrebbe essere necessario visualizzare solo la prima pagina di ogni documento. Anche se questo attributo dell'istruzione può essere simulato nel driver, non c'è nessun motivo per eseguire questa operazione. In particolare, se un'applicazione deve troncare i dati carattere o binario, deve essere associato un buffer di piccole dimensioni e la colonna con **SQLBindCol** e lasciare che il driver troncare i dati.
