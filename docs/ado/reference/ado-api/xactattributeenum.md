---
title: XactAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- XactAttributeEnum
helpviewer_keywords:
- XactAttributeEnum enumeration [ADO]
ms.assetid: e7dcecd3-7dc7-445c-b922-f700c3067fbc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d828c2b9b49138cc4dfd6345d90e70c333554fe0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67947438"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
Specifica gli attributi di transazione di un oggetto [Connection](../../../ado/reference/ado-api/connection-object-ado.md) .  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|Esegue le interruzioni di conservazione chiamando [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) per avviare automaticamente una nuova transazione. Questo comportamento non è supportato da tutti i provider.|  
|**adXactCommitRetaining**|131072|Esegue i commit di conservazione chiamando [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) per avviare automaticamente una nuova transazione. Questo comportamento non è supportato da tutti i provider.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. XactAttribute. ABORTRETAINING|  
|AdoEnums. XactAttribute. COMMITRETAINING|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
