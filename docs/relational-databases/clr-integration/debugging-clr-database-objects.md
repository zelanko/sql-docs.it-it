---
title: Debug di oggetti di Database CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- database objects [CLR integration], debugging
- permissions [CLR integration]
- debugging [CLR integration]
- building database objects [CLR integration], debugging
- common language runtime [SQL Server], debugging
ms.assetid: 1332035c-d6ed-424d-8234-46ad21168319
author: rothja
ms.author: jroth
ms.openlocfilehash: d8dfd76558b4cf6c476849c4f2a41bfdb1f6d28b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118555"
---
# <a name="debugging-clr-database-objects"></a>Debug di oggetti di database CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre il supporto per il debug di oggetti CLR (Common Language Runtime) e [!INCLUDE[tsql](../../includes/tsql-md.md)] nel database. Gli aspetti principali del debug in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono la facilità di installazione e utilizzo e l'integrazione del debugger di SQL Server con il debugger di Microsoft Visual Studio. Inoltre, il debug funziona tra linguaggi diversi. Gli utenti possono passare senza problemi agli oggetti CLR da [!INCLUDE[tsql](../../includes/tsql-md.md)] e viceversa. Il debugger Transact-SQL in SQL Server Management Studio non può essere utilizzato per eseguire il debug di oggetti di database gestiti, ma è possibile eseguire il debug degli oggetti tramite i debugger disponibili in Visual Studio. Il debug di oggetti di database gestiti in Visual Studio supporta tutte le caratteristiche di debug comuni, ad esempio l'esecuzione di istruzioni e routine all'interno di routine in esecuzione nel server. Tramite i debugger è possibile impostare punti di interruzione, controllare lo stack di chiamate, controllare le variabili e modificarne i valori durante il debug. Notare che Visual Studio .NET 2003 non può essere utilizzato per la programmazione o il debug dell'integrazione CLR. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene fornito con .NET Framework preinstallato e non è possibile utilizzare assembly di .NET Framework 2.0 in Visual Studio .NET 2003.  
  
 Per altre informazioni sul debug del codice gestito tramite Visual Studio, vedere la "[Debugging Managed Code](https://go.microsoft.com/fwlink/?LinkId=120377)" argomento nella documentazione di Visual Studio.  
  
## <a name="debugging-permissions-and-restrictions"></a>Debug di autorizzazioni e restrizioni  
 Il debug è un'operazione con privilegiata elevati, pertanto solo i membri del **sysadmin** ruolo predefinito del server possono eseguire questa operazione nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Durante il debug vengono applicate le restrizioni seguenti:  
  
-   Il debug di routine CLR è limitato a un'istanza di debugger alla volta. Questa limitazione viene applicata poiché qualsiasi esecuzione di codice CLR si blocca quando viene raggiunto un punto di interruzione e non continua finché il debugger non supera il punto di interruzione. Tuttavia, è possibile continuare il debug di [!INCLUDE[tsql](../../includes/tsql-md.md)] in altre connessioni. Benché il debug di [!INCLUDE[tsql](../../includes/tsql-md.md)] non blocchi altre esecuzioni nel server, può causare l'attesa di altre connessioni mantenendo un blocco.  
  
-   Non è possibile eseguire il debug delle connessioni esistenti, ma solo di quelle nuove, poiché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede informazioni sul client e sull'ambiente del debugger prima di poter stabilire la connessione.  
  
 A causa delle restrizioni indicate sopra, si consiglia di eseguire il debug del codice [!INCLUDE[tsql](../../includes/tsql-md.md)] e di CLR in un server di prova, non in un server di produzione.  
  
## <a name="overview-of-debugging-managed-database-objects"></a>Cenni preliminari sul debug di oggetti di database gestiti  
 Il debug in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si basa su un modello per connessione. Un debugger può rilevare le attività ed eseguirne il debug solo nella connessione client a cui è connesso. Poiché la funzionalità del debugger non è limitata dal tipo di connessione, è possibile eseguire il debug sia di connessioni del flusso TDS sia di connessioni HTTP. Tuttavia, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente il debug delle connessioni esistenti. Il debug supporta tutte le caratteristiche di debug comuni all'interno di routine in esecuzione nel server. L'interazione tra un debugger e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene effettuata tramite Component Object Model (COM).  
  
 Per altre informazioni e scenari relativi al debug gestite stored procedure, funzioni, trigger, tipi definiti dall'utente e aggregazioni, vedere la "[debug di SQL Server CLR Integration Database](https://go.microsoft.com/fwlink/?LinkId=120378)" argomento in di Visual Studio documentazione.  
  
 È necessario abilitare il protocollo di rete TCP/IP nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per utilizzare Visual Studio per lo sviluppo e il debug remoti. Per altre informazioni su come abilitare il protocollo TCP/IP nel server, vedere [Configure Client Protocols](../../database-engine/configure-windows/configure-client-protocols.md).  
  
