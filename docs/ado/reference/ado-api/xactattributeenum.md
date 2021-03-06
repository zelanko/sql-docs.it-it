---
description: XactAttributeEnum
title: XactAttributeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: bb2a1391e813fd80c394bd685eff07e06015dd5b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987692"
---
# <a name="xactattributeenum"></a>XactAttributeEnum
Specifica gli attributi di transazione di un oggetto [Connection](./connection-object-ado.md) .  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adXactAbortRetaining**|262144|Esegue le interruzioni di conservazione chiamando [RollbackTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) per avviare automaticamente una nuova transazione. Questo comportamento non è supportato da tutti i provider.|  
|**adXactCommitRetaining**|131072|Esegue i commit di conservazione chiamando [CommitTrans](./begintrans-committrans-and-rollbacktrans-methods-ado.md) per avviare automaticamente una nuova transazione. Questo comportamento non è supportato da tutti i provider.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. XactAttribute. ABORTRETAINING|  
|AdoEnums. XactAttribute. COMMITRETAINING|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà Attributes (ADO)](./attributes-property-ado.md)