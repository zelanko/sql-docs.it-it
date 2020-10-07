---
title: Eseguire il debug di oggetti di database CLR (Common Language Runtime)
description: SQL Server fornisce il supporto per il debug di oggetti Transact-SQL e CLR nell'integrazione del SQL Server debugger del database con Microsoft Visual Studio debugger.
ms.date: 10/06/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: how-to
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
ms.openlocfilehash: 2a6e723c8ad5ff8c97a3b57edb554092211da4d7
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785166"
---
# <a name="how-to-debug-clr-database-objects"></a>Come eseguire il debug di oggetti di database CLR

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre il supporto per il debug di oggetti CLR (Common Language Runtime) e [!INCLUDE[tsql](../../includes/tsql-md.md)] nel database. Gli aspetti principali del debug in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono la facilità di installazione e utilizzo e l'integrazione del debugger di SQL Server con il debugger di Microsoft Visual Studio. Inoltre, il debug funziona tra linguaggi diversi. Gli utenti possono passare senza problemi agli oggetti CLR da [!INCLUDE[tsql](../../includes/tsql-md.md)] e viceversa. Il debugger Transact-SQL in SQL Server Management Studio non può essere utilizzato per eseguire il debug di oggetti di database gestiti, ma è possibile eseguire il debug degli oggetti tramite i debugger disponibili in Visual Studio. Il debug di oggetti di database gestiti in Visual Studio supporta tutte le caratteristiche di debug comuni, ad esempio l'esecuzione di istruzioni e routine all'interno di routine in esecuzione nel server. Tramite i debugger è possibile impostare punti di interruzione, controllare lo stack di chiamate, controllare le variabili e modificarne i valori durante il debug. 

> [!NOTE]
> Visual Studio .NET 2003 non può essere utilizzato per la programmazione o il debug dell'integrazione CLR. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene fornito con .NET Framework preinstallato e non è possibile utilizzare assembly di .NET Framework 2.0 in Visual Studio .NET 2003.  
  
## <a name="debugging-permissions-and-restrictions"></a>Debug di autorizzazioni e restrizioni

Il debug è un'operazione con privilegi elevati e pertanto solo i membri del ruolo predefinito del server **sysadmin** possono eseguire questa operazione in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Durante il debug vengono applicate le restrizioni seguenti:  
  
- Il debug di routine CLR è limitato a un'istanza di debugger alla volta. Questa limitazione viene applicata poiché qualsiasi esecuzione di codice CLR si blocca quando viene raggiunto un punto di interruzione e non continua finché il debugger non supera il punto di interruzione. Tuttavia, è possibile continuare il debug di [!INCLUDE[tsql](../../includes/tsql-md.md)] in altre connessioni. Benché il debug di [!INCLUDE[tsql](../../includes/tsql-md.md)] non blocchi altre esecuzioni nel server, può causare l'attesa di altre connessioni mantenendo un blocco.  
  
- Non è possibile eseguire il debug delle connessioni esistenti, ma solo di quelle nuove, poiché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede informazioni sul client e sull'ambiente del debugger prima di poter stabilire la connessione.  
  
A causa delle restrizioni indicate sopra, si consiglia di eseguire il debug del codice [!INCLUDE[tsql](../../includes/tsql-md.md)] e di CLR in un server di prova, non in un server di produzione.  
  
## <a name="overview"></a>Panoramica

Il debug in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si basa su un modello per connessione. Un debugger può rilevare le attività ed eseguirne il debug solo nella connessione client a cui è connesso. Poiché la funzionalità del debugger non è limitata dal tipo di connessione, è possibile eseguire il debug sia di connessioni del flusso TDS sia di connessioni HTTP. Tuttavia, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente il debug delle connessioni esistenti. Il debug supporta tutte le caratteristiche di debug comuni all'interno di routine in esecuzione nel server. L'interazione tra un debugger e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene effettuata tramite Component Object Model (COM).  
  
Per ulteriori informazioni e scenari relativi al debug di stored procedure, funzioni, trigger, tipi definiti dall'utente e aggregati gestiti, vedere [SQL Server debug del database di integrazione CLR](https://go.microsoft.com/fwlink/?LinkId=120378) nella documentazione di Visual Studio.  
  
È necessario abilitare il protocollo di rete TCP/IP nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per utilizzare Visual Studio per lo sviluppo e il debug remoti. Per ulteriori informazioni sull'abilitazione del protocollo TCP/IP nel server, vedere [configure client Protocols](../../database-engine/configure-windows/configure-client-protocols.md).  
  
