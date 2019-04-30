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
manager: craigg
ms.openlocfilehash: 2098830a06f8e5c2ddc38b12f0c035ec513433ca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63206301"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
Specifica gli attributi di transazione di un [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|Esegue la conservazione interruzioni chiamando [RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) avviare automaticamente una nuova transazione. Non tutti i provider supportano questo comportamento.|  
|**adXactCommitRetaining**|131072|Esegue il commit conservando la chiamando [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md) avviare automaticamente una nuova transazione. Non tutti i provider supportano questo comportamento.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.XactAttribute.ABORTRETAINING|  
|AdoEnums.XactAttribute.COMMITRETAINING|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà attributi (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
