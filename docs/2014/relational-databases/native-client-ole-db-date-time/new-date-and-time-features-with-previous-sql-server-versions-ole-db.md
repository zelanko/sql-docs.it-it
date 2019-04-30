---
title: Nuove caratteristiche data e ora con precedenti versioni di SQL Server (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], enhanced behavior with earlier SQL Server versions
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc810ced25733ce77d80c7bec38b03e3aaf3753a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233071"
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>Nuove funzionalità di data e ora con le versioni precedenti di SQL Server (OLE DB)
  In questo argomento viene descritto il comportamento previsto quando un'applicazione client che utilizza caratteristiche avanzate di data e ora comunica con una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriore [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]e quando un client compilato con una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] invia comandi a un server che supporta le avanzate funzionalità di data e ora.  
  
## <a name="down-level-client-behavior"></a>Comportamento dei client legacy  
 Applicazioni client che usano una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] visualizzare i tipi di data/ora di nuovo come `nvarchar` colonne. Il contenuto delle colonne è costituito da rappresentazioni letterali. Per altre informazioni, vedere la "i formati di dati: Sezione stringhe e valori letterali"di [supporto dei tipi di dati per data OLE DB e miglioramenti per la fase](data-type-support-for-ole-db-date-and-time-improvements.md). Le dimensioni di colonna corrispondono alla lunghezza massima in valori letterali per la precisione specificata per la colonna.  
  
 Le API di catalogo restituiranno metadati consistenti con il codice del tipo di dati legacy restituito al client, ad esempio `nvarchar`, e la rappresentazione legacy associata, ad esempio il formato letterale appropriato. Il nome del tipo di dati restituito, tuttavia, coinciderà con il nome effettivo del tipo di dati di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 Quando un'applicazione client legacy viene eseguita in un [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o versione successiva) in cui le modifiche dello schema di data/ora sono stato apportati tipi di server, il comportamento previsto è come segue:  
  
|Tipo di client OLE DB|Tipo di SQL Server 2005|Tipo di SQL Server 2008 (o versioni successive)|Conversione risultati (da server a client)|Conversione parametri (da client a server)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|Datetime|date|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Campi dell'ora impostati su zero.|IRowsetChange avrà esito negativo a causa di un troncamento della stringa se il campo dell'ora è diverso da zero.|  
|DBTYPE_DBTIME||Time(0)|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Campi della data impostati sulla data corrente.|Se i secondi frazionari sono diverse da zero, IRowsetChange avrà esito negativo a causa di un troncamento della stringa.<br /><br /> La data viene ignorata.|  
|DBTYPE_DBTIME||Time(7)|Si verifica un errore: valore letterale di ora non valida.|OK|  
|DBTYPE_DBTIMESTAMP|||Si verifica un errore: valore letterale di ora non valida.|OK|  
|DBTYPE_DBTIMESTAMP||Datetime2 (3)|OK|OK|  
|DBTYPE_DBTIMESTAMP||datetime2(7)|OK|OK|  
|DBTYPE_DBDATE|Smalldatetime|date|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Campi dell'ora impostati su zero.|IRowsetChange avrà esito negativo a causa di un troncamento della stringa se il campo dell'ora è diverso da zero.|  
|DBTYPE_DBTIME||Time(0)|OK|OK|  
|DBTYPE_DBTIMESTAMP|||Campi della data impostati sulla data corrente.|Se i secondi frazionari sono diverse da zero, IRowsetChange avrà esito negativo a causa di un troncamento della stringa.<br /><br /> La data viene ignorata.|  
|DBTYPE_DBTIMESTAMP||datetime2(0)|OK|OK|  
  
 OK indica che un funzionamento corretto in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] corrisponde a un corretto funzionamento anche in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o versioni successive).  
  
 Sono state prese in considerazione solo le modifiche dello schema comuni indicate di seguito:  
  
-   Utilizzo di un nuovo tipo nei casi in cui logicamente un'applicazione richiede solo un valore di data o di ora. Nelle versioni precedenti viene imposto l'utilizzo di `datetime` o di `smalldatetime` all'applicazione in quanto non sono disponibili tipi di data e ora distinti.  
  
-   Utilizzo di un nuovo tipo per ottenere precisione o accuratezza maggiore nei secondi frazionari.  
  
-   Passaggio a `datetime2` in quanto tipo di dati preferito per la data e l'ora.  
  
 Le applicazioni che usano i metadati del server ottenuto tramite set di righe dello schema o ICommandWithParameters:: GetParameterInfo impostare informazioni sul tipo di parametro tramite ICommandWithParameters:: SetParameterInfo avrà esito negativo durante le conversioni client in cui la stringa rappresentazione di un tipo di origine è maggiore rispetto alla rappresentazione di stringa del tipo di destinazione. Se un'associazione client utilizza DBTYPE_DBTIMESTAMP e la colonna server è data, ad esempio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client convertirà il valore da "aaaa-mm-gg fff", ma i metadati del server verranno restituiti come `nvarchar(10)`. L'overflow risultante restituisce DBSTATUS_E_CATCONVERTVALUE. Problemi simili si verificano con le conversioni di dati da IRowsetChange, perché i metadati di set di righe vengono impostati dai metadati del set di risultati.  
  
