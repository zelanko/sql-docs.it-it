---
title: Supporto per regole, trigger, valori predefiniti e stored procedure . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], stored procedures
- FoxPro ODBC driver [ODBC], commands and functions
- commands for FoxPro ODBC driver [ODBC]
- FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], triggers
- stored procedures [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], rules
- FoxPro commands and functions [ODBC]
- rules [ODBC]
- Visual FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], rules
- functions [ODBC], Visual FoxPro
- default values [ODBC]
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro ODBC driver [ODBC], triggers
- FoxPro ODBC driver [ODBC], stored procedures
- Visual FoxPro commands and functions [ODBC]
ms.assetid: e449de20-d6ca-4902-9f8e-814eb6e86650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2fcf8e7c80b2712313cba81199489dc7cb06dce0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301138"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Supporto di regole, trigger, valori predefiniti e stored procedure (driver ODBC Visual FoxPro)
Non è possibile creare regole, trigger, valori predefiniti o stored procedure di Visual FoxPro utilizzando il driver ODBC di Visual FoxPro. Tuttavia, l'applicazione potrebbe interagire con le regole esistenti, i trigger, i valori predefiniti o le stored procedure durante l'inserimento, l'aggiornamento o l'eliminazione dei dati di Visual FoxPro archiviati in un database.  
  
 Nella tabella seguente sono elencati i comandi e le funzioni di Visual FoxPro supportati dal driver ODBC di Visual FoxPro quando i comandi o le funzioni sono presenti in regole, trigger, valori predefiniti o stored procedure.  
  
 Se l'applicazione interagisce con dati le cui regole, trigger, valori predefiniti o stored procedure chiamano altri comandi o funzioni di Visual FoxPro, il driver genera un errore. Vedere [Comandi e funzioni di Visual FoxPro non supportati](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) per un elenco di comandi e funzioni non supportati dal driver.  
  
> [!TIP]  
>  Se si desidera inserire codice condizionale nelle regole, nei trigger o nelle stored procedure che determinano i comandi da eseguire quando vengono chiamati dal driver, è possibile utilizzare la funzione **VERSION( ).** La funzione **VERSION( )** restituisce "Visual FoxPro ODBC Driver * \<version>*" quando viene chiamata dal driver.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Comandi e funzioni di Visual FoxPro supportati in regole, trigger, valori predefiniti e stored procedure  
  
||||  
|-|-|-|  
|Operatore|Operatore %|Comando &|  
|Comando && |Comando|Comando|  
  
## <a name="a"></a>Una  
  
||||  
|-|-|-|  
|AbS( ) Funzione|Funzione ACOPY( )|Comando AGGIUNGI TABLE|  
|Funzione ADATABASES( )|Funzione ADBOBJECTS( )|Funzione AERROR( )|  
|Funzione ADEL( )|Funzione AELEMENT( )|Funzione ALEN( )|  
|Funzione AFIELDS( )|Funzione AINS( )|ALTER TABLE (comando SQL)|  
|Funzione ALIAS( )|Funzione ALLTRIM( )|Comando APPEND FROM ARRAY|  
|Operatore AND|Comando APPEND|Comando APPEND MEMO|  
|Comando APPEND FROM|Comando APPEND GENERAL|Funzione ASCAN( )|  
|Comando APPEND PROCEDURES|Funzione ASC( )|Funzione ASUBSCRIPT( )|  
|Funzione ARCIN( )|Funzione ASORT( )|Funzione ATAN( )|  
|Funzione AT( )|Funzione AT_C( )|Funzione ATCLINE( )|  
|ATC( ) Funzione|Funzione ATCC( )|Funzione AUSED( )|  
|Funzione ATLINE( )|Funzione ATN2( )||  
|Comando MEDIA|Funzione ACOS( )||  
  
## <a name="b"></a>b  
  
