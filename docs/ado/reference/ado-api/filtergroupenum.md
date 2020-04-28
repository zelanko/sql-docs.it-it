---
title: FilterGroupEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FilterGroupEnum
helpviewer_keywords:
- FilterGroupEnum enumeration [ADO]
ms.assetid: b22e725e-84bd-4286-a070-290c278c3783
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 97add08a1d656e8c163600bb0ea8dda7fca264b5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932649"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
Specifica il gruppo di record da filtrare da un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adFilterAffectedRecords**|2|Filtri per la visualizzazione dei soli record interessati dall'ultima chiamata a [Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md), [Resync](../../../ado/reference/ado-api/resync-method.md), [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)o [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) .|  
|**adFilterConflictingRecords**|5|Filtri per la visualizzazione dei record che non hanno superato l'ultimo aggiornamento batch.|  
|**adFilterFetchedRecords**|3|Filtri per la visualizzazione dei record nella cache corrente, ovvero i risultati dell'ultima chiamata per recuperare record dal database.|  
|**adFilterNone**|0|Rimuove il filtro corrente e ripristina tutti i record per la visualizzazione.|  
|**adFilterPendingRecords**|1|Filtri per la visualizzazione dei soli record che sono stati modificati ma che non sono ancora stati inviati al server. Applicabile solo per la modalità di aggiornamento batch.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. FilterGroup. AFFECTEDRECORDS|  
|AdoEnums. FilterGroup. CONFLICTINGRECORDS|  
|AdoEnums. FilterGroup. FETCHEDRECORDS|  
|AdoEnums. FilterGroup. NONE|  
|AdoEnums. FilterGroup. PENDINGRECORDS|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà Filter](../../../ado/reference/ado-api/filter-property.md)
