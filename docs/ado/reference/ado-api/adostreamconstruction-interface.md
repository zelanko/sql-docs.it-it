---
description: Interfaccia ADOStreamConstruction
title: Interfaccia ADOStreamConstruction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: f6e32b076fa0faa43a3dff46aed66bcadaa2f1ae
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976162"
---
# <a name="adostreamconstruction-interface"></a>Interfaccia ADOStreamConstruction
L'interfaccia **ADOStreamConstruction** viene utilizzata per costruire un oggetto **flusso** ADO da un oggetto OLE DB **IStream** in un'applicazione C/C++.  
  
## <a name="properties"></a>Proprietà  
  
|Proprietà|Descrizione|  
|-|-|  
|[Flusso](./stream-property.md)|Lettura/Scrittura. Ottiene o imposta un oggetto **flusso** OLE DB.|  
  
## <a name="methods"></a>Metodi  
 Nessuno.  
  
## <a name="events"></a>Events  
 No.  
  
## <a name="remarks"></a>Osservazioni  
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
  
 **Libreria:** msado15.dll  
  
 **UUID:** 00000283-0000-0010-8000-00AA006D2EA4  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni di riferimento sull'API ADO](./ado-api-reference.md)