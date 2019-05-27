---
title: Configurazione di PowerPivot tramite Windows PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 4d83e53e-04f1-417d-9039-d9e81ae0483d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1b57ea1f69933d4d2c73ec12cc4cc18ff86d112d
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071294"
---
# <a name="powerpivot-configuration-using-windows-powershell"></a>Configurazione di PowerPivot tramite Windows PowerShell
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] include i cmdlet di Windows PowerShell che è possibile usare per configurare un'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]. Per configurazione completamente un'installazione con PowerShell, è necessario utilizzare cmdlet sia di SharePoint che di PowerPivot per SharePoint. La maggior parte della configurazione può essere completata usando uno degli strumenti di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Per altre informazioni sugli strumenti, vedere [strumenti di configurazione PowerPivot](power-pivot-configuration-tools.md).  
  
> [!IMPORTANT]  
>  Per una farm di SharePoint 2010, prima di poter configurare PowerPivot per SharePoint o una farm di SharePoint in cui viene utilizzato un server di database [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] è necessario che SharePoint 2010 SP1 sia installato. Se il Service Pack non è ancora stato installato, eseguire questa operazione prima di iniziare a configurare il server.  
  
## <a name="benefits-of-configuring-powerpivot-for-sharepoint-using-powershell"></a>Vantaggi della configurazione di PowerPivot per SharePoint utilizzando PowerShell  
 È possibile compilare i file di script di Windows PowerShell (con estensione ps1) per rendere automatiche le attività di configurazione. Si consiglia di adottare questo approccio se sono necessari passaggi di installazione e configurazione controllati da script eseguibili in qualsiasi server. Uno script di questo tipo può essere necessario come parte di un piano di ripristino di emergenza per ricompilare un server in caso di errore hardware.  
  
## <a name="view-a-list-of-the-powerpivot-cmdlets-on-a-server"></a>Visualizzare un elenco di cmdlet PowerPivot in un server  
 Per visualizzare il contenuto ed esempi del [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cmdlet, vedere [informazioni di riferimento di PowerShell per PowerPivot per SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint).  
  
 Per utilizzare PowerShell per visualizzare un elenco di cmdlet di PowerPivot:  
  
1.  Aprire una shell di gestione di SharePoint usando l'opzione **Esegui come amministratore** .  
  
2.  Immettere il comando seguente:  
  
    ```  
    Get-help *powerpivot*  
    ```  
  
     Dovrebbe venire visualizzato un elenco di cmdlet nel cui nome è incluso PowerPivot. Ad esempio `Get-PowerPivotServiceApplication`. Il numero di cmdlet disponibili dipende dalla versione di Analysis Services in uso.  
  
    -   10 cmdlet con il server SQL Server 2012 SP1 Analysis Services configurato nella modalità SharePoint e SharePoint 2013. La versione 2012 SP1 utilizza una nuova architettura che consente l'esecuzione di Analysis Server all'esterno della farm di SharePoint e richiede meno cmdlet di Windows PowerShell di gestione.  
  
    -   17 cmdlet con il server SQL Server 2012 SP1 Analysis Services configurato nella modalità SharePoint e SharePoint 2010.  
  
     Se viene restituito alcun comando nell'elenco o viene visualizzato un messaggio di errore simile a "`get-help could not find *powerpivot* in a help file in this session.`", vedere la sezione successiva in questo argomento per istruzioni sull'abilitazione dei cmdlet PowerPivot nel server.  
  
     Per tutti i cmdlet è disponibile la Guida. Nell'esempio seguente viene illustrato come visualizzare la Guida per il cmdlet `New-PowerPivotServiceApplication`:  
  
    ```  
    Get-help new-powerpivotserviceapplication -full  
    ```  
  
     In alternativa, per visualizzare solo gli esempi, utilizzare la sintassi seguente:  
  
    ```  
    Get-help new-powerpivotserviceapplication -example  
    ```  
  
## <a name="enable-powerpivot-cmdlets-on-a-server"></a>Abilitare i cmdlet di PowerPivot in un server  
 I cmdlet di PowerPivot sono disponibili dopo l'installazione di PowerPivot per SharePoint e la distribuzione della soluzione della farm. Le soluzioni vengono distribuite quando si esegue lo strumento di configurazione PowerPivot. Attenersi a questi passaggi per abilitare l'utilizzo dei cmdlet:  
  
1.  Aprire una shell di gestione di SharePoint usando l'opzione **Esegui come amministratore** .  
  
2.  Eseguire il primo cmdlet:  
  
    ```  
    Add-SPSolution -LiteralPath "C:\Program Files\Microsoft SQL Server\110\Tools\PowerPivotTools\ConfigurationTool\Resources\PowerPivotFarm.wsp"  
    ```  
  
     Il cmdlet restituisce il nome e l'ID della soluzione e Deployed=False. Nel passaggio successivo la soluzione viene distribuita.  
  
3.  Eseguire il secondo cmdlet per distribuire la soluzione:  
  
    ```  
    Install-SPSolution -Identity PowerPivotFarm.wsp -GACDeployment -Force  
    ```  
  
4.  Chiudere la finestra. Riaprirla usando nuovamente l'opzione **Esegui come amministratore** .  
  
## <a name="related-content"></a>Contenuto correlato  
 [Amministrazione e configurazione del server PowerPivot in Amministrazione centrale](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
 [Strumenti di configurazione PowerPivot](power-pivot-configuration-tools.md)  
  
 [Informazioni di riferimento di PowerShell per PowerPivot per SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint)  
  
  
