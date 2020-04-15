---
title: SQLGetInfo (Driver ODBC di Visual FoxPro) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: fbc39e3d-67d9-4331-bf5f-76dbd74c4c45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2d4b976083b46bf632c4890c7fce3b0f13a9a761
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295191"
---
# <a name="sqlgetinfo-visual-foxpro-odbc-driver"></a>SQLGetInfo (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento sono contenute informazioni specifiche del driver ODBC di Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Completo  
  
 Conformità API ODBC: livello 1ODBC API Conformance: Level 1  
  
 Restituisce informazioni generali sul driver ODBC di Visual FoxPro e sull'origine dati associata a un handle di connessione, *hdbc*. Nell'elenco seguente vengono illustrati il valore restituito dal driver ODBC di Visual FoxPro per ogni argomento *fInfoType* e i commenti relativi ai valori restituiti.  
  
 Per ulteriori informazioni, vedere [SQLGetInfo](../../odbc/reference/syntax/sqlgetinfo-function.md) in *ODBC Programmer's Reference*.  
  
## <a name="a"></a>Una  
 SQL_ACCESSIBLE_PROCEDURES restituisce 'N'.  
  
 SQL_ACCESSIBLE_TABLES restituisce 'Y'.  
  
 SQL_ACTIVE_CONNECTIONS restituisce 0.  
  
 SQL_ACTIVE_STATEMENTS restituisce 0.  
  
 SQL_ALTER_TABLE restituisce SQL_AT_ADD_COLUMN o SQL_AT_DROP_COLUMN.  
  
## <a name="b"></a>b  
 SQL_BOOKMARK_PERSISTENCE restituisce SQL_BP_SCROLL.  
  
## <a name="c"></a>C  
 SQL_COLUMN_ALIAS restituisce 'Y'.  
  
 SQL_CONCAT_NULL_BEHAVIOR restituisce SQL_CB_NULL.  
  
 SQL_CONVERT_BIGINT restituisce 0. Il driver ODBC di Visual FoxPro non supporta *BigInt*.  
  
 SQL_CONVERT_BINARY restituisce 0.  
  
 SQL_CONVERT_BIT restituisce 0.  
  
 SQL_CONVERT_CHAR restituisce 0.  
  
 SQL_CONVERT_DATE restituisce 0.  
  
 SQL_CONVERT_DECIMAL restituisce 0.  
  
 SQL_CONVERT_DOUBLE restituisce 0.  
  
 SQL_CONVERT_FLOAT restituisce 0.  
  
 SQL_CONVERT_INTEGER restituisce 0.  
  
 SQL_CONVERT_LONGVARBINARY restituisce 0.  
  
 SQL_CONVERT_LONGVARCHAR restituisce 0.  
  
 SQL_CONVERT_NUMERIC restituisce 0.  
  
 SQL_CONVERT_REAL restituisce 0.  
  
 SQL_CONVERT_SMALLINT restituisce 0.  
  
 SQL_CONVERT_TIME restituisce 0.  
  
 SQL_CONVERT_TIMESTAMP restituisce 0.  
  
 SQL_CONVERT_TINYINT restituisce 0.  
  
 SQL_CONVERT_VARBINARY restituisce 0.  
  
 SQL_CONVERT_VARCHAR restituisce 0.  
  
 SQL_CONVERT_FUNCTIONS restituisce 0.  
  
 SQL_CORRELATION_NAME restituisce SQL_CN_ANY.  
  
 SQL_CURSOR_COMMIT_BEHAVIOR restituisce SQL_CB_PRESERVE.  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR restituisce SQL_CB_PRESERVE.  
  
