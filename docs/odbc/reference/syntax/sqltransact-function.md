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
manager: craigg
ms.openlocfilehash: 4ad40522bd9f97c72a5d0a71d089b9e7c98a7d6b
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793616"
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
