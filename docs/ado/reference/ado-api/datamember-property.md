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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 623f9b1f1e8873ddc4819bb8500c11edf09f5f76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919225"
---
# <a name="datamember-property"></a>Proprietà DataMember
Indica il nome del membro dati che verrà recuperato dal [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) fa riferimento il [DataSource](../../../ado/reference/ado-api/datasource-property-ado.md) proprietà.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **stringa** valore. Il nome non distinzione maiuscole / minuscole.  
  
## <a name="remarks"></a>Note  
 Questa proprietà viene utilizzata per creare controlli associati a dati con l'ambiente dei dati. Gestisce l'ambiente dei dati raccolte di dati (origini dati) che contiene oggetti denominati (membri dati) che verranno rappresentati come una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
 Il **DataMember** e **DataSource** proprietà devono essere usate insieme.  
  
 Il **DataMember** proprietà determina quale oggetto specificato dalle **DataSource** proprietà sarà rappresentata come una **Recordset** oggetto. Il **Recordset** oggetto deve essere chiuso prima di questa proprietà è impostata. Viene generato un errore se il **DataMember** proprietà non viene impostata prima il **DataSource** proprietà, oppure se la **DataMember** nome non è riconosciuto per l'oggetto specificato nel **DataSource** proprietà.  
  
## <a name="usage"></a>Uso  
  
```  
Dim rs as New ADODB.Recordset  
rs.DataMember = "Command"     'Name of the rowset to bind to  
Set rs.DataSource = myDE      'Name of the object containing an IRowset  
```  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà DataSource (ADO)](../../../ado/reference/ado-api/datasource-property-ado.md)
