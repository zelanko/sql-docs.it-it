---
title: 'Utilizzo di IRow:: GetColumns | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1fb748e9a991e3d4ea2bee5a076ea7d5e0e764a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103492"
---
# <a name="using-irowgetcolumns"></a>Utilizzo di IRow::GetColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  L'implementazione di **IRow** consente un accesso sequenziale forward-only alle colonne. È possibile accedere a tutte le colonne nella riga con una sola chiamata a **IRow::GetColumns** o chiamare **IRow::GetColumns** più volte a ogni accesso a diverse colonne nella riga.  
  
 Le chiamate multiple a **IRow::GetColumns** non devono sovrapporsi. Se, ad esempio, la prima chiamata a **IRow::GetColumns** recupera le colonne 1, 2 e 3, la seconda chiamata a **IRow::GetColumns** dovrebbe recuperare le colonne 4, 5 e 6. Se le chiamate successive a **IRow::GetColumns** si sovrappongono, il flag di stato (il campo dwstatus in DBCOLUMNACCESS) viene impostato su DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Vedere anche  
 [Recupero di una sola riga con IRow](../../relational-databases/native-client-ole-db-rowsets/fetching-a-single-row-with-irow.md)  
  
  
