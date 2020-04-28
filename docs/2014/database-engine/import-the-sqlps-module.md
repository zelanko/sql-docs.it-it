---
title: Importare il modulo SQLPS | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1916be8c443799fa41680341e72889bd10551b4a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "74200421"
---
# <a name="import-the-sqlps-module"></a>Importare il modulo SQLPS
  Il metodo consigliato per gestire [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da PowerShell consiste nell'importare il modulo `sqlps` in un ambiente Windows PowerShell 2.0. Il modulo carica e registra gli snap-in e gli assembly di gestibilità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
1.  **Prima di iniziare:**  [Sicurezza](#Security)  
  
2.  **Per caricare il modulo:**  [Caricare il Modulo sqlps](#LoadSqlps)  
  
## <a name="before-you-begin"></a>Prima di iniziare  
 Dopo avere importato il modulo `sqlps` in Windows PowerShell, è quindi possibile:  
  
-   Eseguire in modo interattivo comandi di Windows PowerShell.  
  
-   Eseguire file script di Windows PowerShell.  
  
-   Eseguire cmdlet di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Utilizzare i percorsi del provider di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per spostarsi nella gerarchia degli oggetti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Utilizzare i modelli a oggetti per la gestibilità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , ad esempio Microsoft.SqlServer.Management.Smo, per gestire oggetti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  I verbi utilizzati nei nomi di due SQL Server cmdlet (`Encode-Sqlname` e `Decode-Sqlname`) non corrispondono ai verbi approvati per Windows PowerShell 2.0. Ciò non ha effetto sull'operazione, tuttavia Windows PowerShell genera un avviso quando il modulo `sqlps` viene importato in una sessione.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
 Per impostazione predefinita, Windows PowerShell viene eseguito con i criteri di esecuzione degli script impostati su **Restricted**, che impediscono l'esecuzione degli script di Windows PowerShell. Per caricare il modulo `sqlps`, è possibile utilizzare il cmdlet `Set-ExecutionPolicy` per abilitare l'esecuzione di script firmati o di qualsiasi script. Eseguire solo script da origini attendibili e proteggere tutti i file di input e output utilizzando le autorizzazioni NTFS appropriate. Per altre informazioni sull'abilitazione degli script di Windows PowerShell, vedere [Running Windows PowerShell Scripts](https://docs.microsoft.com/powershell/scripting/getting-started/starting-windows-powershell?view=powershell-6#how-to-enable-windows-powershell-ise-on-earlier-releases-of-windows)(Esecuzione di script di Windows PowerShell).  
  
##  <a name="load-the-sqlps-module"></a><a name="LoadSqlps"></a> Caricare il Modulo sqlps  

### <a name="to-load-the-sqlps-module-in-windows-powershell"></a>Per caricare il modulo sqlps in Windows PowerShell
  
1.  Utilizzare il cmdlet `Set-ExecutionPolicy` per impostare i criteri di esecuzione degli script appropriati.  
  
2.  Utilizzare il cmdlet `Import-Module` per importare il modulo sqlps. Specificare il parametro `DisableNameChecking` se si desidera eliminare l'avviso su `Encode-Sqlname` e `Decode-Sqlname`.  
  
### <a name="example-powershell"></a>Esempio (PowerShell)  
 In questo esempio viene caricato il modulo `sqlps` con verifica del nome disabilitata.  
  
```powershell
## Import the SQL Server Module.  
  
Import-Module "sqlps" -DisableNameChecking  
```  

## <a name="see-also"></a>Vedere anche  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)   
 [Provider di SQL Server PowerShell](../powershell/sql-server-powershell-provider.md)   
 [Utilizzo di cmdlet del motore di database](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
