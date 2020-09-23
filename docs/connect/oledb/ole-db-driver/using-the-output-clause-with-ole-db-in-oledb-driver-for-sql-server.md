---
title: Uso della clausola OUTPUT con OLE DB nel driver OLE DB per SQL Server | Microsoft Docs
description: Informazioni sull'uso della clausola OUTPUT in un comando INSERT, UPDATE, DELETE o MERGE in OLE DB Driver per SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1374dab2ac4954d173d8d131d59bfa4b39f2ad0a
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861510"
---
# <a name="using-the-output-clause-with-ole-db-in-ole-db-driver-for-sql-server"></a>Uso della clausola OUTPUT con OLE DB nel driver OLE DB per SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Se si utilizza una clausola OUTPUT in un comando INSERT, UPDATE, DELETE o MERGE, il numero di righe interessate non risulta disponibile. L'applicazione deve contare il numero di righe nel set di righe restituito dalla clausola OUTPUT.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un driver OLE DB per applicazione SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md) 
  
  
