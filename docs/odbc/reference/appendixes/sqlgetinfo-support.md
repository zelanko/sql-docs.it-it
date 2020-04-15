---
title: 'Supporto di SQLGetInfo : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a21c035a14814f51d4344894ef253b2cc844f4c2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307802"
---
# <a name="sqlgetinfo-support"></a>Supporto per SQLGetInfo
Quando un ODBC 2. *X* applicazione chiama **SQLGetInfo** a un driver ODBC 3 *.x,* il *InfoType* argomenti nella tabella seguente deve essere supportato.  
  
|*Infotype*|Valori di codice restituiti|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0) **Nota:** questo tipo di informazioni non è deprecato; le maschere di bit nella colonna a destra sono deprecate.|Maschera di bit SQLINTEGER che enumera le clausole nell'istruzione **ALTER TABLE** supportata dall'origine dati.<br /><br /> Le maschere di bit seguenti vengono utilizzate per determinare quali clausole sono supportate:The following bitmasks are used to determine which clauses are supported:<br /><br /> SQL_AT_DROP_COLUMN: la possibilità di eliminare le colonne è supportata. Se questo risulta in cascata o limitare il comportamento è driver-defined. (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN: è supportata la possibilità di aggiungere più colonne in una singola istruzione ALTER TABLE. Questo bit non viene combinato con altri bit SQL_AT_ADD_COLUMN_XXX o SQL_AT_CONSTRAINT_XXX bit. (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> Il tipo di informazioni è stato introdotto in ODBC 1.0. ogni maschera di bit è etichettata con la versione in cui è stata introdotta.|Maschera di bit SQLINTEGER che enumera le opzioni di direzione di recupero supportate.<br /><br /> Le maschere di bit seguenti vengono utilizzate insieme al flag per determinare le opzioni supportate:<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|Maschera di bit SQLINTEGER che enumera i tipi di blocco supportati per l'argomento *fLock* in **SQLSetPos**.<br /><br /> Le maschere di bit seguenti vengono utilizzate insieme al flag per determinare quali tipi di blocco sono supportati:<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|Valore SQLSMALLINT che indica il livello di conformità ODBC.<br /><br /> SQL_OAC_NONE - Nessuno<br /><br /> SQL_OAC_LEVEL1 - Livello 1 supportato<br /><br /> SQL_OAC_LEVEL2 - Livello 2 supportato|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|Valore SQLSMALLINT che indica la grammatica SQL supportata dal driver. Vedere [Appendice C: Grammatica SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) per una definizione dei livelli di conformità SQL.<br /><br /> SQL_OSC_MINIMUM- Grammatica minima supportata<br /><br /> SQL_OSC_CORE- Grammatica di base supportata<br /><br /> SQL_OSC_EXTENDED - Grammatica estesa supportata|  
|SQL_POS_OPERATIONS (ODBC 2.0)|Maschera di bit SQLINTEGER che enumera le operazioni supportate in **SQLSetPos**.<br /><br /> Le maschere di bit seguenti vengono utilizzate in combinazione con il flag per determinare le opzioni supportate:<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0) (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|Maschera di bit SQLINTEGER che enumera le istruzioni SQL posizionate supportate.<br /><br /> Le maschere di bit seguenti vengono utilizzate per determinare quali istruzioni sono supportate:The following bitmasks are used to determine which statements are supported:<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|Maschera di bit SQLINTEGER che enumera le opzioni di controllo della concorrenza supportate per il cursore.<br /><br /> Le maschere di bit seguenti vengono utilizzate per determinare le opzioni supportate:The following bitmasks are used to determine which options are supported:<br /><br /> SQL_SCCO_READ_ONLY il cursore è di sola lettura. Non sono consentiti aggiornamenti.<br /><br /> SQL_SCCO_LOCK cursore utilizza il livello più basso di blocco sufficiente per garantire che la riga possa essere aggiornata.<br /><br /> SQL_SCCO_OPT_ROWVER: il cursore utilizza il controllo della concorrenza ottimistica, confrontando le versioni di riga, ad esempio SQLBase ROWID o Sybase TIMESTAMP.<br /><br /> SQL_SCCO_OPT_VALUES: il cursore utilizza il controllo della concorrenza ottimistica, confrontando i valori.|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|Maschera di bit SQLINTEGER che enumera se le modifiche apportate da un'applicazione a un cursore statico o basato su keyset tramite **SQLSetPos** o istruzioni di aggiornamento o eliminazione posizionate possono essere rilevate da tale applicazione.<br /><br /> SQL_SS_ADDITIONS: le righe aggiunte sono visibili al cursore; il cursore può scorrere fino a queste righe. Dove queste righe vengono aggiunte al cursore dipende dal driver.<br /><br /> SQL_SS_DELETIONS - Le righe eliminate non sono più disponibili per il cursore e non lasciano un "buco" nel set di risultati; dopo che il cursore scorre da una riga eliminata, non può tornare a tale riga.<br /><br /> SQL_SS_UPDATES: gli aggiornamenti alle righe sono visibili al cursore; se il cursore scorre da e ritorna a una riga aggiornata, i dati restituiti dal cursore sono i dati aggiornati, non i dati originali. Questa opzione si applica solo ai cursori statici o agli aggiornamenti sui cursori basati su keyset che non aggiornano la chiave. Questa opzione non si applica a un cursore dinamico o nel caso in cui un tasto venga modificato in un cursore misto.<br /><br /> La possibilità di rilevare le modifiche apportate ad altri utenti da parte di un'applicazione dipende dal tipo di cursore.|  
  
 Un'applicazione ODBC 3 *.x* che utilizza un driver *.x* ODBC 3 non deve chiamare **SQLGetInfo** con gli argomenti *InfoType* descritti nella tabella precedente, ma deve utilizzare gli argomenti *InfoType* ODBC 3 *.x* elencati nel paragrafo seguente. Non esiste una corrispondenza uno-a-uno tra gli argomenti *InfoType* utilizzati in ODBC 2. *x* e quelli utilizzati in ODBC 3 *.x*. Un'applicazione *.x* ODBC 3 che utilizza un ODBC 2. *x* driver, d'altra parte, deve utilizzare gli argomenti *InfoType* descritti in precedenza.  
  
 Alcuni dei tipi di informazioni nella tabella precedente sono deprecati a favore dei tipi di informazioni sugli attributi del cursore. Questi tipi di informazioni deprecate sono SQL_FETCH_DIRECTION, SQL_LOCK_TYPES, SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY e SQL_STATIC_SENSITIVITY. I nuovi tipi di attributi del cursore vengono SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2, dove XXX è uguale a DYNAMIC, FORWARD_ONLY, KEYSET_DRIVEN o STATIC. Ognuno dei nuovi tipi indica le funzionalità del driver per un singolo tipo di cursore. Per altre informazioni su queste opzioni, vedere la descrizione della funzione [SQLGetInfo.For](../../../odbc/reference/syntax/sqlgetinfo-function.md) more information about these options, see the SQLGetInfo function description.
