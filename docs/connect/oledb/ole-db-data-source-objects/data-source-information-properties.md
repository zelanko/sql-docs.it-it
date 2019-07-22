---
title: Proprietà informazioni origine dati | Microsoft Docs
description: Proprietà delle informazioni sulle origini dati
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, data source properties
- properties [OLE DB]
- data source properties [OLE DB]
- information properties [OLE DB]
- OLE DB data source properties [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ba9fa21f0c22c342922946a43124216a25ba09ef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68016028"
---
# <a name="data-source-information-properties"></a>Proprietà delle informazioni sulle origini dati
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Nel set di proprietà DBPROPSET_SQLSERVERDATASOURCEINFO specifico del provider il driver OLE DB per SQL Server definisce le seguenti proprietà delle informazioni sulle origini dati.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|SSPROP_COLUMNLEVELCOLLATION|Tipo: VT_BOOL<br /><br /> L/S: Lettura<br /><br /> Impostazione predefinita: VARIANT_TRUE<br /><br /> Descrizione: utilizzato per determinare se le regole di confronto a livello di colonna sono supportate.<br /><br /> VARIANT_TRUE: le regole di confronto a livello di colonna sono supportate.<br /><br /> VARIANT_FALSE: le regole di confronto a livello di colonna non sono supportate.|  
|SSPROP_UNICODELCID|Tipo: VT_I4 L/S: Lettura<br /><br /> Descrizione: ID delle impostazioni locali Unicode.<br /><br /> Si tratta delle impostazioni locali utilizzate per l'ordinamento dei dati Unicode.|  
|SSPROP_UNICODECOMPARISONSTYLE|Tipo: VT_I4 L/S: Lettura<br /><br /> Descrizione: stile di confronto Unicode.<br /><br /> Opzioni di ordinamento utilizzate per l'ordinamento dei dati Unicode.|  
  
 Nel set di proprietà DBPROPSET_SQLSERVERSTREAM specifico del provider il driver OLE DB per SQL Server definisce le proprietà aggiuntive indicate di seguito.  
  
|ID proprietà|Descrizione|  
|-----------------|-----------------|  
|SSPROP_STREAM_XMLROOT|Tipo: VT_BSTR L/S: Lettura/Scrittura<br /><br /> Descrizione: il risultato di una query FOR XML potrebbe non essere un documento corretto. Quando questa proprietà viene specificata, viene eseguito il wrapping del risultato di una query 'select ... for XML' nel tag radice fornito dalla proprietà per restituire un documento XML corretto. Se la query viene eseguita nel browser, è possibile che nel browser stesso vengano visualizzati errori del parser durante il caricamento del risultato. Per evitare l'errore, SQL ISAPI supporta la parola chiave ROOT che viene mappata alla proprietà SSPROP_STREAM_XMLROOT.|  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetti &#40;origine dati OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
