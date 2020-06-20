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
author: rothja
ms.author: jroth
ms.openlocfilehash: e5d44756131b6133baec69e34da11055a965e2da
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022729"
---
# <a name="sqlendtran"></a>SQLEndTran
  Per impostazione predefinita, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client chiude il cursore associato di un'istruzione quando **SQLEndTran** esegue il commit o il rollback di un'operazione. I cursori del server vengono chiusi a meno che non siano statici. Quando **SQLEndTran** esegue il commit o il rollback di un'operazione, il comportamento del cursore associato dell'istruzione è determinato dal valore dell'attributo di connessione ODBC specifico del driver SQL_COPT_SS_PRESERVE_CURSORS, impostato da [SQLSetConnectAttr](sqlsetconnectattr.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)   
 [SQLEndTran Function](https://go.microsoft.com/fwlink/?LinkId=59342)  
  
  
