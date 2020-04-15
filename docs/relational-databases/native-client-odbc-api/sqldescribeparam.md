---
title: Proprietà SQLDescribeParam . Documenti Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDescribeParam function
ms.assetid: 396e74b1-5d08-46dc-b404-2ef2003e4689
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: efe1fdccbef4f5c4a393083f6eb81efee759be5c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302583"
---
# <a name="sqldescribeparam"></a>SQLDescribeParam
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Per descrivere i parametri di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qualsiasi istruzione SQL, il driver [!INCLUDE[tsql](../../includes/tsql-md.md)] ODBC Native Client compila ed esegue un'istruzione SELECT quando SQLDescribeParam viene chiamato su un handle di istruzione ODBC preparato. I metadati del set di risultati determinano le caratteristiche dei parametri dell'istruzione preparata. SQLDescribeParam può restituire qualsiasi codice di errore che SQLExecute o SQLExecDirect potrebbe restituire.  
  
 I miglioramenti nel motore [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] di database che iniziano con consentono a SQLDescribeParam di ottenere descrizioni più accurate dei risultati previsti. Questi risultati più accurati possono differire dai valori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]restituiti da SQLDescribeParam nelle versioni precedenti di . Per altre informazioni, vedere [Metadata Discovery](../../relational-databases/native-client/features/metadata-discovery.md).  
  
 Anche nuovo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]in , *ParameterSizePtr* ora restituisce un valore allineato alla definizione per la dimensione, in caratteri, della colonna o dell'espressione dell'indicatore di parametro corrispondente come definito nella [specifica ODBC.](https://go.microsoft.com/fwlink/?LinkId=207044) Nelle versioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precedenti di Native Client, *ParameterSizePtr* potrebbe essere il valore corrispondente di **SQL_DESC_OCTET_LENGTH** per il tipo o un valore di dimensione di colonna irrilevante fornito a SQLBindParameter per un tipo, il cui valore deve essere ignorato (**SQL_INTEGER**, ad esempio ).  
  
 Il driver non supporta la chiamata SQLDescribeParam nelle situazioni seguenti:The driver does not support calling SQLDescribeParam in the following situations:  
  
-   Dopo SQLExecDirect [!INCLUDE[tsql](../../includes/tsql-md.md)] per tutte le istruzioni UPDATE o DELETE contenenti la clausola FROM.  
  
-   Per qualsiasi istruzione ODBC o [!INCLUDE[tsql](../../includes/tsql-md.md)] contenente un parametro in una clausola HAVING o confrontata con il risultato di una funzione SUM.  
  
-   Per qualsiasi istruzione ODBC o [!INCLUDE[tsql](../../includes/tsql-md.md)] a seconda di una subquery che contiene parametri.  
  
-   Per le istruzioni ODBC SQL che contengono marcatori di parametro in entrambe le espressioni di un predicato di confronto, LIKE o quantificato.  
  
-   Per qualsiasi query in cui uno dei parametri è il parametro di una funzione.  
  
-   Quando sono presenti commenti \*(/ / [!INCLUDE[tsql](../../includes/tsql-md.md)] /) nel comando.  
  
 Durante l'elaborazione di un batch di [!INCLUDE[tsql](../../includes/tsql-md.md)] istruzioni, il driver non supporta inoltre la chiamata di SQLDescribeParam per gli indicatori di parametro nelle istruzioni dopo la prima istruzione nel batch.  
  
 Quando si descrivono i parametri delle stored procedure preparate, SQLDescribeParam utilizza la stored procedure di sistema [sp_sproc_columns](../../relational-databases/system-stored-procedures/sp-sproc-columns-transact-sql.md) per recuperare le caratteristiche dei parametri. sp_sproc_columns possibile segnalare i dati per le stored procedure all'interno del database utente corrente. La preparazione di un nome di stored procedure completo consente l'esecuzione di SQLDescribeParam tra database. Ad esempio, la stored procedure di sistema [sp_who](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) può essere preparata ed eseguita in qualsiasi database come:  
  
```  
SQLPrepare(hstmt, "{call sp_who(?)}", SQL_NTS);  
```  
  
 L'esecuzione di SQLDescribeParam dopo la preparazione restituisce un set di righe vuoto quando si è connessi a qualsiasi database ma **master**. La stessa chiamata, preparata come segue, fa sì che SQLDescribeParam abbia esito positivo indipendentemente dal database utente corrente:  
  
```  
SQLPrepare(hstmt, "{call master..sp_who(?)}", SQL_NTS);  
```  
  
 Per i tipi di dati valore di grandi dimensioni, il valore restituito in *DataTypePtr* è SQL_VARCHAR, SQL_VARBINARY o SQL_NVARCHAR. Per indicare che la dimensione del parametro del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati valore grande è "illimitata", il driver ODBC Native Client imposta *ParameterSizePtr* su 0. I valori delle dimensioni effettive vengono restituiti per i parametri **varchar** standard.  
  
> [!NOTE]  
>  Se il parametro è già stato associato alle dimensioni massime del parametro SQL_VARCHAR, SQL_VARBINARY o SQL_WVARCHAR, vengono restituite le dimensioni associate limitate del parametro.  
  
 Per associare un parametro di input di dimensioni illimitate, è necessario utilizzare data-at-execution. Non è possibile associare un parametro di output di dimensione "illimitato" (non esiste alcun metodo per lo streaming di dati da un parametro di output, come [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) esegue per i set di risultati).  
  
 Per i parametri di output è necessario associare un buffer. Se il valore è troppo grande, il buffer viene riempito e vengono restituiti un messaggio SQL_SUCCESS_WITH_INFO e un avviso "Troncamento a destra della stringa di dati". I dati troncati verranno quindi eliminati.  
  
## <a name="sqldescribeparam-and-table-valued-parameters"></a>SQLDescribeParam e parametri con valori di tabella  
 Un'applicazione può recuperare informazioni sui parametri con valori di tabella per un'istruzione preparata con SQLDescribeParam.An application can retrieve table-valued parameter information for a prepared statement with SQLDescribeParam. Per ulteriori informazioni, vedere [Metadati dei](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameter-metadata-for-prepared-statements.md)parametri con valori di tabella per istruzioni preparate .  
  
 Per ulteriori informazioni sui parametri con valori di tabella in generale, vedere Parametri con valori di [tabella &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqldescribeparam-support-for-enhanced-date-and-time-features"></a>Supporto di SQLDescribeParam per le caratteristiche avanzate di data e ora  
 I valori restituiti per i tipi di data/ora sono i seguenti:  
  
||*DataTypePtr*|*ParameterSizePtr*|*DecimalDigitsPtr*|  
|-|-------------------|------------------------|------------------------|  
|Datetime|SQL_TYPE_TIMESTAMP|23|3|  
|smalldatetime|SQL_TYPE_TIMESTAMP|16|0|  
|Data|SQL_TYPE_DATE|10|0|  
|time|SQL_SS_TIME2|8, 10..16|0..7|  
|datetime2|SQL_TYPE_TIMESTAMP|19, 21..27|0..7|  
|datetimeoffset|SQL_SS_TIMESTAMPOFFSET|26, 28..34|0..7|  
  
 Per ulteriori informazioni, vedere [Miglioramenti di data e ora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqldescribeparam-support-for-large-clr-udts"></a>Supporto di SQLDescribeParam per i tipi CLR definiti dall'utente di grandi dimensioni  
 **SQLDescribeParam** supporta tipi CLR definiti dall'utente (UDT) di grandi dimensioni. Per ulteriori informazioni, vedere [Tipi CLR di grandi dimensioni definiti dall'utente &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLDescribeParamSQLDescribeParam Function](https://go.microsoft.com/fwlink/?LinkId=59339)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
