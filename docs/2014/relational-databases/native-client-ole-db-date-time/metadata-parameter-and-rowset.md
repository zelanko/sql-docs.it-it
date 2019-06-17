---
title: Metadati per parametri e set di righe | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
ms.assetid: 31b318a4-20e7-4db0-b367-eb9938859029
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b96876a050f9ba46363792eec22d76640ee6fc2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62655627"
---
# <a name="parameter-and-rowset-metadata"></a>Metadati per parametri e set di righe
  In questo argomento vengono fornite informazioni sul tipo e sui membri di tipo seguenti, relativi ai miglioramenti apportati alle funzionalità di data e ora OLE DB.  
  
-   Struttura DBBINDING  
  
-   `ICommandWithParameters::GetParameterInfo`  
  
-   `ICommandWithParameters::SetParameterInfo`  
  
-   `IColumnsRowset::GetColumnsRowset`  
  
-   `IColumnsInfo::GetColumnInfo`  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 Le informazioni seguenti vengono restituite nella struttura DBPARAMINFO attraverso *prgParamInfo*:  
  
|Tipo di parametro|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|-------------------|------------------|--------------|-----------------------------------------------------|  
|Data|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|Impostare|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19,21..27|0..7|Impostare|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26,28..34|0..7|Impostare|  
  
 Tenere presente che in alcuni casi gli intervalli di valori non sono continui Ciò è dovuto all'aggiunta di un separatore decimale quando la precisione frazionaria è maggiore di zero.  
  
 DBPARAMFLAGS_SS_ISVARIABLESCALE è valido solo se si è connessi a un server [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o versioni successive). DBPARAMFLAGS_SS_ISVARIABLESCALE non viene mai impostato quando si è connessi a server legacy.  
  
## <a name="icommandwithparameterssetparameterinfo-and-implied-parameter-types"></a>ICommandWithParameters::SetParameterInfo e tipi di parametri impliciti  
 Le informazioni specificate nella struttura DBPARAMBINDINFO devono essere conformi agli elementi seguenti:  
  
|*pwszDataSourceType*<br /><br /> (specifico del provider)|*pwszDataSourceType*<br /><br /> (generico di OLE DB)|*ulParamSize*|*bScale*|  
|----------------------------------------------------|-------------------------------------------------|-------------------|--------------|  
||DBTYPE_DATE|6|Ignorato|  
|Data|DBTYPE_DBDATE|6|Ignorato|  
||DBTYPE_DBTIME|10|Ignorato|  
|time|DBTYPE_DBTIME2|10|0..7|  
|smalldatetime||16|Ignorato|  
|datetime||16|Ignorato|  
|datetime2 o DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|16|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|0..7|  
  
 Il *bPrecision* parametro viene ignorato.  
  
 "DBPARAMFLAGS_SS_ISVARIABLESCALE" viene ignorato in caso di invio di dati al server. Le applicazioni possono forzare l'utilizzo di tipi di flusso TDS (Tabular-Data Stream) legacy utilizzando i nomi di tipo specifici del provider "`datetime`" e "`smalldatetime`". Quando connesso a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o versione successiva) Server, "`datetime2`"viene usato il formato e una conversione server implicita verificherà, se necessario, quando è il nome del tipo"`datetime2`" o "DBTYPE_DBTIMESTAMP". *bScale* viene ignorata se i nomi di tipo specifico del provider "`datetime`"o"`smalldatetime`" vengono usati. In caso contrario, è necessario assicurarsi che *bScale* sia impostata correttamente. Applicazioni aggiornate da MDAC e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] che utilizzano "DBTYPE_DBTIMESTAMP" avrà esito negativo se non viene impostato *bScale* correttamente. In caso di connessione a istanze server precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], un valore di *bScale* diverso da 0 o 3 con "DBTYPE_DBTIMESTAMP" è un errore e comporta la restituzione di E_FAIL.  
  
 Quando non viene chiamato ICommandWithParameters:: SetParameterInfo, il provider Ricava il server di tipo dal tipo di associazione come specificato in IAccessor:: CreateAccessor come indicato di seguito:  
  
|Tipo di associazione|*pwszDataSourceType*<br /><br /> (specifico del provider)|  
|------------------|----------------------------------------------------|  
|DBTYPE_DATE|datetime2(0)|  
|DBTYPE_DBDATE|Data|  
|DBTYPE_DBTIME|time(0)|  
|DBTYPE_DBTIME2|time(7)|  
|DBTYPE_DBTIMESTAMP|datetime2(7)|  
|DBTYPE_DBTIMESTAMPOFFSET|datetimeoffset(7)|  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 `IColumnsRowset::GetColumnsRowset` restituisce le colonne seguenti:  
  
|Tipo di colonna|DBCOLUMN_TYPE|DBCOLUM_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|DBCOLUMN_FLAGS, DBCOLUMNFLAGS_SS_ISVARIABLESCALE|  
|-----------------|--------------------|-------------------------|-------------------------|--------------------------------------------------|---------------------------------------------------------|  
|Data|DBTYPE_DBDATE|6|10|0|Clear|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|Impostare|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Impostare|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Impostare|  
  
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
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE è valido solo quando si è connessi a un server [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versioni successive. DBCOLUMNFLAGS_SS_ISVARIABLESCALE non è definito quando si è connessi a server legacy.  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 La struttura DBCOLUMNINFO restituisce le informazioni seguenti:  
  
|Tipo di parametro|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|Data|DBTYPE_DBDATE|6|10|0|Clear|  
|time(1..7)|DBTYPE_DBTIME2|10|8, 10..16|0..7|Impostare|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Clear|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|Clear|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Impostare|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Impostare|  
  
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
 [Metadati &#40;OLE DB&#41;](../../database-engine/dev-guide/metadata-ole-db.md)  
  
  
