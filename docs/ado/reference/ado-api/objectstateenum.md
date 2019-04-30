---
title: ObjectStateEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ObjectStateEnum
helpviewer_keywords:
- ObjectStateEnum enumeration [ADO]
ms.assetid: 32746558-097b-4749-989e-519aadf7e3f4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 560e95bdafe3f5bbae82b200d8f7db0dcb121911
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217720"
---
# <a name="objectstateenum"></a>ObjectStateEnum
Specifica se un oggetto è aperto o chiuso, ci si connette a un'origine dati, l'esecuzione di un comando o il recupero dei dati.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adStateClosed**|0|Indica che l'oggetto è chiuso.|  
|**adStateOpen**|1|Indica che l'oggetto è aperto.|  
|**adStateConnecting**|2|Indica che si connette l'oggetto.|  
|**adStateExecuting**|4|Indica che l'oggetto è in esecuzione un comando.|  
|**adStateFetching**|8|Indica che le righe dell'oggetto vengono recuperate.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.ObjectState.CLOSED|  
|AdoEnums.ObjectState.OPEN|  
|AdoEnums.ObjectState.CONNECTING|  
|AdoEnums.ObjectState.EXECUTING|  
|AdoEnums.ObjectState.FETCHING|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Proprietà State (ADO MD)](../../../ado/reference/ado-md-api/state-property-ado-md.md)|[Proprietà State (ADO)](../../../ado/reference/ado-api/state-property-ado.md)|
