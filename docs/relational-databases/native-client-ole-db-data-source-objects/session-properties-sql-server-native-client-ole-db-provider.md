---
description: Proprietà sessione - Provider OLE DB di SQL Server Native Client
title: Proprietà della sessione OLE DB
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7e06e5ff01bdc3928c63982749081903347dcb22
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455761"
---
# <a name="session-properties---sql-server-native-client-ole-db-provider"></a>Proprietà sessione - Provider OLE DB di SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client interpreta OLE DB proprietà della sessione come indicato di seguito.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client supporta tutti i livelli di isolamento delle transazioni con autocommit, ad eccezione del livello chaos DBPROPVAL_TI_CHAOS.|  
|||

 Nel set di proprietà specifico del provider DBPROPSET_SQLSERVERSESSION il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB di Native Client definisce la seguente proprietà di sessione aggiuntiva.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Digitare: VT_BOOL<br /><br /> R/W (L/S): Lettura/Scrittura<br /><br /> Predefinito: VARIANT_FALSE<br /><br /> Descrizione: gli identificatori tra virgolette consentiti nella restrizione CATALOG.<br /><br /> VARIANT_TRUE: gli identificatori tra virgolette sono riconosciuti per una restrizione per catalogo per i set di righe dello schema che forniscono il supporto query distribuito.<br /><br /> VARIANT_FALSE: gli identificatori tra virgolette non sono riconosciuti per una restrizione per catalogo per i set di righe dello schema che forniscono il supporto di query distribuite.<br /><br /> Per altre informazioni sui set di righe dello schema che offrono il supporto di query distribuite, vedere [Supporto di query distribuite nei set di righe dello schema](../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md).|  
|SSPROP_ALLOWNATIVEVARIANT|Digitare: VT_BOOL<br /><br /> R/W (L/S): Lettura/Scrittura<br /><br /> Predefinito: VARIANT_FALSE<br /><br /> Descrizione: determina se i dati recuperati appartengono alla categoria DBTYPE_VARIANT o DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: il tipo di colonna viene restituito come DBTYPE_SQLVARIANT e in tal caso il buffer conserva la struttura SSVARIANT.<br /><br /> VARIANT_FALSE: il tipo di colonna viene restituito come DBTYPE_VARIANT e il buffer presenta la struttura VARIANT.|  
|SSPROP_ASYNCH_BULKCOPY|Per utilizzare la modalità asincrona, impostare la proprietà di sessione SSPROP_ASYNCH_BULKCOPY specifica del provider su VARIANT_TRUE prima di chiamare il metodo BCPExec. Questa proprietà è disponibile nel set di proprietà DBPROPSET_SQLSERVERSESSION.|  
|||

## <a name="see-also"></a>Vedere anche  
 [Oggetti di origine dati &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
