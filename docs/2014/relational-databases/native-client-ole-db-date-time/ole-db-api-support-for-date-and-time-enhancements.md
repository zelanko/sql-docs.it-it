---
title: Supporto dell'API OLE DB per i miglioramenti relativi a data e ora | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, date/time improvements
ms.assetid: e65c9253-bd99-4dc3-9cb8-7613f754c966
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef6334f6fe4671f2563add857f6dd58ce67a2840
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63237840"
---
# <a name="ole-db-api-support-for-date-and-time-enhancements"></a>Supporto dell'API OLE DB per i miglioramenti relativi a data e ora
  Le caratteristiche avanzate di data e ora sono supportate dalle seguenti API OLE DB.  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|IAccessor::CreateAccessor|Un flag viene aggiunto nella struttura DBBINDING per consentire alle applicazioni di distinguere tra i valori `datetime`, `datetime2` e `smalldatetime`. Per ulteriori informazioni, vedere [parametri e metadati del set di righe](metadata-parameter-and-rowset.md).|  
|IBCPSession::BCPColFmt|Per ulteriori informazioni, vedere la pagina relativa alle [modifiche di copia bulk per i tipi di data e ora avanzati &#40;OLE DB e&#41;ODBC ](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).|  
|ICommandWithParameters::GetParameterInfo|Per ulteriori informazioni, vedere[parametri e metadati del set di righe](metadata-parameter-and-rowset.md).|  
|ICommandWithParameters::SetParameterinfo|Per ulteriori informazioni, vedere[parametri e metadati del set di righe](metadata-parameter-and-rowset.md).|  
|IColumnsRowset::GetColumnsRowset|Per ulteriori informazioni, vedere[parametri e metadati del set di righe](metadata-parameter-and-rowset.md).|  
|IColumnsInfo::GetColumnInfo|Per ulteriori informazioni, vedere[parametri e metadati del set di righe](metadata-parameter-and-rowset.md).|  
|IDBSchemaRowset::GetRowset|Per informazioni dettagliate sui set di righe dello schema interessati, vedere[data e ora e set di righe dello schema](../native-client-ole-db-rowsets/rowsets.md).|  
|IRowsetFastLoad|Questa interfaccia supporta i nuovi tipi di data/ora, ma non è stata apportata alcuna modifica all'interfaccia.|  
|ITableDefinition::CreateTable|Per ulteriori informazioni, vedere [supporto dei tipi di dati per OLE DB miglioramenti di data e ora](data-type-support-for-ole-db-date-and-time-improvements.md).|  
  
## <a name="see-also"></a>Vedere anche  
 [Miglioramenti di data e ora &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
