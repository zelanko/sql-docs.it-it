---
title: Creazione di recordset gerarchici | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset fabrication [ADO]
- hierarchical Recordsets [ADO]
- fabricating hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: a584e642-a4a3-418e-bc20-3aff81a5625a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6fcdb630f2391f685080ac594cfdb537edf626a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925328"
---
# <a name="fabricating-hierarchical-recordsets"></a>Creazione di recordset gerarchici
Nell'esempio seguente viene illustrato come creare un oggetto Recordset gerarchico senza un'origine dati sottostante utilizzando i dati di data shaping grammatica per definire le colonne per l'elemento padre, figlio e nipote **recordset**.  
  
 Per creare un modello gerarchico **Recordset**, è necessario specificare il [Microsoft Data shaping per OLE DB (ADO Service Provider)](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (MSDataShape), ed è possibile specificare un valore NONE in Provider di dati di parametro di stringa di connessione del [Open](../../../ado/reference/ado-api/open-method-ado-connection.md) metodo per il [connessione](../../../ado/reference/ado-api/connection-object-ado.md) oggetto. Per altre informazioni, vedere [provider obbligatori per il Data Shaping](../../../ado/guide/data/required-providers-for-data-shaping.md).  
  
```  
Dim cn As New ADODB.Connection  
Dim rsCustomers As New ADODB.Recordset  
  
cn.Open "Provider=MSDataShape;Data Provider=NONE;"  
  
strShape = _  
"SHAPE APPEND NEW adInteger AS CustID," & _  
            " NEW adChar(25) AS FirstName," & _  
            " NEW adChar(25) AS LastName," & _  
            " NEW adChar(12) AS SSN," & _  
            " NEW adChar(50) AS Address," & _  
         " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                        " NEW adInteger AS CustID," & _  
                        " NEW adChar(20) AS BodyColor, " & _  
                     " ((SHAPE APPEND NEW adChar(80) AS VIN_NO," & _  
                                    " NEW adChar(20) AS Make, " & _  
                                    " NEW adChar(20) AS Model," & _  
                                    " NEW adChar(4) AS Year) " & _  
                        " AS VINS RELATE VIN_NO TO VIN_NO))" & _  
            " AS Vehicles RELATE CustID TO CustID) "  
  
rsCustomers.Open strShape, cn, adOpenStatic, adLockOptimistic, -1  
```  
  
 Non appena il **Recordset** è stato creato, può essere popolato, modificato o salvarla in un file.  
  
## <a name="see-also"></a>Vedere anche  
 [Accesso alle righe in un Recordset gerarchico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Grammatica formale per Shape](../../../ado/guide/data/formal-shape-grammar.md)   
 [Provider necessari per il Data Shaping](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Clausola APPEND per Shape](../../../ado/guide/data/shape-append-clause.md)   
 [Comandi Shape in generale](../../../ado/guide/data/shape-commands-in-general.md)
