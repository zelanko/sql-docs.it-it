---
title: Metadati per parametri e set di righe | Microsoft Docs
description: Metadati per parametri e set di righe
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 641859e134a5f3c3201f239023f911b79de1c11e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "67995102"
---
# <a name="metadata---parameter-and-rowset"></a>Metadati - Parametro e set di righe
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Questo articolo contiene informazioni sul tipo e sui membri di tipo seguenti, in relazione ai miglioramenti apportati alle funzionalità di data e ora OLE DB.  
  
-   Struttura DBBINDING  
  
-   **ICommandWithParameters::GetParameterInfo**  
  
-   **ICommandWithParameters::SetParameterInfo**  
  
-   **IColumnsRowset::GetColumnsRowset**  
  
-   **IColumnsInfo::GetColumnInfo**  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 Le informazioni seguenti vengono restituite nella struttura DBPARAMINFO attraverso *prgParamInfo*:  
  
|Tipo di parametro|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|-------------------|------------------|--------------|-----------------------------------------------------|  
|Data|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|Set|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Set|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Set|  
  
 Tenere presente che in alcuni casi gli intervalli di valori non sono continui Ciò è dovuto all'aggiunta di un separatore decimale quando la precisione frazionaria è maggiore di zero.  
  
 DBPARAMFLAGS_SS_ISVARIABLESCALE è valido solo se si è connessi a un server [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (o versioni successive). DBPARAMFLAGS_SS_ISVARIABLESCALE non viene mai impostato quando si è connessi a server legacy.  
  
## <a name="icommandwithparameterssetparameterinfo-and-implied-parameter-types"></a>ICommandWithParameters::SetParameterInfo e tipi di parametri impliciti  
 Le informazioni specificate nella struttura DBPARAMBINDINFO devono essere conformi agli elementi seguenti:  
  
|*pwszDataSourceType*<br /><br /> (specifico del provider)|*pwszDataSourceType*<br /><br /> (generico di OLE DB)|*ulParamSize*|*bScale*|  
|----------------------------------------------------|-------------------------------------------------|-------------------|--------------|  
||DBTYPE_DATE|6|Ignorato|  
|Data|DBTYPE_DBDATE|6|Ignorato|  
||DBTYPE_DBTIME|10|Ignorato|  
|time|DBTYPE_DBTIME2|10|0..7|  
|smalldatetime||16|Ignorato|  
|Datetime||16|Ignorato|  
|datetime2 o DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|16|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|0..7|  
  
 Il parametro *bPrecision* viene ignorato.  
  
 "DBPARAMFLAGS_SS_ISVARIABLESCALE" viene ignorato in caso di invio di dati al server. Le applicazioni possono forzare l'uso di tipi di flusso TDS (Tabular-Data Stream) legacy usando i nomi di tipo specifici del provider "**datetime**" e "**smalldatetime**". Se si è connessi ai server [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (o versioni successive), viene usato il formato "**datetime2**" e si verifica una conversione server implicita, se necessario, quando il nome del tipo è "**datetime2**" o "DBTYPE_DBTIMESTAMP". *bScale* viene ignorato se vengono usati i nomi dei tipi specifici del provider "**datetime**" o "**smalldatetime**". In caso contrario, è necessario verificare che *bScale* sia impostato correttamente nelle applicazioni. Nelle applicazioni aggiornate da MDAC e in OLE DB Driver per SQL Server aggiornato da [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] che usano "DBTYPE_DBTIMESTAMP" si verificherà un errore se *bScale* non viene impostato correttamente. In caso di connessione a istanze server precedenti a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], un valore di *bScale* diverso da 0 o 3 con "DBTYPE_DBTIMESTAMP" è un errore e comporta la restituzione di E_FAIL.  
  
 Quando ICommandWithParameters::SetParameterInfo non viene chiamato, il provider implica il tipo di server dal tipo di associazione come specificato in IAccessor::CreateAccessor come indicato di seguito:  
  
|Tipo di associazione|*pwszDataSourceType*<br /><br /> (specifico del provider)|  
|------------------|----------------------------------------------------|  
|DBTYPE_DATE|datetime2(0)|  
|DBTYPE_DBDATE|Data|  
|DBTYPE_DBTIME|time(0)|  
|DBTYPE_DBTIME2|time(7)|  
|DBTYPE_DBTIMESTAMP|datetime2(7)|  
|DBTYPE_DBTIMESTAMPOFFSET|datetimeoffset(7)|  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 **IColumnsRowset::GetColumnsRowset** restituisce le colonne seguenti:  
  
|Tipo di colonna|DBCOLUMN_TYPE|DBCOLUM_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|DBCOLUMN_FLAGS, DBCOLUMNFLAGS_SS_ISVARIABLESCALE|  
|-----------------|--------------------|-------------------------|-------------------------|--------------------------------------------------|---------------------------------------------------------|  
|Data|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|Set|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Set|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Set|  
  
 In DBCOLUMN_FLAGS il valore di DBCOLUMNFLAGS_ISFIXEDLENGTH è sempre true per i tipi date/time e il valore dei flag seguenti è sempre false:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 I flag restanti (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE e DBCOLUMNFLAGS_WRITEUNKNOWN) possono essere impostati in base alla modalità di definizione della colonna e alla query effettiva.  
  
 In DBCOLUMN_FLAGS è disponibile un nuovo flag DBCOLUMNFLAGS_SS_ISVARIABLESCALE che consente di determinare il tipo di server delle colonne nelle applicazioni, dove DBCOLUMN_TYPE è DBTYPE_DBTIMESTAMP. Per identificare il tipo di server è necessario utilizzare anche DBCOLUMN_SCALE o DBCOLUMN_DATETIMEPRECISION.  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE è valido solo quando si è connessi a un server [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] o versioni successive. DBCOLUMNFLAGS_SS_ISVARIABLESCALE non è definito quando si è connessi a server legacy.  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 La struttura DBCOLUMNINFO restituisce le informazioni seguenti:  
  
|Tipo di parametro|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|Data|DBTYPE_DBDATE|6|10|0|Clear|  
|time(1..7)|DBTYPE_DBTIME2|10|8, 10..16|0..7|Set|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|Datetime|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Set|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Set|  
  
 In *dwFlags* il valore di DBCOLUMNFLAGS_ISFIXEDLENGTH è sempre true per i tipi date/time e il valore dei flag seguenti è sempre false:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER, MAYDEFER  
  
 I flag restanti (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE e DBCOLUMNFLAGS_WRITEUNKNOWN) possono essere impostati.  
  
 In *dwFlags* viene specificato un nuovo flag DBCOLUMNFLAGS_SS_ISVARIABLESCALE per consentire a un'applicazione di determinare il tipo di server delle colonne in cui *wType* è DBTYPE_DBTIMESTAMP. Per identificare il tipo di server usare anche *bScale*.  
  
## <a name="see-also"></a>Vedere anche  
 [Supporto dei tipi di dati per i miglioramenti relativi a data e ora OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
  
  
