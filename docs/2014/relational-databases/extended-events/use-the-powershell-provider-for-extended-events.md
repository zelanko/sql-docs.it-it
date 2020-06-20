---
title: Usare il provider PowerShell per eventi estesi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], xevent
- extended events [SQL Server], PowerShell
- PowerShell [SQL Server], extended events
ms.assetid: 0b10016f-a479-4444-a484-46cb4677cf64
author: rothja
ms.author: jroth
ms.openlocfilehash: 4cdb785a5a053e0b839386c5fbb57e9393f5b9dc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050924"
---
# <a name="use-the-powershell-provider-for-extended-events"></a>Utilizzare il provider PowerShell per eventi estesi
  È possibile gestire eventi estesi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite il provider PowerShell per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La sottocartella XEvent è disponibile all'interno dell'unità SQLSERVER. È possibile accedere alla cartella utilizzando uno dei metodi seguenti:  
  
-   Al prompt dei comandi digitare `sqlps` e quindi premere INVIO. Digitare `cd xevent` e quindi premere INVIO. Da qui è possibile usare il **CD** e i `dir` comandi (oppure i cmdlet **set-location** e **Get-ChildItem** ) per passare al nome del server e al nome dell'istanza.  
  
-   In Esplora oggetti espandere il nome dell'istanza, espandere **Gestione**, fare clic con il pulsante destro del mouse su **Eventi estesi**, quindi scegliere **Avvia PowerShell**. Verrà avviato PowerShell nel percorso seguente:  
  
     PS SqlServer: \ XEvent \\ *nomeserver* \\ *NomeIstanza*>  
  
    > [!NOTE]  
    >  È possibile avviare PowerShell da qualsiasi nodo all'interno di **Eventi estesi**. È possibile, ad esempio, fare clic con il pulsante destro del mouse su **Sessioni**e quindi scegliere **Avvia PowerShell**. Verrà avviato PowerShell a un livello più interno, nella cartella Sessioni.  
  
 È possibile esplorare l'albero delle cartelle XEvent per visualizzare sessioni di eventi estesi esistenti e i relativi eventi, database di destinazione e predicati associati. Ad esempio, dal percorso PS SqlServer: \ XEvent \\ *nomeserver* \\ *NomeIstanza*> digitare, `cd sessions` premere INVIO, digitare `dir` e quindi premere INVIO. è possibile visualizzare l'elenco delle sessioni archiviate in tale istanza. È inoltre possibile visualizzare se la sessione è in esecuzione, e in tal caso per quanto tempo, e se la sessione è configurata per l'avvio all'avvio dell'istanza.  
  
 Per visualizzare gli eventi, i relativi predicati e i database di destinazione associati a una sessione, è possibile passare alla directory con il nome della sessione e quindi visualizzare la cartella degli eventi o dei database di destinazione. Ad esempio, per visualizzare gli eventi e i relativi predicati associati alla sessione di integrità del sistema predefinita, dal percorso PS SqlServer: \ XEvent \\ *ServerName* \\ *NomeIstanza*\Sessions> digitare `cd system_health\events,` premi invio, digitare `dir` e quindi premere INVIO.  
  
 Il provider PowerShell per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è uno strumento potente che consente di creare, modificare e gestire sessioni di eventi estesi. Nella sezione seguente vengono forniti alcuni esempi di base dell'utilizzo di script di PowerShell con eventi estesi.  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti notare quanto segue:  
  
-   Gli script devono essere eseguiti dal prompt PS SQLSERVER: \\> (disponibile digitando `sqlps` al prompt dei comandi).  
  
-   Gli script utilizzano l'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   È necessario salvare gli script con estensione ps1.  
  
-   I criteri di esecuzione di PowerShell devono consentire l'esecuzione dello script. Per impostare i criteri di esecuzione, usare il cmdlet **Set-Executionpolicy** (per altre informazioni, digitare `get-help set-executionpolicy -detailed`, quindi premere INVIO).  
  
 Nello script seguente viene creata una nuova sessione denominata 'TestSession'.  
  
```powershell
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = New-Object Microsoft.SqlServer.Management.XEvent.Session -ArgumentList $store, "TestSession"  
$event = $session.AddEvent("sqlserver.file_written")  
$event.AddAction("package0.callstack")  
$session.Create()  
```  
  
 Nello script seguente viene aggiunta la destinazione del buffer circolare alla sessione creata nell'esempio precedente. In questo esempio si illustra l'utilizzo del metodo `Alter`. Tenere presente che è possibile aggiungere la destinazione quando si crea la sessione per la prima volta.  
  
```powershell
#Script to alter a session.  
cd XEvent  
$h = hostname  
cd $h  
cd DEFAULT\Sessions  
  
#Used to find the specified session.  
$session = dir | where {$_.Name -eq 'TestSession'}  
  
#Add the ring buffer target and call the Alter method.  
$session.AddTarget("package0.ring_buffer")  
$session.Alter()  
```  
  
 Nello script seguente viene creata una nuova sessione in cui è utilizzata un'espressione di predicato. In questo caso la sessione raccoglie informazioni per il momento in cui verrà scritto il file c:\temp.log tramite l'evento sqlserver.file_written.  
  
```powershell
#Script for creating a session.  
cd XEvent  
$h = hostname  
cd $h  
  
#Use the default instance.  
$store = dir | where {$_.DisplayName -ieq 'default'}  
$session = New-Object Microsoft.SqlServer.Management.XEvent.Session -ArgumentList $store, "TestSession2"  
$event = $session.AddEvent("sqlserver.file_written")  
  
#Construct a predicate "equal_i_unicode_string(path, N'c:\temp.log')".  
$column = $store.SqlServerPackage.EventInfoSet["file_written"].DataEventColumnInfoSet["path"]  
$operand = new-object Microsoft.SqlServer.Management.XEvent.PredOperand -argumentlist $column  
$value = new-object Microsoft.SqlServer.Management.XEvent.PredValue -argumentlist "c:\temp.log"  
$compare = $store.Package0Package.PredCompareInfoSet["equal_i_unicode_string"]  
$predicate = new-object Microsoft.SqlServer.Management.XEvent.PredFunctionExpr -ArgumentList $compare, $operand, $value  
$event.SetPredicate($predicate)  
$session.Create()  
```  
  
## <a name="security"></a>Sicurezza  
 Per creare, modificare o eliminare una sessione di eventi estesi, è necessario disporre dell'autorizzazione ALTER ANY EVENT SESSION.  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server PowerShell](../../powershell/sql-server-powershell.md)   
 [Usare la sessione di system_health](use-the-ssms-xe-profiler.md)   
 [Strumenti degli eventi estesi](extended-events-tools.md)  
