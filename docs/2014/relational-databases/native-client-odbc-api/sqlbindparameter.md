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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067817"
---
# <a name="sqlbindparameter"></a>SQLBindParameter
  `SQLBindParameter`può eliminare il carico della conversione dei dati quando viene utilizzato per fornire i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati per il driver ODBC di Native client, ottenendo un miglioramento significativo delle prestazioni per i componenti client e server delle applicazioni. Un altro vantaggio è costituito da un'inferiore perdita di precisione durante l'inserimento o l'aggiornamento di tipi di dati numerici approssimativi.  
  
> [!NOTE]  
>  Quando si inseriscono tipi di dati`char` e `wchar` in una colonna di tipo image, vengono utilizzate le dimensioni dei dati passati anziché le dimensioni dei dati in seguito alla conversione a un formato binario.  
  
 Se il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client rileva un errore in un singolo elemento di matrice di una matrice di parametri, continua a eseguire l'istruzione per gli elementi di matrice rimanenti. Se l'applicazione ha associato una matrice di elementi di stato dei parametri per l'istruzione, le righe di parametri che generano errori possono essere determinate dalla matrice.  
  
 Quando si utilizza il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, specificare SQL_PARAM_INPUT quando si associano parametri di input. Specificare solo SQL_PARAM_OUTPUT o SQL_PARAM_INPUT_OUTPUT quando si associano parametri di stored procedure definiti con la parola chiave OUTPUT.  
  
 [SQLRowCount](sqlrowcount.md) non è affidabile con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il driver ODBC di Native client se un elemento di matrice di una matrice di parametri associati causa un errore nell'esecuzione dell'istruzione. L'attributo SQL_ATTR_PARAMS_PROCESSED_PTR dell'istruzione ODBC indica il numero di righe elaborate prima del verificarsi dell'errore. L'applicazione può quindi attraversare la relativa matrice degli stati dei parametri per individuare il numero di istruzioni eseguite correttamente, se necessario.  
  
## <a name="binding-parameters-for-sql-character-types"></a>Associazione di parametri per i tipi di caratteri SQL  
 Se il tipo di dati SQL passato è un tipo di carattere, *ColumnSize* è la dimensione in caratteri (non byte). Se la lunghezza della stringa di dati in byte è maggiore di 8000, *ColumnSize* deve essere impostato su `SQL_SS_LENGTH_UNLIMITED`, a indicare che non esiste alcun limite per le dimensioni del tipo SQL.  
  
 Ad esempio, se il tipo di dati SQL `SQL_WVARCHAR`è, *ColumnSize* non deve essere maggiore di 4000. Se la lunghezza effettiva dei dati è maggiore di 4000, *ColumnSize* deve essere impostato su `SQL_SS_LENGTH_UNLIMITED` in modo `nvarchar(max)` che verrà usato dal driver.  
  
## <a name="sqlbindparameter-and-table-valued-parameters"></a>SQLBindParameter e parametri con valori di tabella  
 Analogamente ad altri tipi di parametri, i parametri con valori di tabella sono associati da SQLBindParameter.  
  
 Una volta associato un parametro con valori di tabella, vengono associate anche le colonne del parametro. Per associare le colonne, chiamare [SQLSetStmtAttr](sqlsetstmtattr.md) per impostare SQL_SOPT_SS_PARAM_FOCUS sull'ordinale del parametro con valori di tabella. Chiamare quindi SQLBindParameter per ogni colonna nel parametro con valori di tabella. Per tornare alle associazioni di parametro di livello principale, impostare SQL_SOPT_SS_PARAM_FOCUS su 0.  
  
 Per informazioni sul mapping dei parametri ai campi di descrizione per i parametri con valori di tabella, vedere [Binding e trasferimento dati di parametri con valori di tabella e valori di colonna](../native-client-odbc-table-valued-parameters/binding-and-data-transfer-of-table-valued-parameters-and-column-values.md).  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlbindparameter-support-for-enhanced-date-and-time-features"></a>Supporto di SQLBindParameter per le caratteristiche avanzate di data e ora  
 I valori dei parametri di tipo data/ora vengono convertiti come descritto in [conversioni da C a SQL](../native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md). Si noti che per i `time` parametri `datetimeoffset` di tipo e deve essere `SQL_C_DEFAULT` specificato `SQL_C_BINARY` ValueType come o se vengono`SQL_SS_TIME2_STRUCT` utilizzate `SQL_SS_TIMESTAMPOFFSET_STRUCT`le strutture corrispondenti (e). *ValueType*  
  
 Per ulteriori informazioni, vedere [miglioramenti di data e ora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlbindparameter-support-for-large-clr-udts"></a>Supporto di SQLBindParameter per i tipi CLR definiti dall'utente di grandi dimensioni  
 `SQLBindParameter` supporta i tipi CLR definiti dall'utente di grandi dimensioni. Per ulteriori informazioni, vedere [tipi CLR definiti dall'utente di grandi dimensioni &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)   
 [Pagina relativa alla funzione SQLBindParameter](https://go.microsoft.com/fwlink/?LinkId=59328)  
  
  
