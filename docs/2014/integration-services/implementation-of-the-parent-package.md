---
title: Implementazione del pacchetto padre | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- parent packages [Integration Services]
ms.assetid: d8f94830-fa27-4151-88df-cbdc6bf0fc80
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 06adb2034134b7cc49a8313fb501edc845244922
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768149"
---
# <a name="implementation-of-the-parent-package"></a>Implementazione del pacchetto padre
  Quando si esegue il bilanciamento del carico dei pacchetti di SSIS tra più server, dopo la creazione e la distribuzione dei pacchetti figlio e dopo la creazione dei processi remoti di SQL Server Agent per eseguirli, è necessario creare il pacchetto padre. Il pacchetto padre deve contenere più attività Esegui processo di SQL Server Agent, ognuna della quali è responsabile di chiamare un diverso processo di SQL Server Agent che esegue uno dei pacchetti figlio. Le attività Esegui processo di SQL Server Agent nel pacchetto padre eseguono a loro volta i vari processi di SQL Server Agent. Ogni attività nel pacchetto padre contiene informazioni riguardanti ad esempio la modalità di connessione al server remoto e il processo da eseguire su tale server. Per altre informazioni, vedere [Execute SQL Server Agent Job Task](control-flow/execute-sql-server-agent-job-task.md).  
  
 Per identificare il pacchetto padre che esegue i pacchetti figlio, in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] fare clic con il pulsante destro del mouse sul pacchetto in Esplora soluzioni, quindi scegliere **Pacchetto punto di ingresso**.  
  
## <a name="listing-child-packages"></a>Elenco di pacchetti figlio  
 Se si distribuisce un progetto contenente un pacchetto padre e pacchetti figlio nel server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , sarà possibile visualizzare un elenco dei pacchetti figlio eseguiti dal pacchetto padre. Quando si esegue il pacchetto padre, un report **Panoramica** per il pacchetto padre è generato automaticamente in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Il report include un elenco dei pacchetti figlio eseguiti dall'attività Esegui pacchetto contenuta nel pacchetto padre, come illustrato nell'immagine seguente.  
  
 ![Report Panoramica con elenco di pacchetti figlio](media/overviewreport-childpackagelisting.png "Report Panoramica con elenco di pacchetti figlio")  
  
 Per informazioni sull'accesso al report **Panoramica** , vedere [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md).  
  
## <a name="precedence-constraints-in-the-parent-package"></a>Vincoli di precedenza nel pacchetto padre  
 Quando si creano vincoli di precedenza tra le attività Esegui processo di SQL Server Agent nel pacchetto padre, tali vincoli di precedenza controllano solo il momento in cui vengono avviati i processi di SQL Server Agent sui server remoti. I vincoli di precedenza non possono ricevere informazioni sull'esito positivo o negativo dei pacchetti figlio eseguiti dai passaggi dei processi di SQL Server Agent.  
  
 L'esito positivo o negativo di un pacchetto figlio non viene pertanto propagato al pacchetto padre, perché l'attività Esegui processo di SQL Server Agent nel pacchetto padre ha unicamente la funzione di richiedere al processo di SQL Server Agent di eseguire il pacchetto figlio. Se la chiamata al processo di SQL Server Agent viene completata correttamente, il pacchetto padre riceve il risultato <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult.Success>.  
  
 In questo scenario l'eventuale esito negativo indica solamente che si è verificato un errore durante la chiamata remota al processo di SQL Server Agent. Questa situazione si presenta ad esempio quando il server remoto non è disponibile e l'agente non risponde. Finché l'agente è attivo, tuttavia, il pacchetto padre completa correttamente l'attività.  
  
> [!NOTE]  
>  È possibile usare un'attività Esegui SQL contenente un'istruzione Transact-SQL **sp_start_job N'package_name'**. Per altre informazioni, vedere [sp_start_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-start-job-transact-sql).  
  
## <a name="debugging-environment"></a>Ambiente di debug  
 Durante il test del pacchetto padre è possibile accedere all'ambiente di debug della finestra di progettazione scegliendo Avvia debug (F5) dal menu Debug. In alternativa, è possibile usare l'utilità della riga di comando **dtexec**. Per altre informazioni, vedere [dtexec Utility](packages/dtexec-utility.md).  
  
  
