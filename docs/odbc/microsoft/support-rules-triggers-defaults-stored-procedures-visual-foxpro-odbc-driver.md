---
title: Supporto per la Stored procedure, trigger, i valori predefiniti e regole | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47795998b019df22b01852519f75f6e8d3d274dd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63269854"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>Supporto di regole, trigger, valori predefiniti e stored procedure (driver ODBC Visual FoxPro)
È possibile creare regole di Visual FoxPro, trigger, valori predefiniti o le stored procedure usando il Driver ODBC Visual FoxPro. Tuttavia, l'applicazione potrebbe interagire con le regole esistenti, trigger, valori predefiniti o le stored procedure come che inserisce, aggiorna o Elimina i dati archiviati in un database in Visual FoxPro.  
  
 La tabella seguente elenca le funzioni supportate dal Driver ODBC Visual FoxPro quando le funzioni o i comandi sono presenti nelle regole, trigger, valori predefiniti o le stored procedure e comandi di Visual FoxPro.  
  
 Se l'applicazione interagisce con i dati cui le regole, trigger, valori predefiniti o le stored procedure chiamano altri comandi di Visual FoxPro o funzioni, il driver genera un errore. Visualizzare [funzioni e non supportati i comandi Visual FoxPro](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) per un elenco di comandi e funzioni non supportate dal driver.  
  
> [!TIP]  
>  Se si desidera inserire codice condizionale all'interno di regole, trigger o stored procedure che determina i comandi da eseguire quando viene chiamato dal driver, è possibile usare la **(versione)** (funzione). Il **(versione)** restituisce "Driver ODBC Visual FoxPro  *\<versione >* " quando viene chiamato dal driver.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Funzioni supportate in Stored procedure, trigger, valori predefiniti e regole e i comandi di Visual FoxPro  
  
||||  
|-|-|-|  
|Operatore $|% (Operatore)|& Comando|  
|& & Comandi|* Comando|= Comando|  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|Funzione ABS)|Funzione ACOPY)|Comando Aggiungi tabella|  
|Funzione ADATABASES)|Funzione ADBOBJECTS)|Funzione AERROR)|  
|ADEL () (funzione)|Funzione AELEMENT)|Funzione ALEN)|  
|Funzione AFIELDS)|Funzione AINS)|ALTER TABLE (comando SQL)|  
|Funzione ALIAS)|Funzione ALLTRIM)|AGGIUNTA di comandi di matrice|  
|Operatore AND|Aggiungi comando|Aggiungi credito comando|  
|AGGIUNGERE dal comando|AGGIUNGERE comandi generale|Funzione ASCAN)|  
|AGGIUNGERE il comando procedure|Centro sicurezza di AZURE all'indirizzo funzione|Funzione ASUBSCRIPT)|  
|Funzione ASIN)|Funzione ASORT)|Funzione ATAN)|  
|NELLA funzione)|Funzione AT_C)|Funzione ATCLINE)|  
|Funzione () traffico aereo|Funzione ATCC)|Funzione AUSED)|  
|Funzione ATLINE)|Funzione ATN2)||  
|Comando medio|Funzione ACOS)||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|Comando BEGIN TRANSACTION|TRA () (funzione)|Funzione BITNOT)|  
|Funzione BITCLEAR)|Funzione BITLSHIFT)|BITSET () (funzione)|  
|Funzione BITOR)|Funzione BITRSHIFT)|Comando vuota|  
|Funzione BITTEST)|Funzione BITXOR)||  
|Funzione BOF)|Funzione BITAND)||  
  
## <a name="c"></a>c  
  