## <a name="debugging-steps"></a>Passaggi di debug

Per eseguire il debug di un oggetto di database CLR in Microsoft Visual Studio, attenersi alla procedura seguente:

1. Aprire Microsoft Visual Studio e creare un nuovo progetto SQL Server. È possibile usare l'istanza di SQL database locale fornita con Visual Studio.

2. Creare un nuovo tipo CLR SQL (C#):

   1. In **Esplora soluzioni**fare clic con il pulsante destro del mouse sul progetto e scegliere **Aggiungi**, **nuovo elemento...**. 
   1. Dalla finestra **Aggiungi nuovo elemento** selezionare **stored procedure SQL CLR C#**, **funzione definita dall'utente SQL CLR C#**, **tipo SQL CLR definito dall'utente**, **trigger SQL CLR**c#, **aggregazione SQL CLR c#** o **classe**.
   1. Specificare un nome per il file di origine del nuovo tipo e quindi selezionare **Aggiungi**.

3. Aggiungere il codice per il nuovo tipo nell'editor di testo. Per un esempio di codice per un stored procedure di esempio, vedere la sezione di esempio seguente in questo articolo.

4. Aggiungere uno script per il test del tipo: 

   1. In **Esplora soluzioni**fare clic con il pulsante destro del mouse sul nodo del progetto e scegliere **Aggiungi**, **script...**. 
   1. Nella finestra **Aggiungi nuovo elemento** selezionare **script (non in compilazione)** e specificare un nome, ad esempio `Test.sql` . Fare clic sul pulsante **Aggiungi**.
   1. In **Esplora soluzioni**fare doppio clic sul `Test.sql` nodo per aprire il file di origine dello script di test predefinito.
   1. Aggiungere lo script di test (uno che richiama il codice di cui eseguire il debug) nell'editor di testo. Vedere l'esempio nella sezione successiva per uno script di esempio.

5. Inserire uno o più punti di interruzione nel codice sorgente. Fare clic con il pulsante destro del mouse su una riga di codice nell'editor di testo per la funzione o la routine di cui si desidera eseguire il debug. Selezionare punto di **interruzione**, Inserisci punto di **interruzione**. Il punto di interruzione viene aggiunto e la riga di codice viene evidenziata in rosso.

6. Scegliere **Avvia debug** dal menu **debug** per compilare, distribuire e testare il progetto. Lo script di test in `Test.sql` viene eseguito e viene richiamato l'oggetto di database gestito.

7. Quando viene visualizzata la freccia gialla (che designa il puntatore all'istruzione) nel punto di interruzione, l'esecuzione del codice viene sospesa. È quindi possibile eseguire il debug dell'oggetto di database gestito:

   1. Utilizzare **Esegui istruzione/** routine dal menu **debug** per far avanzare il puntatore all'istruzione alla riga di codice successiva.
   1. Utilizzare la finestra **variabili locali** per osservare lo stato degli oggetti attualmente evidenziati dal puntatore all'istruzione.
   1. Aggiungere variabili alla finestra **espressioni di controllo** . È possibile osservare lo stato delle variabili controllate durante la sessione di debug, anche quando la variabile non si trova nella riga di codice attualmente evidenziata dal puntatore all'istruzione. 
   1. Scegliere **continua** dal menu **debug** per far avanzare il puntatore all'istruzione al punto di interruzione successivo o per completare l'esecuzione della routine se non sono presenti altri punti di interruzione.
  
## <a name="example-code"></a>Codice di esempio

Nell'esempio seguente viene restituita al chiamante la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```csharp
using System.Data.SqlClient;
using Microsoft.SqlServer.Server;

public class StoredProcedures
{
    [Microsoft.SqlServer.Server.SqlProcedure]
    public static void GetVersion()
    {
        using (var connection = new SqlConnection("context connection=true"))
        {
            connection.Open();
            var command = new SqlCommand("select @@version", connection);
            SqlContext.Pipe.ExecuteAndSend(command);
        }
    }
}
```

## <a name="example-test-script"></a>Script di test di esempio

Nello script di test seguente viene illustrato come richiamare il `GetVersion` stored procedure definito nell'esempio precedente.  
  
```sql
EXEC GetVersion  
```  

## <a name="next-steps"></a>Passaggi successivi
  
Per altre informazioni sul debug del codice gestito con Visual Studio, vedere [debug del codice gestito](https://go.microsoft.com/fwlink/?LinkId=120377) nella documentazione di Visual Studio.  

Per altre informazioni, vedere [concetti relativi alla programmazione dell'integrazione con Common Language Runtime](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
