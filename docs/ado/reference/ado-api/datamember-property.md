---
title: Proprietà DataMember | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataMember
helpviewer_keywords:
- DataMember property
ms.assetid: 2c8fb09e-10ad-49b5-ab41-2603771780d9
author: rothja
ms.author: jroth
ms.openlocfilehash: 87d525907edde2e3dc99b78eb827c571c604d8b7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763482"
---
# <a name="datamember-property"></a>Proprietà DataMember
Indica il nome del membro dati che verrà recuperato dal [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) a cui fa riferimento la proprietà [DataSource](../../../ado/reference/ado-api/datasource-property-ado.md) .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **stringa** . Per il nome non è prevista distinzione tra maiuscole e minuscole.  
  
## <a name="remarks"></a>Osservazioni  
 Questa proprietà viene utilizzata per creare controlli con associazione a dati con l'ambiente di dati. L'ambiente dati mantiene raccolte di dati (origini dati) che contengono oggetti denominati (membri dati) che verranno rappresentati come un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
 Le proprietà **DataMember** e **DataSource** devono essere utilizzate insieme.  
  
 La proprietà **DataMember** determina quale oggetto specificato dalla proprietà **DataSource** verrà rappresentato come un oggetto **Recordset** . Per impostare questa proprietà, è necessario che l'oggetto **Recordset** sia chiuso. Viene generato un errore se la proprietà **DataMember** non viene impostata prima della proprietà **DataSource** oppure se il nome del **membro** dati non è riconosciuto dall'oggetto specificato nella proprietà **DataSource** .  
  
## <a name="usage"></a>Usage  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà DataSource (ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)
