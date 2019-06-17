---
title: Interfaccia ADORecordsetConstruction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordsetConstruction
helpviewer_keywords:
- ADORecordsetConstruction interface [ADO]
ms.assetid: 08386eba-f1f7-4879-8ffd-8733930ecb2f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f08d007395c85ef6b423c7db6c1aed5b39cb27ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718544"
---
# <a name="adorecordsetconstruction-interface"></a>Interfaccia ADORecordsetConstruction
Il **ADORecordsetConstruction** interfaccia viene utilizzata per costruire un oggetto ADO **Recordset** oggetto da OLE DB **set di righe** oggetto in un'applicazione C/C++.  
  
 Questa interfaccia supporta le proprietà seguenti:  
  
## <a name="properties"></a>Proprietà  
  
|||  
|-|-|  
|[Capitolo](../../../ado/reference/ado-api/chapter-property-ado.md)|Lettura/scrittura.<br />Ottiene o imposta un DB OLE **capitolo** oggetto da/in questa ADO **Recordset** oggetto.|  
|[RowPosition](../../../ado/reference/ado-api/rowposition-property-ado.md)|Lettura/scrittura.<br />Ottiene o imposta un DB OLE **RowPosition** oggetto da/in questa ADO **Recordset** oggetto.|  
|[Rowset](../../../ado/reference/ado-api/rowset-property-ado.md)|Lettura/scrittura.<br />Ottiene o imposta un DB OLE **Rowset** oggetto da/in questa ADO **Recordset** oggetto.|  
  
## <a name="methods"></a>Metodi  
 Nessuna.  
  
## <a name="events"></a>Events  
 Nessuna.  
  
## <a name="remarks"></a>Note  
 Dato un OLE DB **Rowset** oggetto (`pRowset`), la costruzione di un oggetto ADO **Recordset** oggetto (`adoRs`) gli importi per le tre operazioni fondamentali seguenti:  
  
1.  Creare un oggetto ADO **Recordset** oggetto:  
  
    ```  
    Recordset20Ptr adoRs;  
    adoRs.CreateInstance(__uuidof(Recordset));  
    ```  
  
2.  Query di **IADORecordsetConstruction** interfaccia le **Recordset** oggetto:  
  
    ```  
    adoRecordsetConstructionPtr adoRsConstruct=NULL;  
    adoRs->QueryInterface(__uuidof(ADORecordsetConstruction),  
                         (void**)&adoRsConstruct);  
    ```  
  
3.  Chiamare il `IADORecordsetConstruction::put_Rowset` metodo di proprietà da impostare OLE DB `Rowset` sull'oggetto ADO `Recordset` oggetto:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRsConstruct->put_Rowset(pUnk);  
    ```  
  
 I risultanti `adoRs` oggetto rappresenta ora ADO **Recordset** oggetto costruito da OLE DB **Rowset** oggetto.  
  
 È inoltre possibile costruire un oggetto ADO **Recordset** oggetto da OLE DB **capitolo** oppure **RowPosition** oggetto.  
  
## <a name="requirements"></a>Requisiti  
 **Versione:** ADO 2.0 e versioni successiva  
  
 **Libreria:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Proprietà Rowset (ADO)](../../../ado/reference/ado-api/rowset-property-ado.md)
