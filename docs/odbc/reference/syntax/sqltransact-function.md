---
title: Funzione SQLTransact | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTransact
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTransact
helpviewer_keywords:
- SQLTransact function [ODBC]
ms.assetid: 496249e0-8eff-4c60-8358-5543bc3ead9c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c96c903b68dee2d1d215804d318d47b4c39a7a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039502"
---
# <a name="sqltransact-function"></a>Funzione SQLTransact
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: Funzionalità deprecate  
  
 **Riepilogo**  
 In ODBC *3.x*, ODBC *2.x* funzione **SQLTransact** è stato sostituito da **SQLEndTran**. Per altre informazioni, vedere [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  L'attributo SQL_ASYNC_DBC_FUNCTION_ENABLE, che è stata introdotta in ODBC 3.8, non è supportato dal **SQLTransact**. Applicazioni con un'operazione asincrona su un handle di connessione devono utilizzare **SQLEndTran**.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
