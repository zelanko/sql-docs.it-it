---
title: Using System. Transactions | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: a9b99842a92649a42e9a0a42e6732368dc5e06ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081347"
---
# <a name="using-systemtransactions"></a>Utilizzo di System.Transactions
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Il **System. Transactions** spazio dei nomi fornisce un framework per le transazioni completamente integrato con ADO.NET e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrazione common language runtime (CLR). Il **TransactionScope** classe rende un blocco di codice transazionale elencando implicitamente le connessioni in una transazione distribuita. È necessario chiamare il **completa** metodo alla fine del blocco di codice contrassegnato dalle **TransactionScope**. Il **Dispose** metodo viene richiamato quando l'esecuzione del programma lascia un blocco di codice, la transazione siano stati sospesi se la **completa** non viene chiamato. Se è stata generata un'eccezione che determina l'uscita del codice dall'ambito, la transazione non viene più utilizzata.  
  
 È consigliabile impiegare il un **usando** blocco per garantire che le **Dispose** metodo viene chiamato sul **TransactionScope** oggetto quando il **usando**blocco viene chiuso. Tentativo di eseguire il commit o il rollback delle transazioni in sospeso può compromettere notevolmente le prestazioni perché il timeout predefinito per il **TransactionScope** è un minuto. Se non si usa una **usando** istruzione, è necessario eseguire le operazioni in un **provare** blocca e chiamare in modo esplicito il **Dispose** metodo nel **infine**blocco.  
  
 Se si verifica un'eccezione all'interno di **TransactionScope**, la transazione viene contrassegnata come incoerente e viene abbandonata. Si è eseguito il rollback quando il **TransactionScope** viene eliminato. Se non si verifica alcuna eccezione, viene eseguito il commit delle transazioni partecipanti.  
  
 **TransactionScope** deve essere utilizzato solo quando si accede a origini dati locali e remoti o i gestori di risorse esterne. Infatti **TransactionScope** comporta sempre promozione delle transazioni, anche se è utilizzato solo all'interno di una connessione di contesto.  
  
> [!NOTE]  
>  Il **TransactionScope** classe crea una transazione con un **System.Transactions.Transaction.IsolationLevel** dei **Serializable** per impostazione predefinita. A seconda dell'applicazione, è possibile abbassare il livello di isolamento per evitare che si verifichi un numero elevato di contese.  
  
> [!NOTE]  
>  È consigliabile eseguire solo aggiornamenti, inserimenti ed eliminazioni all'interno di transazioni distribuite sui server remoti in quanto tali operazioni comportano un notevole consumo di risorse del database. Se l'operazione viene effettuata sul server locale, non è necessario eseguire una transazione distribuita ed è sufficiente una transazione locale. Le istruzioni SELECT potrebbero bloccare inutilmente risorse del database e in alcuni scenari può essere necessario utilizzare le transazioni per le operazioni di selezione. Tutto il lavoro che non riguarda il database deve essere svolto all'esterno dell'ambito della transazione, a meno che non coinvolga altri gestori di risorse inclusi nella transazione. Sebbene un'eccezione all'interno dell'ambito della transazione impedisca l'esecuzione del commit, il **TransactionScope** classe non è disponibile il rollback delle modifiche al codice apportate all'esterno dell'ambito della transazione se stessa. Se devi eseguire qualche azione quando viene eseguito il rollback della transazione, è necessario scrivere la propria implementazione del **System.Transactions.IEnlistmentNotification** interfaccia ed integrarla esplicitamente nella transazione.  
  
## <a name="example"></a>Esempio  
 Per rivolgersi **System. Transactions**, è necessario disporre di un riferimento al file Transactions.  
  
 Nel codice seguente viene illustrato come creare una transazione che può essere promossa su due istanze diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Queste istanze vengono rappresentate da due diverse **SqlConnection** oggetti, che vengono eseguito il wrapping in un **TransactionScope** blocco. Il codice crea il **TransactionScope** blocco con un **usando** istruzione e viene aperta la prima connessione, elencarla automaticamente nel **TransactionScope**. La transazione viene integrata inizialmente come transazione lightweight, non come transazione completamente distribuita. Il codice presuppone l'esistenza della logica condizionale, omessa per brevità. Apre la seconda connessione solo se necessario, integrandola nel **TransactionScope**. Quando la connessione è aperta, la transazione viene promossa automaticamente a una transazione completamente distribuita. Il codice richiama quindi **TransactionScope.Complete**, che esegue il commit della transazione. Il codice elimina due connessioni quando si esce dal **usando** istruzioni per le connessioni. Il **TransactionScope.Dispose** metodo per il **TransactionScope** viene chiamato automaticamente al termine del **usando** bloccare per il  **TransactionScope**. Se è stata generata un'eccezione in qualsiasi punto nel **TransactionScope** blocco **completa** non viene chiamato e verrà la transazione distribuita eseguire il rollback quando il **TransactionScope**  viene eliminato.  
  
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
 [Integrazione con CLR e transazioni](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
