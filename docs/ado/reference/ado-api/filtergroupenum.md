---
description: FilterGroupEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f8d3c510cfd9fa6c4a28f78005021465b9b0917b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443663"
---
# <a name="filtergroupenum"></a>FilterGroupEnum
Specifica il gruppo di record da filtrare da un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Costante|Valore|Descrizione|  
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
