---
title: SQLFreeHandle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeHandle function
ms.assetid: d374e5c8-ed35-43bf-8dd6-c37e38d9b5f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 197d3e1d36f8513821cec9630cade8f52681a43d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63154667"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
  In modalità di commit manuale, la chiamata **SQLFreeHandle** in un'istruzione handle con una transazione aperta provoca un rollback delle modifiche in sospeso per il database. La chiamata **SQLFreeHandle** in un'istruzione handle sempre chiude tutti i cursori aperti ed Elimina risultati, liberando tutte le risorse associate all'handle di istruzione in sospeso.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLFreeHandle-funzione](https://go.microsoft.com/fwlink/?LinkId=59345)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
