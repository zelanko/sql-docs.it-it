---
title: Visualizzare la Guida di SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Help [PowerShell]
- Help [SQL Server], PowerShell
- PowerShell [SQL Server], help
ms.assetid: 968c316d-db83-4c24-8ea6-9f18736842f7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 67633bcfad7c18679dae93de6e5541f3000a1ccc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779103"
---
# <a name="get-help-sql-server-powershell"></a>Get Help SQL Server PowerShell
  Vi sono diverse fonti di informazione per l'utilizzo dei cmdlet e del provider di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per Windows PowerShell. Tra queste è inclusa la Guida disponibile nell'ambiente di Windows PowerShell.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Per informazioni su Windows PowerShell, vedere la [Guida introduttiva a Windows PowerShell](https://technet.microsoft.com/library/hh857337.aspx).  
  
 Per una panoramica dei cmdlet e del provider di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , vedere [SQL Server PowerShell](../powershell/sql-server-powershell.md).  
  
### <a name="help-in-the-windows-powershell-environment"></a>Guida all'ambiente di Windows PowerShell  
 Usare il cmdlet **Get-Help** per ottenere informazioni sull'ambiente di Windows PowerShell. **Get-Help** fornisce informazioni di base sul linguaggio di Windows PowerShell e sui vari cmdlet e provider disponibili in Windows PowerShell.  
  
 Per altre informazioni sui modi in cui è possibile usare **Get-Help**, vedere [Get-Help: Ottenere informazioni della Guida](https://go.microsoft.com/fwlink/?LinkId=102136).  
  
### <a name="sql-server-powershell-provider-help"></a>Guida del provider PowerShell per SQL Server  
 Il provider PowerShell di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] implementa diverse cartelle su un'unità virtuale SQLSERVER, come ad esempio le cartelle SQLSERVER:\SQL e SQLSERVER:\DAC. Ogni cartella è associata a uno dei modelli a oggetti per la gestione di SQL Server. È possibile elencare i metodi e le proprietà associati a ogni nodo in un percorso di SQL Server, ma non è possibile ottenerne la guida nell'ambiente PowerShell. Per una tabella delle cartelle con i collegamenti al riferimento di programmazione associato, vedere [Provider PowerShell per SQL Server](../powershell/sql-server-powershell-provider.md).  
  
### <a name="invoke-sqlcmd-help"></a>Guida di Invoke-Sqlcmd  
 Il cmdlet **Invoke-Sqlcmd** accetta come input qualsiasi query o file script che può essere eseguito dall'utilità **sqlcmd** . È possibile usare **Get-Help** per ottenere informazioni su **Invoke-Sqlcmd** e i relativi parametri, ma **Get-Help** non fornisce informazioni sulle query **sqlcmd** .  
  
 L'input *-Query* o *-QueryFromFile* può contenere:  
  
-   Variabili e comandi di**sqlcmd** . Per informazioni su variabili e comandi, vedere la sezione Osservazioni di [Utilità sqlcmd](../tools/sqlcmd-utility.md).  
  
-   [!INCLUDE[tsql](../includes/tsql-md.md)] . Per altre informazioni sul linguaggio [!INCLUDE[tsql](../includes/tsql-md.md)], vedere [Guida di riferimento a Transact-SQL &#40;Motore di database&#41;](/sql/t-sql/language-reference).  
  
-   Istruzioni XQuery. Per altre informazioni sul linguaggio XQuery supportato da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], vedere [Riferimento al linguaggio XQuery &#40;SQL Server&#41;](/sql/xquery/xquery-language-reference-sql-server).  
  
## <a name="get-help-for-a-sql-server-cmdlet"></a>Ottenere la Guida per un cmdlet di SQL Server  
 **Per ottenere la Guida per un cmdlet**  
  
-   Eseguire Get-Help specificando il nome del cmdlet e il livello della Guida da restituire.  
  
### <a name="example-cmdlet-get-help"></a>Esempio: cmdlet Get-Help  
 Negli esempi seguenti vengono restituiti vari livelli della Guida per **Invoke-Sqlcmd**:  
  
```  
## Get the basic help.  
Get-Help Invoke-Sqlcmd  
  
## Get the full help.  
Get-Help Invoke-Sqlcmd -Full  
  
## Get the parameter descriptions.  
Get-Help Invoke-Sqlcmd -Parameter *  
  
## Get the code examples.  
Get-Help Invoke-Sqlcmd -Examples  
  
## Get the syntax diagram.  
Get-Help Invoke-Sqlcmd -Syntax  
```  
  
## <a name="get-a-list-of-providers"></a>Ottenere un elenco di provider  
 **Per ottenere un elenco di provider attivi**  
  
1.  Eseguire Get-Help specificando la categoria del provider.  
  
 Per altre informazioni su come ottenere informazioni sul provider in Windows PowerShell, vedere [Unità e provider](https://go.microsoft.com/fwlink/?LinkId=102137).  
  
### <a name="example-get-a-list-of-providers"></a>Esempio: Ottenere un elenco di provider  
 Questo codice restituisce un elenco dei provider attualmente abilitati nella sessione di Windows PowerShell:  
  
```  
Get-Help -Category provider  
```  
  
## <a name="get-help-about-the-sql-server-provider"></a>Ottenere la Guida sul provider SQL Server  
 **Per ottenere la Guida sul provider**  
  
1.  Eseguire Get-Help specificando il nome SQLServer  
  
### <a name="example-get-sql-server-provider-help"></a>Esempio: Ottenere la Guida di Provider SQL Server  
 In questo esempio vengono restituite informazioni di base sul provider di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] :  
  
```  
Get-Help SQLServer  
```  
  
## <a name="list-methods-and-properties"></a>Elencare metodi e proprietà  
 **Per elencare i metodi e le proprietà per un nodo in un percorso del provider SQL Server**  
  
1.  Usare il comando CD in un nodo nel percorso di SQL Server o creare un set di variabili nel percorso.  
  
2.  Eseguire la **Get-Member** cmdlet con il parametro - Type impostato su Methods o Properties  
  
### <a name="examples-listing-methods-and-properties"></a>Esempi: Elenco di metodi e proprietà  
 In questo esempio vengono elencati i metodi supportati per il nodo Database:  
  
```  
Set-Location SQL:\MyComputer\DEFAULT\Databases  
Get-Item . | Get-Member -Type Methods  
```  
  
 In questo esempio vengono elencate le proprietà di una variabile impostata su un oggetto della tabella SMO:  
  
```  
$MyVar = New-Object Microsoft.SqlServer.Management.SMO.Table  
$MyVar | Get-Member -Type Properties  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Provider PowerShell per SQL Server](../powershell/sql-server-powershell-provider.md)   
 [Usare cmdlet del motore di database](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  
