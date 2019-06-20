---
title: SQLBindParameter | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLBindParameter function
ms.assetid: c302c87a-e7f4-4d2b-a0a7-de42210174ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cba973be9b4dc2ec0da286b2d01b636f0ca4e2b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067817"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
  `SQLBindParameter` Consente di eliminare le attività di conversione dei dati quando viene utilizzata per fornire dati per il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client, conseguente notevole miglioramento delle prestazioni per i componenti client e server delle applicazioni. Un altro vantaggio è costituito da un'inferiore perdita di precisione durante l'inserimento o l'aggiornamento di tipi di dati numerici approssimativi.  
  
> [!NOTE]  
>  Quando si inseriscono tipi di dati`char` e `wchar` in una colonna di tipo image, vengono utilizzate le dimensioni dei dati passati anziché le dimensioni dei dati in seguito alla conversione a un formato binario.  
  
 Se il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client rileva un errore in un singolo elemento di matrice di una matrice di parametri, continua a eseguire l'istruzione per gli elementi di matrice rimanenti. Se l'applicazione ha associato una matrice di elementi di stato dei parametri per l'istruzione, le righe di parametri che generano errori possono essere determinate dalla matrice.  
  
 Quando si utilizza il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, specificare SQL_PARAM_INPUT quando si associano parametri di input. Specificare solo SQL_PARAM_OUTPUT o SQL_PARAM_INPUT_OUTPUT quando si associano parametri di stored procedure definiti con la parola chiave OUTPUT.  
  
 [SQLRowCount](sqlrowcount.md) non è affidabile con il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il driver ODBC Native Client se un elemento di matrice di una matrice di parametri di associazione a causa di un errore nell'esecuzione dell'istruzione. L'attributo SQL_ATTR_PARAMS_PROCESSED_PTR dell'istruzione ODBC indica il numero di righe elaborate prima del verificarsi dell'errore. L'applicazione può quindi attraversare la relativa matrice degli stati dei parametri per individuare il numero di istruzioni eseguite correttamente, se necessario.  
  
## <a name="binding-parameters-for-sql-character-types"></a>Associazione di parametri per i tipi di caratteri SQL  
 Se il tipo di dati SQL passato è un tipo di carattere, *ColumnSize* è la dimensione in caratteri (non byte). Se la lunghezza della stringa di dati in byte è maggiore di 8000, *ColumnSize* deve essere impostato su `SQL_SS_LENGTH_UNLIMITED`, che indica che non sono previsti limiti per le dimensioni del tipo SQL.  
  
 Ad esempio, se il tipo di dati SQL `SQL_WVARCHAR`, *ColumnSize* non deve essere maggiore di 4000. Se la lunghezza effettiva dei dati è maggiore di 4000, allora *ColumnSize* deve essere impostato su `SQL_SS_LENGTH_UNLIMITED` in modo che `nvarchar(max)` verrà usato dal driver.  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter e parametri con valori di tabella  
 Gli altri tipi di parametro sono associati parametri valutati a livello di tabella mediante la funzione SQLBindParameter.  
  
 Una volta associato un parametro con valori di tabella, vengono associate anche le colonne del parametro. Per associare le colonne, si chiama [SQLSetStmtAttr](sqlsetstmtattr.md) per impostare SQL_SOPT_SS_PARAM_FOCUS sul numero ordinale del parametro con valori di tabella. Quindi, chiamare la funzione SQLBindParameter per ogni colonna nel parametro valori di tabella. Per tornare alle associazioni di parametro di livello principale, impostare SQL_SOPT_SS_PARAM_FOCUS su 0.  
  
 Per informazioni sul mapping dei parametri ai campi del descrittore per parametri valutati a livello di tabella, vedere [associazione e i parametri Data Transfer of Table-Valued e i valori di colonna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Per altre informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>Supporto di SQLBindParameter per le caratteristiche avanzate di data e ora  
 Valori dei parametri di tipo Data/ora vengono convertiti come indicato [le conversioni da C a SQL](../native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md). Si noti che per i parametri di tipo `time` e `datetimeoffset` deve avere *ValueType* specificato come `SQL_C_DEFAULT` oppure `SQL_C_BINARY` se utilizzano le strutture corrispondenti (`SQL_SS_TIME2_STRUCT` e `SQL_SS_TIMESTAMPOFFSET_STRUCT`) vengono usati.  
  
 Per altre informazioni, vedere [data e miglioramenti per la fase &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>Supporto di SQLBindParameter per i tipi CLR definiti dall'utente di grandi dimensioni  
 `SQLBindParameter` supporta i tipi CLR definiti dall'utente di grandi dimensioni. Per altre informazioni, vedere [Large CLR User-Defined tipi &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Dettagli di implementazione di API ODBC](odbc-api-implementation-details.md)   
 [Funzione SQLBindParameter](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
