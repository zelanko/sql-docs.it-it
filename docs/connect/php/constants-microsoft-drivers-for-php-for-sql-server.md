---
title: Costanti (driver Microsoft per PHP per SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/11/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- constants
ms.assetid: 9727c944-b645-48d6-9012-18dbde35ee3c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 82fa4ef2f47143afe8f2331469a1eb07fd9b2522
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66796228"
---
# <a name="constants-microsoft-drivers-for-php-for-sql-server"></a>Costanti (driver Microsoft per PHP per SQL Server)
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In questo argomento sono descritte le costanti definite per dai [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
## <a name="pdosqlsrv-driver-constants"></a>Costanti del driver PDO_SQLSRV  
Le costanti elencate nel [sito Web PDO](https://php.net/manual/book.pdo.php) sono valide nei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  
  
Di seguito sono descritte le costanti specifiche di Microsoft del driver PDO_SQLSRV.  
  
### <a name="transaction-isolation-level-constants"></a>Costanti del livello di isolamento delle transazioni  
La chiave **TransactionIsolation** usata con [PDO::__construct](../../connect/php/pdo-construct.md)accetta una delle costanti seguenti:  
  
-   PDO::SQLSRV_TXN_READ_UNCOMMITTED  
  
-   PDO::SQLSRV_TXN_READ_COMMITTED  
  
-   PDO::SQLSRV_TXN_REPEATABLE_READ  
  
-   PDO::SQLSRV_TXN_SNAPSHOT  
  
-   PDO::SQLSRV_TXN_SERIALIZABLE  
  
Per altre informazioni sulla chiave **TransactionIsolation** , vedere [Connection Options](../../connect/php/connection-options.md).  
  
### <a name="encoding-constants"></a>Costanti di codifica  
L'attributo PDO::SQLSRV_ATTR_ENCODING può essere passato a [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), [PDO::setAttribute](../../connect/php/pdo-setattribute.md), [PDO::prepare](../../connect/php/pdo-prepare.md), [PDOStatement::bindColumn](../../connect/php/pdostatement-bindcolumn.md) e [PDOStatement::bindParam](../../connect/php/pdostatement-bindparam.md).  
  
I valori disponibili da passare a PDO::SQLSRV_ATTR_ENCODING sono  
  
|Costante del driver PDO_SQLSRV|Descrizione|  
|-------------------------------|---------------|  
|PDO::SQLSRV_ENCODING_BINARY|I dati sono un flusso di byte non elaborati proveniente dal server senza alcuna codifica o conversione.<br /><br />Non valido per PDO::setAttribute.|  
|PDO::SQLSRV_ENCODING_SYSTEM|I dati sono caratteri a 8 bit come specificato nella tabella codici delle impostazioni locali di Windows impostate nel sistema. Eventuali caratteri multibyte o che non eseguono il mapping in questa tabella codici vengono sostituiti con un carattere punto interrogativo (?) a byte singolo.|  
|PDO::SQLSRV_ENCODING_UTF8|I dati hanno il formato di codifica UTF-8. Si tratta della codifica predefinita.|  
|PDO::SQLSRV_ENCODING_DEFAULT|Usa PDO::SQLSRV_ENCODING_SYSTEM se specificato durante la connessione.<br /><br />Usare la codifica della connessione se specificato in un'istruzione prepare.|  
  
### <a name="query-timeout"></a>Timeout query  
L'attributo PDO::SQLSRV_ATTR_QUERY_TIMEOUT è un intero non negativo che rappresenta il periodo di timeout espresso in secondi. L'impostazione predefinita è zero (0) e indica nessun timeout.  
  
È possibile specificare l'attributo PDO::SQLSRV_ATTR_QUERY_TIMEOUT con [PDOStatement::setAttribute](../../connect/php/pdostatement-setattribute.md), [PDO::setAttribute](../../connect/php/pdo-setattribute.md) e [PDO::prepare](../../connect/php/pdo-prepare.md).  
  
### <a name="direct-or-prepared-execution"></a>Esecuzione diretta o preparata  
È possibile selezionare l'esecuzione di query diretta o l'esecuzione di istruzione preparata con l'attributo PDO::SQLSRV_ATTR_DIRECT_QUERY. PDO::SQLSRV_ATTR_DIRECT_QUERY può essere impostato con [PDO::prepare](../../connect/php/pdo-prepare.md) o [PDO::setAttribute](../../connect/php/pdo-setattribute.md). Per altre informazioni su PDO::SQLSRV_ATTR_DIRECT_QUERY, vedere [Esecuzione di istruzioni diretta e preparata nel driver PDO_SQLSRV](../../connect/php/direct-statement-execution-prepared-statement-execution-pdo-sqlsrv-driver.md).  

### <a name="handling-numeric-fetches"></a>Gestione delle operazioni di recupero numerico
L'attributo PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE utilizzabile per gestire operazioni di recupero numerici dalle colonne con tipi numerici SQL (bit, integer, smallint, tinyint, float e real). Quando PDO::SQLSRV_ATTR_FETCHES_NUMERIC_TYPE è impostata su true, i risultati di una colonna integer sono rappresentati come valori int, mentre si muove SQL reals sono rappresentati come valori a virgola mobile. Questo attributo può essere impostato con [pdostatement:: SetAttribute](../../connect/php/pdostatement-setattribute.md). 

È possibile modificare il comportamento di formattazione decimale predefinito con gli attributi PDO::SQLSRV_ATTR_FORMAT_DECIMALS e PDO::SQLSRV_ATTR_DECIMAL_PLACES. Il comportamento di questi attributi è identico per le opzioni corrispondenti sul lato SQLSRV (**FormatDecimals** e **DecimalPlaces**), ad eccezione del fatto che i parametri di output non sono supportati per la formattazione. Questi attributi possono essere impostati a livello di connessione o di istruzione con [PDO:: SetAttribute](../../connect/php/pdo-setattribute.md) oppure [pdostatement:: SetAttribute](../../connect/php/pdostatement-setattribute.md), ma verrà esegue l'override di qualsiasi attributo di istruzione corrispondente attributo di connessione. Per altri dettagli, vedere [Formattazione di stringhe decimali e valori money (driver PDO_SQLSRV)](../../connect/php/formatting-decimals-pdo-sqlsrv-driver.md).

### <a name="handling-date-and-time-fetches"></a>Gestione di recuperi di data e ora

Il PDO::SQLSRV_ATTR_FETCHES_DATETIME_TYPE specifica se recuperare i tipi di data e ora come [DateTime PHP](http://php.net/manual/en/class.datetime.php) oggetti. Se false, il comportamento predefinito è restituirli come stringhe. Questo attributo può essere impostato a livello di connessione o di istruzione con [PDO:: SetAttribute](../../connect/php/pdo-setattribute.md) oppure [pdostatement:: SetAttribute](../../connect/php/pdostatement-setattribute.md), ma eseguirà l'override dell'attributo di istruzione corrispondente attributo di connessione. Per altre informazioni, vedere [Procedura: Recuperare i tipi di data e ora come oggetti DateTime PHP usando il driver PDO_SQLSRV](../../connect/php/how-to-retrieve-datetime-objects-using-pdo-sqlsrv-driver.md).

## <a name="sqlsrv-driver-constants"></a>SQLSRV  
Nelle sezioni seguenti sono elencate le costanti usate dal driver SQLSRV.  
  
### <a name="err-constants"></a>Costanti ERR  
Nella tabella seguente vengono elencate le costanti usate per specificare se [sqlsrv_errors](../../connect/php/sqlsrv-errors.md) restituisce errori, avvisi o entrambi.  
  
|valore|Descrizione|  
|---------|---------------|  
|SQLSRV_ERR_ALL|Vengono restituiti gli errori e gli avvisi generati nell'ultima chiamata di funzione **sqlsrv** . Si tratta del valore predefinito.|  
|SQLSRV_ERR_ERRORS|Vengono restituiti gli errori generati nell'ultima chiamata di funzione **sqlsrv** .|  
|SQLSRV_ERR_WARNINGS|Vengono restituiti gli avvisi generati nell'ultima chiamata di funzione **sqlsrv** .|  
  
### <a name="fetch-constants"></a>Costanti FETCH  
Nella tabella seguente sono elencate le costanti usate per specificare il tipo di matrice restituita da [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md).  
  
|Costante SQLSRV|Descrizione|  
|-------------------|---------------|  
|SQLSRV_FETCH_ASSOC|**sqlsrv_fetch_array** restituisce la riga di dati successiva come matrice associativa.|  
|SQLSRV_FETCH_BOTH|**sqlsrv_fetch_array** restituisce la riga di dati successiva come matrice con chiavi numeriche e associative. Si tratta del valore predefinito.|  
|SQLSRV_FETCH_NUMERIC|**sqlsrv_fetch_array** restituisce la riga di dati successiva come matrice indicizzata numericamente.|  
  
### <a name="logging-constants"></a>Costanti di registrazione  
In questa sezione sono elencate le costanti usate per modificare le impostazioni di registrazione con [sqlsrv_configure](../../connect/php/sqlsrv-configure.md). Per altre informazioni sulla registrazione, vedere [Logging Activity](../../connect/php/logging-activity.md).  
  
Nella tabella seguente sono elencate le costanti che possono essere usate come valore dell'impostazione **LogSubsystems** :  
  
|Costante SQLSRV (intero equivalente tra parentesi)|Descrizione|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL (-1)|Attiva la registrazione di tutti i sottosistemi.|  
|SQLSRV_LOG_SYSTEM_CONN (2)|Attiva la registrazione dell'attività di connessione.|  
|SQLSRV_LOG_SYSTEM_INIT (1)|Attiva la registrazione dell'attività di inizializzazione.|  
|SQLSRV_LOG_SYSTEM_OFF (0)|Disattiva la registrazione.|  
|SQLSRV_LOG_SYSTEM_STMT (4)|Attiva la registrazione delle attività delle istruzioni.|  
|SQLSRV_LOG_SYSTEM_UTIL (8)|Attiva la registrazione delle attività delle funzioni di errore, ad esempio **handle_error** e **handle_warning**.|  
  
Nella tabella seguente sono elencate le costanti che possono essere usate come valore dell'impostazione **LogSeverity** :  
  
|Costante SQLSRV (intero equivalente tra parentesi)|Descrizione|  
|----------------------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL (-1)|Specifica la registrazione di errori, avvisi e notifiche.|  
|SQLSRV_LOG_SEVERITY_ERROR (1)|Specifica la registrazione degli errori.|  
|SQLSRV_LOG_SEVERITY_NOTICE (4)|Specifica la registrazione delle notifiche.|  
|SQLSRV_LOG_SEVERITY_WARNING (2)|Specifica la registrazione degli avvisi.|  
  
### <a name="nullable-constants"></a>Costanti di ammissione dei valori Null  
Nella tabella seguente sono elencate le costanti che è possibile usare per determinare se una colonna ammette i valori Null o se queste informazioni non sono disponibili. È possibile confrontare il valore della chiave **Nullable** restituita da [sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md) per determinare se la colonna ammette valori Null.  
  
|Costante SQLSRV (intero equivalente tra parentesi)|Descrizione|  
|----------------------------------------------------------|---------------|  
|SQLSRV_NULLABLE_YES (0)|La colonna ammette i valori Null.|  
|SQLSRV_NULLABLE_NO (1)|La colonna non ammette i valori Null.|  
|SQLSRV_NULLABLE_UNKNOWN (2)|Non è noto se la colonna ammette i valori Null.|  
  
### <a name="param-constants"></a>Costanti PARAM  
Di seguito sono elencate le costanti che specificano la direzione dei parametri quando si chiama [sqlsrv_query](../../connect/php/sqlsrv-query.md) o [sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md).  
  
|Costante SQLSRV|Descrizione|  
|-------------------|---------------|  
|SQLSRV_PARAM_IN|Indica un parametro di input.|  
|SQLSRV_PARAM_INOUT|Indica un parametro bidirezionale.|  
|SQLSRV_PARAM_OUT|Indica un parametro di output.|  
  
### <a name="phptype-constants"></a>Costanti PHPTYPE  
Nella tabella seguente sono elencate le costanti che vengono usate per descrivere i tipi di dati PHP. Per informazioni sui tipi di dati PHP, vedere [Tipi PHP](https://php.net/manual/en/language.types.php).  
  
|Costante SQLSRV|Tipo di dati PHP|  
|-------------------|-----------------|  
|SQLSRV_PHPTYPE_INT|Valore intero|  
|SQLSRV_PHPTYPE_DATETIME|DATETIME|  
|SQLSRV_PHPTYPE_FLOAT|float|  
|SQLSRV_PHPTYPE_STREAM($encoding<sup>1</sup>)|STREAM|  
|SQLSRV_PHPTYPE_STRING($encoding<sup>1</sup>)|String|  
  
1. **SQLSRV_PHPTYPE_STREAM** e **SQLSRV_PHPTYPE_STRING** accettano un parametro che specifica la codifica del flusso. Nella tabella seguente sono elencate le costanti SQLSRV che sono parametri accettabili e viene fornita una descrizione della codifica corrispondente.  
  
|Costante SQLSRV|Descrizione|  
|-------------------|---------------|  
|SQLSRV_ENC_BINARY|I dati vengono restituiti come flusso di byte non elaborati proveniente dal server senza alcuna codifica o conversione.|  
|SQLSRV_ENC_CHAR|I dati vengono restituiti come caratteri a 8 bit come specificato nella tabella codici delle impostazioni locali di Windows impostate nel sistema. Eventuali caratteri multibyte o che non eseguono il mapping in questa tabella codici vengono sostituiti con un carattere punto interrogativo (?) a byte singolo.<br /><br />Si tratta della codifica predefinita.|  
|"UTF-8"|I dati vengono restituiti nel formato di codifica UTF-8. Questa costante è stata aggiunta nella versione 1.1 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. Per altre informazioni sul supporto UTF-8, vedere [Procedura: Invio e recupero di dati UTF-8 con il supporto incorporato di UTF-8](../../connect/php/how-to-send-and-retrieve-utf-8-data-using-built-in-utf-8-support.md).|  
  
> [!NOTE]  
> Quando si usa **SQLSRV_PHPTYPE_STREAM** oppure **SQLSRV_PHPTYPE_STRING**, è necessario specificare la codifica. Se non viene fornito alcun parametro, verrà restituito un errore.  
  
Per altre informazioni su queste costanti, vedere [Procedura: Specificare i tipi di dati PHP](../../connect/php/how-to-specify-php-data-types.md), [Procedura: Recupero di dati di tipo carattere come flusso usando il driver SQLSRV](../../connect/php/how-to-retrieve-character-data-as-a-stream-using-the-sqlsrv-driver.md).  
  
### <a name="sqltype-constants"></a>Costanti SQLTYPE  
Nella tabella seguente sono elencate le costanti che vengono usate per descrivere i tipi di dati di SQL Server. Alcune costanti sono simili a funzione e possono accettare parametri che corrispondono alla precisione, scala e lunghezza.  Quando si associano parametri, usare le costanti di tipo funzione. Per i confronti di tipo, le costanti (funzione non-like) standard sono necessari. Per informazioni sui tipi di dati di SQL Server, vedere [Tipi di dati (Transact-SQL).](../../t-sql/data-types/data-types-transact-sql.md) Per informazioni su precisione, scala e lunghezza, vedere [Precisione, scala e lunghezza (Transact-SQL)](../../t-sql/data-types/precision-scale-and-length-transact-sql.md).  
  
|Costante SQLSRV|Tipo di dati di SQL Server|  
|-------------------|------------------------|  
|SQLSRV_SQLTYPE_BIGINT|BIGINT|  
|SQLSRV_SQLTYPE_BINARY|BINARY|  
|SQLSRV_SQLTYPE_BIT|bit|  
|SQLSRV_SQLTYPE_CHAR|char<sup>5</sup>|  
|SQLSRV_SQLTYPE_CHAR($charCount)|char|  
|SQLSRV_SQLTYPE_DATE|date<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIME|DATETIME|  
|SQLSRV_SQLTYPE_DATETIME2|datetime2<sup>4</sup>|  
|SQLSRV_SQLTYPE_DATETIMEOFFSET|datetimeoffset<sup>4</sup>|  
|SQLSRV_SQLTYPE_DECIMAL|decimal<sup>5</sup>|
|SQLSRV_SQLTYPE_DECIMAL($precision, $scale)|Decimal|  
|SQLSRV_SQLTYPE_FLOAT|FLOAT|  
|SQLSRV_SQLTYPE_IMAGE|image<sup>1</sup>|  
|SQLSRV_SQLTYPE_INT|INT|  
|SQLSRV_SQLTYPE_MONEY|money| 
|SQLSRV_SQLTYPE_NCHAR|nchar<sup>5</sup>|   
|SQLSRV_SQLTYPE_NCHAR($charCount)|NCHAR|  
|SQLSRV_SQLTYPE_NUMERIC|numeric<sup>5</sup>|
|SQLSRV_SQLTYPE_NUMERIC($precision, $scale)|NUMERIC|  
|SQLSRV_SQLTYPE_NVARCHAR|nvarchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_NVARCHAR($charCount)|NVARCHAR|  
|SQLSRV_SQLTYPE_NVARCHAR('max')|nvarchar(MAX)|  
|SQLSRV_SQLTYPE_NTEXT|ntext<sup>2</sup>|  
|SQLSRV_SQLTYPE_REAL|REAL|  
|SQLSRV_SQLTYPE_SMALLDATETIME|smalldatetime|  
|SQLSRV_SQLTYPE_SMALLINT|SMALLINT|  
|SQLSRV_SQLTYPE_SMALLMONEY|SMALLMONEY|  
|SQLSRV_SQLTYPE_TEXT|text<sup>3</sup>|  
|SQLSRV_SQLTYPE_TIME|time<sup>4</sup>|  
|SQLSRV_SQLTYPE_TIMESTAMP|TIMESTAMP|  
|SQLSRV_SQLTYPE_TINYINT|TINYINT|  
|SQLSRV_SQLTYPE_UNIQUEIDENTIFIER|UNIQUEIDENTIFIER|  
|SQLSRV_SQLTYPE_UDT|UDT (tipo definito dall'utente)|  
|SQLSRV_SQLTYPE_VARBINARY|varbinary<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARBINARY($byteCount)|varbinary|  
|SQLSRV_SQLTYPE_VARBINARY('max')|varbinary(MAX)|  
|SQLSRV_SQLTYPE_VARCHAR|varchar<sup>5</sup>|  
|SQLSRV_SQLTYPE_VARCHAR($charCount)|varchar|  
|SQLSRV_SQLTYPE_VARCHAR('max')|varchar(MAX)|  
|SQLSRV_SQLTYPE_XML|xml|  
  
1.  Si tratta di un tipo legacy che esegue il mapping al tipo varbinary(max).  
  
2.  Si tratta di un tipo legacy che esegue il mapping al nuovo tipo nvarchar.  
  
3.  Si tratta di un tipo legacy che esegue il mapping al nuovo tipo varchar.  
  
4.  Il supporto di questo tipo è stato aggiunto nella versione 1.1 dei [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)].  

5.  Queste costanti devono essere utilizzate nelle operazioni di confronto di tipo e non sostituiscono le costanti di tipo funzione con una sintassi simile. Per l'associazione di parametri, è necessario utilizzare le costanti di tipo funzione.

  
Nella tabella seguente sono elencate le costanti SQLTYPE che accettano parametri e l'intervallo di valori consentito per il parametro.  
  
|SQLTYPE|Parametro|Intervallo consentito per il parametro|  
|-----------|-------------|---------------------------------|  
|SQLSRV_SQLTYPE_CHAR,<br /><br />SQLSRV_SQLTYPE_VARCHAR|charCount|1 - 8000|  
|SQLSRV_SQLTYPE_NCHAR,<br /><br />SQLSRV_SQLTYPE_NVARCHAR|charCount|1 - 4000|  
|SQLSRV_SQLTYPE_BINARY,<br /><br />SQLSRV_SQLTYPE_VARBINARY|byteCount|1 - 8000|  
|SQLSRV_SQLTYPE_DECIMAL,<br /><br />SQLSRV_SQLTYPE_NUMERIC|precisione|1 - 38|  
|SQLSRV_SQLTYPE_DECIMAL,<br /><br />SQLSRV_SQLTYPE_NUMERIC|scala|1 - precisione|  
  
### <a name="transaction-isolation-level-constants"></a>Costanti del livello di isolamento delle transazioni  
La chiave **TransactionIsolation** usata con [sqlsrv_connect](../../connect/php/sqlsrv-connect.md)accetta una delle costanti seguenti:  
  
-   SQLSRV_TXN_READ_UNCOMMITTED  
  
-   SQLSRV_TXN_READ_COMMITTED  
  
-   SQLSRV_TXN_REPEATABLE_READ  
  
-   SQLSRV_TXN_SNAPSHOT  
  
-   SQLSRV_TXN_SERIALIZABLE  
  
### <a name="cursor-and-scrolling-constants"></a>Costanti di cursore e scorrimento  
Le seguenti costanti specificano il tipo di cursore che è possibile usare in un set di risultati:  
  
-   SQLSRV_CURSOR_FORWARD  
  
-   SQLSRV_CURSOR_STATIC  
  
-   SQLSRV_CURSOR_DYNAMIC  
  
-   SQLSRV_CURSOR_KEYSET  
  
-   SQLSRV_CURSOR_CLIENT_BUFFERED  
  
Le seguenti costanti specificano la riga da selezionare nel set di risultati:  
  
-   SQLSRV_SCROLL_NEXT  
  
-   SQLSRV_SCROLL_PRIOR  
  
-   SQLSRV_SCROLL_FIRST  
  
-   SQLSRV_SCROLL_LAST  
  
-   SQLSRV_SCROLL_ABSOLUTE  
  
-   SQLSRV_SCROLL_RELATIVE  
  
Per informazioni sull'uso delle costanti, vedere [Specifying a Cursor Type and Selecting Rows](../../connect/php/specifying-a-cursor-type-and-selecting-rows.md).  
  
## <a name="see-also"></a>Vedere anche  
[Riferimento all'API del driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  
