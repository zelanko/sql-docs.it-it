---
title: Proprietà sessione - provider di SQL Server Native Client OLE DB | Documenti di Microsoft
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d17b673a12a915318e523000081fcd6114e8185c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128546"
---
# <a name="session-properties---sql-server-native-client-ole-db-provider"></a>Proprietà sessione - Provider OLE DB di SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client interpreta le proprietà di sessione di OLE DB, come indicato di seguito.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta tutti i livelli di isolamento delle transazioni autocommit ad eccezione del livello chaos DBPROPVAL_TI_CHAOS.|  
  
 Nel provider specifici set di proprietà DBPROPSET_SQLSERVERSESSION il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client definisce le proprietà di sessione aggiuntive seguenti.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Digitare:  VT_BOOL<br /><br /> L/S: lettura/scrittura<br /><br /> Valore predefinito: VARIANT_FALSE<br /><br /> Descrizione: Gli identificatori consentiti nella restrizione CATALOG tra virgolette.<br /><br /> VARIANT_TRUE: Gli identificatori tra virgolette sono riconosciuti per una restrizione per catalogo per i set di righe dello schema che forniscono il supporto di query distribuite.<br /><br /> VARIANT_FALSE: Gli identificatori delimitati non sono riconosciuti per una restrizione per catalogo per i set di righe dello schema che forniscono il supporto di query distribuite.<br /><br /> Per altre informazioni sui set di righe dello schema che offrono il supporto di query distribuite, vedere [Supporto di query distribuite nei set di righe dello schema](../../relational-databases/native-client/ole-db/schema-rowsets-distributed-query-support.md).|  
|SSPROP_ALLOWNATIVEVARIANT|Digitare:  VT_BOOL<br /><br /> L/S: Lettura/scrittura<br /><br /> Valore predefinito: VARIANT_FALSE<br /><br /> Descrizione: Determina se i dati recuperati come DBTYPE_VARIANT o DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: Tipo di colonna viene restituito come DBTYPE_SQLVARIANT nel quale caso il buffer conserva la struttura SSVARIANT.<br /><br /> VARIANT_FALSE: Tipo di colonna viene restituito come DBTYPE_VARIANT e il buffer presenta la struttura VARIANT.|  
|SSPROP_ASYNCH_BULKCOPY|Per utilizzare la modalità asincrona, impostare la proprietà di sessione SSPROP_ASYNCH_BULKCOPY specifica del provider su VARIANT_TRUE prima di chiamare il metodo BCPExec. Questa proprietà è disponibile nel set di proprietà DBPROPSET_SQLSERVERSESSION.|  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetti origine dati &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
