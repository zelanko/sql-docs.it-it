---
title: Interfaccia ADOStreamConstruction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADOStreamConstruction
helpviewer_keywords:
- ADOStreamConstruction interface [ADO]
ms.assetid: 92f5a939-3e1a-4b14-a9dd-90e6ce2dec74
author: rothja
ms.author: jroth
ms.openlocfilehash: 2c120667a0ce279ea03922adf487f58c1fdc92de
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82747053"
---
# <a name="adostreamconstruction-interface"></a>Interfaccia ADOStreamConstruction
L'interfaccia **ADOStreamConstruction** viene utilizzata per costruire un oggetto **flusso** ADO da un oggetto OLE DB **IStream** in un'applicazione C/C++.  
  
## <a name="properties"></a>Proprietà  
  
|||  
|-|-|  
|[Proprietà Stream](../../../ado/reference/ado-api/stream-property.md)|Lettura/Scrittura. Ottiene o imposta un oggetto **flusso** OLE DB.|  
  
## <a name="methods"></a>Metodi  
 No.  
  
## <a name="events"></a>Eventi  
 No.  
  
## <a name="remarks"></a>Commenti  
 Dato un oggetto OLE DB **IStream** ( `pStream` ), la costruzione di un oggetto **flusso** ADO ( `adoStr` ) equivale alle tre operazioni di base seguenti:  
  
1.  Creazione di un oggetto **flusso** ADO:  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  Eseguire una query sull'interfaccia **IADOStreamConstruction** sull'oggetto **Stream** :  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 Chiamare il `IADOStreamConstruction::get_Stream` Metodo Property per impostare il OLE DB oggetto **IStream** sull'oggetto **flusso** ADO:  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 L'oggetto risultante `adoStr` rappresenta ora l'oggetto **flusso** ADO costruito dal OLE DB oggetto **IStream** .  
  
## <a name="requirements"></a>Requisiti  
 **Versione:** ADO 2,0 o versione successiva  
  
 **Libreria:** msado15. dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento API ADO](../../../ado/reference/ado-api/ado-api-reference.md)
