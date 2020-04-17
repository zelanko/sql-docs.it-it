---
title: Utilizzo di System.Transactions Documenti Microsoft
description: Lo spazio dei nomi System.Transactions fornisce un framework di transazioni completamente integrato con l'integrazione CLR di ADO.NET e SQL Server.
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
ms.openlocfilehash: 7fa98e9e13062d358a6a1810485d45c8d9d3e911
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488497"
---
# <a name="using-systemtransactions"></a>Utilizzo di System.Transactions
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Lo spazio dei nomi **System.Transactions** fornisce un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] framework di transazioni completamente integrato con l'integrazione di ADO.NET e Common Language Runtime (CLR). La classe **System.Transactions.TransactionScope** esegue una transazione di un blocco di codice inserendo in modo implicito le connessioni in una transazione distribuita. È necessario chiamare il metodo **Complete** alla fine del blocco di codice contrassegnato da **TransactionScope**. Il **metodo Dispose** viene richiamato quando l'esecuzione del programma lascia un blocco di codice, causando la sospensione della transazione se il metodo **Complete** non viene chiamato. Se è stata generata un'eccezione che determina l'uscita del codice dall'ambito, la transazione non viene più utilizzata.  
  
 È consigliabile utilizzare un blocco **using** per assicurarsi che il metodo **Dispose** venga chiamato sull'oggetto **TransactionScope** quando il blocco **using** viene chiuso. Il mancato commit o il rollback delle transazioni in sospeso può ridurre seriamente le prestazioni perché il timeout predefinito per **TransactionScope** è di un minuto. Se non si utilizza **un'istruzione using,** è necessario eseguire tutte le operazioni in un blocco **Try** e chiamare in modo esplicito il metodo **Dispose** nel blocco **Finally.**  
  
 Se si verifica un'eccezione all'interno di **TransactionScope**, la transazione viene contrassegnata come incoerente e viene abbandonata. Viene eseguito il rollback quando il **TransactionScope** viene eliminato. Se non si verifica alcuna eccezione, viene eseguito il commit delle transazioni partecipanti.  
  
 **TransactionScope** deve essere utilizzato solo quando si accede a origini dati locali e remote o gestori di risorse esterni. Ciò è dovuto al fatto che **TransactionScope** determina sempre la promozione delle transazioni, anche se viene utilizzato solo all'interno di una connessione di contesto.  
  
> [!NOTE]  
>  La classe **TransactionScope** crea una transazione con **System.Transactions.Transaction.IsolationLevel** di **Serializable** per impostazione predefinita. A seconda dell'applicazione, è possibile abbassare il livello di isolamento per evitare che si verifichi un numero elevato di contese.  
  
> [!NOTE]  
>  È consigliabile eseguire solo aggiornamenti, inserimenti ed eliminazioni all'interno di transazioni distribuite sui server remoti in quanto tali operazioni comportano un notevole consumo di risorse del database. Se l'operazione viene effettuata sul server locale, non è necessario eseguire una transazione distribuita ed è sufficiente una transazione locale. Le istruzioni SELECT potrebbero bloccare inutilmente risorse del database e in alcuni scenari può essere necessario utilizzare le transazioni per le operazioni di selezione. Tutto il lavoro che non riguarda il database deve essere svolto all'esterno dell'ambito della transazione, a meno che non coinvolga altri gestori di risorse inclusi nella transazione. Sebbene un'eccezione nell'ambito della transazione impedisca il commit della transazione, la classe **TransactionScope** non prevede il rollback delle modifiche apportate dal codice all'esterno dell'ambito della transazione stessa. Se è necessario eseguire un'azione quando viene eseguito il rollback della transazione, è necessario scrivere la propria implementazione dell'interfaccia **System.Transactions.IEnlistmentNotification** ed eseguire l'iscrizione esplicita nella transazione.  
  
## <a name="example"></a>Esempio  
 Per utilizzare **System.Transactions**, è necessario disporre di un riferimento al file System.Transactions.dll.  
  
 Nel codice seguente viene illustrato come creare una transazione che può essere promossa su due istanze diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Queste istanze sono rappresentate da due diversi **oggetti System.Data.SqlClient.SqlConnection,** di cui viene eseguito il wrapping in un blocco **TransactionScope.** Il codice crea il **transactionScope** blocco con un **using** istruzione e apre la prima connessione, che lo inserisce automaticamente nel **TransactionScope**. La transazione viene integrata inizialmente come transazione lightweight, non come transazione completamente distribuita. Il codice presuppone l'esistenza della logica condizionale, omessa per brevità. Apre la seconda connessione solo se è necessaria, inserirla in **TransactionScope**. Quando la connessione è aperta, la transazione viene promossa automaticamente a una transazione completamente distribuita. Il codice richiama quindi **TransactionScope.Complete**, che esegue il commit della transazione. Il codice elimina le due connessioni quando si esce dalle istruzioni **using** per le connessioni. Il metodo **TransactionScope.Dispose** per **TransactionScope** viene chiamato automaticamente alla chiusura del blocco **using** per **TransactionScope**. Se è stata generata un'eccezione in qualsiasi punto del blocco **TransactionScope,** **Complete** non viene chiamato e la transazione distribuita verrà eseguito il rollback quando **il TransactionScope** viene eliminato.  
  
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
  
  
