---
title: Proprietà StayInSync | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::StayInSync
- Recordset20::put_StayInSync
- Recordset20::PutStayInSync
- Recordset20::get_StayInSync
- Recordset20::GetStayInSync
helpviewer_keywords:
- StayInSync property
ms.assetid: 502d69b5-dc9a-455d-b115-a03bd39a552b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50cf569f6e0af5e753cca7fba030b8fc2caa4a86
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743127"
---
# <a name="stayinsync-property"></a>Proprietà StayInSync
Indica, in un modello gerarchico [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto, se il riferimento a record figlio sottostanti (vale a dire, il *capitolo*) le modifiche quando la riga padre di posizionare le modifiche.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **booleana** valore. Il valore predefinito è **True**. Se **True**, il capitolo verrà aggiornato se l'elemento padre **Recordset** posizione; della riga delle modifiche degli oggetti se **False**, il capitolo continueranno a fare riferimento ai dati nel capitolo precedente anche se l'elemento padre **Recordset** oggetto ha cambiato posizione della riga.  
  
## <a name="remarks"></a>Note  
 Questa proprietà si applica a recordset gerarchici, ad esempio quelli supportati per il [Microsoft Data shaping per OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)e deve essere impostato sull'oggetto padre **Recordset** prima l'elemento figlio  **Recordset** viene recuperato. Questa proprietà consente di semplificare lo spostamento di recordset gerarchici.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà StayInSync (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [Microsoft Data Shaping Service per OLE DB (ADO Service Provider)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
