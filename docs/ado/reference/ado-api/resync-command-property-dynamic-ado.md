---
title: Risincronizza comando proprietà dinamica (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Resync Command property [ADO]
ms.assetid: 4e2bb601-0fe8-4d61-b00e-38341d85a6bb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e81fa9ffb28ba31f50d77cacf372bc24d09787ba
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917142"
---
# <a name="resync-command-property-dynamic-ado"></a>Proprietà dinamica Resync Command (ADO)
Specifica un comando fornito dall'utente di stringhe che il [Risincronizza](../../../ado/reference/ado-api/resync-method.md) i problemi di metodi per aggiornare i dati nella tabella denominata nel [tabella univoca](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) proprietà dinamica.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **stringa** valore che è una stringa di comando.  
  
## <a name="remarks"></a>Note  
 Il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto è il risultato di un'operazione di JOIN eseguita in più tabelle di base. Righe interessate dipendono il *AffectRecords* parametro del [Risincronizza](../../../ado/reference/ado-api/resync-method.md) (metodo). Lo standard **Risincronizza** metodo viene eseguito se il [Unique Table](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e **Resync Command** non vengono impostate proprietà.  
  
 La stringa di comando del **Resync Command** proprietà è un comando con parametri o stored procedure che identifica in modo univoco la riga da aggiornare e restituisce una singola riga con lo stesso numero e ordine delle colonne della riga da aggiornati. La stringa di comando contiene un parametro per ogni colonna chiave primaria nella **Unique Table**; in caso contrario, viene restituito un errore di run-time. I parametri vengono compilati automaticamente con valori di chiave primaria della riga da aggiornare.  
  
 Di seguito sono riportati due esempi basati su SQL:  
  
 1\) il **Recordset** è definita da un comando:  
  
```  
SELECT * FROM Customers JOIN Orders ON   
   Customers.CustomerID = Orders.CustomerID  
   WHERE city = 'Seattle'  
   ORDER BY CustomerID  
```  
  
 Il **Resync Command** è impostata su:  
  
```  
"SELECT * FROM   
   (SELECT * FROM Customers JOIN Orders   
   ON Customers.CustomerID = Orders.CustomerID  
   city = 'Seattle' ORDER BY CustomerID)  
WHERE Orders.OrderID = ?"  
```  
  
 Il **tabelle univoche** viene *ordini* e la relativa chiave primaria, *OrderID*, con i parametri. Sub-select fornisce un modo semplice per garantire a livello di codice che lo stesso numero e ordine delle colonne vengono restituite come dal comando originale.  
  
 2\) il **Recordset** è definito da una stored procedure:  
  
```  
CREATE PROC Custorders @CustomerID char(5) AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID   
WHERE Customers.CustomerID = @CustomerID  
```  
  
 Il **Risincronizza** metodo deve eseguire la stored procedure seguente:  
  
```  
CREATE PROC CustordersResync @ordid int AS   
SELECT * FROM Customers JOIN Orders ON   
Customers.CustomerID = Orders.CustomerID  
WHERE Orders.ordid  = @ordid  
```  
  
 Il **Resync Command** è impostata su:  
  
```  
"{call CustordersResync (?)}"  
```  
  
 Ancora una volta, il **tabelle univoche** viene *ordini* e la relativa chiave primaria, *OrderID*, con i parametri.  
  
 **Comando Risincronizza** viene aggiunta una proprietà dinamica per il **Recordset** oggetto [proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) raccolta quando la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) è impostata su **adUseClient**.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
