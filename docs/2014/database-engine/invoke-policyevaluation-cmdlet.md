---
title: Cmdlet Invoke-PolicyEvaluation | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, Invoke-PolicyEvaluation
- Policy-Based Management, PowerShell
- Invoke-PolicyEvaluation cmdlet
- Cmdlets [SQL Server], Invoke-PolicyEvaluation
- PowerShell [SQL Server], Invoke-PolicyEvaluation
ms.assetid: 3e6d4f5a-59b7-4203-b95a-f7e692c0f131
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c1239d2dea1a4f73b54f78345f769c9550c262b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66064689"
---
# <a name="invoke-policyevaluation-cmdlet"></a>cmdlet Invoke-PolicyEvaluation
  **Invoke-PolicyEvaluation** è un cmdlet di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] che segnala se un set di destinazioni di oggetti di SQL Server è conforme alle condizioni specificate in uno o più criteri della gestione basata su criteri.  
  
## <a name="using-invoke-policyevaluation"></a>Utilizzo di Invoke-PolicyEvaluation  
 **Invoke-PolicyEvaluation** valuta uno o più criteri rispetto a un set di oggetti di SQL Server denominato set di destinazioni. Il set di oggetti di destinazione proviene da un server di destinazione. I criteri definiscono delle condizioni, che sono gli stati consentiti per gli oggetti di destinazione. Ad esempio, i criteri **Database con proprietà trustworthy** dichiarano che la proprietà di database TRUSTWORTHY deve essere impostata su OFF.  
  
 Il parametro **-AdHocPolicyEvaluationMode** specifica le azioni intraprese:  
  
 Controlla  
 Consente di segnalare lo stato di conformità degli oggetti di destinazione utilizzando le credenziali dell'accesso corrente. Non riconfigura alcun oggetto. Si tratta dell'impostazione predefinita.  
  
 CheckSqlScriptAsProxy  
 Consente di segnalare lo stato di conformità degli oggetti di destinazione usando le credenziali dell'accesso proxy **##MS_PolicyTSQLExecutionLogin##** . Non riconfigura alcun oggetto.  
  
 Configura  
 Consente di segnalare lo stato di conformità degli oggetti di destinazione utilizzando le credenziali dell'accesso corrente. Riconfigura qualsiasi opzione deterministica e configurabile che non è conforme ai criteri.  
  
## <a name="specifying-polices"></a>Definizione di criteri  
 La modalità utilizzata per specificare i criteri dipende dalla posizione di archiviazione dei criteri. I criteri possono essere archiviati in due formati:  
  
-   Possono essere oggetti archiviati in un archivio criteri, ad esempio un'istanza del Motore di database. È possibile utilizzare la cartella SQLSERVER:\SQLPolicy per specificare il percorso di criteri in un archivio criteri. È possibile utilizzare i cmdlet di Windows PowerShell per filtrare i criteri di input in base alle relative proprietà, ad esempio utilizzando Where-Object per applicare il filtro in base alla categoria di criteri oppure Get-Item per applicare il filtro in base al nome dei criteri.  
  
-   I criteri possono essere esportati come file XML. È possibile utilizzare un'unità del file system, ad esempio D:, per specificare il percorso dei file XML. È possibile utilizzare i cmdlet di Windows PowerShell, ad esempio Where-Object, per filtrare i criteri in base alle proprietà dei file, ad esempio il nome del file.  
  
 Se i criteri vengono archiviati in un archivio criteri, è necessario passare un set di oggetti PSObject che punta ai criteri da valutare. Questo avviene in genere inoltrando tramite pipe a **Invoke-PolicyEvaluation**l'output di un cmdlet, ad esempio Get-Item, e non richiede la specifica del parametro **-Policy** . Ad esempio, se sono stati importati i criteri delle procedure consigliate Microsoft nell'istanza del motore di database, questo comando valuta i criteri **Stato del database** :  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Get-Item "Database Status" | Invoke-PolicyEvaluation -TargetServerName "MYCOMPUTER"  
```  
  
 Questo esempio illustra l'uso di Where-Object per filtrare più criteri da un archivio criteri in base alla relativa proprietà **PolicyCategory** . Gli oggetti dall'output inoltrato tramite pipe di **Where-Object** vengono usati da **Invoke-PolicyEvaluation**.  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
gci | Where-Object {$_.PolicyCategory -eq "Microsoft Best Practices: Maintenance"} | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
 Se i criteri sono archiviati come file XML, è necessario usare il parametro **-Policy** per specificare il percorso e il nome per tutti i criteri. Se non si specifica un percorso nel parametro **-Policy** , **Invoke-PolicyEvaulation** usa l'impostazione corrente del percorso **sqlps** . Ad esempio, questo comando valuta uno dei criteri di Procedura consigliata di Microsoft installato con SQL Server rispetto al database predefinito per l'accesso:  
  
```  
Invoke-PolicyEvaluation -Policy "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033\Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 Questo comando consente di eseguire la stessa operazione, solo che usa il percorso **sqlps** corrente per stabilire il percorso del file XML dei criteri:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MYCOMPUTER"  
```  
  
 Questo esempio illustra l'uso del cmdlet **Get-ChildItem** per recuperare più file XML di criteri e inoltrare tramite pipe gli oggetti in **Invoke-PolicyEvaluation**:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
gci "Database Status.xml", "Trustworthy Database.xml" | Invoke-PolicyEvaluation -TargetServer "MYCOMPUTER"  
```  
  
