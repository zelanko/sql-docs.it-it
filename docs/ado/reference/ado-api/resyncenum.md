---
title: ResyncEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ResyncEnum
helpviewer_keywords:
- ResyncEnum enumeration [ADO]
ms.assetid: d3df2c90-e570-4c40-a79a-25b3448a009c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4a872ee5f4af49d9fbe97621a5d2549fd9472202
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67931231"
---
# <a name="resyncenum"></a>ResyncEnum
Specifica se i valori sottostanti vengono sovrascritti da una chiamata alla [Risincronizzazione](../../../ado/reference/ado-api/resync-method.md).  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adResyncAllValues**|2|Default. Sovrascrive i dati e gli aggiornamenti in sospeso vengono annullati.|  
|**adResyncUnderlyingValues**|1|Non sovrascrive i dati e gli aggiornamenti in sospeso non vengono annullati.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. Resync. ALLVALUES|  
|AdoEnums. Resync. UNDERLYINGVALUES|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Resync](../../../ado/reference/ado-api/resync-method.md)
