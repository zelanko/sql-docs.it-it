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
author: rothja
ms.author: jroth
ms.openlocfilehash: f36eace18280cd810341c5eeeec1fb294999e6ec
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759637"
---
# <a name="stayinsync-property"></a>Proprietà StayInSync
Indica, in un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) gerarchico, se il riferimento ai record figlio sottostanti (ovvero il *capitolo*) cambia quando la posizione della riga padre cambia.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **booleano** . Il valore predefinito è **True**. Se **true**, il capitolo verrà aggiornato se l'oggetto **Recordset** padre modifica la posizione della riga; Se **false**, il capitolo continuerà a fare riferimento ai dati del capitolo precedente anche se per l'oggetto **Recordset** padre è stata modificata la posizione della riga.  
  
## <a name="remarks"></a>Commenti  
 Questa proprietà si applica ai recordset gerarchici, ad esempio quelli supportati dal [servizio di data shaping Microsoft per OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)e deve essere impostato sul **Recordset** padre prima che venga recuperato il **Recordset** figlio. Questa proprietà semplifica l'esplorazione di recordset gerarchici.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà StayInSync (VB)](../../../ado/reference/ado-api/stayinsync-property-example-vb.md)   
 [Servizio Data Shaping Microsoft per OLE DB (provider di servizi ADO)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)
