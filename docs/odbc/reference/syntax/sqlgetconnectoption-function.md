---
title: Funzione SQLGetConnectOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30d91302161b236cee5634196bea33f61411f046
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63259572"
---
# <a name="sqlgetconnectoption-function"></a>Funzione SQLGetConnectOption
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: Deprecato  
  
 **Riepilogo**  
 In ODBC 3 *. x*, l'API ODBC 2 *. x* funzione **SQLGetConnectOption** è stato sostituito da **SQLGetConnectAttr**. Per altre informazioni, vedere [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md).  
  
> [!NOTE]
>  Per altre informazioni su ciò che Gestione Driver esegue il mapping a questa funzione quando un ODBC 2 *. x* applicazione funziona con un'applicazione ODBC 3 *. x* driver, vedere [Mapping di funzioni deprecate](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)nell'appendice g: Driver linee guida per la compatibilità con le versioni precedenti.  
> 
> [!NOTE]
>  L'attributo SQL_ASYNC_DBC_FUNCTION_ENABLE introdotte in ODBC 3.8 non è supportato dal **SQLGetConnectOption**. Le applicazioni che usano l'operazione asincrona su un handle di connessione devono utilizzare **SQLGetConnectAttr**.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