||||  
|-|-|-|  
|CALCOLARE comando|Funzioni CANDIDATE)|Funzione di tra due CHR)|  
|Funzione () CDX|Funzione CEILING)|Chiudi i comandi|  
|Funzione CHRTRAN)|Funzione CHRTRANC)|Comando COPY di indici|  
|Funzione CMONTH)|CONTINUARE a comando|Copia il comando estesa di struttura|  
|Comando COPY di procedure|Comando COPY di struttura|COPIA al comando|  
|Copia il comando TAG|COPIARE il comando di matrice|Funzione CPCONVERT)|  
|COS () funziona|Comando COUNT|Funzione CTOD)|  
|Funzione CPCURRENT)|Funzione CPDBF)|Funzione CURSORSETPROP)|  
|Funzione CTOT)|Funzione CURSORGETPROP)||  
|Funzione CURVAL)|Funzione CDOW)||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|Funzione DATE)|Funzione DATETIME)|Funzione DAY)|  
|Funzione () a due byte|Funzione DBF)|Funzione DBGETPROP)|  
|Funzione DBUSED)|DELETE (comando SQL)|Comando DELETE|  
|DELETE TAG (comando)|Funzione (eliminato)|Ordine DECRESCENTE () (funzione)|  
|Funzione DIFFERENCE)|DIMENSIONI comando|Funzione () su disco insufficiente|  
|DMY () (funzione)|ESEGUIRE L'OPERAZIONE DI CASE... Comando ENDCASE|Comando|  
|ISTRUZIONE DO WHILE... Comando ENDDO|Funzione di DOW)|Funzione DTOC)|  
|Funzione DTOR)|Gli oggetti DTO () (funzione)|Funzione DTOT)|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|Funzione (vuoto)|VALUTARE la funzione)|Comando EXIT|  
|Funzione di errore)|Funzione EXP)||  
|Comando END TRANSACTION|EOF (funzione))||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|Funzione FCOUNT)|Funzione FDATE)|Funzione di campo)|  
|Funzione FILE)|Funzione FILTER)|Funzione FLDLIST)|  
|Funzione () BRANCO|Funzione FLOOR)|Comando SCARICAMENTO|  
|FOR... Comando ENDFOR|PER la funzione)|TROVATO () (funzione)|  
|Comando TABLE gratuito|Funzione FSIZE)|FTIME (funzione))|  
|FULLPATH (funzione))|Comando (funzione)|Funzione Val)|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|La raccolta di comandi|Funzione GETNEXTMODIFIED)|Comando GO/Vai a|  
|Funzione GETFLDSTATE)|Funzione GOMONTH)||  
|Funzione GETCP)|GETENV () (funzione)||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|Funzione di intestazione)|Funzione HOUR)|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|Funzione IDXCOLLATE)|IF... Comando ENDIF|Funzione IIF)|  
|Funzione INDBC)|INDEX (comando)|Funzione di elenco)|  
|Comando INSERT-SQL|Funzione INT)|ISALPHA (funzione))|  
|Funzione ISBLANK)|ISDIGIT (funzione))|Funzione ISEXCLUSIVE)|  
|ISLEADBYTE (funzione))|ISLOWER (funzione))|Funzione ISNULL)|  
|Funzione ISREADONLY)|ISUPPER (funzione))||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|CHIAVE () (funzione)|Funzione KEYMATCH)||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|Funzione LEFT)|Funzione LEFTC)|Funzione LIKEC)|  
|Funzione LENC)|Ad esempio () (funzione)|LOCK () (funzione)|  
|Comando locale|TROVARE comandi|Funzione LOOKUP)|  
|Funzione LOG)|Funzione LOG10)|Funzione LTRIM)|  
|Funzione LOWER)|Comando LPARAMETERS||  
|Funzione LUPDATE)|Funzione LEN)||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|Variabile di memoria di sistema _MLINE|Funzione MAX)|Funzione MDX)|  
|Funzione MDY)|Funzione MEMLINES)|Funzione MESSAGE)|  
|Funzione MIN)|Funzione MINUTE)|Funzione MLINE)|  
|Funzione MOD)|Funzione MONTH)|Funzione MTON)|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|Funzione NDX)|NORMALIZE () (funzione)|NOT (operatore)|  
|Comando nota|Funzione NTOM)|Funzione NVL)|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Si verifica all'indirizzo (funzione)|Funzione OLDVAL)|NEL comando di errore|  
|NEL comando di tasti|NELLA funzione)|Comando Apri DATABASE|  
|Operatore OR|Funzione di ordine)|Funzione () del sistema operativo|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|Comando PACK|Funzione PARAMETERS)|Funzione di pagamento)|  
|Parametri comando|Funzione primaria)|Comando privato|  
|Funzione PI)|Funzione () del programma|Funzione (corretto)|  
|PROCEDURE (comando)|Funzione va)||  
|Comando pubblica|PADL( ) &#124; PADR( ) &#124; PADC( ) Functions||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|Funzione RAND)|Funzione () RAT|Funzione RATC)|  
|Funzione RATLINE)|Richiama comando|Funzione RECCOUNT)|  
|Funzione RECNO)|Funzione RECSIZE)|Comando a livello di area|  
|Funzione di relazione)|Rimuovi tabella comandi|Comando Sostituisci|  
|Sostituire dal comando di matrice|REPLICATE (funzione))|Ripetere i comandi|  
|RESTITUIRE comando|Funzione RIGHT)|Funzione RIGHTC)|  
|Funzione RLOCK)|Comando di ROLLBACK|Funzione ROUND)|  
|Funzione RTOD)|Funzione RTRIM)||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|ANALISI... Comando ENDSCAN|Grafico a dispersione comando|Funzione () al secondo|  
|Funzione () secondi|Comando di ricerca|SEEK (funzione))|  
|Selezionare comando|Funzione SELECT)|Comando SELECT-SQL|  
|SET BLOCKSIZE (comando)|SET CARRY (comando)|Comando secolo SET|  
|SET COLLATE (comando)|Comando DATABASE SET|Comando Data SET|  
|SET (comando) predefinito|SET DELETED (comando)|SET EXACT (comando)|  
|SET EXCLUSIVE (comando)|Comando FDOW SET|I campi di SET (comando)|  
|FILTRO di SET (comando)|SET fisso (comando)|Comando FULLPATH SET|  
|Comando FWEEK SET|IMPOSTARE le ore di comando|Comando dell'indice SET|  
|Comando LOCK SET|Comando MULTILOCKS SET|IMPOSTARE prossimità del comando|  
|Comando NOCPTRANS SET|SET di comando di notifica|SET NULL (comando)|  
|Comando OPTIMIZE SET|ORDINE di SET (comando)|SET PATH (comando)|  
|SET di PROCEDURE (comando)|Comando di impostazione relazione|RELAZIONE SET disattiva comandi|  
|SET REPROCESS (comando)|Comando Ignora SET|Comando UDFPARMS SET|  
|SET UNIQUE (comando)|Comando SET del VOLUME|Funzione SET)|  
|Funzione SETFLDSTATE)|Funzione SIGN)|Funzione SIN)|  
|Comando Ignora|Comando SORT|Funzione SPACE)|  
|Funzione SQRT)|Comando di archiviazione|Funzione STR)|  
|Funzione STRCONV)|Funzione STRTRAN)|Funzione STUFF)|  
|Funzione STUFFC)|SUBSTR () (funzione)|Funzione SUBSTRC)|  
|Comando SUM|SYS(2011) (funzione)||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY System Memory Variable|Variabile di memoria di sistema _TRIGGERLEVEL|Funzione TAGCOUNT)|  
|Funzione TABLEUPDATE)|TAG () (funzione)|Funzione di destinazione)|  
|Funzione TAGNO)|Funzione TAN)|TRIM () (funzione)|  
|Funzione TIME)|TOTALI comandi|Funzione TXNLEVEL)|  
|TTOC( ) Function|Funzione TTOD)||  
|Funzione di tipo)|Funzione TABLEREVERT)||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|Funzione (univoco)|UNLOCK-comando|USARE il comando|  
|Comando UPDATE|Funzione (superiore)||  
|UTILIZZATO () (funzione)|UPDATE (comando SQL)||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|Funzione VAL)|Funzione di versione)||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|SETTIMANA ()-funzione|||  
  
## <a name="y"></a>Y  
  
||||  
|-|-|-|  
|Funzione YEAR)|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|Comando ZAP|||
