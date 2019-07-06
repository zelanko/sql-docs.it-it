---
title: Proprietà DataSource (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::DataSource
helpviewer_keywords:
- DataSource property [ADO]
ms.assetid: 300a702a-3544-48c5-b759-83b511fe97e0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4c62953f958ef14134d7463c899f5b842d94f596
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597576"
---
# <a name="datasource-property-ado"></a>Proprietà DataSource (ADO)
Indica un oggetto che contiene i dati per essere rappresentato come un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
## <a name="remarks"></a>Note  
 Questa proprietà viene utilizzata per creare controlli associati a dati con l'ambiente dei dati. Gestisce l'ambiente dei dati raccolte di dati (origini dati) che contiene oggetti denominati (membri dati) che verranno rappresentati come una **Recordset** oggetto.  
  
 Il [DataMember](../../../ado/reference/ado-api/datamember-property.md) e **DataSource** proprietà devono essere usate in combinazione.  
  
 L'oggetto di riferimento deve implementare il **IDataSource** l'interfaccia e deve contenere un' **IRowset** interfaccia.  
  
## <a name="usage"></a>Uso  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to.  
Set rs.DataSource = myDE      'Name of the object containing an IRowset.  
```  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà DataMember](../../../ado/reference/ado-api/datamember-property.md)
