---
title: Supporto dell'API OLE DB per i miglioramenti relativi a data e ora | Microsoft Docs
description: Supporto dell'API OLE DB per i miglioramenti relativi a data e ora
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c2671b3df6432e63c0e0b36a24bade60286f72a7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015677"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Supporto dell'API OLE DB per i miglioramenti relativi a data e ora
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Le caratteristiche avanzate di data e ora sono supportate dalle seguenti API OLE DB.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Un flag viene aggiunto nella struttura DBBINDING per consentire alle applicazioni di distinguere tra i valori **datetime**, **datetime2** e **smalldatetime**. Per altre informazioni, vedere [Metadati per parametri e set di righe](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Per altre informazioni, vedere [Modifiche apportate alla copia bulk per i tipi di data e ora migliorati &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md).|  
|ICommandWithParameters::GetParameterInfo|Per altre informazioni, vedere [Metadati per parametri e set di righe](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Per altre informazioni, vedere [Metadati per parametri e set di righe](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Per altre informazioni, vedere [Metadati per parametri e set di righe](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Per altre informazioni, vedere [Metadati per parametri e set di righe](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Per informazioni dettagliate sui set di righe dello schema interessati, vedere[Set di righe dello schema e dei tipi Date e Time](../../oledb/ole-db-date-time/metadata-date-and-time-and-schema-rowsets.md).|  
|IRowsetFastLoad|Questa interfaccia supporta i nuovi tipi di data/ora, ma non è stata apportata alcuna modifica all'interfaccia.|  
|ITableDefinition::CreateTable|Per altre informazioni, vedere [Supporto dei tipi di dati per i miglioramenti relativi a data e ora OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Miglioramenti relativi a data e ora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
