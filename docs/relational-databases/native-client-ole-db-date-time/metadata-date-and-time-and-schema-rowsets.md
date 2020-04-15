---
title: Data e ora e set di righe dello schema
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
ms.assetid: 8c35e86f-0597-4ef4-b2b8-f643e53ed4c2
author: markingmyname
ms.author: maghan
ms.custom: seo-dt-2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 66aad8634cdb4d71ba765da94e1e395fc1583226
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301075"
---
# <a name="metadata---date-and-time-and-schema-rowsets"></a>Metadati - Set di righe dello schema e di data e ora
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  In questo argomento vengono fornite informazioni sui set di righe COLUMNS e PROCEDURE_PARAMETERS. Tali informazioni fanno riferimento ai miglioramenti apportati alla data e all'ora di OLE DB per [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="columns-rowset"></a>Set di righe COLUMNS  
 Per i tipi di data/ora vengono restituiti i valori di colonna seguenti:  
  
|Tipo di colonna|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|Data|DBTYPE_DBDATE|Clear|0|  
|time|DBTYPE_DBTIME2|Set|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|Clear|0|  
|Datetime|DBTYPE_DBTIMESTAMP|Clear|3|  
|datetime2|DBTYPE_DBTIMESTAMP|Set|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|Set|0..7|  
  
 In COLUMN_FLAGS il valore di DBCOLUMNFLAGS_ISFIXEDLENGTH è sempre true per i tipi date/time e il valore dei flag seguenti è sempre false:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 I flag restanti (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE e DBCOLUMNFLAGS_WRITEUNKNOWN) possono essere impostati in base alla modalità di definizione della colonna.  
  
 In COLUMN_FLAGS è disponibile un nuovo flag DBCOLUMNFLAGS_SS_ISVARIABLESCALE che consente di determinare il tipo di server delle colonne nelle applicazioni, dove DATA_TYPE è DBTYPE_DBTIMESTAMP. Per identificare il tipo di server è necessario utilizzare anche DATETIME_PRECISION.  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE è valido solo quando si è connessi a un server [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o versioni successive). DBCOLUMNFLAGS_SS_ISFIXEDSCALE non è definito quando si è connessi a server legacy.  
  
## <a name="procedure_parameters-rowset"></a>Set di righe PROCEDURE_PARAMETERS  
 DATA_TYPE contiene gli stessi valori del set di righe dello schema COLUMNS e TYPE_NAME contiene il tipo di server.  
  
 Una nuova colonna, SS_DATETIME_PRECISION, è stata aggiunta per restituire la precisione del tipo come nella colonna DATETIME_PRECISION, in modo analogo al set di righe COLUMNS.  
  
## <a name="provider_types-rowset"></a>Set di righe PROVIDER_TYPES  
 Per i tipi di data/ora vengono restituite le righe seguenti:  
  
|Tipo -><br /><br /> Colonna|Data|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|Data|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_DBDATE|DBTYPE_DBTIME2|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|scala|NULL|NULL|scala|scala|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|Data|time|smalldatetime|Datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|0|NULL|NULL|0|0|  
|MAXIMUM_SCALE|NULL|7|NULL|NULL|7|7|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE a meno che non si verifichi una delle condizioni seguenti:<br /><br /> Il client è connesso a un server legacy.<br /><br /> La proprietà della connessione della compatibilità dei tipi di dati specifica un livello di compatibilità pari a 80.|VARIANT_TRUE a meno che non si verifichi una delle condizioni seguenti:<br /><br /> Il client è connesso a un server legacy.<br /><br /> La proprietà della connessione della compatibilità dei tipi di dati specifica un livello di compatibilità pari a 80.|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 Poiché OLE DB definisce solo MINIMUM_SCALE e MAXIMUM_SCALE per i tipi numerici e decimali, l'utilizzo da parte di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client di queste colonne per time, datetime2 e datetimeoffset è di tipo non standard.  
  
## <a name="see-also"></a>Vedere anche  
 [Metadati &#40;OLE DB&#41;](https://msdn.microsoft.com/library/605e3be5-aeea-4573-9847-b866ed3c8bff)  
  
  
