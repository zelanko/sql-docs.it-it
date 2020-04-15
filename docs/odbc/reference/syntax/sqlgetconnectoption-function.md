---
title: Funzione SQLGetConnectOption . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94a29637365862990ea067f663023fae04a7af3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285571"
---
# <a name="sqlgetconnectoption-function"></a>Funzione SQLGetConnectOption
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: Deprecated  
  
 **Riepilogo**  
 In ODBC *3.x*la funzione ODBC *2.x* **SQLGetConnectOption** è stata sostituita da **SQLGetConnectAttr**. Per ulteriori informazioni, vedere [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md).  
  
> [!NOTE]
>  Per ulteriori informazioni su ciò che Gestione Driver esegue il mapping di questa funzione a quando un'applicazione ODBC *2.x* utilizza un driver ODBC *3.x,* vedere mapping di [funzioni deprecate](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) nell'appendice G: Linee guida del driver per la compatibilità con le versioni precedenti.  
> 
> [!NOTE]
>  L'attributo SQL_ASYNC_DBC_FUNCTION_ENABLE introdotto in ODBC 3.8 non è supportato da **SQLGetConnectOption.** Le applicazioni che utilizzano l'operazione asincrona su un handle di connessione devono utilizzare **SQLGetConnectAttr**.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
