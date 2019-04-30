---
title: SQLGetDescField e SQLGetDescRec (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66361572427c3264a1b25fe1c851685a07b2e029
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188761"
---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField e SQLGetDescRec (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLGetDescField** e **SQLGetDescRec** funzioni della libreria di cursori. Per informazioni generali su queste funzioni, vedere [funzione SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) e [funzione SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md).  
  
 Esegue la libreria di cursori **SQLGetDescRec** per restituire i metadati per colonne di segnalibri. Esegue la libreria di cursori **SQLGetDescField** da restituire gli stessi campi restituiti da **SQLGetDescRec**, che sono SQL_DESC_NAME, SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_ LUNGHEZZA, SQL_DESC_PRECISION, SQL_DESC_SCALE e SQL_DESC_NULLABLE. Per coerenza, **SQLGetDescField** restituisce inoltre SQL_DESC_UNNAMED.  
  
 Esegue la libreria di cursori **SQLGetDescField** quando viene chiamato per restituire il valore dei seguenti campi che vengono impostate per l'associazione di colonne di segnalibri: SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR e SQL_DESC_LENGTH.  
  
 Esegue la libreria di cursori **SQLGetDescField** quando viene chiamato per restituire il valore del campo SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE o SQL_DESC_ROW_STATUS_PTR. Questi campi possono essere restituiti per ogni riga, non solo la riga di segnalibro.  
  
 Se un'applicazione chiama **SQLGetDescField** per restituire il valore di qualsiasi campo diverse da quelle indicate in precedenza, la libreria di cursori passa la chiamata del driver.
