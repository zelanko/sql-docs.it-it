---
title: Modifica del comportamento del Driver ODBC quando si gestiscono le conversioni di caratteri | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 682a232a-bf89-4849-88a1-95b2fbac1467
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 38a7eb08d65717b20891225e6f4ff61e4fbcb99b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62744417"
---
# <a name="odbc-driver-behavior-change-when-handling-character-conversions"></a>Modifica del comportamento del driver ODBC quando si gestiscono le conversioni di caratteri
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Il [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Driver ODBC di Native Client (SQLNCLI11.dll) stata modificata la modalità di SQL_WCHAR * (nchar e SQL_CHAR\* (narchar conversioni. Tramite le funzioni ODBC, ad esempio SQLGetData, SQLBindCol, SQLBindParameter viene restituito (-4) SQL_NO_TOTAL come parametro di lunghezza/indicatore quando si utilizza il driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client. Dalle versioni precedenti del driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client viene restituito un valore di lunghezza che può essere errato.  
  
## <a name="sqlgetdata-behavior"></a>Comportamento di SQLGetData  
 Tramite le numerose funzioni di Windows è possibile specificare dimensioni del buffer pari a 0 e la lunghezza restituita corrisponde alle dimensioni dei dati restituiti. Di seguito è riportato un modello comune per i programmatori di Windows:  
  
```  
int iSize = 0;  
BYTE * pBuffer = NULL;  
GetMyFavoriteAPI(pBuffer, &iSize);   // Returns needed size in iSize  
pBuffer = new BYTE[iSize];   // Allocate buffer   
GetMyFavoriteAPI(pBuffer, &iSize);   // Retrieve actual data  
```  
  
 Tuttavia **SQLGetData** non deve essere utilizzato in questo scenario. Non è consigliabile utilizzare il modello seguente:  
  
```  
// bad  
int iSize = 0;  
WCHAR * pBuffer = NULL;  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)0x1, 0, &iSize);   // Get storage size needed  
pBuffer = new WCHAR[(iSize/sizeof(WCHAR)) + 1];   // Allocate buffer  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)pBuffer, iSize, &iSize);   // Retrieve data  
```  
  
 **SQLGetData** può essere chiamato solo per recuperare blocchi di dati effettivi. Usando **SQLGetData** per ottenere le dimensioni dei dati non è supportata.  
  
 Di seguito viene illustrato l'impatto della modifica del driver quando si utilizza il modello errato. Questa query di applicazione un' **varchar** colonna e l'associazione come Unicode (SQL_UNICODE/SQL_WCHAR):  
  
 Query:  `select convert(varchar(36), '123')`  
  
```  
SQLGetData(hstmt, SQL_WCHAR, ....., (SQLPOINTER*) 0x1, 0 , &iSize);   // Attempting to determine storage size needed  
```  
  
|Versione del driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client|Risultato della lunghezza o dell'indicatore|Descrizione|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client o versioni precedenti|6|È stato erroneamente presupposto dal driver che la conversione di CHAR in WCHAR potesse essere effettuata come lunghezza * 2.|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (versione 11.0.2100.60) o successive|-4 (SQL_NO_TOTAL)|Il driver non presume più che la conversione da CHAR a WCHAR o da WCHAR a CHAR sia un' (moltiplicazione) \*2 o () / 2 azioni.<br /><br /> La chiamata **SQLGetData** non restituisce più la lunghezza della conversione prevista. Tramite il driver viene rilevata la conversione a o da CHAR e WCHAR e viene restituito (-4) SQL_NO_TOTAL anziché il comportamento *2 o /2 che potrebbe essere errato.|  
  
 Uso **SQLGetData** per recuperare i blocchi di dati. (di seguito è riportato uno pseudocodice):  
  
```  
while( (SQL_SUCCESS or SQL_SUCCESS_WITH_INFO) == SQLFetch(...) ) {  
   SQLNumCols(...iTotalCols...)  
   for(int iCol = 1; iCol < iTotalCols; iCol++) {  
      WCHAR* pBufOrig, pBuffer = new WCHAR[100];  
      SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get original chunk  
      while(NOT ALL DATA RETREIVED (SQL_NO_TOTAL, ...) ) {  
         pBuffer += 50;   // Advance buffer for data retrieved  
         // May need to realloc the buffer when you reach current size  
         SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get next chunk  
      }  
   }  
}  
```  
  
## <a name="sqlbindcol-behavior"></a>Comportamento di SQLBindCol  
 Query:  `select convert(varchar(36), '1234567890')`  
  
```  
SQLBindCol(... SQL_W_CHAR, ...)   // Only bound a buffer of WCHAR[4] - Expecting String Data Right Truncation behavior  
```  
  
|Versione del driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client|Risultato della lunghezza o dell'indicatore|Descrizione|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client o versioni precedenti|20|**SQLFetch** segnala che vi sia un troncamento a destra dei dati.<br /><br /> La lunghezza corrisponde a quella dei dati restituiti e non di quelli archiviati (viene presupposta una conversione *2 CHAR a WCHAR che potrebbe essere errata per i glifi).<br /><br /> I dati archiviati nel buffer sono 123\0. Viene garantito che la terminazione del buffer sia NULL.|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (versione 11.0.2100.60) o successive|-4 (SQL_NO_TOTAL)|**SQLFetch** segnala che vi sia un troncamento a destra dei dati.<br /><br /> Tramite la lunghezza viene indicato -4 (SQL_NO_TOTAL) poiché il resto dei dati non è stato convertito.<br /><br /> I dati archiviati nel buffer sono 123\0. - Viene garantito che la terminazione del buffer sia NULL.|  
  
## <a name="sqlbindparameter-output-parameter-behavior"></a>SQLBindParameter (comportamento del parametro OUTPUT)  
 Query:  `create procedure spTest @p1 varchar(max) OUTPUT`  
  
 `select @p1 = replicate('B', 1234)`  
  
```  
SQLBindParameter(... SQL_W_CHAR, ...)   // Only bind up to first 64 characters  
```  
  
|Versione del driver ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client|Risultato della lunghezza o dell'indicatore|Descrizione|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client o versioni precedenti|2468|**SQLFetch** non restituisce dati più disponibili.<br /><br /> **SQLMoreResults** non restituisce dati più disponibili.<br /><br /> Tramite la lunghezza vengono indicate le dimensioni dei dati restituiti dal server e non di quelli archiviati nel buffer.<br /><br /> Nel buffer originale sono contenuti 63 byte e un carattere di terminazione NULL. Viene garantito che la terminazione del buffer sia NULL.|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (versione 11.0.2100.60) o successive|-4 (SQL_NO_TOTAL)|**SQLFetch** non restituisce dati più disponibili.<br /><br /> **SQLMoreResults** non restituisce dati più disponibili.<br /><br /> Tramite la lunghezza viene indicato (-4) SQL_NO_TOTAL poiché il resto dei dati non è stato convertito.<br /><br /> Nel buffer originale sono contenuti 63 byte e un carattere di terminazione NULL. Viene garantito che la terminazione del buffer sia NULL.|  
  
## <a name="performing-char-and-wchar-conversions"></a>Esecuzione delle conversioni CHAR e WCHAR  
 Nel driver ODBC di [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client sono disponibili diverse modalità di esecuzione delle conversioni CHAR e WCHAR. La logica è simile alla modifica di BLOB (varchar (max), nvarchar, (max)...):  
  
-   I dati vengono salvati o troncati nel buffer specificato durante l'associazione con **SQLBindCol** oppure **SQLBindParameter**.  
  
-   Se non è possibile associare, è possibile recuperare i dati in blocchi mediante **SQLGetData** e **SQLParamData**.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
