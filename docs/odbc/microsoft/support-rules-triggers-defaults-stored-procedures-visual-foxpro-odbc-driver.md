---
title: Supporto per regole, trigger, valori predefiniti e stored procedure | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301138"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Supporto di regole, trigger, valori predefiniti e stored procedure (driver ODBC Visual FoxPro)
Non è possibile creare regole, trigger, valori predefiniti o stored procedure Visual FoxPro utilizzando il driver ODBC Visual FoxPro. Tuttavia, l'applicazione potrebbe interagire con regole, trigger, valori predefiniti o stored procedure esistenti durante l'inserimento, l'aggiornamento o l'eliminazione dei dati Visual FoxPro archiviati in un database.  
  
 Nella tabella seguente sono elencati i comandi e le funzioni di Visual FoxPro supportati dal driver ODBC Visual FoxPro quando i comandi o le funzioni sono presenti in regole, trigger, valori predefiniti o stored procedure.  
  
 Se l'applicazione interagisce con i dati le cui regole, trigger, valori predefiniti o stored procedure chiamano qualsiasi altra funzione o comando Visual FoxPro, il driver genera un errore. Vedere [comandi e funzioni Visual FoxPro](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) non supportati per un elenco di comandi e funzioni non supportati dal driver.  
  
> [!TIP]  
>  Se si desidera inserire codice condizionale nelle regole, nei trigger o nelle stored procedure che determinano i comandi da eseguire quando vengono chiamati dal driver, è possibile utilizzare la funzione **Version ()** . La funzione **Version ()** restituisce "Visual FoxPro ODBC driver * \<Version>*" quando viene chiamato dal driver.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Comandi e funzioni di Visual FoxPro supportati in regole, trigger, valori predefiniti e stored procedure  
  
||||  
|-|-|-|  
|Operatore $|Operatore %|Comando &|  
|Comando && |* Comando|= (Comando)|  
  
## <a name="a"></a>Una  
  
||||  
|-|-|-|  
|Funzione ABS ()|Funzione ACOPY ()|Comando Aggiungi tabella|  
|Funzione ADATABASES ()|Funzione ADBOBJECTS ()|Funzione AERROR ()|  
|Funzione ADEL ()|Funzione AELEMENT ()|Funzione ALEN ()|  
|()-Funzione|Funzione AINS ()|ALTER TABLE (comando SQL)|  
|Funzione ALIAS ()|Funzione ALLTRIM ()|Comando ACCODA da matrice|  
|Operatore AND|Comando APPEND|Comando APPEND MEMO|  
|Comando ACCODA da|ACCODA comando generale|Funzione ASCAN ()|  
|Comando APPEND PROCEDURES|Funzione ASC ()|Funzione ASUBSCRIPT ()|  
|ASIN () (funzione)|Funzione ASORT ()|Funzione ATAN ()|  
|AT () (funzione)|Funzione AT_C ()|Funzione ATCLINE ()|  
|Funzione ATC ()|Funzione ATCC ()|Funzione AUSED ()|  
|Funzione ATLINE ()|Funzione ATN2 ()||  
|MEDIA comando|Funzione ARCCOS ()||  
  
## <a name="b"></a>b  
  
