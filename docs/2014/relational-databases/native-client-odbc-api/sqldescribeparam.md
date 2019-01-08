---
title: SQLDescribeParam | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d52d68cc0cd31e9dbb3da25c46901e126252607
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53359493"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
  Per descrivere i parametri di qualsiasi istruzione SQL, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client compila ed esegue un [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzione SELECT quando SQLDescribeParam viene chiamato su un handle di istruzione ODBC preparato. I metadati del set di risultati determinano le caratteristiche dei parametri dell'istruzione preparata. SQLDescribeParam può restituire qualsiasi codice di errore che potrebbero restituire SQLExecute o SQLExecDirect.  
  
 Miglioramenti apportati al motore di database a partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] consentire SQLDescribeParam ottenere descrizioni più accurate dei risultati previsti. Questi risultati più accurati differiscano dai valori restituiti da SQLDescribeParam nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Metadata Discovery](../native-client/features/metadata-discovery.md).  
  
 Altra novità [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], *ParameterSizePtr* ora restituisce un valore che si allinea con la definizione per le dimensioni, in caratteri, della colonna o espressione del marcatore di parametro corrispondente come definito nel [ODBC specifica](https://go.microsoft.com/fwlink/?LinkId=207044). Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, *ParameterSizePtr* potrebbe essere il valore corrispondente di `SQL_DESC_OCTET_LENGTH` per il tipo o un valore di dimensione di colonna irrilevante fornito a SQLBindParameter per un tipo, il valore di cui deve essere ignorata (`SQL_INTEGER`, ad esempio).  
  
 Il driver non supporta SQLDescribeParam chiamante nelle situazioni seguenti:  
  
-   Dopo aver SQLExecDirect per qualsiasi [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzioni UPDATE o DELETE contenente la clausola FROM.  
  
-   Per qualsiasi istruzione ODBC o [!INCLUDE[tsql](../../includes/tsql-md.md)] contenente un parametro in una clausola HAVING o confrontata con il risultato di una funzione SUM.  
  
-   Per qualsiasi istruzione ODBC o [!INCLUDE[tsql](../../includes/tsql-md.md)] a seconda di una subquery che contiene parametri.  
  
-   Per le istruzioni ODBC SQL che contengono marcatori di parametro in entrambe le espressioni di un predicato di confronto, LIKE o quantificato.  
  
-   Per qualsiasi query in cui uno dei parametri è il parametro di una funzione.  
  
-   Quando sono presenti commenti (/ * \*/) nel [!INCLUDE[tsql](../../includes/tsql-md.md)] comando.  
  
 Durante l'elaborazione di un batch di [!INCLUDE[tsql](../../includes/tsql-md.md)] (istruzioni), il driver non supporta inoltre la chiamata di SQLDescribeParam per i marcatori di parametro nelle istruzioni dopo la prima istruzione nel batch.  
  
 Quando si descrive i parametri della stored procedure preparate, SQLDescribeParam utilizza la stored procedure di sistema [sp_sproc_columns](/sql/relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql) per recuperare le caratteristiche del parametro. sp_sproc_columns può riportare dati per le stored procedure all'interno del database utente corrente. Preparazione di un nome di stored procedure completo consente di SQLDescribeParam per l'esecuzione tra database. Ad esempio, di stored procedure di sistema [sp_who](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql) possono essere preparata ed eseguita in qualsiasi database come:  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 L'esecuzione di SQLDescribeParam dopo la preparazione riuscita restituisce una riga vuota impostata quando si è connessi a qualsiasi database ma `master`. La stessa chiamata, preparata come segue, fa sì che SQLDescribeParam abbia esito positivo indipendentemente dal database utente corrente:  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 Per i tipi di dati di valori di grandi dimensioni, il valore restituito in *DataTypePtr* è SQL_VARCHAR, SQL_VARBINARY o SQL_NVARCHAR. Per indicare che la dimensione del parametro del tipo di dati di valori di grandi dimensioni è "illimitata", il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] set di driver ODBC di Native Client *ParameterSizePtr* su 0. Vengono restituiti i valori delle dimensioni effettive per i parametri `varchar` standard.  
  
> [!NOTE]  
>  Se il parametro è già stato associato alle dimensioni massime del parametro SQL_VARCHAR, SQL_VARBINARY o SQL_WVARCHAR, vengono restituite le dimensioni associate limitate del parametro.  
  
 Per associare un parametro di input di dimensioni illimitate, è necessario utilizzare data-at-execution. Non è possibile associare un parametro di output di una dimensione "illimitata" (nessun metodo per lo streaming di dati da un parametro di output, ad esempio [SQLGetData](sqlgetdata.md) per set di risultati).  
  
 Per i parametri di output è necessario associare un buffer. Se il valore è troppo grande, il buffer viene riempito e vengono restituiti un messaggio SQL_SUCCESS_WITH_INFO e un avviso "Troncamento a destra della stringa di dati". I dati troncati verranno quindi eliminati.  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam e parametri con valori di tabella  
 Un'applicazione può recuperare informazioni sui parametri con valori di tabella per un'istruzione preparata con SQLDescribeParam. Per altre informazioni, vedere [metadati del parametro con valori di tabella per istruzioni preparate](../native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md).  
  
 Per altre informazioni sui parametri con valori di tabella, in generale, vedere [parametri con valori di tabella &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>Supporto di SQLDescribeParam per le caratteristiche avanzate di data e ora  
 I valori restituiti per i tipi di data/ora sono i seguenti:  
  
||*DataTypePtr*|*ParameterSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|------------------------|------------------------|  
|DATETIME|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|Data|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Per altre informazioni, vedere [data e miglioramenti per la fase &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>Supporto di SQLDescribeParam per i tipi CLR definiti dall'utente di grandi dimensioni  
 `SQLDescribeParam` supporta i tipi CLR definiti dall'utente di grandi dimensioni. Per altre informazioni, vedere [Large CLR User-Defined tipi &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLDescribeParam](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
