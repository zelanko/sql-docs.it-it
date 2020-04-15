---
title: SQLSetDescField e SQLSetDescRec (libreria di cursori) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDescField function [ODBC], Cursor Library
- SQLSetDescRec function [ODBC], Cursor Library
ms.assetid: 4ccff067-85cd-4bfa-a6cd-7f28051fb5b9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b85eb84cdf48a1c2a441b8994076a9023d254f2d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300551"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField and SQLSetDescRec (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo delle funzioni **SQLSetDescField** e **SQLSetDescRec** nella libreria di cursori. Per informazioni generali su queste funzioni, vedere [Funzione SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) e [Funzione SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 La libreria di cursori esegue **SQLSetDescField** quando viene chiamata per restituire il valore dei campi impostati per le colonne segnalibro:  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_DATETIME_INTERVAL_CODE  
  
 SQL_DESC_SCALE  
  
 SQL_DESC_PRECISION  
  
 SQL_DESC_TYPE  
  
 SQL_DESC_NAME  
  
 SQL_DESC_UNNAMED  
  
 SQL_DESC_NULLABLE  
  
 La libreria di cursori esegue chiamate a **SQLSetDescRec** per una colonna segnalibro.  
  
 Quando si utilizza un driver ODBC *2.x,* la libreria di cursori restituisce SQLSTATE HY090 (stringa non valida o lunghezza del buffer) quando **SQLSetDescField** o **SQLSetDescRec** viene chiamato per impostare il campo SQL_DESC_OCTET_LENGTH per il record del segnalibro di un ARD su un valore diverso da 4. Quando si utilizza un driver ODBC *3.x,* la libreria di cursori consente al buffer di avere qualsiasi dimensione.  
  
 La libreria di cursori esegue **SQLSetDescField** quando viene chiamata per restituire il valore del campo SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE o SQL_DESC_ROW_STATUS_PTR. Questi campi possono essere restituiti per qualsiasi riga, non solo per la riga del segnalibro.  
  
 La libreria di cursori non esegue **SQLSetDescField** per modificare qualsiasi campo descrittore diverso dai campi menzionati in precedenza. Se un'applicazione chiama **SQLSetDescField** per impostare qualsiasi altro campo mentre viene caricata la libreria di cursori, la chiamata viene passata al driver.  
  
 La libreria di cursori supporta la modifica dinamica dei campi SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR e SQL_DESC_OCTET_LENGTH_PTR di qualsiasi riga di un descrittore di riga dell'applicazione (dopo una chiamata a **SQLExtendedFetch**, **SQLFetch**o **SQLFetchScroll**). Il campo SQL_DESC_OCTET_LENGTH_PTR può essere modificato in un puntatore null solo per annullare l'associazione del buffer di lunghezza per una colonna.  
  
 La libreria di cursori non supporta la modifica del campo SQL_DESC_BIND_TYPE in un APD o ARD quando un cursore è aperto. Il campo SQL_DESC_BIND_TYPE può essere modificato solo dopo la chiusura del cursore e prima dell'apertura di un nuovo cursore. Gli unici campi descrittore che la libreria di cursori supporta la modifica quando un cursore è aperto sono SQL_DESC_ARRAY_STATUS_PTR, SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_ROWS_PROCESSED_PTR.  
  
 La libreria di cursori non supporta la modifica del campo SQL_DESC_COUNT dell'ARD dopo la chiamata a **SQLExtendedFetch** o **SQLFetchScroll** e prima che il cursore sia stato chiuso.
