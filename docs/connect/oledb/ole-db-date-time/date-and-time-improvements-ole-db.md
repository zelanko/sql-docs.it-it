---
title: Data e ora miglioramenti (OLE DB) | Microsoft Docs
description: Miglioramenti relativi a data e ora (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 5518461fade08e6f23e1594056c284865957274c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66769342"
---
# <a name="date-and-time-improvements-ole-db"></a>Miglioramenti relativi a data e ora (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  In [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] sono stati introdotti nuovi tipi di dati di data e ora. Questa sezione descrive come questi nuovi tipi vengono esposti come estensioni nel Driver OLE DB per SQL Server. Per una panoramica del Driver OLE DB per il supporto di SQL Server per i nuovi tipi data e ora dei dati, vedere [data e ora miglioramenti](../../oledb/features/date-and-time-improvements.md). Per un esempio, vedere [utilizzo avanzate di data e ora funzionalità &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md).  
  
 Per informazioni più generali sui tipi di dati di data e ora, vedere [datetime &#40;Transact-SQL&#41;](../../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Supporto dei tipi di dati per i miglioramenti relativi a data e ora OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 Fornisce informazioni su OLE DB (Driver OLE DB per SQL Server) i tipi che supportano [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipi di dati di data e ora.  
  
 [Metadati &#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
 Contiene informazioni sulla struttura DBBINDING, **ICommandWithParameters:: GetParameterInfo**, **ICommandWithParameters:: SetParameterInfo**, **IColumnsRowset:: GetColumnsRowset**e voglio**ColumnsInfo::GetColumnInfo**. Vengono inoltre fornite informazioni sugli aggiornamenti ai set di righe dello schema OLE DB.  
  
 [Associazioni e conversioni &#40;OLE DB&#41;](../../oledb/ole-db-date-time/conversions-ole-db.md)  
 Vengono illustrate le regole per la conversione fra server e client per tipi di dati sia nuovi che esistenti.  
  
 [Modifiche apportate alla copia bulk per i tipi di data e ora migliorati &#40;OLE DB&#41;](../../oledb/ole-db-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db.md)  
 Vengono descritti i miglioramenti apportati ai tipi di data/ora per supportare le operazioni di copia bulk.  
  
 [Supporto dell'API OLE DB per i miglioramenti relativi a data e ora](../../oledb/ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 Vengono descritte le API OLE DB che supportano le caratteristiche avanzate dei tipi di dati date/time.  
  
 [Possibilità di confronto per IRowsetFind](../../oledb/ole-db-date-time/comparability-for-irowsetfind.md)  
 Vengono descritti i tipi data/ora e **IRowsetFind**.  
 
  
## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per programmazione con SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
