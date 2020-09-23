---
title: Uso di IRow::GetColumns (OLE DB Driver)
description: Informazioni su come usare IRow::GetColumns per accedere a tutte le colonne in una riga in OLE DB Driver per SQL Server. IRow consente l'accesso sequenziale forward-only alle colonne.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [OLE DB Driver for SQL Server]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60ded2ad36346bcb05d75add252f0357c48398e7
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859930"
---
# <a name="using-irowgetcolumns"></a>Utilizzo di IRow::GetColumns
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  L'implementazione di **IRow** consente un accesso sequenziale forward-only alle colonne. È possibile accedere a tutte le colonne nella riga con una sola chiamata a **IRow::GetColumns** o chiamare **IRow::GetColumns** più volte a ogni accesso a diverse colonne nella riga.  
  
 Le chiamate multiple a **IRow::GetColumns** non devono sovrapporsi. Se, ad esempio, la prima chiamata a **IRow::GetColumns** recupera le colonne 1, 2 e 3, la seconda chiamata a **IRow::GetColumns** dovrebbe recuperare le colonne 4, 5 e 6. Se le chiamate successive a **IRow::GetColumns** si sovrappongono, il flag di stato (il campo dwstatus in DBCOLUMNACCESS) viene impostato su DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Vedere anche  
 [Recupero di una sola riga con IRow](../../oledb/ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
