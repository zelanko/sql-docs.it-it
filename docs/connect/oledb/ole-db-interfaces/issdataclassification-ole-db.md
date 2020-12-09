---
title: ISSDataClassification | Microsoft Docs
description: Interfaccia ISSDataClassification
ms.custom: ''
ms.date: 09/30/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSDataClassification
apitype: COM
helpviewer_keywords:
- ISSDataClassification interface
author: bazizi
ms.author: v-beaziz
ms.openlocfilehash: 328110f81f993c66a9455324ff8ec830b329b41b
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506660"
---
# <a name="issdataclassification"></a>ISSDataClassification
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW](../../../includes/applies-to-version/sql-asdb-asa.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  L'interfaccia **ISSDataClassification** consente di recuperare i dati di classificazione di riservatezza per il set di righe attivo così come vengono ricevuti da SQL Server.
  

## <a name="methods"></a>Metodi

|Metodo|Descrizione|  
|------------|-----------------|  
|[ISSDataClassification::GetSensitivityClassification](../../oledb/ole-db-interfaces/issdataclassification-getsensitivityclassification-ole-db.md)|Restituisce un puntatore a una struttura SENSITIVITYCLASSIFICATION che contiene informazioni relative alla classificazione di riservatezza.|  

## <a name="see-also"></a>Vedere anche  
 [Interfacce &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)   
 [Set di righe](../ole-db-rowsets/rowsets.md)   
 [Uso della classificazione dei dati](../features/using-data-classification.md)