## <a name="specifying-the-target-set"></a>Specifica del set di destinazioni  
 Utilizzare tre parametri per specificare il set di oggetti di destinazione:  
  
-   **-TargetServerName** consente di specificare l'istanza di SQL Server che contiene gli oggetti di destinazione. È possibile specificare le informazioni in una stringa che utilizza il formato definito per la proprietà ConnectionString della classe <xref:System.Data.SqlClient.SqlConnection> . È possibile usare la classe <xref:System.Data.SqlClient.SqlConnectionStringBuilder> per compilare una stringa di connessione con formato corretto. È inoltre possibile creare un oggetto <xref:Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection> e passarlo a **-TargetServer**. Se si specifica una stringa che contiene solo il nome del server, **Invoke-PolicyEvaluation** userà l'autenticazione di Windows per connettersi al server.  
  
-   **-TargetObjects** accetta un oggetto o una matrice di oggetti che rappresenta gli oggetti di SQL Server nel set di destinazioni. È possibile ad esempio creare una matrice di oggetti di classe <xref:Microsoft.SqlServer.Management.Smo.Database> da passare in **-TargetObjects**.  
  
-   **-TargetExpressions** consente di prendere una stringa contenente un'espressione di query che specifica gli oggetti nel set di destinazioni. L'espressione di query è nel formato di nodi separati dal carattere barra (/). Ogni nodo è nel formato ObjectType[Filter]. ObjectType è uno degli oggetti in una gerarchia di oggetti SMO (SQL Server Management Objects). Filter è un'espressione che filtra gli oggetti in corrispondenza di quel nodo. Per altre informazioni, vedere [Espressioni di query e Uniform Resource Name](../powershell/query-expressions-and-uniform-resource-names.md).  
  
 Specificare il parametro **-TargetObjects** o **-TargetExpression**, ma non entrambi.  
  
 In questo esempio viene utilizzato un oggetto Sfc.SqlStoreConnection per specificare il server di destinazione:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
$conn = New-Object Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection("server='MYCOMPUTER';Trusted_Connection=True")  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName $conn  
```  
  
 In questo esempio viene usato **-TargetExpression** per identificare il database specifico da valutare:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\DatabaseEngine\1033"  
Invoke-PolicyEvaluation -Policy "Database Status.xml" -TargetServerName "MyComputer" -TargetExpression "Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']"  
```  
  
## <a name="evaluating-analysis-services-policies"></a>Valutazione di criteri di Analysis Services  
 Per valutare i criteri rispetto a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], è necessario caricare e registrare un assembly in PowerShell, creare una variabile con un oggetto di connessione di Analysis Services e passarla al parametro **-TargetObject** . In questo esempio viene illustrata la valutazione dei criteri di configurazione della superficie di attacco di Procedure consigliate per [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\AnalysisServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.AnalysisServices")  
$SSASsvr = new-object Microsoft.AnalysisServices.Server  
$SSASsvr.Connect("Data Source=Localhost")  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Analysis Services Features.xml" -TargetObject $SSASsvr  
```  
  
## <a name="evaluating-reporting-services-policies"></a>Valutazione di criteri di Reporting Services  
 Per valutare criteri di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , è necessario caricare e registrare un assembly in PowerShell, creare una variabile con un oggetto di connessione di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e passarla al parametro **-TargetObject** . In questo esempio viene illustrata la valutazione dei criteri di configurazione della superficie di attacco di Procedure consigliate per [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]:  
  
```  
sl "C:\Program Files\Microsoft SQL Server\120\Tools\Policies\ReportingServices\1033"  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Dmf.Adapters")  
$SSRSsvr = new-object Microsoft.SqlServer.Management.Adapters.RSContainer('MyComputer')  
Invoke-PolicyEvaluation -Policy "Surface Area Configuration for Reporting Services 2008 Features.xml" -TargetObject $SSRSsvr  
```  
  
## <a name="formatting-output"></a>Formattazione dell'output  
 Per impostazione predefinita, l'output di **Invoke-PolicyEvaluation** viene visualizzato nella finestra del prompt dei comandi sotto forma di breve report in formato leggibile. Usare il parametro **-OutputXML** per specificare che dal cmdlet venga generato invece un report dettagliato come file XML. **Invoke-PolicyEvaluation** usa lo schema SML-IF (Systems Modeling Language Interchange Format) affinché il file sia leggibile tramite i lettori SML-IF.  
  
```  
sl "SQLSERVER:\SQLPolicy\MyComputer\DEFAULT\Policies"  
Invoke-PolicyEvaluation -Policy "Datbase Status" -TargetServer "MYCOMPUTER" -OutputXML > C:\MyReports\DatabaseStatusReport.xml  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di cmdlet del motore di database](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  
