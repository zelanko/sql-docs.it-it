---
title: SQLEndTran | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLEndTran function
ms.assetid: 95cff841-c2d5-4e1e-a18d-f3d4696a5b85
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5425fdc189febd23e9fc61765f4ad56fe484111
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63067592"
---
# <a name="sqlendtran"></a>SQLEndTran
  Per impostazione predefinita, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il driver ODBC di Native client chiude il cursore associato di un'istruzione quando **SQLEndTran** esegue il commit o il rollback di un'operazione. I cursori del server vengono chiusi a meno che non siano statici. Quando **SQLEndTran** esegue il commit o il rollback di un'operazione, il comportamento del cursore associato dell'istruzione è determinato dal valore dell'attributo di connessione ODBC specifico del driver SQL_COPT_SS_PRESERVE_CURSORS, impostato da [SQLSetConnectAttr](sqlsetconnectattr.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)   
 [SQLEndTran Function](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
