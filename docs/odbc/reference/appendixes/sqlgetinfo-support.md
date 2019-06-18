---
title: SQLGetInfo Support | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6eb6bedb20e1f61c48776d03df59aa6865cfb2a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62751211"
---
# <a name="sqlgetinfo-support"></a>Supporto per SQLGetInfo
Quando un'applicazione ODBC 2. *x* chiamate dell'applicazione **SQLGetInfo** a un'applicazione ODBC 3*x* driver, il *InfoType* argomenti nella tabella seguente devono essere supportati.  
  
|*InfoType*|Valori di codice restituiti|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0) **Note:**  Informazioni di questo tipo non sono deprecata. le maschere di bit della colonna a destra sono deprecati.|Una maschera di bit SQLINTEGER l'enumerazione le clausole nel **ALTER TABLE** istruzione supportata dall'origine dati.<br /><br /> Le maschere di bit seguenti vengono usate per determinare quali clausole sono supportate:<br /><br /> SQL_AT_DROP_COLUMN = è supportata la possibilità di eliminare le colonne. Se ciò comporterà a catena o limitare il comportamento è definito dal driver. (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = la possibilità di aggiungere più colonne in un'unica istruzione ALTER TABLE è supportato. Questo bit non combinare con altri bits SQL_AT_ADD_COLUMN_XXX o bits SQL_AT_CONSTRAINT_XXX. (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> Il tipo di informazioni è stata introdotta in ODBC 1.0; ogni maschera di bit viene etichettato con la versione in cui è stato introdotto in.|Maschera di bit SQLINTEGER l'enumerazione le opzioni di direzione di recupero supportate.<br /><br /> Le maschere di bit seguenti vengono utilizzate in combinazione con il flag per determinare quali opzioni sono supportate:<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|I tipi di una maschera di bit SQLINTEGER l'enumerazione di blocco supportati per il *branco* nell'argomento **SQLSetPos**.<br /><br /> Le maschere di bit seguenti vengono utilizzate in combinazione con il flag per determinare i tipi di blocco supportati:<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|Un valore SQLSMALLINT che indica il livello di conformità di ODBC.<br /><br /> SQL_OAC_NONE = nessuno<br /><br /> SQL_OAC_LEVEL1 = Level 1 supported<br /><br /> SQL_OAC_LEVEL2 = Level 2 supported|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|Un valore SQLSMALLINT che indica la grammatica SQL supportata dal driver. Vedere [appendice c: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) per una definizione dei livelli di conformità SQL.<br /><br /> SQL_OSC_MINIMUM = grammatica minima supportata<br /><br /> SQL_OSC_CORE = supportata la sintassi di base<br /><br /> SQL_OSC_EXTENDED = grammatica estesa supportata|  
|SQL_POS_OPERATIONS (ODBC 2.0)|Una maschera di bit SQLINTEGER l'enumerazione le operazioni supportate nella **SQLSetPos**.<br /><br /> Le maschere di bit seguenti sono utilizzati in abbinamento con il flag per determinare quali opzioni sono supportate:<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH   (ODBC 2.0) SQL_POS_UPDATE     (ODBC 2.0) SQL_POS_DELETE     (ODBC 2.0) SQL_POS_ADD          (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|Una maschera di bit SQLINTEGER l'enumerazione supportata posizionati istruzioni SQL.<br /><br /> Le maschere di bit seguenti vengono usate per determinare quali le istruzioni sono supportate:<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|Maschera di bit SQLINTEGER l'enumerazione le opzioni di controllo di concorrenza supportate per il cursore.<br /><br /> Le maschere di bit seguenti vengono usate per determinare quali opzioni sono supportate:<br /><br /> SQL_SCCO_READ_ONLY = cursore è di sola lettura. Non sono consentiti aggiornamenti.<br /><br /> SQL_SCCO_LOCK = cursore utilizza il livello più basso di blocco sufficienti a garantire che la riga può essere aggiornata.<br /><br /> SQL_SCCO_OPT_ROWVER = cursore utilizza il controllo della concorrenza, confronto tra le versioni di riga, ad esempio SQLBase ROWID o Sybase TIMESTAMP.<br /><br /> SQL_SCCO_OPT_VALUES = cursore utilizza il controllo della concorrenza, confronto di valori.|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|Un'enumerazione di maschera di bit SQLINTEGER se le modifiche apportate da un'applicazione a un cursore statico o gestito da keyset attraverso **SQLSetPos** o istruzioni delete o update posizionata possono essere rilevate dall'applicazione.<br /><br /> SQL_SS_ADDITIONS = sono state aggiunte le righe sono visibili fino al cursore; il cursore è possibile scorrere a queste righe. In cui queste righe vengono aggiunte al cursore dipende dal driver.<br /><br /> SQL_SS_DELETIONS = Deleted righe non sono più disponibili fino al cursore e non lascino un' "area libera" nel set di risultati. Dopo che il cursore passa da una riga eliminata, non può restituire a tale riga.<br /><br /> SQL_SS_UPDATES = gli aggiornamenti alle righe sono visibili fino al cursore; Se il cursore consente di scorrere da e restituisce una riga aggiornata, i dati restituiti dal cursore sono i dati aggiornati, non i dati originali. Questa opzione si applica solo a cursori o gli aggiornamenti su cursori che non si aggiornano la chiave. Questa opzione non è applicabile per un cursore dynamic o nel caso in cui viene modificata una chiave in un cursore misto.<br /><br /> Se un'applicazione può rilevare le modifiche apportate da altri utenti, inclusi altri cursori nella stessa applicazione, set di risultati varia a seconda del tipo di cursore.|  
  
 Un'applicazione ODBC 3 *. x* funziona con un'applicazione ODBC 3 *. x* driver non deve chiamare **SQLGetInfo** con il *InfoType* gli argomenti descritti in precedente tabella, ma che devono usare ODBC 3 *. x* *InfoType* argomenti elencati nel paragrafo seguente. Non esiste una corrispondenza uno a uno tra *InfoType* gli argomenti utilizzati in ODBC 2. *x* sia quelli utilizzati in ODBC 3*x*. Un'applicazione ODBC 3 *. x* funziona con un'API ODBC 2. *x* driver, d'altra parte, deve utilizzare il *InfoType* gli argomenti descritti in precedenza.  
  
 Alcuni dei tipi di informazioni nella tabella precedente sono deprecate a favore di tipi di informazioni di attributi del cursore. Questi deprecato tipi sono SQL_FETCH_DIRECTION SQL_LOCK_TYPES, SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY e SQL_STATIC_SENSITIVITY informazioni. I nuovi tipi di attributi del cursore sono SQL_XXX_CURSOR_ATTRIBUTES2 SQL_XXX_CURSOR_ATTRIBUTES1and, dove XXX è uguale a DYNAMIC, FORWARD_ONLY, KEYSET_DRIVEN o STATIC. Ognuno dei nuovi tipi indica le funzionalità di driver per un tipo di cursore singolo. Per altre informazioni su queste opzioni, vedere la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrizione della funzione.
