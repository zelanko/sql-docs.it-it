---
title: SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47b0d30ac70ff3b7974f7d0530b9fb50494ac424
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63188749"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
  Il [riferimento per programmatori ODBC](https://go.microsoft.com/fwlink/?LinkId=45250) definisce il modo in cui i driver ODBC devono interpretare le specifiche dell'attributo **SQLSetEnvAttr** dalle applicazioni scritte in ODBC 2. *x* o ODBC 3. API *x* . Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client è conforme a tali regole.  
  
 Uno degli attributi controllati da **SQLSetEnvAttr** è se deve essere usato il pool di connessioni. Se il pool di connessioni viene utilizzato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il driver ODBC di Native client, il parametro *DriverCompletion* deve essere impostato su SQL_DRIVER_NOPROMPT durante la connessione con [SQLDriverConnect](sqldriverconnect.md) o **SQLConnect**.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLSetEnvAttr (funzione)](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
