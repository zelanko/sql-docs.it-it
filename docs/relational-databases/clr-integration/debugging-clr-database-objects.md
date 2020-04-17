---
title: Debug di oggetti di database CLR - Documenti Microsoft
description: SQL ServerSQL Server fornisce il supporto per il debug di oggetti Transact-SQLTransact-SQL e CLR nel database che integra il debugger di SQL Server con il debugger di Microsoft Visual Studio.
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
ms.openlocfilehash: 71a766dc473c1bef47a8104ae76c0e70bd8b31b8
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488397"
---
# <a name="debugging-clr-database-objects"></a>Debug di oggetti di database CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] offre il supporto per il debug di oggetti CLR (Common Language Runtime) e [!INCLUDE[tsql](../../includes/tsql-md.md)] nel database. Gli aspetti principali del debug in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono la facilità di installazione e utilizzo e l'integrazione del debugger di SQL Server con il debugger di Microsoft Visual Studio. Inoltre, il debug funziona tra linguaggi diversi. Gli utenti possono passare senza problemi agli oggetti CLR da [!INCLUDE[tsql](../../includes/tsql-md.md)] e viceversa. Il debugger Transact-SQL in SQL Server Management Studio non può essere utilizzato per eseguire il debug di oggetti di database gestiti, ma è possibile eseguire il debug degli oggetti tramite i debugger disponibili in Visual Studio. Il debug di oggetti di database gestiti in Visual Studio supporta tutte le caratteristiche di debug comuni, ad esempio l'esecuzione di istruzioni e routine all'interno di routine in esecuzione nel server. Tramite i debugger è possibile impostare punti di interruzione, controllare lo stack di chiamate, controllare le variabili e modificarne i valori durante il debug. Notare che Visual Studio .NET 2003 non può essere utilizzato per la programmazione o il debug dell'integrazione CLR. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene fornito con .NET Framework preinstallato e non è possibile utilizzare assembly di .NET Framework 2.0 in Visual Studio .NET 2003.  
  
 Per ulteriori informazioni sul debug di codice gestito tramite Visual Studio, vedere l'argomento " Debug di[codice gestito](https://go.microsoft.com/fwlink/?LinkId=120377)" nella documentazione di Visual Studio.  
  
## <a name="debugging-permissions-and-restrictions"></a>Debug di autorizzazioni e restrizioni  
 Il debug è un'operazione con privilegi elevati e pertanto solo i [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]membri del ruolo predefinito del server **sysadmin** sono autorizzati a farlo in .  
  
 Durante il debug vengono applicate le restrizioni seguenti:  
  
-   Il debug di routine CLR è limitato a un'istanza di debugger alla volta. Questa limitazione viene applicata poiché qualsiasi esecuzione di codice CLR si blocca quando viene raggiunto un punto di interruzione e non continua finché il debugger non supera il punto di interruzione. Tuttavia, è possibile continuare il debug di [!INCLUDE[tsql](../../includes/tsql-md.md)] in altre connessioni. Benché il debug di [!INCLUDE[tsql](../../includes/tsql-md.md)] non blocchi altre esecuzioni nel server, può causare l'attesa di altre connessioni mantenendo un blocco.  
  
-   Non è possibile eseguire il debug delle connessioni esistenti, ma solo di quelle nuove, poiché [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] richiede informazioni sul client e sull'ambiente del debugger prima di poter stabilire la connessione.  
  
 A causa delle restrizioni indicate sopra, si consiglia di eseguire il debug del codice [!INCLUDE[tsql](../../includes/tsql-md.md)] e di CLR in un server di prova, non in un server di produzione.  
  
