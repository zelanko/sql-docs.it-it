---
title: Utilizzo di System. Transactions | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TransactionScope class
- Dispose method
- System.Transactions namespace
ms.assetid: 79656ce5-ce46-4c5e-9540-cf9869bd774b
author: rothja
ms.author: jroth
ms.openlocfilehash: 40bdbcd98e70ae8ea318ba8ca0243f11107bd61b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954931"
---
# <a name="using-systemtransactions"></a>Utilizzo di System.Transactions
  Tramite lo spazio dei nomi `System.Transactions` vengono forniti un framework di transazioni pienamente integrato con ADO.NET e l'integrazione con CRL di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La classe `System.Transactions.TransactionScope` rende transazionale un blocco di codice attraverso un'integrazione implicita delle connessioni in una transazione distribuita. È necessario chiamare il metodo `Complete` alla fine del blocco di codice contrassegnato da `TransactionScope`. Il metodo `Dispose` viene richiamato quando l'esecuzione del programma lascia un blocco di codice. Se il metodo `Complete` non viene chiamato, la transazione non viene più utilizzata. Se è stata generata un'eccezione che determina l'uscita del codice dall'ambito, la transazione non viene più utilizzata.  
  
 È consigliabile utilizzare un blocco `using` per far sì che il metodo `Dispose` venga chiamato sull'oggetto `TransactionScope` al termine del blocco `using`. L'impossibilità di eseguire il commit o il rollback delle transazioni in sospeso può compromettere notevolmente le prestazioni in quanto il timeout predefinito per `TransactionScope` è pari a un minuto. Se non si utilizza un'istruzione `using`, è necessario eseguire tutto il lavoro in un blocco `Try` e chiamare in modo esplicito il metodo `Dispose` all'interno del blocco `Finally`.  
  
 Se si verifica un'eccezione all'interno di `TransactionScope`, la transazione viene contrassegnata come incoerente e quindi abbandonata. Ne viene eseguito il rollback all'eliminazione di `TransactionScope`. Se non si verifica alcuna eccezione, viene eseguito il commit delle transazioni partecipanti.  
  
 È opportuno utilizzare `TransactionScope` solo quando si accede a origini dati locali e remote o a gestori di risorse esterni in quanto Questo perché `TransactionScope` causa sempre l'innalzamento di livello delle transazioni, anche se viene utilizzato solo all'interno di una connessione di contesto.  
  
> [!NOTE]  
>  Per impostazione predefinita, la classe `TransactionScope` crea una transazione con un `System.Transactions.Transaction.IsolationLevel` di `Serializable`. A seconda dell'applicazione, è possibile abbassare il livello di isolamento per evitare che si verifichi un numero elevato di contese.  
  
> [!NOTE]  
>  È consigliabile eseguire solo aggiornamenti, inserimenti ed eliminazioni all'interno di transazioni distribuite sui server remoti in quanto tali operazioni comportano un notevole consumo di risorse del database. Se l'operazione viene effettuata sul server locale, non è necessario eseguire una transazione distribuita ed è sufficiente una transazione locale. Le istruzioni SELECT potrebbero bloccare inutilmente risorse del database e in alcuni scenari può essere necessario utilizzare le transazioni per le operazioni di selezione. Tutto il lavoro che non riguarda il database deve essere svolto all'esterno dell'ambito della transazione, a meno che non coinvolga altri gestori di risorse inclusi nella transazione. Sebbene un'eccezione all'interno dell'ambito della transazione impedisca il commit di quest'ultima, la classe `TransactionScope` non consente di eseguire il rollback delle modifiche apportate al codice all'esterno dell'ambito della transazione stessa. Per intraprendere qualche azione durante il rollback della transazione, è necessario scrivere un'implementazione personalizzata dell'interfaccia `System.Transactions.IEnlistmentNotification` ed integrarla esplicitamente nella transazione.  
  
## <a name="example"></a>Esempio  
 Per utilizzare `System.Transactions`, è necessario disporre di un riferimento al file System.Transactions.dll.  
  
 Nel codice seguente viene illustrato come creare una transazione che può essere promossa su due istanze diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Queste istanze vengono rappresentate da due oggetti `System.Data.SqlClient.SqlConnection` diversi, di cui viene eseguito il wrapping in un blocco `TransactionScope`. Il codice crea il blocco `TransactionScope` con un'istruzione `using` e apre la prima connessione, che comporta un'integrazione automatica in `TransactionScope`. La transazione viene integrata inizialmente come transazione lightweight, non come transazione completamente distribuita. Il codice presuppone l'esistenza della logica condizionale, omessa per brevità. Apre la seconda connessione solo se necessario, integrandola in `TransactionScope`. Quando la connessione è aperta, la transazione viene promossa automaticamente a una transazione completamente distribuita. Il codice quindi richiama `TransactionScope.Complete`, che esegue il commit della transazione, ed elimina le due connessioni al termine delle istruzioni `using` per le connessioni. Il metodo `TransactionScope.Dispose` per `TransactionScope` viene chiamato automaticamente al termine del blocco `using` per `TransactionScope`. Se in un punto qualsiasi del blocco `TransactionScope` è stata generata un'eccezione, `Complete` non viene chiamato e viene eseguito il rollback della transazione distribuita al momento dell'eliminazione di `TransactionScope`.  
  
 Visual Basic  
  
```  
Using transScope As New TransactionScope()  
    Using connection1 As New SqlConnection(connectString1)  
        ' Opening connection1 automatically enlists it in the   
        ' TransactionScope as a lightweight transaction.  
        connection1.Open()  
  
        ' Do work in the first connection.  
  
        ' Assumes conditional logic in place where the second  
        ' connection will only be opened as needed.  
        Using connection2 As New SqlConnection(connectString2)  
            ' Open the second connection, which enlists the   
            ' second connection and promotes the transaction to  
            ' a full distributed transaction.  
            connection2.Open()  
  
            ' Do work in the second connection.  
  
        End Using  
    End Using  
  
    ' Commit the transaction.  
    transScope.Complete()  
End Using  
```  
  
 C#  
  
```  
using (TransactionScope transScope = new TransactionScope())  
{  
    using (SqlConnection connection1 = new   
       SqlConnection(connectString1))  
    {  
        // Opening connection1 automatically enlists it in the   
        // TransactionScope as a lightweight transaction.  
        connection1.Open();  
  
        // Do work in the first connection.  
  
        // Assumes conditional logic in place where the second  
        // connection will only be opened as needed.  
        using (SqlConnection connection2 = new   
            SqlConnection(connectString2))  
        {  
            // Open the second connection, which enlists the   
            // second connection and promotes the transaction to  
            // a full distributed transaction.   
            connection2.Open();  
  
            // Do work in the second connection.  
        }  
    }  
    //  The Complete method commits the transaction.  
    transScope.Complete();  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Integrazione con CLR e transazioni](../native-client-ole-db-transactions/transactions.md)  
  
  
