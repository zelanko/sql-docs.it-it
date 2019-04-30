---
title: Eliminazione di una tabella di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- deleting tables
- SQL Server Native Client OLE DB provider, tables
- removing tables
- dropping tables
ms.assetid: b6d6c4de-43c6-473e-92aa-34ffddd58cbe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7af3d096d9e58b1cb75e2d7cab15988183578fdd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046466"
---
# <a name="dropping-a-sql-server-table"></a>Eliminazione di una tabella di SQL Server
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client espone il **itabledefinition:: DropTable** (funzione). Ciò consente ai consumer di rimuovere un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabella da un database.  
  
 I consumer specificano il nome della tabella come stringa di caratteri Unicode nel membro *pwszName* dell'unione *uName* nel parametro *pTableID*. Il membro *eKind* di*pTableID* deve essere DBKIND_NAME.  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle e indici](tables-and-indexes.md)  
  
  
