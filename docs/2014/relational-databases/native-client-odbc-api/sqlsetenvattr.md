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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 113c4508489e0f1dad8d134db7f86fc42371b456
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702154"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
  Il [riferimento per programmatori ODBC](https://go.microsoft.com/fwlink/?LinkId=45250) definisce il modo in cui i driver ODBC devono interpretare le specifiche dell'attributo **SQLSetEnvAttr** dalle applicazioni scritte in ODBC 2. *x* o ODBC 3. API *x* . Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client è conforme a tali regole.  
  
 Uno degli attributi controllati da **SQLSetEnvAttr** è se deve essere usato il pool di connessioni. Se il pool di connessioni viene utilizzato con il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client, il parametro *DriverCompletion* deve essere impostato su SQL_DRIVER_NOPROMPT durante la connessione con [SQLDriverConnect](sqldriverconnect.md) o **SQLConnect**.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLSetEnvAttr (funzione)](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