### <a name="parameter-and-rowset-metadata"></a>Metadati per parametri e set di righe  
 Questa sezione vengono descritti i metadati per parametri, le colonne di risultati e set di righe dello schema per i client compilati con una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 La struttura DBPARAMINFO restituisce le informazioni seguenti tramite il *prgParamInfo* parametro:  
  
|Tipo di parametro|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|Data|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
 Si noti che alcuni di questi intervalli di valori non sono continui. Nell'intervallo 8,10..16, ad esempio, non è presente il valore 9. Ciò è dovuto all'aggiunta di un separatore decimale quando la precisione frazionaria è maggiore di zero.  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 Vengono restituite le colonne seguenti:  
  
|Tipo di colonna|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|Data|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 La struttura DBCOLUMNINFO restituisce le informazioni seguenti:  
  
|Tipo di parametro|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|Data|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
### <a name="schema-rowsets"></a>Set di righe dello schema  
 In questa sezione vengono descritti i metadati per parametri, colonne dei risultati e set di righe dello schema per i nuovi tipi di dati. Queste informazioni sono utili è è disponibile un provider client sviluppato utilizzando strumenti anteriore [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
#### <a name="columns-rowset"></a>Set di righe COLUMNS  
 Per i tipi di data/ora vengono restituiti i valori di colonna seguenti:  
  
|Tipo di colonna|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|Data|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|NULL|  
  
#### <a name="procedureparameters-rowset"></a>Set di righe PROCEDURE_PARAMETERS  
 Per i tipi di data/ora vengono restituiti i valori di colonna seguenti:  
  
|Tipo di colonna|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|Data|DBTYPE_WSTR|10|20|Data|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|datetime|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|datetimeoffset|  
  
#### <a name="providertypes-rowset"></a>Set di righe PROVIDER_TYPES  
 Per i tipi di data/ora vengono restituite le righe seguenti:  
  
|Tipo -><br /><br /> colonna|Data|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|Data|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|Data|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>Comportamento dei server legacy  
 Quando si è connessi a un server di una versione precedente a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], qualsiasi tentativo di usare i nuovi nomi server (ad esempio, con ICommandWithParameters:: SetParameterInfo o itabledefinition:: CreateTable) comporterà DB_E_BADTYPENAME.  
  
 Se vengono associati nuovi tipi per parametri o risultati senza l'utilizzo di un nome del tipo e il nuovo tipo viene utilizzato per specificare in modo implicito il tipo di server o non è disponibile una conversione valida dal tipo di server al tipo di client, viene restituito DB_E_ERRORSOCCURRED e DBBINDSTATUS_UNSUPPORTED_CONVERSION viene impostato come stato dell'associazione per la funzione di accesso utilizzata in fase di esecuzione.  
  
 Se è disponibile una conversione client supportata dal tipo di buffer al tipo di server per la versione del server nella connessione, è possibile utilizzare tutti i tipi di buffer client. In questo contesto *tipo di server* significa che il tipo specificato dal ICommandWithParameters:: SetParameterInfo, o dal tipo di buffer in cui è inclusa se ICommandWithParameters:: SetParameterInfo non è stato chiamato. Di conseguenza, è possibile utilizzare DBTYPE_DBTIME2 e DBTYPE_DBTIMESTAMPOFFSET con i server legacy o quando DataTypeCompatibility=80, se la conversione client a un tipo di server supportato ha esito positivo. Se il tipo di server non è corretto, potrebbe essere segnalato un errore dal server se questo non è in grado di eseguire una conversione implicita al tipo di server effettivo.  
  
## <a name="sspropinitdatatypecompatibility-behavior"></a>Comportamento di SSPROP_INIT_DATATYPECOMPATIBILITY  
 Quando SSPROP_INIT_DATATYPECOMPATIBILITY è impostato su SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000, i tipi data/ora nuovi e i metadati associati vengono visualizzati ai client così come appaiono per i client legacy, come descritto in [modifiche apportate alla copia Bulk per Enhanced tipi data e ora &#40;OLE DB e ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
## <a name="comparability-for-irowsetfind"></a>Possibilità di confronto per IRowsetFind  
 Per i nuovi tipi di data/ora sono consentiti tutti gli operatori di confronto, in quanto vengono visualizzati come tipi stringa anziché come tipi di data/ora.  
  
## <a name="see-also"></a>Vedere anche  
 [Miglioramenti relativi a data e ora &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
