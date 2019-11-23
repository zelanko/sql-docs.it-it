---
title: Cmdlet Invoke-Sqlcmd | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- PowerShell [SQL Server], Invoke-Sqlcmd
- Cmdlets [SQL Server], Invoke-Sqlcmd
- Invoke-Sqlcmd cmdlet
- sqlcmd utility, PowerShell
ms.assetid: 0c74d21b-84a5-4fa4-be51-90f0f7230044
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c6aff97c8bee8fe8ccc469c2ee57bc94466e1e31
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797863"
---
# <a name="invoke-sqlcmd-cmdlet"></a>Cmdlet Invoke-Sqlcmd
  **Invoke-Sqlcmd** è un cmdlet di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che esegue script contenenti istruzioni provenienti dai linguaggi ([!INCLUDE[tsql](../includes/tsql-md.md)] e XQuery) e dai comandi supportati dall'utilità **sqlcmd**.  
  
## <a name="using-invoke-sqlcmd"></a>Utilizzo di Invoke-Sqlcmd  
 Il cmdlet **Invoke-Sqlcmd** consente di eseguire file di script **sqlcmd** in un ambiente Windows PowerShell. Molte delle operazioni consentite da **sqlcmd** possono essere eseguite anche tramite il cmdlet **Invoke-Sqlcmd**.  
  
 In questo esempio il cmdlet Invoke-Sqlcmd viene chiamato per eseguire una query semplice, analoga a **sqlcmd** con le opzioni **-Q** e **-S** :  
  
```powershell
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance"  
```  
  
 In questo esempio il cmdlet **Invoke-Sqlcmd**viene chiamato specificando un file di input e inviando il pipe a un file, analogamente a quando si specifica **sqlcmd** con le opzioni **-i** e **-o** :  
  
```powershell
Invoke-Sqlcmd -InputFile "C:\MyFolder\TestSQLCmd.sql" | Out-File -FilePath "C:\MyFolder\TestSQLCmd.rpt"  
```  
  
 In questo esempio una matrice di Windows PowerShell viene usata per passare più variabili di scripting **sqlcmd** a **Invoke-Sqlcmd**. Per i caratteri "$" che identificano le variabili di scripting **sqlcmd** nell'istruzione SELECT è stato usato il carattere di escape di PowerShell "`" (apice inverso):  
  
