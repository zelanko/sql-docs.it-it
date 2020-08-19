---
description: 'Uso di IRow:: GetColumns in SQL Server Native Client'
title: 'Utilizzo di IRow:: GetColumns (provider OLE DB Native Client)'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c40a0d54e3c8b7efa09933ae4998f66efc3ec32c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448289"
---
# <a name="using-irowgetcolumns-in-sql-server-native-client"></a>Uso di IRow:: GetColumns in SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  L'implementazione di **IRow** consente un accesso sequenziale forward-only alle colonne. È possibile accedere a tutte le colonne nella riga con una sola chiamata a **IRow::GetColumns** o chiamare **IRow::GetColumns** più volte a ogni accesso a diverse colonne nella riga.  
  
 Le chiamate multiple a **IRow::GetColumns** non devono sovrapporsi. Se, ad esempio, la prima chiamata a **IRow::GetColumns** recupera le colonne 1, 2 e 3, la seconda chiamata a **IRow::GetColumns** dovrebbe recuperare le colonne 4, 5 e 6. Se le chiamate successive a **IRow::GetColumns** si sovrappongono, il flag di stato (il campo dwstatus in DBCOLUMNACCESS) viene impostato su DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Vedere anche  
 [Recupero di una sola riga con IRow](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