## <a name="overview-of-debugging-managed-database-objects"></a>Cenni preliminari sul debug di oggetti di database gestiti  
 Il debug in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si basa su un modello per connessione. Un debugger può rilevare le attività ed eseguirne il debug solo nella connessione client a cui è connesso. Poiché la funzionalità del debugger non è limitata dal tipo di connessione, è possibile eseguire il debug sia di connessioni del flusso TDS sia di connessioni HTTP. Tuttavia, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente il debug delle connessioni esistenti. Il debug supporta tutte le caratteristiche di debug comuni all'interno di routine in esecuzione nel server. L'interazione tra un debugger e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene effettuata tramite Component Object Model (COM).  
  
 Per ulteriori informazioni e scenari sul debug di stored procedure gestite, funzioni, trigger, tipi definiti dall'utente e aggregazioni, vedere l'argomento " Debug del database di[integrazione CLR](https://go.microsoft.com/fwlink/?LinkId=120378)di SQL Server " nella documentazione di Visual Studio.  
  
 È necessario abilitare il protocollo di rete TCP/IP nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per utilizzare Visual Studio per lo sviluppo e il debug remoti. Per ulteriori informazioni sull'abilitazione del protocollo TCP/IP sul server, vedere Configurazione dei [protocolli client](../../database-engine/configure-windows/configure-client-protocols.md).  
  
#### <a name="to-debug-a-managed-database-object"></a>Per eseguire il debug di un oggetto di database gestito  
  
1.  Aprire Microsoft Visual Studio, creare un nuovo progetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e stabilire una connessione a un database in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
2.  Creare un nuovo tipo. In **Esplora soluzioni**fare clic con il pulsante destro del mouse sul progetto, scegliere **Aggiungi** e **nuovo elemento...** Nella finestra **Aggiungi nuovo elemento** selezionare Stored **procedure**, Funzione **definita dall'utente**, **Tipo definito dall'utente**, **Trigger**, **Aggregazione**o **Classe**. Specificare un nome per il file di origine del nuovo tipo e fare clic su **Aggiungi**.  
  
3.  Aggiungere il codice per il nuovo tipo nell'editor di testo. Per un codice di esempio relativo a un esempio di stored procedure, vedere la sezione più avanti in questo argomento.  
  
4.  Aggiungere uno script di test per il tipo. In **Esplora soluzioni**espandere la directory **TestScripts** doppio clic su **Test.sql** per aprire il file di origine dello script di test predefinito. Aggiungere nell'editor di testo uno script di test che richiama il codice di cui eseguire il debug. Di seguito viene fornito uno script di esempio.  
  
5.  Inserire uno o più punti di interruzione nel codice sorgente. Fare clic con il pulsante destro del mouse su una riga di codice nell'editor di testo, all'interno della funzione o della routine di cui si desidera eseguire il debug, quindi scegliere **Punto di interruzione** e Inserisci punto di **interruzione**. Il punto di interruzione viene aggiunto e la riga di codice viene evidenziata in rosso.  
  
6.  Nel **Debug** menu, selezionare **Avvia debug** per compilare, distribuire e testare il progetto. Verrà eseguito lo script di test in Test.sql e verrà richiamato l'oggetto di database gestito.  
  
7.  Quando la freccia gialla che indica il puntatore all'istruzione viene visualizzata in corrispondenza del punto di interruzione, l'esecuzione del codice viene sospesa ed è possibile avviare il debug dell'oggetto di database gestito. È possibile eseguire il **passaggio** dal menu **Debug** per far avanzare il puntatore all'istruzione alla riga di codice successiva. La finestra **Variabili locali** viene utilizzata per osservare lo stato degli oggetti attualmente evidenziati dal puntatore all'istruzione. Le variabili possono essere aggiunte alla finestra **Espressioni di controllo.** È possibile osservare lo stato delle variabili controllate durante l'intera sessione di debug, non solo quando la variabile si trova nella riga di codice attualmente evidenziata dal puntatore all'istruzione. Scegliere Continua dal menu Debug per fare avanzare il puntatore all'istruzione al successivo punto di interruzione o per completare l'esecuzione della routine se non sono presenti altri punti di interruzione.  
  
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
  
  
