---
description: Proprietà StayInSync
title: Proprietà StayInSync | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 9677a776273e83ad31fecde3a7ea436138d3784e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88988622"
---
# <a name="stayinsync-property"></a>Proprietà StayInSync
Indica, in un oggetto [Recordset](./recordset-object-ado.md) gerarchico, se il riferimento ai record figlio sottostanti (ovvero il *capitolo*) cambia quando la posizione della riga padre cambia.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **booleano** . Il valore predefinito è **True**. Se **true**, il capitolo verrà aggiornato se l'oggetto **Recordset** padre modifica la posizione della riga; Se **false**, il capitolo continuerà a fare riferimento ai dati del capitolo precedente anche se per l'oggetto **Recordset** padre è stata modificata la posizione della riga.  
  
## <a name="remarks"></a>Osservazioni  
 Questa proprietà si applica ai recordset gerarchici, ad esempio quelli supportati dal [servizio di data shaping Microsoft per OLE DB](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)e deve essere impostato sul **Recordset** padre prima che venga recuperato il **Recordset** figlio. Questa proprietà semplifica l'esplorazione di recordset gerarchici.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà StayInSync (VB)](./stayinsync-property-example-vb.md)   
 [Servizio Data Shaping Microsoft per OLE DB (provider di servizi ADO)](../../guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md)