#### <a name="to-debug-a-managed-database-object"></a>Per eseguire il debug di un oggetto di database gestito  
  
1.  Aprire Microsoft Visual Studio, creare un nuovo progetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e stabilire una connessione a un database in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Creare un nuovo tipo. Nelle **Esplora soluzioni**, fare clic sul progetto, selezionare **Add** e **nuovo elemento...** Dal **Aggiungi nuovo elemento** finestra, seleziona **Stored Procedure**, **funzione definita dall'utente**, **tipo definito dall'utente**,  **Trigger**, **aggregazione**, o **classe**. Specificare un nome per il file di origine del nuovo tipo e fare clic su **Add**.  
  
3.  Aggiungere il codice per il nuovo tipo nell'editor di testo. Per un codice di esempio relativo a un esempio di stored procedure, vedere la sezione più avanti in questo argomento.  
  
4.  Aggiungere uno script di test per il tipo. Nelle **Esplora soluzioni**, espandere il **TestScripts** directory fare doppio clic su **test** per aprire il file di origine script di test predefinito. Aggiungere nell'editor di testo uno script di test che richiama il codice di cui eseguire il debug. Di seguito viene fornito uno script di esempio.  
  
5.  Inserire uno o più punti di interruzione nel codice sorgente. Fare clic su una riga di codice nell'editor di testo, all'interno della funzione o routine che si desidera eseguire il debug, e selezionare **punto di interruzione** e **Inserisci punto di interruzione**. Il punto di interruzione viene aggiunto e la riga di codice viene evidenziata in rosso.  
  
6.  Nel **Debug** dal menu **Avvia debug** per compilare, distribuire e testare il progetto. Verrà eseguito lo script di test in Test.sql e verrà richiamato l'oggetto di database gestito.  
  
7.  Quando la freccia gialla che indica il puntatore all'istruzione viene visualizzata in corrispondenza del punto di interruzione, l'esecuzione del codice viene sospesa ed è possibile avviare il debug dell'oggetto di database gestito. È possibile **Esegui istruzione/routine** dalle **Debug** menu per far avanzare il puntatore all'istruzione per la riga successiva del codice. Il **variabili locali** finestra consente di osservare lo stato degli oggetti attualmente evidenziati dal puntatore all'istruzione. È possibile aggiungere variabili per il **Watch** finestra. È possibile osservare lo stato delle variabili controllate durante l'intera sessione di debug, non solo quando la variabile si trova nella riga di codice attualmente evidenziata dal puntatore all'istruzione. Scegliere Continua dal menu Debug per fare avanzare il puntatore all'istruzione al successivo punto di interruzione o per completare l'esecuzione della routine se non sono presenti altri punti di interruzione.  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente viene restituita al chiamante la versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 C#  
  
```  
using System;  
using System.Data;  
using System.Data.SqlTypes;  
using System.Data.SqlClient;  
using Microsoft.SqlServer.Server;   
  
public class StoredProcedures   
{  
   [Microsoft.SqlServer.Server.SqlProcedure]  
   public static void GetVersion()  
   {  
   using(SqlConnection connection = new SqlConnection("context connection=true"))   
   {  
      connection.Open();  
      SqlCommand command = new SqlCommand("select @@version",  
                                           connection);  
      SqlContext.Pipe.ExecuteAndSend(command);  
      }  
   }  
}  
```  
  
 Visual Basic  
  
```  
Imports System  
Imports System.Data  
Imports System.Data.Sql  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlClient  
  
Partial Public Class StoredProcedures   
    <Microsoft.SqlServer.Server.SqlProcedure> _  
    Public Shared Sub GetVersion()  
        Using connection As New SqlConnection("context connection=true")  
            connection.Open()  
            Dim command As New SqlCommand("SELECT @@VERSION", connection)  
            SqlContext.Pipe.ExecuteAndSend(command)  
        End Using  
    End Sub  
End Class  
```  
  
 Di seguito viene fornito uno script di test che richiama la stored procedure GetVersion definita sopra.  
  
```  
EXEC GetVersion  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Concetti relativi alla programmazione dell'integrazione con CLR &#40;Common Language Runtime&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  