## <a name="d"></a>D  
 SQL_DATA_SOURCE_NAME restituisce il valore passato come DSN a [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)o [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md); restituisce una stringa vuota se non viene specificato alcun DSN.  
  
 SQL_DATA_SOURCE_READ_ONLY restituisce 'N'.  
  
 SQL_DATABASE_NAME restituisce un percorso UNC completo al database corrente se l'origine dati è un [database](../../odbc/microsoft/visual-foxpro-terminology.md). Se l'origine dati si connette a una directory di [tabelle](../../odbc/microsoft/visual-foxpro-terminology.md), la funzione restituisce il percorso della directory.  
  
 SQL_DBMS_NAME restituisce "Visual FoxPro".  
  
 SQL_DBMS_VER restituisce "03.00.0000".  
  
 SQL_DEFAULT_TXN_ISOLATION restituisce SQL_TXN_READ_COMMITTED. Le letture sporche non sono possibili, ma sono possibili letture e fantasmi non ripetibili.  
  
 SQL_DRIVER_HDBC viene implementata da Gestione Driver.  
  
 SQL_DRIVER_HENV viene implementata da Gestione Driver.  
  
 SQL_DRIVER_HLIB viene implementata da Gestione Driver.  
  
 SQL_DRIVER_HSTMT viene implementata da Gestione Driver.  
  
 SQL_DRIVER_NAME restituisce "vfpodbc.dll".  
  
 SQL_DRIVER_ODBC_VER restituisce "02.50" (SQL_SPEC_MAJOR, SQL_SPEC_MINOR).  
  
 SQL_DRIVER_VER restituisce "01.00.0000".  
  
## <a name="e"></a>E  
 SQL_EXPRESSIONS_IN_ORDERBY restituisce 'N'.  
  
## <a name="f"></a>F  
 SQL_FETCH_DIRECTION restituisce:  
  
-   SQL_FD_FETCH_NEXT  
  
-   SQL_FD_FETCH_FIRST  
  
-   SQL_FD_FETCH_LAST  
  
-   SQL_FD_FETCH_PRIOR  
  
-   SQL_FD_FETCH_ABSOLUTE  
  
-   SQL_FD_FETCH_RELATIVE  
  
-   SQL_FD_FETCH_BOOKMARK.  
  
 SQL_FILE_USAGE restituisce SQL_FILE_QUALIFIER sia per le origini dati di database (file con estensione dbc) che per le origini dati di tabella libera (file con estensione dbf).  
  
## <a name="g-h"></a>G-H  
 SQL_GETDATA_EXENSIONS restituisce:  
  
-   SQL_GD_ANY_COLUMN  
  
-   SQL_GD_ANY_BLOCK  
  
-   SQL_GD_ANY_BOUND  
  
-   SQL_GD_ANY_ORDER  
  
 SQL_GROUP_BY restituisce SQL_GB_NO_RELATION.  
  
## <a name="i-j"></a>I-J  
 SQL_IDENTIFIER_CASE restituisce SQL_IC_MIXED.  
  
 SQL_IDENTIFIER_QUOTE_CHAR restituisce '.  
  
## <a name="k"></a>K  
 SQL_KEYWORDS restituisce "".  
  
## <a name="l"></a>L  
 SQL_LIKE_ESCAPE_CLAUSE restituisce 'N'.  
  
 SQL_LOCK_TYPES restituisce SQL_LCK_NO_CHANGE.  
  
## <a name="m"></a>M  
 SQL_MAX_BINARY_LITERAL_LEN restituisce 0.  
  
 SQL_MAX_CHAR_LITERAL_LEN restituisce 254.  
  
 SQL_MAX_COLUMN_NAME_LEN restituisce 128.  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY restituisce 16.  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY restituisce 16.  
  
 SQL_MAX_COLUMNS_IN_INDEX restituisce 0.  
  
 SQL_MAX_COLUMNS_IN_SELECT restituisce 254.  
  
 SQL_MAX_COLUMNS_IN_TABLE restituisce 254.  
  
 SQL_MAX_CURSOR_NAME_LEN restituisce 254.  
  
 SQL_MAX_INDEX_SIZE restituisce 0.  
  
 SQL_MAX_OWNER_NAME_LEN restituisce 0.  
  
 SQL_MAX_PROCEDURE_NAME_LEN restituisce 0. Il driver ODBC di Visual FoxPro non consente l'accesso diretto alle stored procedure di Visual FoxPro.  
  
 SQL_MAX_QUALIFIER_NAME_LEN restituisce la lunghezza massima del percorso del sistema operativo.  
  
 SQL_MAX_ROW_SIZE restituisce 254.2.  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG restituisce 'N'.  
  
 SQL_MAX_STATEMENT_LEN restituisce 8192.  
  
 SQL_MAX_TABLE_NAME_LEN restituisce 128.  
  
 SQL_MAX_TABLES_IN_SELECT restituisce 16.  
  
 SQL_MAX_USER_NAME_LEN restituisce 0.  
  
 SQL_MULT_RESULT_SETS restituisce 'Y'.  
  
 SQL_MULTIPLE_ACTIVE_TXN restituisce 'Y'. Più connessioni possono avere più transazioni aperte contemporaneamente.  
  
