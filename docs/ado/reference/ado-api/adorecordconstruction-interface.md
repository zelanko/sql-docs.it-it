---
title: Interfaccia ADORecordConstruction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction
helpviewer_keywords:
- ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c56ba0b9d7ebebbf4a9e4baf669bbdc6eb84355e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920803"
---
# <a name="adorecordconstruction-interface"></a>Interfaccia ADORecordConstruction
L'interfaccia **ADORecordConstruction**viene utilizzata per costruire un oggetto **record** ADO da un oggetto OLE DB **Row** in un'applicazione C/C++.  
  
 Questa interfaccia supporta le proprietà seguenti:  
  
## <a name="properties"></a>Proprietà  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|Sola scrittura.<br />Imposta il contenitore di un oggetto OLE DB **riga** su questo oggetto **record** ADO.|  
|[Riga](../../../ado/reference/ado-api/row-property-ado.md)|Lettura/Scrittura.<br />Ottiene o imposta un oggetto OLE DB **riga** da/in questo oggetto **record** ADO.|  
  
## <a name="methods"></a>Metodi  
 No.  
  
## <a name="events"></a>Eventi  
 No.  
  
## <a name="remarks"></a>Osservazioni  
 Dato un oggetto OLE DB **Row** (`pRow`), la costruzione di un oggetto **record** ADO (`adoR`), equivale alle tre operazioni di base seguenti:  
  
1.  Creazione di un oggetto **record** ADO:  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  Eseguire una query sull'interfaccia **IADORecordConstruction** sull'oggetto **record** :  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  Chiamare il metodo della proprietà **IADORecordConstruction::p ut_Row** per impostare l'oggetto **riga** OLE DB sull'oggetto **record** ADO:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 L'oggetto **adore** risultante rappresenta ora l'oggetto **record** ADO costruito dall'oggetto OLE DB **riga** .  
  
 È anche possibile costruire un oggetto **record** ADO dal contenitore di un oggetto OLE DB **Row** .  
  
## <a name="requirements"></a>Requisiti  
 **Versione:** ADO 2,0 e versioni successive  
  
 **Libreria:** msado15. dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
