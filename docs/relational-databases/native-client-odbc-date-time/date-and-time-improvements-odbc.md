---
title: Miglioramenti di data e ora (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC]
- ODBC, date/time improvements
ms.assetid: e31d5ca5-2103-498f-954c-1ee93e217186
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7cc697c60857f47630dd041762f90f789dd170d5
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73783885"
---
# <a name="date-and-time-improvements-odbc"></a>Miglioramenti relativi a data e ora (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] sono stati introdotti nuovi tipi di dati di data e ora. In questa sezione viene descritto il modo in cui questi nuovi tipi vengono esposti come estensioni in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Per una panoramica del supporto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client per i nuovi tipi di dati relativi a data e ora, vedere [miglioramenti di data e ora](../../relational-databases/native-client/features/date-and-time-improvements.md). Per un esempio che illustra il supporto ODBC per data/ora, vedere [usare i tipi di data e ora](../../relational-databases/native-client-odbc-how-to/use-date-and-time-types.md).  
  
 Per informazioni più generali sui tipi di dati di data e ora, vedere [DateTime &#40;Transact&#41;-SQL](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Supporto dei tipi di dati per i miglioramenti relativi a data e ora ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 Vengono fornite informazioni sui tipi ODBC che supportano i tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di data e ora.  
  
 [ODBC &#40;metadati&#41;](https://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
 Vengono descritte le informazioni restituite nei campi del descrittore del parametro di implementazione (dpi) e del descrittore della riga di implementazione (IRD), nonché i metadati della colonna restituiti da **SQLColumns** e **SQLProcedureColumns**. Descrive anche i metadati del tipo di dati restituiti da **SQLGetTypeInfo**.  
  
 [conversioni di tipi di dati &#40;DateTime ODBC&#41;](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-odbc.md)  
 Viene descritto come eseguire la conversione tra i valori datetime e datetimeoffset.  
  
 [Supporto sql_variant per i tipi di data e ora](../../relational-databases/native-client-odbc-date-time/sql-variant-support-for-date-and-time-types.md)  
 Viene descritto il supporto della funzione SQL_VARIANT per la funzionalità avanzata di data e ora.  
  
 [Modifiche della copia bulk per i tipi &#40;di data e ora avanzati OLE DB e ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Vengono descritti i miglioramenti apportati ai tipi di data/ora per supportare le operazioni di copia bulk.  
  
 [Comportamento del tipo di data e ora migliorato con le &#40;versioni precedenti di SQL Server ODBC&#41;](../../relational-databases/native-client-odbc-date-time/enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 Viene descritto il comportamento previsto quando un'applicazione client che utilizza le caratteristiche avanzate di data e ora comunica con una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quando un client compilato con una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client invia comandi a un server che supporta le caratteristiche avanzate di data e ora.  
  
 [Supporto delle API ODBC per le funzionalità avanzate di data e ora](../../relational-databases/native-client-odbc-date-time/odbc-api-support-for-enhanced-date-and-time-features.md)  
 Vengono elencate le funzioni ODBC che supportano la funzionalità avanzata di data e ora.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