## <a name="n"></a>N  
 SQL_NEED_LONG_DATA_LEN restituisce 'N'.  
  
 SQL_NON_NULLABLE_COLUMNS restituisce SQL_NNC_NON_NULL.  
  
 SQL_NULL_COLLATION restituisce SQL_NC_LOW.  
  
 SQL_NUMERIC_FUNCTIONS restituisce tutte le funzioni ad eccezione di SQL_FN_NUM_POWER, che non è supportata dal driver ODBC di Visual FoxPro. Sono supportate le seguenti funzioni:  
  
-   SQL_FN_NUM_ABS  
  
-   SQL_FN_NUM_ACOS  
  
-   SQL_FN_NUM_ASIN  
  
-   SQL_FN_NUM_ATAN  
  
-   SQL_FN_NUM_ATAN2  
  
-   SQL_FN_NUM_CELING  
  
-   SQL_FN_NUM_COS  
  
-   SQL_FN_NUM_COT  
  
-   SQL_FN_NUM_DEGREES  
  
-   SQL_FN_NUM_EXP  
  
-   SQL_FN_NUM_FLOOR  
  
-   SQL_FN_NUM_LOG  
  
-   SQL_FN_NUM_LOG10  
  
-   SQL_FN_NUM_MOD  
  
-   SQL_FN_NUM_PI  
  
-   SQL_FN_NUM_RADIANS  
  
-   SQL_FN_NUM_RAND  
  
-   SQL_FN_NUM_ROUND  
  
-   SQL_FN_NUM_SIGN  
  
-   SQL_FN_NUM_SIN  
  
-   SQL_FN_NUM_SQRT  
  
-   SQL_FN_NUM_TAN  
  
## <a name="o"></a>O  
 SQL_ODBC_API_CONFORMANCE restituisce SQL_OAC_LEVEL1.  
  
 SQL_ODBC_SAG_CLI_CONFORMANCE restituisce SQL_OSCC_COMPLIANT.  
  
 SQL_ODBC_SQL_CONFORMANCE restituisce SQL_OSC_MINIMUM. Sintassi SQL minima supportata.  
  
 SQL_ODBC_SQL_OPT_IEF restituisce "N".  
  
 SQL_ODBC_VER viene implementata da Gestione Driver.  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT restituisce "N".  
  
 SQL_OUTER_JOINS restituisce "N".  
  
 SQL_OWNER_TERM restituisce "". Il driver ODBC di Visual FoxPro non supporta i proprietari per i relativi oggetti.  
  
 SQL_OWNER_USAGE restituisce 0. Il driver ODBC di Visual FoxPro non supporta i proprietari per i relativi oggetti.  
  
## <a name="p"></a>P  
 SQL_POS_OPERATIONS restituisce SQL_POS_POSITION.  
  
 SQL_POSITIONED_STATEMENTS restituisce 0.  
  
 SQL_PROCEDURE_TERM restituisce "".  
  
 SQL_PROCEDURES restituisce 'N'.  
  
