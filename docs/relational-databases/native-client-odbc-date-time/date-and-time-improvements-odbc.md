---
title: Data e ora miglioramenti (ODBC) | Documenti di Microsoft
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
ms.openlocfilehash: 65a083b1aac2661ac013bf005d1d442d73a86f99
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030507"
---
# <a name="date-and-time-improvements-odbc"></a>Miglioramenti relativi a data e ora (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] sono stati introdotti nuovi tipi di dati di data e ora. In questa sezione viene descritto come questi nuovi tipi vengono esposti come estensioni in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Per una panoramica delle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il supporto Client nativo per la nuova data e tipi di dati di ora, vedere [data e ora miglioramenti](../../relational-databases/native-client/features/date-and-time-improvements.md). Per un esempio che illustra il supporto per ODBC Data/ora, vedere [Usa data e ora tipi](../../relational-databases/native-client-odbc-how-to/use-date-and-time-types.md).  
  
 Per ulteriori informazioni generali sui tipi di dati di data e ora, vedere [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md).  
  
## <a name="in-this-section"></a>In questa sezione  
 [Supporto dei tipi di dati per i miglioramenti relativi a data e ora ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md)  
 Vengono fornite informazioni sui tipi ODBC che supportano i tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di data e ora.  
  
 [Metadati &#40;ODBC&#41;](https://msdn.microsoft.com/library/99133efc-b1f2-46e9-8203-d90c324a8e4c)  
 Descrive le informazioni restituite nel descrittore del parametro di implementazione (IPD) e campi di implementazione riga descrittore (IRD.), così come metadati della colonna restituito da **SQLColumns** e **SQLProcedureColumns**. Descrive inoltre i metadati del tipo di dati restituito da **SQLGetTypeInfo**.  
  
 [Conversioni di tipi di dati DateTime &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-odbc.md)  
 Viene descritto come eseguire la conversione tra i valori datetime e datetimeoffset.  
  
 [Supporto sql_variant per i tipi di data e ora](../../relational-databases/native-client-odbc-date-time/sql-variant-support-for-date-and-time-types.md)  
 Viene descritto il supporto della funzione SQL_VARIANT per la funzionalità avanzata di data e ora.  
  
 [Le modifiche apportate alla copia di massa per data avanzata e tipi in fase di &#40;OLE DB e ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md)  
 Vengono descritti i miglioramenti apportati ai tipi di data/ora per supportare le operazioni di copia bulk.  
  
 [Enhanced Data e ora il comportamento dei tipi con le versioni precedenti di SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/enhanced-date-and-time-type-behavior-with-previous-sql-server-versions-odbc.md)  
 Viene descritto il comportamento previsto quando un'applicazione client che utilizza le caratteristiche avanzate di data e ora comunica con una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quando un client compilato con una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client invia comandi a un server che supporta le caratteristiche avanzate di data e ora.  
  
 [Supporto delle API ODBC per le funzionalità avanzate di data e ora](../../relational-databases/native-client-odbc-date-time/odbc-api-support-for-enhanced-date-and-time-features.md)  
 Vengono elencate le funzioni ODBC che supportano la funzionalità avanzata di data e ora.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
