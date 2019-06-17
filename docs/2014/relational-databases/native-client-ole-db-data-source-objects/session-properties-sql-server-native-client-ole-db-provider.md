---
title: Proprietà della sessione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- SQL Server Native Client OLE DB provider, sessions
ms.assetid: 2498fbad-b3db-4bea-8fc6-fef5317d3eba
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 19ce2c6ca7b36a5d2147e7efda657fb2433aef25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63062534"
---
# <a name="session-properties"></a>Proprietà di sessione
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client interpreta le proprietà di sessione di OLE DB, come indicato di seguito.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client supporta tutti i livelli di isolamento delle transazioni autocommit ad eccezione del livello chaos DBPROPVAL_TI_CHAOS.|  
  
 Nel provider specifici set di proprietà DBPROPSET_SQLSERVERSESSION il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider OLE DB Native Client definisce le proprietà di sessione aggiuntive seguenti.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Digitare:  VT_BOOL<br /><br /> L/S: lettura/scrittura<br /><br /> Impostazione predefinita: VARIANT_FALSE<br /><br /> Descrizione: Gli identificatori consentiti nella restrizione CATALOG tra virgolette.<br /><br /> VARIANT_TRUE: Gli identificatori tra virgolette sono riconosciuti per una restrizione per catalogo per i set di righe dello schema che forniscono il supporto di query distribuite.<br /><br /> VARIANT_FALSE: Gli identificatori delimitati non sono riconosciuti per una restrizione per catalogo per i set di righe dello schema che forniscono il supporto di query distribuite.<br /><br /> Per altre informazioni sui set di righe dello schema che offrono il supporto di query distribuite, vedere [Supporto di query distribuite nei set di righe dello schema](../native-client/ole-db/schema-rowsets-distributed-query-support.md).|  
|SSPROP_ALLOWNATIVEVARIANT|Digitare:  VT_BOOL<br /><br /> L/S: Lettura/scrittura<br /><br /> Impostazione predefinita: VARIANT_FALSE<br /><br /> Descrizione: Determina se i dati recuperati come DBTYPE_VARIANT o DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: Tipo di colonna viene restituito come DBTYPE_SQLVARIANT nel quale caso il buffer conserva la struttura SSVARIANT.<br /><br /> VARIANT_FALSE: Tipo di colonna viene restituito come DBTYPE_VARIANT e il buffer presenta la struttura VARIANT.|  
|SSPROP_ASYNCH_BULKCOPY|Per utilizzare la modalità asincrona, impostare la proprietà di sessione SSPROP_ASYNCH_BULKCOPY specifica del provider su VARIANT_TRUE prima di chiamare il metodo BCPExec. Questa proprietà è disponibile nel set di proprietà DBPROPSET_SQLSERVERSESSION.|  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetti origine dati &#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
