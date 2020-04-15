---
title: 'Mapping DI SQLSTATE : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ec58c0e41869529bbba5fd31ad534976923a990d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299741"
---
# <a name="sqlstate-mappings"></a>Mapping di SQLSTATE
In questo argomento vengono illustrati i valori SQLSTATE per ODBC *2.x* e ODBC *3.x*. Per ulteriori informazioni sui valori SQLSTATE di ODBC *3.x,* vedere [Appendice A: Codici di errore ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md).  
  
 In ODBC *3.x*vengono restituiti SQLSTATEs anziché S1xxx e vengono restituiti SQLSTATE 42Sxx anziché S00XX. Questo è stato fatto per allinearsi con gli standard Open Group e ISO. In molti casi, il mapping non è uno a uno perché gli standard hanno ridefinito l'interpretazione di diversi SQLSTATEs.  
  
 Quando un'applicazione ODBC *2.x* viene aggiornata a un'applicazione ODBC *3.x,* l'applicazione deve essere modificata in modo che si aspetti ODBC *3.x* SQLSTATEs anziché SQLSTATES ODBC *2.x.* Nella tabella seguente sono elencati i SQLSTATE DI ODBC *3.x* a cui viene eseguito il mapping di ogni SQLSTATE DI ODBC *2.x.*  
  
 Quando l'attributo di ambiente SQL_ATTR_ODBC_VERSION è impostato su SQL_OV_ODBC2, il driver invia ODBC *2.x* SQLSTATEs anziché ODBC *3.x* SQLSTATEs quando **SQLGetDiagField** o **SQLGetDiagRec** viene chiamato. Un mapping specifico può essere determinato notando ODBC *2.x* SQLSTATE nella colonna 1 della tabella seguente che corrisponde a ODBC *3.x* SQLSTATE nella colonna 2.  
  
|ODBC *2.x* SQLSTATE|ODBC *3.x* SQLSTATE|Commenti|  
|-------------------------|-------------------------|--------------|  
|01S03|01001||  
|01S04 (in questo stato di|01001||  
|22003|HY019||  
|22008|22007||  
|22005|22018||  
|24000|07005||  
|37000|42000||  
|70100|HY018 (INFORMAZIONI in cui è INSTATO)||  
|S0001|42S01||  
|S0002|42S02 (in questo)||  
|S0011|42S11||  
|S0012 (in questo)|42S12||  
|S0021|42S21||  
|S0022 (in questo s2)|42S22||  
|S0023|42S23||  
|S1000 (in questo s2)|HY000||  
|S1001 (in modo s18)|I001||  
|S1002 (in questo s2)|07009|ODBC *2.x* SQLSTATE S1002 è mappato a ODBC *3.x* SQLSTATE 07009 se la funzione sottostante è **SQLBindCol**, **SQLColAttribute**, **SQLExtendedFetch**, **SQLFetch**, **SQLFetchScroll**o **SQLGetData**.|  
|S1003 (informazioni in cui si è invitato)|HY003||  
|S1004 (in questo s2)|HY004||  
|S1008 (informazioni in cui si è invitato)|I008||  
|S1009 (informazioni in stato di sinfamisso)|I009|Restituito per un utilizzo non valido di un puntatore null.|  
|S1009 (informazioni in stato di sinfamisso)|HY024 (informazioni in base al|Restituito per un valore di attributo non valido.|  
|S1009 (informazioni in stato di sinfamisso)|I092 (informazioni in stato IN CUI|Restituito per l'aggiornamento o l'eliminazione di dati da una chiamata a **SQLSetPos**o l'aggiunta, l'aggiornamento o l'eliminazione di dati da una chiamata a **SQLBulkOperations**, quando la concorrenza è di sola lettura.|  
|S1010 (informazioni in stato in questo stato del sistema)|HY007 HY010|SQLSTATE S1010 viene mappato a SQLSTATE HY007 quando **SQLDescribeCol** viene chiamato prima di chiamare **SQLPrepare**, **SQLExecDirect**o una funzione di catalogo per *StatementHandle*. In caso contrario, SQLSTATE S1010 viene mappato a SQLSTATE HY010.|  
|S1011 (informazioni in questo stati in comsisscio|HY011||  
|S1012 (informazioni in stato in questo stato del sistema)|HY012||  
|S1090 (informazioni in questo stati in comandato).|I090||  
|S1091 (informazioni in cui si è invitato)|I091||  
|S1092 (informazioni in questo stati su sin)|I092 (informazioni in stato IN CUI||  
|S1093 (informazioni in cui si è invitato)|07009|ODBC *3.x* SQLSTATE 07009 è mappato a ODBC *2.x* SQLSTATE S1093 se la funzione sottostante è **SQLBindParameter** o **SQLDescribeParam**.|  
|S1096 (informazioni in inglese)|I096||  
|S1097 (informazioni in questo stati in comsissisma|I097 (informazioni in stato INCUI)||  
|S1098 (informazioni in questo stati in comandato)|I098 (informazioni in stato IN CUI||  
|S1099 (informazioni in questo stati in comsistrasystemo|I099||  
|S1100 (in questo s2)|I100||  
|S1101 (in vi es.|HY101||  
|S1103 (informazioni in stato di scente)|I103||  
|S1104 (in questo s2)|I104||  
|S1105 (in questo stato)|HY105||  
|S1106 (in inglese)|I106||  
|S1107 (informazioni in questo stati in due)|I107||  
|S1108 (informazioni in questo stati in due)|I108||  
|S1109 (informazioni in questo stati in due)|I109||  
|S1110 (in questo s2)|HY110||  
|S11111|HY111||  
|S1C00 (in questo stato)|HYC00||  
|S1T00 (in questo s1).|HYT00||  
  
> [!NOTE]  
>  ODBC *3.x* SQLSTATE 07008 è mappato a ODBC *2.x* SQLSTATE S1000.
