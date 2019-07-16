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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67920803"
---
# <a name="adorecordconstruction-interface"></a>Interfaccia ADORecordConstruction
Il **ADORecordConstruction**interfaccia viene utilizzata per costruire un oggetto ADO **Record** oggetto da OLE DB **riga** oggetto in un'applicazione C/C++.  
  
 Questa interfaccia supporta le proprietà seguenti:  
  
## <a name="properties"></a>Proprietà  
  
|||  
|-|-|  
|[ParentRow](../../../ado/reference/ado-api/parentrow-property-ado.md)|Sola scrittura.<br />Imposta il contenitore di OLE DB **riga** oggetto questo ADO **Record** oggetto.|  
|[Riga](../../../ado/reference/ado-api/row-property-ado.md)|Lettura/scrittura.<br />Ottiene o imposta un DB OLE **riga** oggetto da/in questa ADO **Record** oggetto.|  
  
## <a name="methods"></a>Metodi  
 No.  
  
## <a name="events"></a>Events  
 No.  
  
## <a name="remarks"></a>Note  
 Dato un OLE DB **riga** oggetto (`pRow`), la costruzione di un oggetto ADO **Record** oggetto (`adoR`), gli importi per le tre operazioni fondamentali seguenti:  
  
1.  Creare un oggetto ADO **Record** oggetto:  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  Query di **IADORecordConstruction** interfaccia le **Record** oggetto:  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  Chiamare il **IADORecordConstruction::** metodo di proprietà da impostare OLE DB **riga** sull'oggetto ADO **Record** oggetto:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 I risultanti **adoR** oggetto rappresenta ora ADO **Record** oggetto costruito da OLE DB **riga** oggetto.  
  
 Un oggetto ADO **Record** oggetto può anche essere costruito dal contenitore di OLE DB **riga** oggetto.  
  
## <a name="requirements"></a>Requisiti  
 **Versione:** ADO 2.0 e versioni successiva  
  
 **Libreria:** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4
