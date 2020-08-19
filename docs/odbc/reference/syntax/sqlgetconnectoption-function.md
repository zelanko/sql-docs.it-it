---
description: Funzione SQLGetConnectOption
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df3fd7dc9a024348c4371fabdbcabfab63a6f071
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421285"
---
# <a name="sqlgetconnectoption-function"></a>Funzione SQLGetConnectOption
**Conformità**  
 Versione introdotta: conformità agli standard ODBC 1,0: deprecato  
  
 **Summary**  
 In ODBC *3. x*la funzione ODBC *2. x* **SQLGetConnectOption** è stata sostituita da **SQLGetConnectAttr**. Per ulteriori informazioni, vedere [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md).  
  
> [!NOTE]
>  Per ulteriori informazioni su ciò che Gestione driver esegue il mapping di questa funzione a quando un'applicazione ODBC *2. x* utilizza un driver ODBC *3. x* , vedere [mapping di funzioni deprecate](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) in Appendice G: linee guida per la compatibilità con le versioni precedenti.  
> 
> [!NOTE]
>  L'attributo SQL_ASYNC_DBC_FUNCTION_ENABLE introdotto in ODBC 3,8 non è supportato da **SQLGetConnectOption**. Le applicazioni che usano l'operazione asincrona su un handle di connessione devono usare **SQLGetConnectAttr**.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni di riferimento sulle API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