||||  
|-|-|-|  
|Comando BEGIN TRANSACTION|Funzione BETWEEN( )|Funzione BITNOT( )|  
|Funzione BITCLEAR( )|Funzione BITLSHIFT( )|Funzione BITSET( )|  
|Funzione BITOR( )|Funzione BITRSHIFT( )|Comando BLANK|  
|Funzione BITTEST( )|Funzione BITXOR( )||  
|Funzione BOF( )|Funzione BITAND( )||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Comando CALCULATE|Funzione CANDIDATE( )|Funzione CHR( )|  
|Funzione CDX( )|Funzione CEILING( )|Comandi CLOSE|  
|Funzione CHRTRAN( )|Funzione CHRTRANC( )|Comando COPY INDEXES|  
|Funzione CMONTH( )|Comando CONTINUE|Comando COPY STRUCTURE EXTENDED|  
|Comando COPY PROCEDURES|Comando COPY STRUCTURE|Comando COPY TO|  
|Comando COPY TAG|Comando COPIA A ARRAY|Funzione CPCONVERT( )|  
|Funzione COS( )|Comando COUNT|Funzione CTOD( )|  
|Funzione CPCURRENT( )|Funzione CPDBF( )|Funzione CURSORSETPROP( )|  
|Funzione CTOT( )|Funzione CURSORGETPROP( )||  
|Funzione CURVAL( )|Funzione CDOW( )||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Funzione DATE( )|Funzione DATETIME( )|Funzione DAY( )|  
|Funzione DBC( )|Funzione DBF( )|Funzione DBGETPROP( )|  
|DbUSED( ) (funzione)|DELETE (comando SQL)|Comando DELETE|  
|DELETE TAG (comando)|Funzione DELETED( )|Funzione DESCENDING( )|  
|Funzione DIFFERENCE( )|Comando DIMENSION|Funzione DISKSPACE( )|  
|Funzione DMY( )|FARE CASO ... Comando ENDCASE|Comando DO|  
|FARE MENTRE ... Comando ENDDO|Funzione DOW( )|Funzione DTOC( )|  
|Funzione DTOR( )|Funzione DTOS( )|Funzione DTOT( )|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Funzione EMPTY( )|Funzione EVALUATE( )|Comando EXIT|  
|Funzione ERROR( )|Funzione EXP( )||  
|Comando END TRANSACTION|Funzione EOF( )||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|FCOUNT( ) Funzione|Funzione FDATE( )|Funzione FIELD( )|  
|Funzione FILE( )|Funzione FILTER( )|Funzione FLDLIST( )|  
|Funzione FLOCK( )|Funzione FLOOR( )|Comando FLUSH|  
|Per... Comando ENDFOR|Funzione FOR( )|Funzione FOUND( )|  
|Comando TABELLA GRATUITO|Funzione FSI-E( )|FTIME( ) Funzione|  
|Funzione FULLPATH( )|Comando FUNCTION|FV( ) Funzione|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|Comando GATHER|Funzione GETNEXTMODIFIED( )|Comando GO/GOTO|  
|Funzione GETFLDSTATE( )|Funzione GOMONTH( )||  
|Funzione GETCP( )|Funzione GETENV( )||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|Funzione HEADER( )|Funzione HOUR( )|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Funzione IDXCOLLATE( )|Se... Comando ENDIF|Funzione IIF( )|  
|Funzione INDBC( )|INDEX (comando)|Funzione INLIST( )|  
|Comando INSERT-SQL|Funzione INT( )|Funzione ISALPHA( )|  
|Funzione ISBLANK( )|Funzione ISDIGIT( )|Funzione ISEXCLUSIVE( )|  
|Funzione ISLEADBYTE( )|Funzione ISLOWER( )|Funzione ISNULL( )|  
|Funzione ISREADONLY( )|Funzione ISUPPER( )||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Funzione KEY( )|Funzione KEYMATCH( )||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Funzione LEFT( )|Funzione LEFTC( )|Funzione LIKEC( )|  
|Funzione LENC( )|Funzione LIKE( )|Funzione LOCK( )|  
|Comando LOCAL|Comando LOCATE|Funzione LOOKUP( )|  
|Funzione LOG( )|Funzione LOG10( )|Funzione LTRIM( )|  
|Funzione LOWER( )|Comando LPARAMETERS||  
|Funzione LUPDATE( )|Funzione LEN( )||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE variabile di memoria di sistema|Funzione MAX( )|Funzione MDX( )|  
|Funzione MDY( )|Funzione MEMLINES( )|Funzione MESSAGE( )|  
|Funzione MIN( )|Funzione MINUTE( )|Funzione MLINE( )|  
|Funzione MOD( )|Funzione MONTH( )|Funzione MTON( )|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Funzione NDX( )|Funzione DI CONESI.|Operatore NOT|  
|NOTE Comando|Funzione NTOM( )|Funzione NVL( )|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Funzione OCCURS( )|Funzione OLDVAL( )|On ERRORE Comando|  
|Comando ON KEY|Funzione ON( )|Comando OPEN DATABASE|  
|Operatore OR|Funzione ORDER( )|Funzione OS( )|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Comando PACK|Funzione PARAMETERS( )|Funzione PAYMENT( )|  
|Comando PARAMETERS|Funzione PRIMARY( )|Comando PRIVATE|  
|Funzione PI( )|Funzione PROGRAM( )|Funzione MAIUSC( )|  
|Comando PROCEDURE|Funzione PV( )||  
|Comando PUBBLICO|Funzioni PADL( ) &#124; PADR( ) &#124; PADC( )||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Funzione RAND( )|Funzione RAT( )|Funzione RATC( )|  
|Funzione RATLINE( )|Comando RECALL|Funzione RECCOUNT( )|  
|Funzione RECNO( )|Funzione RECSI-E( )|Comando REGIONALE|  
|Funzione RELATION( )|Comando REMOVE TABLE|Comando REPLACE|  
|Comando REPLACE FROM ARRAY|Funzione REPLICATE( )|Comando RETRY|  
|Comando RETURN|Funzione RIGHT( )|Funzione RIGHTC( )|  
|Funzione RLOCK( )|Comando ROLLBACK|Funzione ROUND( )|  
|Funzione RTOD( )|Funzione RTRIM( )||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|Scansione... Comando ENDSCAN|Comando SCATTER|Funzione SEC( )|  
|Funzione SECONDS( )|Comando SEEK|Funzione SEEK( )|  
|Comando SELECT|Funzione SELECT( )|Comando SELECT-SQL|  
|SET BLOCKSIZE (comando)|Comando SET CARRY|Comando SET CENTURY|  
|SET COLLATE (comando)|Comando SET DATABASE|Comando SET DATE|  
|Comando SET DEFAULT|SET DELETED (comando)|SET EXACT (comando)|  
|SET EXCLUSIVE (comando)|Comando SET FDOW|Comando SET FIELDS|  
|Comando SET FILTER|Comando SET FIXED|Comando SET FULLPATH|  
|Comando SET FWEEK|Comando SET HOURS|Comando SET INDEX|  
|Comando SET LOCK|Comando SET MULTILOCKS|Comando SET NEAR|  
|Comando SET NOCPTRANS|Comando SET NOTIFY|SET NULL (comando)|  
|Comando SET OPTIMIE|Comando SET ORDER|SET PATH (comando)|  
|Comando SET PROCEDURE|Comando SET RELATION|Comando SET RELATION OFF|  
|SET REPROCESS (comando)|Comando SET SKIP|Comando SET UDFPARMS|  
|SET UNIQUE (comando)|Comando SET VOLUME|Funzione SET( )|  
|Funzione SETFLDSTATE( )|Funzione SIGN ( )|Funzione SIN( )|  
|Comando SKIP|Comando SORT|Funzione SPACE( )|  
|Funzione SQRT( )|Comando STORE|Funzione STR( )|  
|Funzione STRCONV( )|Funzione STRTRAN( )|Funzione STUFF( )|  
|Funzione STUFFC( )|Funzione SUBSTR( )|Funzione SUBSTRC( )|  
|Comando SOMMA|Funzione SYS(2011)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY variabile di memoria di sistema|_TRIGGERLEVEL variabile di memoria di sistema|Funzione TAGCOUNT( )|  
|Funzione TABLEUPDATE( )|Funzione TAG( )|Funzione TARGET( )|  
|Funzione TAGNO( )|Funzione TAN( )|Funzione TRIM( )|  
|Funzione TIME( )|Comando TOTALE|Funzione TXNLEVEL( )|  
|Funzione TTOC( )|Funzione TTOD( )||  
|Funzione TYPE( )|Funzione TABLEREVERT( )||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Funzione UNIQUE( )|Comando UNLOCK|Comando USO|  
|Comando UPDATE|Funzione UPPER( )||  
|Funzione USED( )|UPDATE (comando SQL)||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Funzione VAL( )|Funzione VERSION( )||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Funzione WEEK( )|||  
  
## <a name="y"></a>S  
  
||||  
|-|-|-|  
|Funzione ANNO( )|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando AP|||
