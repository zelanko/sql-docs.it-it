---
title: Creazione di trigger DML per gestire più righe di dati
ms.custom: seo-dt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- multiple row DML triggers
- UPDATE statement [SQL Server], DML triggers
- DELETE statement [SQL Server], DML triggers
- multirow DML triggers [SQL Server]
- INSERT statement [SQL Server], DML triggers
- DML triggers, multirow
ms.assetid: d476c124-596b-4b27-a883-812b6b50a735
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d5e3c8d9876545e1e68a9795b7c327ac1e47e2d6
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74096013"
---
# <a name="create-dml-triggers-to-handle-multiple-rows-of-data"></a>Creazione di trigger DML per gestire più righe di dati
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Quando si scrive il codice di un trigger DML, è importante considerare che l'istruzione che attiva il trigger può essere singola e interessare più righe di dati, anziché una sola riga. Questo funzionamento è comune per i trigger UPDATE e DELETE perché queste istruzioni in genere interessano più righe, mentre è meno comune per i trigger INSERT perché l'istruzione INSERT di base aggiunge soltanto una riga singola. Dato però che un trigger INSERT può essere attivato da un'istruzione INSERT INTO (*table_name*) SELECT, l'inserimento di molte righe può causare la chiamata a un unico trigger.  
  
 Queste considerazioni sono di particolare importanza quando la funzione di un trigger DML consiste nel ricalcolare automaticamente i valori di riepilogo di una tabella e archiviare i risultati in un'altra tabella per i conteggi.  
  
> [!NOTE]  
>  Non è consigliabile utilizzare cursori nei trigger dato che possono potenzialmente ridurre le prestazioni. Per progettare un trigger che interessa più righe, utilizzare una logica basata su set di righe invece che su cursori.  
  
## <a name="examples"></a>Esempi  
 I trigger DML negli esempi seguenti sono progettati per archiviare il totale parziale di una colonna in un'altra tabella del database di esempio di [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
### <a name="a-storing-a-running-total-for-a-single-row-insert"></a>R. Archiviazione di un totale parziale per l'inserimento di una riga singola  
 La prima versione del trigger DML funziona correttamente per l'inserimento di una singola riga, quando una riga di dati viene caricata nella tabella `PurchaseOrderDetail` . Il trigger DML viene attivato da un'istruzione INSERT e la nuova riga viene caricata nella tabella **inserted** per la durata dell'esecuzione del trigger. L'istruzione `UPDATE` legge il valore della colonna `LineTotal` per la riga e lo aggiunge al valore esistente nella colonna `SubTotal` della tabella `PurchaseOrderHeader` . La clausola `WHERE` verifica che la riga aggiornata nella tabella `PurchaseOrderDetail` corrisponda al valore di `PurchaseOrderID` della riga nella tabella **inserted** .  
  
```  
-- Trigger is valid for single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID ;  
```  
  
### <a name="b-storing-a-running-total-for-a-multirow-or-single-row-insert"></a>B. Archiviazione di un totale parziale per l'inserimento di una riga singola o di più righe  
 Nel caso di un'istruzione che interessa più righe, il trigger DML dell'esempio A potrebbe non funzionare correttamente. Nell'espressione a destra di un'espressione di assegnazione in un'istruzione UPDATE (`SubTotal` + `LineTotal`) è possibile includere un valore singolo, non un elenco di valori. L'effetto del trigger è quindi quello di recuperare un valore dalle righe singole della tabella **inserted** e aggiungerlo al valore esistente `SubTotal` nella tabella `PurchaseOrderHeader` per un determinato valore di `PurchaseOrderID` . L'effetto dell'operazione potrebbe non essere quello atteso se un singolo valore di `PurchaseOrderID` compare più volte nella tabella **inserted** .  
  
 Per aggiornare la tabella `PurchaseOrderHeader` correttamente, il trigger deve tener conto della possibile presenza di più righe nella tabella **inserted** . Ciò può essere ottenuto utilizzando la funzione `SUM` per calcolare il valore `LineTotal` totale relativo a un gruppo di righe nella tabella **inserted** per ogni `PurchaseOrderID`. La funzione `SUM` viene inclusa in una sottoquery correlata (l'istruzione `SELECT` in parentesi). Questa sottoquery restituisce un singolo valore per ogni `PurchaseOrderID` nella tabella **inserted** che corrisponde o è correlato a un valore `PurchaseOrderID` nella tabella `PurchaseOrderHeader` .  
  
```  
-- Trigger is valid for multirow and single-row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail2  
ON Purchasing.PurchaseOrderDetail  
AFTER INSERT AS  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted);  
```  
  
 Questo trigger funziona inoltre correttamente per l'inserimento di una riga singola. La somma dei valori della colonna `LineTotal` corrisponde alla somma di una riga singola. Con questo trigger, tuttavia, la sottoquery correlata e l'operatore `IN` utilizzato nella clausola `WHERE` comportano un'ulteriore elaborazione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], non necessaria per l'inserimento di una riga singola.  
  
### <a name="c-storing-a-running-total-based-on-the-type-of-insert"></a>C. Archiviazione di un totale parziale sulla base del tipo di inserimento  
 È possibile modificare il trigger per utilizzare il metodo ottimale in base al numero di righe. È ad esempio possibile utilizzare la funzione `@@ROWCOUNT` nella logica del trigger per distinguere tra l'inserimento di una riga singola e di più righe.  
  
```  
-- Trigger valid for multirow and single row inserts  
-- and optimal for single row inserts.  
USE AdventureWorks2012;  
GO  
CREATE TRIGGER NewPODetail3  
ON Purchasing.PurchaseOrderDetail  
FOR INSERT AS  
IF @@ROWCOUNT = 1  
BEGIN  
   UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal + LineTotal  
   FROM inserted  
   WHERE PurchaseOrderHeader.PurchaseOrderID = inserted.PurchaseOrderID  
END  
ELSE  
BEGIN  
      UPDATE Purchasing.PurchaseOrderHeader  
   SET SubTotal = SubTotal +   
      (SELECT SUM(LineTotal)  
      FROM inserted  
      WHERE PurchaseOrderHeader.PurchaseOrderID  
       = inserted.PurchaseOrderID)  
   WHERE PurchaseOrderHeader.PurchaseOrderID IN  
      (SELECT PurchaseOrderID FROM inserted)  
END;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Trigger DML](../../relational-databases/triggers/dml-triggers.md)  
  
  
