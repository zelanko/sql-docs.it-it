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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 70a6dd02722a34159b345a83b32897aa8c38d0ff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920781"
---
# <a name="adostreamconstruction-interface"></a>Interfaccia ADOStreamConstruction
Il **ADOStreamConstruction** interfaccia viene utilizzata per costruire un oggetto ADO **Stream** oggetto da OLE DB **IStream** oggetto in un'applicazione C/C++.  
  
## <a name="properties"></a>Proprietà  
  
|||  
|-|-|  
|[Proprietà Stream](../../../ado/reference/ado-api/stream-property.md)|Lettura/scrittura. Ottiene o imposta un DB OLE **Stream** oggetto.|  
  
## <a name="methods"></a>Metodi  
 No.  
  
## <a name="events"></a>Events  
 No.  
  
## <a name="remarks"></a>Note  
 Dato un OLE DB **IStream** oggetto (`pStream`), la costruzione di un oggetto ADO **Stream** oggetto (`adoStr`) gli importi per le tre operazioni fondamentali seguenti:  
  
1.  Creare un oggetto ADO **Stream** oggetto:  
  
    ```  
    Stream20Ptr adoStr;  
    adoStr.CreateInstance(__uuidof(Stream));  
    ```  
  
2.  Query di **IADOStreamConstruction** interfaccia le **Stream** oggetto:  
  
    ```  
    adoStreamConstructionPtr adoStrConstruct=NULL;  
    adoStr->QueryInterface(__uuidof(ADOStreamConstruction),  
                         (void**)&adoStrConstruct);  
    ```  
  
 Chiamare il `IADOStreamConstruction::get_Stream` metodo di proprietà da impostare OLE DB **IStream** sull'oggetto ADO **Stream** oggetto:  
  
```  
IUnknown *pUnk=NULL;  
pRowset->QueryInterface(IID_IUnknown, (void**)&pUnk);  
adoStrConstruct->put_Stream(pUnk);  
```  
  
 I risultanti `adoStr` oggetto rappresenta ora ADO **Stream** oggetto costruito da OLE DB **IStream** oggetto.  
  
## <a name="requirements"></a>Requisiti  
 **Versione:** ADO 2.0 o versione successiva  
  
 **Libreria:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento API ADO](../../../ado/reference/ado-api/ado-api-reference.md)
