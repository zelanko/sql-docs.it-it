---
title: SQLRowCount | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ff2a744f68cf6152330179eb8dcab1f33911914
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046606"
---
# <a name="sqlrowcount"></a>SQLRowCount
  Quando vengono associate matrici di valori di parametro per l'esecuzione di `SQLRowCount` istruzioni, restituisce SQL_ERROR se una riga di valori di parametro genera una condizione di errore nell'esecuzione dell'istruzione. Tramite l'argomento *RowCountPtr* della funzione non viene restituito alcun valore.  
  
 L'applicazione può sfruttare l'attributo di istruzione SQL_ATTR_PARAMS_PROCESSED_PTR per acquisire il numero di parametri elaborati prima del verificarsi dell'errore.  
  
 L'applicazione può inoltre utilizzare una matrice di valori di stato, associata tramite l'attributo di istruzione SQL_ATTR_PARAM_STATUS_PTR, per acquisire gli offset della matrice di righe di parametri con errori. L'applicazione può attraversare la matrice di stati per determinare il numero effettivo di righe elaborate.  
  
 Quando viene [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguita un'istruzione INSERT, Update, DELETE o merge con una clausola output, SQLRowCount non restituisce il numero di righe interessate finché non vengono utilizzate tutte le righe del set di risultati generato dalla clausola output. Per annullare queste righe, chiamare SQLFetch o SQLFetchScroll. SQLResultCols restituirà-1 fino a quando non saranno state utilizzate tutte le righe di risultati. Quando SQLFetch o SQLFetchScroll restituisce SQL_NO_DATA, l'applicazione deve chiamare SQLRowCount per determinare il numero di righe interessate prima di chiamare SQLMoreResults per passare al risultato successivo.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLRowCount (funzione)](https://go.microsoft.com/fwlink/?LinkId=59367)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