```powershell
$MyArray = "MyVar1 = 'String1'", "MyVar2 = 'String2'"  
Invoke-Sqlcmd -Query "SELECT `$(MyVar1) AS Var1, `$(MyVar2) AS Var2;" -Variable $MyArray  
```  
  
 In questo esempio il provider [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per Windows PowerShell viene usato per passare a un'istanza del [!INCLUDE[ssDE](../includes/ssde-md.md)], quindi viene usato il cmdlet **Get-Item** di Windows PowerShell per recuperare un oggetto server SMO per l'istanza e passarlo a **Invoke-Sqlcmd**:  
  
```powershell
Set-Location SQLSERVER:\SQL\MyComputer\MyInstance  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance (Get-Item .)  
```  
  
 Il parametro -Query è un parametro basato sulla posizione e non deve essere denominato. Se la prima stringa passata a **Invoke-Sqlcmd**è senza nome, viene trattata come parametro -Query.  
  
```powershell
Invoke-Sqlcmd "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance"  
```  
  
## <a name="path-context-in-invoke-sqlcmd"></a>Contesto del percorso in Invoke-Sqlcmd  
 Se non si utilizza il parametro -Database, il contesto del database per Invoke-Sqlcmd viene impostato dal percorso che è attivo al momento della chiamata di cmdlet.  
  
|percorso|Contesto del database|  
|----------|----------------------|  
|Inizia con un'unità diversa da SQLSERVER:|Il database predefinito per l'ID di accesso nell'istanza predefinita nel computer locale.|  
|SQLSERVER:\SQL|Il database predefinito per l'ID di accesso nell'istanza predefinita nel computer locale.|  
|SQLSERVER:\SQL\NomeComputer|Il database predefinito per l'ID di accesso nell'istanza predefinita nel computer specificato.|  
|SQLSERVER:\SQL\NomeComputer\NomeIstanza|Il database predefinito per l'ID di accesso nell'istanza specificata nel computer specificato.|  
|SQLSERVER:\SQL\NomeComputer\NomeIstanza\\Database|Il database predefinito per l'ID di accesso nell'istanza specificata nel computer specificato.|  
|SQLSERVER:\SQL\NomeComputer\NomeIstanza\\Database\NomeDatabase|Il database specificato nell'istanza specificata nel computer specificato. Vale anche per i percorsi più lunghi, ad esempio un percorso che specifica il nodo Tabelle e Colonne all'interno di un database.|  
  
 Ad esempio, si supponga che il database predefinito per l'account di Windows nell'istanza predefinita del computer locale sia master. I seguenti comandi restituirebbero master:  
  
```powershell
Set-Location SQLSERVER:\SQL  
Invoke-Sqlcmd "SELECT DB_NAME() AS DatabaseName;"  
```  
  
 I seguenti comandi restituirebbero [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]:  
  
```powershell
Set-Location SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Person  
Invoke-Sqlcmd "SELECT DB_NAME() AS DatabaseName;"  
```  
  
 Tramite Invoke-Sqlcmd viene visualizzato un avviso quando viene utilizzato il contesto del database per il percorso. È possibile utilizzare il parametro -SuppressProviderContextWarning per disattivare il messaggio di avviso. Il parametro -IgnoreProviderContext può essere utilizzato per indicare a Invoke-Sqlcmd di utilizzare sempre il database predefinito per l'accesso.  
  
## <a name="comparing-invoke-sqlcmd-and-the-sqlcmd-utility"></a>Confronto tra Invoke-Sqlcmd e l'utilità sqlcmd  
 Il cmdlet**Invoke-Sqlcmd** può essere usato per eseguire molti degli script eseguibili tramite l'utilità **sqlcmd** . Il cmdlet **Invoke-Sqlcmd** viene tuttavia eseguito in un ambiente Windows PowerShell diverso dall'ambiente del prompt dei comandi in cui viene eseguito **sqlcmd** . Il comportamento di **Invoke-Sqlcmd** è stato modificato per l'uso in un ambiente Windows PowerShell.  
  
 Non tutti i comandi **sqlcmd** sono implementati in **Invoke-Sqlcmd**. I comandi non implementati sono: **:!!** , **:connect**, **:error**, **:out**, **:ed**, **:list**, **:listvar**, **:reset**, **:perftrace**e **:serverlist**.  
  
 Il cmdlet**Invoke-Sqlcmd** non inizializza l'ambiente o le variabili di scripting di **sqlcmd** , ad esempio SQLCMDDBNAME o SQLCMDWORKSTATION.  
  
 Il cmdlet**Invoke-Sqlcmd** non visualizza i messaggi, ad esempio l'output di istruzioni PRINT, a meno che non venga specificato il parametro comune **-Verbose** di Windows PowerShell. Ad esempio:  
  
```powershell
Invoke-Sqlcmd -Query "PRINT N'abc';" -Verbose  
```  
  
 In un ambiente PowerShell non sono necessari tutti i parametri **sqlcmd** . Windows PowerShell, ad esempio, formatta tutto l'output dei cmdlet, pertanto i parametri **sqlcmd** che specificano le opzioni di formattazione non vengono implementati in **Invoke-Sqlcmd**. Nella tabella seguente viene specificata la relazione tra i parametri di **Invoke-Sqlcmd** e le opzioni **sqlcmd** :  
  
|Descrizione|Opzione sqlcmd|Parametro Invoke-Sqlcmd|  
|-----------------|-------------------|------------------------------|  
|Nome server e istanza.|-S|-ServerInstance|  
|Database iniziale da utilizzare.|-d|-Database|  
|Esegue la query specificata ed esce.|-Q|-Query|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|-U|-Username|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|-p|-Password|  
|Definizione della variabile.|-v|-Variable|  
|Intervallo di timeout della query.|-t|-QueryTimeout|  
|Arresta l'esecuzione in caso di errore|-b|-AbortOnError|  
|Connessione amministrativa dedicata.|-a|-DedicatedAdministratorConnection|  
|Disabilita i comandi interattivi, gli script di avvio e le variabili di ambiente.|-x|-DisableCommands|  
|Disabilita la sostituzione delle variabili.|-x|-DisableVariables|  
|Livello minimo di gravità da segnalare.|-v|-SeverityLevel|  
|Livello minimo di errore da segnalare.|-m|-ErrorLevel|  
|Intervallo di timeout di accesso.|-l|-ConnectionTimeout|  
|Nome host.|-h|-HostName|  
|Consente di modificare la password e di uscire.|-Z|-NewPassword|  
|File di input che contiene una query.|-i|-InputFile|  
|Lunghezza massima dell'output di caratteri.|-w|-MaxCharLength|  
|Lunghezza massima dell'output binario.|-w|-MaxBinaryLength|  
|Stabilisce la connessione utilizzando la crittografia SSL.|Nessun parametro|-EncryptConnection|  
|Visualizza gli errori|Nessun parametro|-OutputSqlErrors|  
|Esegue l'output dei messaggi in stderr.|-r|Nessun parametro|  
|Utilizza le impostazioni locali del client|-r|Nessun parametro|  
|Esegue la query specificata e rimane in esecuzione.|-q|Nessun parametro|  
|Tabella codici da utilizzare per i dati di output.|-f|Nessun parametro|  
|Modifica una password e rimane in esecuzione|-Z|Nessun parametro|  
|Dimensioni pacchetto|-a|Nessun parametro|  
|Separatore delle colonne|-s|Nessun parametro|  
|Controlla le intestazioni di output|-H|Nessun parametro|  
|Specifica i caratteri di controllo|-k|Nessun parametro|  
|Larghezza visualizzazione lunghezza fissa|-y|Nessun parametro|  
|Larghezza visualizzazione lunghezza variabile|-y|Nessun parametro|  
|Echo input|-E|Nessun parametro|  
|Abilita gli identificatori delimitati|-I|Nessun parametro|  
|Rimuove gli spazi finali|-W|Nessun parametro|  
|Elenca le istanze|-L|Nessun parametro|  
|Imposta il formato dell'output come Unicode|-U|Nessun parametro|  
|Stampa statistiche|-p|Nessun parametro|  
|Fine comando|-c|Nessun parametro|  
|Stabilisce la connessione utilizzando l'autenticazione di Windows|-E|Nessun parametro|  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di cmdlet del motore di database](../../2014/database-engine/use-the-database-engine-cmdlets.md)   
 [Utilità sqlcmd](../tools/sqlcmd-utility.md)   
 [Utilizzo dell'utilità sqlcmd](../relational-databases/scripting/sqlcmd-use-the-utility.md)  
