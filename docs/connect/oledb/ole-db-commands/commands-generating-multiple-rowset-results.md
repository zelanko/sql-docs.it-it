---
title: Comandi che generano risultati con più set di righe | Microsoft Docs
description: Comandi che generano risultati con più set di righe
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- multiple rowsets
- rowsets [OLE DB], multiple
- OLE DB Driver for SQL Server, commands
- OLE DB Driver for SQL Server, multiple rowsets
- commands [OLE DB]
- multiple-rowset results
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 5374e1ccd1024993369091b431a025676bccf1f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016061"
---
# <a name="commands-generating-multiple-rowset-results"></a>Comandi che generano risultati con più set di righe
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Il driver OLE DB per SQL Server può restituire più set di righe [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dalle istruzioni. Tramite le istruzioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono restituiti più set di righe nelle condizioni seguenti:  
  
-   Le istruzioni SQL in batch vengono inviate come singolo comando.  
  
-   Le stored procedure consentono di implementare un batch di istruzioni SQL.  
  
## <a name="batches"></a>Batch  
 Il driver OLE DB per SQL Server riconosce il carattere punto e virgola come delimitatore di batch per le istruzioni SQL:  
  
```  
WCHAR*       wSQLString = L"SELECT * FROM Categories; "  
                          L"SELECT * FROM Products";  
```  
  
 L'invio di più istruzioni SQL in un batch è più efficiente dell'esecuzione separata delle singole istruzioni SQL. Questo tipo di invio riduce infatti i round trip in rete dal client al server.  
  
## <a name="stored-procedures"></a>Stored procedure  
 Tramite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene restituito un set di risultati per ogni istruzione di una stored procedure. Pertanto, dalla maggior parte delle stored procedure di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengono restituiti più set di risultati.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Uso di IMultipleResults per elaborare più set di risultati](../../oledb/ole-db-commands/using-imultipleresults-to-process-multiple-result-sets.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Comandi](../../oledb/ole-db-commands/commands.md)  
  
  
