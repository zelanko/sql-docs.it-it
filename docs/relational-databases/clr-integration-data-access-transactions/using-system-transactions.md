---
title: Utilizzo di System. Transactions | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081347"
---
# <a name="using-systemtransactions"></a>Utilizzo di System.Transactions
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Lo spazio dei nomi **System. Transactions** fornisce un Framework di transazione completamente integrato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con ADO.NET e l'integrazione con Common Language Runtime (CLR). La classe **System. Transactions. TransactionScope** rende un blocco di codice transazionale, integrando in modo implicito le connessioni in una transazione distribuita. È necessario chiamare il metodo **complete** alla fine del blocco di codice contrassegnato da **TransactionScope**. Il metodo **Dispose** viene richiamato quando l'esecuzione del programma lascia un blocco di codice, facendo in modo che la transazione venga sospesa se non viene chiamato il metodo **completo** . Se è stata generata un'eccezione che determina l'uscita del codice dall'ambito, la transazione non viene più utilizzata.  
  
 Si consiglia di utilizzare un blocco **using** per garantire che il metodo **Dispose** venga chiamato sull'oggetto **TransactionScope** quando viene terminato il blocco **using** . L'impossibilità di eseguire il commit o il rollback delle transazioni in sospeso può causare un grave peggioramento delle prestazioni perché il timeout predefinito per **TransactionScope** è un minuto. Se non si usa un'istruzione **using** , è necessario eseguire tutte le operazioni in un blocco **try** e chiamare in modo esplicito il metodo **Dispose** nel blocco **finally** .  
  
 Se si verifica un'eccezione all'interno di **TransactionScope**, la transazione viene contrassegnata come incoerente e viene abbandonata. Viene eseguito il rollback quando **TransactionScope** viene eliminato. Se non si verifica alcuna eccezione, viene eseguito il commit delle transazioni partecipanti.  
  
 È consigliabile utilizzare **TransactionScope** solo quando si accede a origini dati locali e remote o a gestori di risorse esterni. Questo perché **TransactionScope** causa sempre la promozione delle transazioni, anche se viene usata solo all'interno di una connessione di contesto.  
  
> [!NOTE]  
>  Per impostazione predefinita, la classe **TransactionScope** crea una transazione con **System. Transactions. Transaction. IsolationLevel** di **Serializable** . A seconda dell'applicazione, è possibile abbassare il livello di isolamento per evitare che si verifichi un numero elevato di contese.  
  
> [!NOTE]  
>  È consigliabile eseguire solo aggiornamenti, inserimenti ed eliminazioni all'interno di transazioni distribuite sui server remoti in quanto tali operazioni comportano un notevole consumo di risorse del database. Se l'operazione viene effettuata sul server locale, non è necessario eseguire una transazione distribuita ed è sufficiente una transazione locale. Le istruzioni SELECT potrebbero bloccare inutilmente risorse del database e in alcuni scenari può essere necessario utilizzare le transazioni per le operazioni di selezione. Tutto il lavoro che non riguarda il database deve essere svolto all'esterno dell'ambito della transazione, a meno che non coinvolga altri gestori di risorse inclusi nella transazione. Sebbene un'eccezione nell'ambito della transazione impedisca l'esecuzione del commit della transazione, la classe **TransactionScope** non dispone di alcun provisioning per eseguire il rollback di tutte le modifiche apportate dal codice al di fuori dell'ambito della transazione stessa. Se è necessario eseguire un'azione quando viene eseguito il rollback della transazione, è necessario scrivere un'implementazione personalizzata dell'interfaccia **System. Transactions. IEnlistmentNotification** e integrarla in modo esplicito nella transazione.  
  
## <a name="example"></a>Esempio  
 Per utilizzare **System. Transactions**, è necessario disporre di un riferimento al file System. Transactions. dll.  
  
 Nel codice seguente viene illustrato come creare una transazione che può essere promossa su due istanze diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Queste istanze sono rappresentate da due oggetti **System. Data. SqlClient. SqlConnection** diversi, di cui viene eseguito il wrapper in un blocco **TransactionScope** . Il codice crea il blocco **TransactionScope** con un'istruzione **using** e apre la prima connessione, che la integra automaticamente in **TransactionScope**. La transazione viene integrata inizialmente come transazione lightweight, non come transazione completamente distribuita. Il codice presuppone l'esistenza della logica condizionale, omessa per brevità. Viene aperta la seconda connessione solo se necessaria, che viene integrata in **TransactionScope**. Quando la connessione è aperta, la transazione viene promossa automaticamente a una transazione completamente distribuita. Il codice richiama quindi **TransactionScope. complete**, che consente di eseguire il commit della transazione. Il codice elimina le due connessioni quando si esce dalle istruzioni **using** per le connessioni. Il metodo **TransactionScope. Dispose** per **TransactionScope** viene chiamato automaticamente alla chiusura del blocco **using** per **TransactionScope**. Se è stata generata un'eccezione in qualsiasi punto del blocco **TransactionScope** , **complete** non viene chiamato e viene eseguito il rollback della transazione distribuita quando **TransactionScope** viene eliminato.  
  
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
  
  
