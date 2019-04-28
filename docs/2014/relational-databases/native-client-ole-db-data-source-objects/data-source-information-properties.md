---
title: Proprietà delle informazioni dell'origine dati | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [SQL Server Native Client]
ms.assetid: 7fd80e47-5bd9-41e2-a3d3-091a7c8c5f2b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 946c6d39bd02bbccd898262da6642813fbb3c94f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62679789"
---
# <a name="data-source-information-properties"></a>Proprietà delle informazioni sulle origini dati
  Nel set di proprietà DBPROPSET_SQLSERVERDATASOURCEINFO specifico del provider il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client definisce le seguenti proprietà delle informazioni sulle origini dati.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|Digitare:  VT_BOOL<br /><br /> L/S: lettura<br /><br /> Impostazione predefinita: VARIANT_TRUE<br /><br /> Descrizione: Utilizzato per determinare se le regole di confronto colonna è supportata.<br /><br /> VARIANT_TRUE: Regole di confronto a livello di colonna è supportata.<br /><br /> VARIANT_FALSE: Regole di confronto a livello di colonna non è supportato.|  
|SSPROP_UNICODELCID|Digitare:  VT_I4 R/W: lettura<br /><br /> Descrizione: ID impostazioni locali di Unicode.<br /><br /> Si tratta delle impostazioni locali utilizzate per l'ordinamento dei dati Unicode.|  
|SSPROP_UNICODECOMPARISONSTYLE|Digitare:  VT_I4 R/W: lettura<br /><br /> Descrizione: Stile di confronto Unicode.<br /><br /> Opzioni di ordinamento utilizzate per l'ordinamento dei dati Unicode.|  
  
 Nel set di proprietà DBPROPSET_SQLSERVERSTREAM specifico del provider il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client definisce le proprietà di sessione aggiuntive indicate di seguito.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|Digitare:  VT_BSTR R/W: Lettura/scrittura<br /><br /> Descrizione: Il risultato di una query FOR XML non può essere un documento in formato corretto. Quando questa proprietà viene specificata, viene eseguito il wrapping del risultato di una query 'select ... for XML' nel tag radice fornito dalla proprietà per restituire un documento XML corretto. Se la query viene eseguita nel browser, è possibile che nel browser stesso vengano visualizzati errori del parser durante il caricamento del risultato. Per evitare l'errore, SQL ISAPI supporta la parola chiave ROOT che viene mappata alla proprietà SSPROP_STREAM_XMLROOT.|  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetti origine dati &#40;OLE DB&#41;](data-source-objects-ole-db.md)  
  
  