||||  
|-|-|-|  
|Comando BEGIN TRANSACTION|Funzione BETWEEN ()|Funzione BITNOT ()|  
|Funzione BITCLEAR ()|Funzione BITLSHIFT ()|Funzione BITSt ()|  
|Funzione BITOR ()|Funzione BITRSHIFT ()|Comando BLANK|  
|Funzione BITTEST ()|Funzione BITXOR ()||  
|Funzione BOF ()|Funzione BITAND ()||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|Comando CALCULATE|Funzione CANDIDAta ()|Funzione CHR ()|  
|Funzione CDX ()|Funzione CEILING ()|Chiudi comandi|  
|Funzione CHRTRAN ()|Funzione CHRTRANC ()|Comando copia indici|  
|Funzione CMONTH ()|Comando CONTINUE|COPY STRUCTURE-comando esteso|  
|Comando COPY PROCEDURES|Comando Copia struttura|COPIA in comando|  
|Comando COPY TAG|Comando COPY TO ARRAY|Funzione CPCONVERT ()|  
|Funzione COS ()|Comando COUNT|Funzione CTOD ()|  
|Funzione CPCURRENT ()|Funzione CPDBF ()|Funzione CURSORSETPROP ()|  
|Funzione CTOT ()|Funzione CURSORGETPROP ()||  
|Funzione curvy ()|Funzione CDOW ()||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Funzione DATE ()|DATETIME () (funzione)|Funzione DAY ()|  
|Funzione DBC ()|Funzione DBF ()|Funzione DBGETPROP ()|  
|Funzione DBUSed ()|DELETE (comando SQL)|Comando DELETE|  
|DELETE TAG (comando)|Funzione DELETED ()|Funzione Descending ()|  
|Funzione DIFFERENCE ()|Comando DIMENSION|Funzione DISKSPACE ()|  
|Funzione DMY ()|FAI CASO... Comando ENDCASE|Comando DO|  
|ESEGUI... Comando ENDDO|Funzione DOW ()|Funzione DTOC ()|  
|Funzione DTOR ()|Funzione DTO ()|Funzione DTOT ()|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Funzione EMPTY ()|Funzione EVALUATE ()|Comando EXIT|  
|Funzione ERROR ()|Funzione EXP ()||  
|Comando END TRANSACTION|Funzione EOF ()||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Funzione FCOUNT ()|Funzione FDATE ()|Funzione FIELD ()|  
|Funzione FILE ()|Funzione FILTER ()|Funzione FLDLIST ()|  
|Funzione FLOCK ()|Funzione FLOOR ()|Scarica comando|  
|PER... Comando ENDFOR|Funzione FOR ()|Funzione FOUND ()|  
|Comando tabella gratuita|Funzione FSIZE ()|Funzione FTIME ()|  
|FULLPATH () (funzione)|Comando FUNCTION|Funzione FV ()|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|Raccogli comando|Funzione GETNEXTMODIFIED ()|Comando GO/GOTO|  
|Funzione GETFLDSTATE ()|Funzione GOMONTH ()||  
|Funzione GETCP ()|Funzione GETENV ()||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|Funzione HEADER ()|Funzione HOUR ()|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Funzione IDXCOLLATE ()|SE... ENDIF (comando)|Funzione IIF ()|  
|Funzione INDBC ()|INDEX (comando)|Funzione INLIST ()|  
|Comando INSERT-SQL|INT () (funzione)|Funzione α ()|  
|Funzione BLANK ()|Funzione undigit ()|Funzione unexclusive ()|  
|Funzione ISLEADBYTE ()|Funzione LOWER ()|ISNULL () (funzione)|  
|Funzione ISREADONLY ()|Funzione ToUpper ()||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|Funzione KEY ()|Funzione di combinazione di maiuscole ()||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|LEFT () (funzione)|Funzione LEFTC ()|Funzione LIKEC ()|  
|Funzione LENC ()|LIKE () (funzione)|Funzione LOCK ()|  
|Comando locale|INDIVIDUA comando|Funzione LOOKUP ()|  
|Funzione LOG ()|Funzione LOG10 ()|Funzione LTRIM ()|  
|LOWER ()-funzione|Comando LPARAMETERS||  
|Funzione LUPDATE ()|Funzione LEN ()||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _MLINE|Funzione MAX ()|MDX () (funzione)|  
|Funzione MDY ()|Funzione MEMLINES ()|Funzione MESSAGE ()|  
|Funzione MIN ()|Funzione MINUTE ()|Funzione lineam ()|  
|Funzione MOD ()|Funzione MONTH ()|Funzione MTON ()|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Funzione NDX ()|Funzione Normalize ()|Operatore NOT|  
|Comando Nota|Funzione NTOM ()|Funzione NVL ()|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Funzione OCCURs ()|Funzione OLDVAL ()|Comando ON ERROR|  
|Comando tasto ON|Funzione ON ()|Comando Apri DATABASE|  
|Operatore OR|Funzione ORDER ()|Funzione OS ()|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Comando PACK|Funzione PARAMETERS ()|Funzione PAYMENT ()|  
|Comando PARAMETERS|Funzione PRIMARY ()|Comando privato|  
|Funzione PI ()|Funzione PROGRAM ()|Funzione PROPER ()|  
|Comando PROCEDURE|Funzione PV ()||  
|PUBLIC (comando)|Funzioni PADL () &#124; PADR () &#124; PADC ()||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Funzione RAND ()|Funzione RAT ()|Funzione RATC ()|  
|Funzione RATLINE ()|RICHIAMA comando|Funzione RECCOUNT ()|  
|Funzione RECNO ()|Funzione RECSIZE ()|Comando REGIONAL|  
|Funzione RELATION ()|Comando Rimuovi tabella|SOSTITUISCi comando|  
|Comando SOSTITUISCi da matrice|Funzione REPLICAte ()|Comando RETRY|  
|RETURN (comando)|RIGHT () (funzione)|Funzione RIGHTC ()|  
|Funzione RLOCK ()|ROLLBACK (comando)|Funzione ROUND ()|  
|Funzione RTOD ()|Funzione RTRIM ()||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|ANALIZZA... Comando ENDSCAN|SCATTER (comando)|Funzione SEC ()|  
|Funzione SECONDS ()|Comando SEEK|Funzione SEEK ()|  
|Comando SELECT|Funzione SELECT ()|Comando SELECT-SQL|  
|SET BLOCKSIZE (comando)|IMPOSTA comando CARRY|SET CENTURY (comando)|  
|SET COLLATE (comando)|Comando SET DATABASE|Comando imposta data|  
|IMPOSTA comando predefinito|SET DELETED (comando)|SET EXACT (comando)|  
|SET EXCLUSIVE (comando)|Comando SET FDOW|Comando imposta campi|  
|Comando Imposta filtro|IMPOSTA comando fisso|IMPOSTA comando FULLPATH|  
|Comando SET FWEEK|Comando SET HOURs|SET INDEX (comando)|  
|SET LOCK (comando)|IMPOSTA comando per più blocchi|IMPOSTA il comando NEAR|  
|Comando SET NOCPTRANS|Imposta notifica comando|SET NULL (comando)|  
|SET OPTIMIZe (comando)|Comando Imposta ordine|SET PATH (comando)|  
|Comando SET PROCEDURE|SET RELATION (comando)|SET RELATION OFF-comando|  
|SET REPROCESS (comando)|SET SKIP (comando)|Comando SET UDFPARMS|  
|SET UNIQUE (comando)|Comando imposta VOLUME|Funzione SET ()|  
|Funzione SETFLDSTATE ()|Funzione SIGN ()|Funzione SIN ()|  
|Comando SKIP|Ordina comando|Funzione SPACE ()|  
|Funzione SQRT ()|Comando STORE|Funzione STR ()|  
|Funzione STRCONV ()|Funzione STRTRAN ()|Funzione STUFF ()|  
|Funzione STUFFC ()|Funzione substr ()|Funzione SUBSTRC ()|  
|Comando SUM|Funzione SYS (2011)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _TALLY|Variabile di memoria di sistema _TRIGGERLEVEL|Funzione TAGCOUNT ()|  
|Funzione TABLEUPDATE ()|Funzione TAG ()|Funzione TARGET ()|  
|Funzione TAGNO ()|Funzione TAN ()|Funzione TRIM ()|  
|Funzione TIME ()|Comando TOTAL|Funzione TXNLEVEL ()|  
|Funzione TTOC ()|Funzione TTOD ()||  
|Funzione TYPE ()|Funzione TABLEREVERT ()||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|UNIQUE () (funzione)|Comando di sblocco|Comando USE|  
|Aggiorna comando|Funzione UPPER ()||  
|Funzione USED ()|UPDATE (comando SQL)||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Funzione VAL ()|Funzione VERSION ()||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|Funzione WEEK ()|||  
  
## <a name="y"></a>S  
  
||||  
|-|-|-|  
|Funzione YEAR ()|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando ZAP|||
