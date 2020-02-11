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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63154667"
---
# <a name="sqlfreehandle"></a>SQLFreeHandle
  In modalità di commit manuale, la chiamata di **SQLFreeHandle** su un handle di istruzione con una transazione aperta causa un rollback delle modifiche in sospeso al database. La chiamata di **SQLFreeHandle** su un handle di istruzione chiude sempre tutti i cursori aperti e ignora i risultati in sospeso, liberando tutte le risorse associate all'handle di istruzione.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLFreeHandle (funzione)](https://go.microsoft.com/fwlink/?LinkId=59345)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
