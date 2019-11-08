---
title: Miglioramenti di data e ora (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB]
- OLE DB, date/time improvements
ms.assetid: 71614aaf-0fa4-4fe0-b522-68e2e0b66f43
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c1ac0b0d93c35986b3eeedaf7148339770af1933
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73772810"
---
# <a name="date-and-time-improvements-ole-db"></a>Miglioramenti relativi a data e ora (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] sono stati introdotti nuovi tipi di dati di data e ora. In questa sezione viene descritto il modo in cui questi nuovi tipi vengono esposti come estensioni in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Per una panoramica del supporto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client per i nuovi tipi di dati relativi a data e ora, vedere [miglioramenti di data e ora](../../relational-databases/native-client/features/date-and-time-improvements.md). Per un esempio, vedere [usare le funzionalità &#40;avanzate di data e&#41;ora OLE DB](../../relational-databases/native-client-ole-db-how-to/use-enhanced-date-and-time-features-ole-db.md).  
  
 Per informazioni più generali sui tipi di dati di data e ora, vedere [DateTime &#40;Transact&#41;-SQL](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Supporto dei tipi di dati per i miglioramenti relativi a data e ora OLE DB](../../relational-databases/native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
 Vengono fornite informazioni sui tipi OLE DB ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client) che supportano i tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] data e ora.  
  
 [OLE DB &#40;metadati&#41;](https://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
 Contiene informazioni sulla struttura DBBINDING, **ICommandWithParameters:: GetParameterInfo**, **ICommandWithParameters:: separameterinfo**, **IColumnsRowset:: GetColumnsRowset**e i**ColumnsInfo:: GetColumnInfo** . Vengono inoltre fornite informazioni sugli aggiornamenti ai set di righe dello schema OLE DB.  
  
 [Associazioni e conversioni &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/conversions-ole-db.md)  
 Vengono illustrate le regole per la conversione fra server e client per tipi di dati sia nuovi che esistenti.  
  
 [Modifiche della copia bulk per i tipi &#40;di data e ora avanzati OLE DB e ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Vengono descritti i miglioramenti apportati ai tipi di data/ora per supportare le operazioni di copia bulk.  
  
 [Supporto dell'API OLE DB per i miglioramenti relativi a data e ora](../../relational-databases/native-client-ole-db-date-time/ole-db-api-support-for-date-and-time-enhancements.md)  
 Vengono descritte le API OLE DB che supportano le caratteristiche avanzate dei tipi di dati date/time.  
  
 [Possibilità di confronto per IRowsetFind](../../relational-databases/native-client-ole-db-date-time/comparability-for-irowsetfind.md)  
 Descrive i tipi di data/ora e **IRowsetFind**.  
  
 [Nuove funzionalità di data e ora con versioni &#40;precedenti di SQL Server OLE DB&#41;](../../relational-databases/native-client-ole-db-date-time/new-date-and-time-features-with-previous-sql-server-versions-ole-db.md)  
 Viene descritto il comportamento previsto quando un'applicazione client che utilizza le caratteristiche avanzate dei tipi date e time comunica con una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quando un client compilato con una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client invia comandi a un server che supporta tali caratteristiche avanzate.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
