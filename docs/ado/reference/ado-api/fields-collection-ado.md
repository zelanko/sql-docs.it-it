---
title: I campi Collection (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords:
- Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 8483a908e31b9e4554c5594ecc5bbf186bbef88f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695039"
---
# <a name="fields-collection-ado"></a>Raccolta Fields (ADO)
Contiene tutti i [campo](../../../ado/reference/ado-api/field-object.md) gli oggetti di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oppure [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetto.  
  
## <a name="remarks"></a>Note  
 Oggetto **Recordset** oggetto dispone di un **campi** raccolta costituita da **campo** oggetti. Ciascuna **campo** corrisponde a una colonna in oggetto il **Recordset**. È possibile popolare la **campi** raccolta prima di aprire le **Recordset** chiamando il [Aggiorna](../../../ado/reference/ado-api/refresh-method-ado.md) metodo per la raccolta.  
  
> [!NOTE]
>  Vedere le **campo** argomento di oggetto per una spiegazione più dettagliata di come usare **campo** oggetti.  
  
 Il **i campi** raccolta ha un [Append](../../../ado/reference/ado-api/append-method-ado.md) metodo, che crea e aggiunge temporaneamente una **campo** oggetto alla raccolta e un **aggiornare**metodo, che consente di finalizzare qualsiasi aggiunta o eliminazione.  
  
 Oggetto **Record** oggetto dispone di due campi speciali che possono essere indicizzati con [FieldEnum](../../../ado/reference/ado-api/fieldenum.md) costanti. Una costante di accede a un campo che contiene il flusso predefinito per il **Record**, e l'altro accede a un campo che contiene la stringa URL assoluta per il **Record**.  
  
 Alcuni provider (ad esempio, il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) possono popolare il **campi** insieme con un subset dei campi disponibili per il **Record** oppure **Recordset**. Gli altri campi non essere aggiunti alla raccolta fino a quando non vengono prima di tutto fatto riferimento in base al nome o indicizzati dal codice.  
  
 Se si tenta di fare riferimento a un campo inesistente in base al nome, una nuova **campo** verrà aggiunto all'oggetto il **campi** insieme con un [stato](../../../ado/reference/ado-api/status-property-ado-field.md) di  **adFieldPendingInsert**. Quando si chiama [Update](../../../ado/reference/ado-api/update-method.md), ADO creerà un nuovo campo nell'origine dati se consentito dal provider.  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Le proprietà della raccolta campi, metodi ed eventi](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)
