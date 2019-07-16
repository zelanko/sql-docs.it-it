---
title: SchemaEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SchemaEnum
helpviewer_keywords:
- SchemaEnum enumeration [ADO]
ms.assetid: 21c97651-297f-469f-b5b5-c48af72b62a8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c064120e3c658cafd88a96953ff00e18fbaa9b88
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931114"
---
# <a name="schemaenum"></a>SchemaEnum
Specifica il tipo di schema **Recordset** che il [OpenSchema](../../../ado/reference/ado-api/openschema-method.md) recuperata dal metodo.  
  
## <a name="remarks"></a>Note  
 Informazioni aggiuntive relative alla funzione e le colonne restituite per ogni costante ADO è disponibili negli argomenti di [appendice b: I set di righe dello schema](https://msdn.microsoft.com/2b5fbf03-e50d-44ee-bc57-5a57666c55f1) di riferimento per programmatori OLE DB. Il nome di ogni argomento è elencato tra parentesi nella sezione Descrizione della tabella seguente.  
  
 Informazioni aggiuntive relative alla funzione e le colonne restituite per ogni costante di ADO MD è disponibili negli argomenti di [OLE DB per gli oggetti OLAP e i set di righe dello Schema](https://msdn.microsoft.com/d20bb2a6-68bd-423f-9ec8-eb930cd0c144) in OLE DB per la documentazione Online Analytical Processing (OLAP). Il nome di ogni argomento è elencato tra parentesi nella colonna Descrizione della tabella seguente.  
  
 È possibile convertire i tipi di dati delle colonne nella documentazione di OLE DB ai tipi di dati ADO facendo riferimento alla colonna Descrizione della ADO [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) argomento. Ad esempio, un tipo di dati OLE DB di **DBTYPE_WSTR** equivale a un tipo di dati ADO **adWChar**.  
  
 ADO genera risultati dello schema per le costanti **adSchemaDBInfoKeywords** e **adSchemaDBInfoLiterals**. ADO crea una **Recordset**e quindi ogni riga viene riempita con i valori restituiti rispettivamente dalle **IDBInfo:: GetKeywords** e **IDBInfo::** metodi. Informazioni aggiuntive su questi metodi sono reperibili nel [IDBInfo](https://msdn.microsoft.com/3f5ad97f-3fc6-4f21-b691-f6911e4007f3) sezione di riferimento delle per programmatori OLE DB.  
  
|Costante|Value|Descrizione|Colonne del vincolo|  
|--------------|-----------|-----------------|------------------------|  
|**adSchemaAsserts**|0|Restituisce le asserzioni definite nel catalogo appartenenti a un determinato utente.<br /><br /> ASSERZIONI (set di righe)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCatalogs**|1|Restituisce gli attributi fisici associati a cataloghi accessibili dal sistema DBMS.<br /><br /> (Set di righe cataloghi)|CATALOG_NAME|  
|**adSchemaCharacterSets**|2|Restituisce i set di caratteri definiti nel catalogo accessibili a un determinato utente.<br /><br /> (Rowset CHARACTER_SETS)|CHARACTER_SET_CATALOG CHARACTER_SET_SCHEMA CHARACTER_SET_NAME|  
|**adSchemaCheckConstraints**|5|Restituisce i vincoli check definiti nel catalogo appartenenti a un determinato utente.<br /><br /> (CHECK_CONSTRAINTS) Set di righe)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaCollations**|3|Restituisce i carattere regole di confronto definite nel catalogo accessibile a un determinato utente.<br /><br /> Le regole di confronto (set di righe)|COLLATION_CATALOG COLLATION_SCHEMA COLLATION_NAME|  
|**adSchemaColumnPrivileges**|13|Restituisce i privilegi sulle colonne di tabelle definiti nel catalogo, disponibili o concessi da un determinato utente.<br /><br /> (Set di righe COLUMN_PRIVILEGES)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|**adSchemaColumns**|4|Restituisce le colonne di tabelle, comprese le visualizzazioni, definite nel catalogo accessibili a un determinato utente.<br /><br /> (Set di righe COLUMNS)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaColumnsDomainUsage**|11|Restituisce le colonne definite nel catalogo che dipendono da un dominio definite nel catalogo e appartenenti a un determinato utente.<br /><br /> (Set di righe COLUMN_DOMAIN_USAGE)|DOMAIN_CATALOG DOMAIN_SCHEMA NOME_DOMINIO COLUMN_NAME|  
|**adSchemaConstraintColumnUsage**|6|Restituisce le colonne utilizzate da vincoli referenziali, vincoli unique, vincoli check e asserzioni, definite nel catalogo e appartenenti a un determinato utente.<br /><br /> (Set di righe CONSTRAINT_COLUMN_USAGE)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaConstraintTableUsage**|7|Restituisce le tabelle utilizzate da vincoli referenziali, vincoli unique, vincoli check e le asserzioni definite nel catalogo e appartenenti a un determinato utente.<br /><br /> (CONSTRAINT_TABLE_USAGE Rowset)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaCubes**|32|Restituisce informazioni sui cubi disponibili in uno schema (o il catalogo, se il provider non supporta gli schemi).<br /><br /> (Set di righe di CUBI *)|CATALOG_NAME SCHEMA_NAME CUBE_NAME|  
|**adSchemaDBInfoKeywords**|30|Restituisce un elenco di parole chiave specifiche del provider.<br /><br /> (IDBInfo:: GetKeywords)|\<Nessuno >|  
|**adSchemaDBInfoLiterals**|31|Restituisce un elenco di valori letterali specifici del provider usato nei comandi di testo.<br /><br /> (IDBInfo::GetLiteralInfo)|\<Nessuno >|  
|**adSchemaDimensions**|33|Restituisce informazioni sulle dimensioni nel cubo specificato. Include una riga per ogni dimensione.<br /><br /> (Set di righe di dimensioni)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_NAME DIMENSION_UNIQUE_NAME|  
|**adSchemaForeignKeys**|27|Restituisce le colonne chiave esterne definite nel catalogo da un determinato utente.<br /><br /> (Nel set di righe)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|**adSchemaHierarchies**|34|Restituisce informazioni sulle gerarchie disponibili in una dimensione.<br /><br /> GERARCHIE (set di righe)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_NAME HIERARCHY_UNIQUE_NAME|  
|**adSchemaIndexes**|12|Restituisce gli indici definiti nel catalogo appartenenti a un determinato utente.<br /><br /> (Set di righe INDEXES)|TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TIPO TABLE_NAME|  
|**adSchemaKeyColumnUsage**|8|Restituisce le colonne definite nel catalogo che sono vincolate come chiavi di un determinato utente.<br /><br /> (Set di righe KEY_COLUMN_USAGE)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME|  
|**adSchemaLevels**|35|Restituisce informazioni sui livelli di una dimensione.<br /><br /> (Set di righe livelli)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_NAME LEVEL_UNIQUE_NAME|  
|**adSchemaMeasures**|36|Restituisce informazioni sulle misure disponibili.<br /><br /> MISURE (set di righe)|CATALOG_NAME SCHEMA_NAME CUBE_NAME MEASURE_NAME MEASURE_UNIQUE_NAME|  
|**adSchemaMembers**|38|Restituisce informazioni sui membri disponibili.<br /><br /> I membri (set di righe)|Operatore CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME LEVEL_NUMBER MEMBER_NAME MEMBER_UNIQUE_NAME MEMBER_CAPTION MEMBER_TYPE albero. Per altre informazioni, vedere OLE DB per Online Analytical Processing (OLAP).|  
|**adSchemaPrimaryKeys**|28|Restituisce le colonne chiave primarie definite nel catalogo da un determinato utente.<br /><br /> (Set di righe PRIMARY_KEYS)|PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME|  
|**adSchemaProcedureColumns**|29|Restituisce informazioni sulle colonne di set di righe restituite da procedure.<br /><br /> (Set di righe PROCEDURE_COLUMNS)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME COLUMN_NAME|  
|**adSchemaProcedureParameters**|26|Restituisce informazioni sui parametri e i codici restituiti da procedure.<br /><br /> (Set di righe PROCEDURE_PARAMETERS)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|**adSchemaProcedures**|16|Restituisce le procedure definite nel catalogo appartenenti a un determinato utente.<br /><br /> (Set di righe procedure)|PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PROCEDURE_TYPE|  
|**adSchemaProperties**|37|Restituisce informazioni sulle proprietà disponibili per ogni livello della dimensione.<br /><br /> (Proprietà set di righe)|CATALOG_NAME SCHEMA_NAME CUBE_NAME DIMENSION_UNIQUE_NAME HIERARCHY_UNIQUE_NAME LEVEL_UNIQUE_NAME MEMBER_UNIQUE_NAME PROPERTY_TYPE PROPERTY_NAME|  
|**adSchemaProviderSpecific**|-1|Utilizzato se il provider definisce la propria query dello schema non standard.|\<Specifico del provider >|  
|**adSchemaProviderTypes**|22|Restituisce i tipi di dati (base) supportati dal provider di dati.<br /><br /> (Set di righe PROVIDER_TYPES)|DATA_TYPE BEST_MATCH|  
|**AdSchemaReferentialConstraints**|9|Restituisce i vincoli referenziali definiti nel catalogo appartenenti a un determinato utente.<br /><br /> REFERENTIAL_CONSTRAINTS (set di righe)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME|  
|**adSchemaSchemata**|17|Restituisce gli schemi (oggetti di database) che appartengono a un determinato utente.<br /><br /> (Set di righe degli schemi)|CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|**adSchemaSQLLanguages**|18|Restituisce i livelli di conformità, le opzioni e i sottolinguaggi supportati dall'implementazione SQL con l'elaborazione dati definiti nel catalogo.<br /><br /> (Set di righe SQL_LANGUAGES)|\<Nessuno >|  
|**adSchemaStatistics**|19|Restituisce le statistiche definite nel catalogo appartenenti a un determinato utente.<br /><br /> (Set di righe delle statistiche)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaTableConstraints**|10|Restituisce i vincoli di tabella definiti nel catalogo appartenenti a un determinato utente.<br /><br /> (Set di righe TABLE_CONSTRAINTS)|CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|**adSchemaTablePrivileges**|14|Restituisce i privilegi sulle tabelle definiti nel catalogo, disponibili o concessi da un determinato utente.<br /><br /> (Set di righe TABLE_PRIVILEGES)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|**adSchemaTables**|20|Restituisce le tabelle (comprese le visualizzazioni) definite nel catalogo accessibili a un determinato utente.<br /><br /> (Set di righe di tabelle)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|**adSchemaTranslations**|21|Restituisce le conversioni dei caratteri definite nel catalogo accessibili a un determinato utente.<br /><br /> TRADUZIONI (set di righe)|TRANSLATION_CATALOG TRANSLATION_SCHEMA TRANSLATION_NAME|  
|**adSchemaTrustees**|39|Riservato per utilizzi futuri.||  
|**adSchemaUsagePrivileges**|15|Restituisce i privilegi USAGE sugli oggetti definiti nel catalogo che sono disponibili o concessi da un determinato utente.<br /><br /> (Set di righe USAGE_PRIVILEGES)|ALL'UTENTE AUTORIZZATO GRANTOR OBJECT_TYPE OBJECT_CATALOG OBJECT_SCHEMA OBJECT_NAME|  
|**adSchemaViewColumnUsage**|24|Restituisce le colonne in cui le tabelle visualizzate, definite nel catalogo e appartenenti a un determinato utente, sono dipendenti.<br /><br /> (Set di righe VIEW_COLUMN_USAGE)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
|**adSchemaViews**|23|Restituisce le viste definite nel catalogo accessibile a un determinato utente.<br /><br /> VISTE (set di righe)|TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|**adSchemaViewTableUsage**|25|Restituisce le tabelle in cui le tabelle visualizzate, definite nel catalogo e appartenenti a un determinato utente, sono dipendenti.<br /><br /> (Set di righe VIEW_TABLE_USAGE)|VIEW_CATALOG VIEW_SCHEMA VIEW_NAME|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.Schema.ASSERTS|  
|AdoEnums.Schema.CATALOGS|  
|AdoEnums.Schema.CHARACTERSETS|  
|AdoEnums.Schema.CHECKCONSTRAINTS|  
|AdoEnums.Schema.COLLATIONS|  
|AdoEnums.Schema.COLUMNPRIVILEGES|  
|AdoEnums.Schema.COLUMNS|  
|AdoEnums.Schema.COLUMNSDOMAINUSAGE|  
|AdoEnums.Schema.CONSTRAINTCOLUMNUSAGE|  
|AdoEnums.Schema.CONSTRAINTTABLEUSAGE|  
|AdoEnums.Schema.CUBES|  
|AdoEnums.Schema.DBINFOKEYWORDS|  
|AdoEnums.Schema.DBINFOLITERALS|  
|AdoEnums.Schema.DIMENSIONS|  
|AdoEnums.Schema.FOREIGNKEYS|  
|AdoEnums.Schema.HIERARCHIES|  
|AdoEnums.Schema.INDEXES|  
|AdoEnums.Schema.KEYCOLUMNUSAGE|  
|AdoEnums.Schema.LEVELS|  
|AdoEnums.Schema.MEASURES|  
|AdoEnums.Schema.MEMBERS|  
|AdoEnums.Schema.PRIMARYKEYS|  
|AdoEnums.Schema.PROCEDURECOLUMNS|  
|AdoEnums.Schema.PROCEDUREPARAMETERS|  
|AdoEnums.Schema.PROCEDURES|  
|AdoEnums.Schema.PROPERTIES|  
|AdoEnums.Schema.PROVIDERSPECIFIC|  
|AdoEnums.Schema.PROVIDERTYPES|  
|AdoEnums.Schema.REFERENTIALCONTRAINTS|  
|AdoEnums.Schema.SCHEMATA|  
|AdoEnums.Schema.SQLLANGUAGES|  
|AdoEnums.Schema.STATISTICS|  
|AdoEnums.Schema.TABLECONSTRAINTS|  
|AdoEnums.Schema.TABLEPRIVILEGES|  
|AdoEnums.Schema.TABLES|  
|AdoEnums.Schema.TRANSLATIONS|  
|AdoEnums.Schema.TRUSTEES|  
|AdoEnums.Schema.USAGEPRIVILEGES|  
|AdoEnums.Schema.VIEWCOLUMNUSAGE|  
|AdoEnums.Schema.VIEWS|  
|AdoEnums.Schema.VIEWTABLEUSAGE|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo OpenSchema](../../../ado/reference/ado-api/openschema-method.md)
