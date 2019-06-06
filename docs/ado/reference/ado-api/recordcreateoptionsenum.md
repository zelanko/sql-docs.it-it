---
title: RecordCreateOptionsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordCreateOptionsEnum
helpviewer_keywords:
- RecordCreateOptionsEnum enumeration [ADO]
ms.assetid: 6d746670-0850-4065-9cd4-168dea1d3ea9
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d57f1bc241e5e27618a9598895ea7be089ce20dd
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66712020"
---
# <a name="recordcreateoptionsenum"></a>RecordCreateOptionsEnum
Specifica se un oggetto esistente **Record** deve essere aperto o una nuova **Record** creato per il [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetto [Open](../../../ado/reference/ado-api/open-method-ado-record.md) (metodo). I valori possono essere combinati con l'operatore AND.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adCreateCollection**|0x2000|Crea un nuovo **Record** in corrispondenza del nodo specificato da *origine* parametro, invece di aprire un oggetto esistente **Record**. Se l'origine fa riferimento a un nodo esistente, si verifica un errore di run-time, a meno che **adCreateCollection** viene combinato con **adOpenIfExists** oppure **adCreateOverwrite**.|  
|**adCreateNonCollection**|0|Crea un nuovo **Record** typu [adSimpleRecord](../../../ado/reference/ado-api/recordtypeenum.md).|  
|**adCreateOverwrite**|0x4000000|Modifica il flag di creazione **adCreateCollection**, **adCreateNonCollection**, e **adCreateStructDoc**. Quando o viene usato con questo valore e uno dei valori dei flag di creazione, se l'URL di origine fa riferimento a un nodo esistente o **Record**, quindi esistenti **Record** viene sovrascritto e un nuovo ne viene creata al suo posto. Questo valore non può essere utilizzato assieme **adOpenIfExists**.|  
|**adCreateStructDoc**|0x80000000|Crea un nuovo **Record** typu [adStructDoc oggetto](../../../ado/reference/ado-api/recordtypeenum.md), invece di aprire un oggetto esistente **Record**.|  
|**adFailIfNotExists**|-1|Valore predefinito. Determina se un errore di run-time *origine* punta a un nodo inesistente.|  
|**adOpenIfExists**|0x2000000|Modifica il flag di creazione **adCreateCollection**, **adCreateNonCollection**, e **adCreateStructDoc**. Quando o viene usato con questo valore e uno dei valori dei flag di creazione, se l'URL di origine fa riferimento a un nodo esistente o **Record** dell'oggetto, quindi il provider deve aprire esistenti **Record** anziché creare un nuovo uno. Questo valore non può essere utilizzato assieme **adCreateOverwrite**.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Queste costanti non dispongono di equivalenti di ADO o WFC.  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Open (record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)