## <a name="q"></a>Q  
 SQL_QUALIFIER_LOCATION restituisce SQL_QL_START.  
  
 SQL_QUALIFIER_NAME_SEPARATOR restituisce '!' o '\\'. Il separatore tra database e tabella è '!'\\per le origini dati connesse [ai database](../../odbc/microsoft/visual-foxpro-terminology.md)e ' ' per le origini dati che sono directory di tabelle [libere.](../../odbc/microsoft/visual-foxpro-terminology.md)  
  
 SQL_QUALIFIER_TERM restituisce "database" o "directory". Il qualificatore è "database" per le origini dati connesse [ai database](../../odbc/microsoft/visual-foxpro-terminology.md)e "directory" per le origini dati che sono directory di [tabelle libere](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 SQL_QUALIFIER_USAGE non supporta SQL_QU_PRIVILEGE_DEFINITION; restituisce SQL_QU_DML_STATEMENT o SQL_QU_TABLE_DEFINITION.  
  
 SQL_QUOTED_IDENTIFIER_CASE restituisce SQL_IC_MIXED.  
  
## <a name="r"></a>R  
 SQL_ROW_UPDATES restituisce "N". Il driver ODBC di Visual FoxPro supporta solo cursori statici e di inoltro.  
  
## <a name="s"></a>S  
 SQL_SCROLL_CONCURRENCY restituisce SQL_SCCO_READ_ONLY.  
  
 SQL_SCROLL_OPTIONS restituisce SQL_SO_STATIC o SQL_SO_READONLY.  
  
 SQL_SEARCH_PATTERN_ESCAPE restituisce "\\".  
  
 SQL_SERVER_NAME restituisce "".  
  
 SQL_SPECIAL_CHARACTERS restituisce il valore ""% "" .  
  
 SQL_STATIC_SENSITIVITY restituisce 0. Il driver ODBC di Visual FoxPro non supporta gli aggiornamenti posizionali.  
  
 SQL_STRING_FUNCTIONS non supporta SQL_FN_STR_INSERT, SQL_FN_STR_LOCATE, SQL_FN_STR_LOCATE_2 o SQL_FN_STR_SOUNDEX.  
  
 Il risultato è il seguente:  
  
-   SQL_FN_STR_ASCII  
  
-   SQL_FN_STR_CHAR  
  
-   SQL_FN_STR_CONCAT  
  
-   SQL_FN_STR_DIFFERENCE  
  
-   SQL_FN_STR_LCASE  
  
-   SQL_FN_STR_LEFT  
  
-   SQL_FN_STR_LENGTH  
  
-   SQL_FN_STR_LTRIM  
  
-   SQL_FN_STR_REPEAT  
  
-   SQL_FN_STR_REPLACE  
  
-   SQL_FN_STR_RIGHT  
  
-   SQL_FN_STR_RTRIM  
  
-   SQL_FN_STR_SUBSTRING  
  
-   SQL_FN_STR_UCASE  
  
-   SQL_FN_STR_SPACE.  
  
 SQL_SUBQUERIES restituisce:  
  
-   SQL_SQ_CORRELATED_SUBQUERIES  
  
-   SQL_SQ_COMPARISON  
  
-   SQL_SQ_EXISTS  
  
-   SQL_SQ_IN  
  
-   SQL_SQ_QUANTIFIED.  
  
 SQL_SYSTEM_FUNCTIONS restituisce:  
  
-   SQL_FN_SYS_DBNAME  
  
-   SQL_FN_SYS_IFNULL  
  
 ma non:  
  
-   SQL_FN_SYS_USERNAME  
  
## <a name="t"></a>T  
 SQL_TABLE_TERM restituisce "tabella".  
  
 SQL_TIMEDATE_ADD_INTERVALS restituisce:  
  
-   SQL_FN_TSI_ SECONDO  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 ma non:  
  
-   SQL_FN_TSI_FRAC_SECOND  
  
-   SQL_FN_TSI_WEEK  
  
-   SQL_FN_TSI_QUARTER  
  
 SQL_TIMEDATE_DIFF_INTERVALS restituisce:  
  
-   SQL_FN_TSI_ SECONDO  
  
-   SQL_FN_TSI_MINUTE  
  
-   SQL_FN_TSI_HOUR  
  
-   SQL_FN_TSI_DAY  
  
-   SQL_FN_TSI_MONTH  
  
-   SQL_FN_TSI_YEAR  
  
 SQL_TIMEDATE_FUNCTIONS non supporta SQL_FN_TD_QUARTER, SQL_FN_TD_TIMESTAMPADD, SQL_FN_TD_DAYOFYEAR o SQL_FN_TD_WEEK.  
  
 Il risultato è il seguente:  
  
-   SQL_FN_TD_CURDATE  
  
-   SQL_FN_TD_CURTIME  
  
-   SQL_FN_TD_DAYNAME  
  
-   SQL_FN_TD_DAYOFMONTH  
  
-   SQL_FN_TD_DAYOFWEEK  
  
-   SQL_FN_TD_HOUR  
  
-   SQL_FN_TD_MINUTE  
  
-   SQL_FN_TD_MONTH  
  
-   SQL_FN_TD_MONTHNAME  
  
-   SQL_FN_TD_NOW  
  
-   SQL_FN_TD_SECOND  
  
-   SQL_FN_TD_TIMESTAMPDIFF  
  
-   SQL_FN_TD_YEAR .  
  
 SQL_TXN_CAPABLE restituisce SQL_TC_DML.  
  
 SQL_TXN_ISOLATION_OPTION restituisce SQL_TXN_READ_COMMITTED.  
  
## <a name="u-z"></a>U-Z  
 SQL_UNION restituisce SQL_U_UNION o SQL_U_UNION_ALL.  
  
 SQL_USER_NAME \<restituisce> vuoto.
