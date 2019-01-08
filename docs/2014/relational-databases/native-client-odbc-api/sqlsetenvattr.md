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
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354330"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
  Il [riferimento per programmatori ODBC](https://go.microsoft.com/fwlink/?LinkId=45250) definisce come i driver ODBC è necessario interpretare il **SQLSetEnvAttr** attributo specifiche dalle applicazioni scritte in ODBC 2. *x* o ODBC 3. *x* API. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client è conforme a tali regole.  
  
 Uno degli attributi controllati da **SQLSetEnvAttr** se il pool di connessioni è utilizzabile. Se il pool di connessioni viene usato con il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client, il *DriverCompletion* parametro deve essere impostato su SQL_DRIVER_NOPROMPT quando ci si connette con uno [SQLDriverConnect](sqldriverconnect.md) o **SQLConnect**.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLSetEnvAttr-funzione](https://go.microsoft.com/fwlink/?LinkId=59369)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
