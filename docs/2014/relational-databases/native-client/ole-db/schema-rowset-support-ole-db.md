---
title: Supporto di set di righe dello schema (OLE DB) | Documenti di Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- SQL Server Native Client OLE DB provider, schema rowsets
- rowsets [OLE DB], schema
ms.assetid: a75b4b69-b095-4690-9b31-a2b32a67489e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83b6ea8594d22527f2f9b87a77d70671c5724111
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62625961"
---
# <a name="schema-rowset-support-ole-db"></a>Supporto dei set di righe dello schema (OLE DB)
  Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta inoltre che restituiscono informazioni sullo schema da un server collegato durante l'elaborazione [!INCLUDE[tsql](../../../includes/tsql-md.md)] query distribuite.  
  
> [!NOTE]  
>  Benché [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporti i sinonimi, non vengono restituiti metadati per i sinonimi da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
 Nelle tabelle seguenti sono i rowset dello schema di elenco e le colonne di restrizione supportate dal [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provider OLE DB Native Client.  
  
|Set di righe dello schema|Colonne di restrizione|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMN_PRIVILEGES|Sono supportate tutte le restrizioni.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|DBSCHEMA_COLUMNS|Sono supportate tutte le restrizioni.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME<br /><br /> Le colonne aggiuntive seguenti sono specifiche di  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:<br /><br /> -COLUMN_LCID, che rappresenta l'ID impostazioni locali delle regole di confronto. COLUMN_LCID coincide con il valore dell'LCID di Windows.<br />-COLUMN_COMPFLAGS definisce i confronti supportati per le regole di confronto. Il formato di dati corrisponde a DBPROB_FINDCOMPAREOPS.<br />-COLUMN_SORTID, che rappresenta il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] stile per le regole di confronto di ordinamento.<br />-COLUMN_TDSCOLLATION, che rappresenta il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] regole di confronto per la colonna.<br />-IS_COMPUTED, che è VARIANT_TRUE se la colonna è una colonna calcolata e VARIANT_FALSE in caso contrario.|  
|DBSCHEMA_FOREIGN_KEYS|Sono supportate tutte le restrizioni.<br /><br /> PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|DBSCHEMA_INDEXES|Sono supportate le restrizioni 1, 2, 3 e 5.<br /><br /> TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TABLE_NAME|  
|DBSCHEMA_PRIMARY_KEYS|Sono supportate tutte le restrizioni.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_PROCEDURE_PARAMETERS|Sono supportate tutte le restrizioni.<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|DBSCHEMA_PROCEDURES|Sono supportate le restrizioni 1, 2 e 3.<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME<br /><br /> DBSCHEMA_PROCEDURES restituisce solo le procedure che possono essere eseguite dall'utente corrente o per cui l'utente corrente dispone dell'autorizzazione VIEW DEFINITION.|  
|DBSCHEMA_PROVIDER_TYPES|Sono supportate tutte le restrizioni.<br /><br /> DATA_TYPE BEST_MATCH|  
|DBSCHEMA_SCHEMATA|Sono supportate tutte le restrizioni.<br /><br /> CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|DBSCHEMA_STATISTICS|Sono supportate tutte le restrizioni.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_TABLE_CONSTRAINTS|Sono supportate tutte le restrizioni.<br /><br /> CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|DBSCHEMA_TABLE_PRIVILEGES|Sono supportate tutte le restrizioni.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|DBSCHEMA_TABLES|Sono supportate tutte le restrizioni.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|DBSCHEMA_TABLES_INFO|Sono supportate tutte le restrizioni.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
  
## <a name="in-this-section"></a>In questa sezione  
 [Supporto di query distribuite nei set di righe dello schema](schema-rowsets-distributed-query-support.md)  
  
 [LINKEDSERVERS Rowset &#40;OLE DB&#41;](schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;OLE DB&#41;](sql-server-native-client-ole-db.md)   
 [Uso dei tipi definiti dall'utente](../features/using-user-defined-types.md)  
  
  
