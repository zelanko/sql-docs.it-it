---
title: Comandi che generano risultati di più set di righe | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- SQL Server Native Client OLE DB provider, commands
- SQL Server Native Client OLE DB provider, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
ms.assetid: 4567668d-35fd-4162-b61f-f7536862cdcb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 04a7db670171f6f890f55a89e2da987ef2309f0e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62657681"
---
# <a name="commands-generating-multiple-rowset-results"></a>Comandi che generano risultati con più set di righe
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client può restituire più set di righe da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istruzioni. Tramite le istruzioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono restituiti più set di righe nelle condizioni seguenti:  
  
-   Le istruzioni SQL in batch vengono inviate come singolo comando.  
  
-   Le stored procedure consentono di implementare un batch di istruzioni SQL.  
  
## <a name="batches"></a>Batch  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client riconosce il carattere punto e virgola come delimitatore di batch per le istruzioni SQL:  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 L'invio di più istruzioni SQL in un batch è più efficiente dell'esecuzione separata delle singole istruzioni SQL. Questo tipo di invio riduce infatti i round trip in rete dal client al server.  
  
## <a name="stored-procedures"></a>Stored procedure  
 Tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene restituito un set di risultati per ogni istruzione di una stored procedure. Pertanto, dalla maggior parte delle stored procedure di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono restituiti più set di risultati.  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Uso di IMultipleResults per elaborare più set di risultati](using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Comandi](commands.md)  
  
  
