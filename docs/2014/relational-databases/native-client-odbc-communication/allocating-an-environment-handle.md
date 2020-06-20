---
title: Allocazione di un handle di ambiente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c655b5e9a406c3e1881c9dd199a92666377918f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021116"
---
# <a name="allocating-an-environment-handle"></a>Allocazione di un handle di ambiente
  Prima di poter chiamare una funzione ODBC, un'applicazione deve inizializzare l'ambiente ODBC e allocare un handle di ambiente. Si tratta dell'handle dell'ambito globale che funge da segnaposto per gli altri handle in ODBC. A tale scopo, chiamare **SQLAllocHandle** con il parametro *HandleType* impostato su SQL_HANDLE_ENV e *InputHandle puntare* impostato su SQL_NULL_HANDLE.  
  
 Dopo avere allocato l'handle di ambiente, l'applicazione deve impostare gli attributi di ambiente per indicare la versione delle chiamate alle funzioni ODBC che verrà utilizzata. Per utilizzare ODBC 3. funzioni *x* , chiamare [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) con il parametro *attribute* impostato su SQL_ATTR_ODBC_VERSION e *ValuePtr* impostato su SQL_OV_ODBC3.  
  
## <a name="see-also"></a>Vedere anche  
 [Comunicazione con SQL Server &#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
