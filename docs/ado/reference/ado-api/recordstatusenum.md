---
title: RecordStatusEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordStatusEnum
helpviewer_keywords:
- RecordStatusEnum enumeration [ADO]
ms.assetid: 506fdd70-4452-4e83-95d5-c94311988dfa
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7c57878b73c3c6a20f8dc0a8abd422c12a0446a2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711729"
---
# <a name="recordstatusenum"></a>RecordStatusEnum
Specifica la [stato](../../../ado/reference/ado-api/status-property-ado-recordset.md) di un record per quanto riguarda gli aggiornamenti in batch e altre operazioni bulk.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adRecCanceled**|0x100|Indica che il record non è stato salvato perché è stata annullata l'operazione.|  
|**adRecCantRelease**|0x400|Indica che il nuovo record non è stato salvato il record esistente è stato bloccato.|  
|**adRecConcurrencyViolation**|0x800|Indica che il record non è stato salvato perché la concorrenza ottimistica era in uso.|  
|**adRecDBDeleted**|0x40000|Indica che il record è già stato eliminato dall'origine dati.|  
|**adRecDeleted**|0x4|Indica che il record sia stato eliminato.|  
|**adRecIntegrityViolation**|0x1000|Indica che il record non è stato salvato in quanto l'utente ha violato i vincoli di integrità.|  
|**adRecInvalid**|0x10|Indica che il record non è stato salvato in quanto il segnalibro non è valido.|  
|**adRecMaxChangesExceeded**|0x2000|Indica che il record non è stato salvato perché si sono verificati troppi le modifiche in sospeso.|  
|**adRecModified**|0x2|Indica che il record è stato modificato.|  
|**adRecMultipleChanges**|0x40|Indica che il record non è stato salvato perché potrebbe influire su più record.|  
|**adRecNew**|0x1|Indica che il record è nuovo.|  
|**adRecObjectOpen**|0x4000|Indica che il record non è stato salvato a causa di un conflitto con un oggetto di archiviazione aperto.|  
|**adRecOK**|0|Indica che il record è stato aggiornato correttamente.|  
|**adRecOutOfMemory**|0x8000|Indica che il record non è stato salvato in quanto il computer ha esaurito la memoria.|  
|**adRecPendingChanges**|0x80|Indica che il record non è stato salvato perché fa riferimento a un inserimento in sospeso.|  
|**adRecPermissionDenied**|0x10000|Indica che il record non è stato salvato poiché l'utente ha autorizzazioni sufficienti.|  
|**adRecSchemaViolation**|0x20000|Indica che il record non è stato salvato perché viola la struttura del database sottostante.|  
|**adRecUnmodified**|0x8|Indica che il record non è stato modificato.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 AdoEnums.RecordStatus.  
  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.RecordStatus.CANCELED|  
|AdoEnums.RecordStatus.CANTRELEASE|  
|AdoEnums.RecordStatus.CONCURRENCYVIOLATION|  
|AdoEnums.RecordStatus.DBDELETED|  
|AdoEnums.RecordStatus.DELETED|  
|AdoEnums.RecordStatus.INTEGRITYVIOLATION|  
|AdoEnums.RecordStatus.INVALID|  
|AdoEnums.RecordStatus.MAXCHANGESEXCEEDED|  
|AdoEnums.RecordStatus.MODIFIED|  
|AdoEnums.RecordStatus.MULTIPLECHANGES|  
|AdoEnums.RecordStatus.NEW|  
|AdoEnums.RecordStatus.OBJECTOPEN|  
|AdoEnums.RecordStatus.OK|  
|AdoEnums.RecordStatus.OUTOFMEMORY|  
|AdoEnums.RecordStatus.PENDINGCHANGES|  
|AdoEnums.RecordStatus.PERMISSIONDENIED|  
|AdoEnums.RecordStatus.SCHEMAVIOLATION|  
|AdoEnums.RecordStatus.UNMODIFIED|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà Status (Recordset ADO)](../../../ado/reference/ado-api/status-property-ado-recordset.md)
