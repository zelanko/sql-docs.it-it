---
title: Processi di SQL Server Agent per i pacchetti | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- jobs [Integration Services]
- automatic package execution
- scheduling packages [Integration Services]
- SQL Server Agent [Integration Services]
ms.assetid: ecf7a5f9-b8a7-47f1-9ac0-bac07cb89e31
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 312469e8355fb5720f1a1ce13a58a59f759da4ec
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964808"
---
# <a name="sql-server-agent-jobs-for-packages"></a>Processi di SQL Server Agent per i pacchetti
  È possibile automatizzare e pianificare l'esecuzione dei pacchetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. È possibile pianificare i pacchetti distribuiti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e archiviati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nell'archivio pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)] e nel file system.  
  
## <a name="sections-in-this-topic"></a>Sezioni dell'argomento  
 In questo argomento sono incluse le sezioni seguenti:  
  
-   [Pianificazione dei processi in SQL Server Agent](#jobs)  
  
-   [Pianificazione dei pacchetti di Integration Services](#packages)  
  
-   [Risoluzione dei problemi dei pacchetti pianificati](#trouble)  
  
##  <a name="scheduling-jobs-in-sql-server-agent"></a><a name="jobs"></a>Pianificazione dei processi in SQL Server Agent  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è il servizio installato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che consente di automatizzare e pianificare le attività eseguendo processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. È possibile eseguire automaticamente processi solo se il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è in esecuzione. Per altre informazioni, vedere [Configure SQL Server Agent](../../ssms/agent/configure-sql-server-agent.md).  
  
 Il nodo **SQL Server Agent** viene visualizzato in Esplora oggetti in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] quando ci si connette a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Per automatizzare un'attività periodica, viene creato un processo usando la finestra di dialogo **Nuovo processo** . Per altre informazioni, vedere [Implementazione di processi](../../ssms/agent/implement-jobs.md).  
  
 Dopo aver creato il processo, è necessario aggiungere almeno un passaggio. In un processo possono essere inclusi più passaggi che consentono di effettuare attività diverse. Per altre informazioni, vedere [Gestire passaggi di processo](../../ssms/agent/manage-job-steps.md).  
  
 Dopo aver creato il processo e i relativi passaggi, è possibile creare una pianificazione per l'esecuzione del processo. È tuttavia possibile creare anche un processo non pianificato che viene eseguito manualmente. Per altre informazioni, vedere [Creare e collegare le pianificazioni ai processi](../../ssms/agent/create-and-attach-schedules-to-jobs.md).  
  
 È possibile migliorare il processo impostando opzioni di notifica, ad esempio aggiungendo avvisi o specificando l'operatore che deve inviare un messaggio di posta elettronica al completamento del processo. Per altre informazioni, vedere [Avvisi](../../ssms/agent/alerts.md).  
  
##  <a name="scheduling-integration-services-packages"></a><a name="packages"></a> Scheduling Integration Services Packages  
 Quando si crea un processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per pianificare i pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , è necessario aggiungere almeno un passaggio e impostare il tipo di passaggio su **Pacchetto SQL Server Integration Services**. In un processo possono essere inclusi più passaggi che consentono di eseguire pacchetti diversi.  
  
 L'esecuzione di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] da un passaggio di processo è simile all'esecuzione di un pacchetto tramite le utilità **dtexec** (dtexec.exe) e **DTExecUI** (dtexecui.exe). Le opzioni di runtime per un pacchetto non vengono impostate tramite opzioni della riga di comando o nella finestra di dialogo **Utilità di esecuzione pacchetti** , ma nella finestra di dialogo **Nuovo passaggio di processo** . Per altre informazioni sulle opzioni per l'esecuzione di un pacchetto, vedere [Utilità dtexec](dtexec-utility.md).  
  
 Per altre informazioni, vedere [Pianificare un pacchetto tramite SQL Server Agent](../schedule-a-package-by-using-sql-server-agent.md).  
  
 Per visualizzare un video in cui viene illustrato come usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per l'esecuzione di un pacchetto, vedere la home page del video [Procedura: Automazione dell'esecuzione di un pacchetto SSIS utilizzando SQL Server Agent (video di SQL Server)](https://go.microsoft.com/fwlink/?LinkId=141771)in MSDN Library.  
  
##  <a name="troubleshooting"></a><a name="trouble"></a> Risoluzione dei problemi  
 Un passaggio di processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent potrebbe non riuscire ad avviare un pacchetto anche se il pacchetto viene eseguito correttamente in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e dalla riga di comando. Per questo problema esistono alcuni motivi comuni e diverse soluzioni consigliate. Per ulteriori informazioni, vedere le risorse seguenti.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Articolo della Knowledge Base [Pacchetto SSIS non viene eseguito quando viene chiamato da un passaggio di processo SQL Server Agent](https://support.microsoft.com/kb/918760)  
  
-   Video, [risoluzione dei problemi: esecuzione di pacchetti tramite SQL Server Agent (SQL Server video)](https://go.microsoft.com/fwlink/?LinkId=141772)in MSDN Library.  
  
 Dopo l'avvio di un pacchetto tramite un passaggio di processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, l'esecuzione del pacchetto potrebbe avere esito negativo oppure positivo ma con risultati imprevisti. È possibile utilizzare gli strumenti seguenti per risolvere questi problemi.  
  
-   Per i pacchetti archiviati nel database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] MSDB, nell'archivio pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)] o in una cartella del computer locale, è possibile usare **Visualizzatore file di log** , nonché qualsiasi log e file di dump del debug generato durante l'esecuzione del pacchetto.  
  
     **Per utilizzare Visualizzatore file di log, effettuare le operazioni seguenti.**  
  
    1.  Fare clic con il pulsante destro del mouse sul processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, quindi fare clic su **Visualizza cronologia**.  
  
    2.  Individuare l'esecuzione del processo nella casella **Riepilogo file di log** con il messaggio **Processo non riuscito** nella colonna **Messaggio** .  
  
    3.  Espandere il nodo del processo e fare clic sul passaggio di processo per visualizzare i dettagli del messaggio nell'area sotto la casella **Riepilogo file di log** .  
  
-   Per i pacchetti archiviati nel database SSISDB, è inoltre possibile usare **Visualizzatore file di log** , nonché qualsiasi log e file di dump del debug generato durante l'esecuzione del pacchetto. Inoltre, è possibile usare i report per il server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     **Per trovare informazioni nei report per l'esecuzione del pacchetto associata all'esecuzione del processo, effettuare le operazioni seguenti.**  
  
    1.  Attenersi ai passaggi precedenti per visualizzare i dettagli del messaggio per il passaggio di processo.  
  
    2.  Individuare l'ID esecuzione elencato nel messaggio.  
  
    3.  Espandere il nodo Catalogo di Integration Services in Esplora oggetti.  
  
    4.  Fare clic con il pulsante destro del mouse su SSISDB, scegliere Report, Report standard e quindi fare clic su Tutte le esecuzioni.  
  
    5.  Nel report **Tutte le esecuzioni** individuare l'ID esecuzione nella colonna **ID** . Fare clic su **Panoramica**, **Tutti i messaggi**o **Prestazioni di esecuzione** per visualizzare informazioni sull'esecuzione di questo pacchetto.  
  
         Per altre informazioni sui report Panoramica, Tutti i messaggi e Prestazioni di esecuzione, vedere [Report per il server Integration Services](../reports-for-the-integration-services-server.md).  
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Articolo della Knowledge Base [Pacchetto SSIS non viene eseguito quando viene chiamato da un passaggio di processo SQL Server Agent](https://support.microsoft.com/kb/918760)nel sito Web di [!INCLUDE[msCoName](../../includes/msconame-md.md)]  
  
-   Video [Risoluzione dei problemi: Esecuzione di un pacchetto con SQL Server Agent (video di SQL Server)](https://go.microsoft.com/fwlink/?LinkId=141772)in MSDN Library  
  
-   Video [Procedura: Automazione dell'esecuzione di un pacchetto SSIS utilizzando SQL Server Agent (video di SQL Server)](https://go.microsoft.com/fwlink/?LinkId=141771)in MSDN Library  
  
-   Articolo tecnico [Checking SQL Server Agent jobs using Windows PowerShell](https://go.microsoft.com/fwlink/?LinkId=165675)(Verifica dei processi di SQL Server Agent tramite Windows PowerShell) su mssqltips.com  
  
-   Articolo tecnico [Auto alert for SQL Agent jobs when they are enabled or disabled](https://go.microsoft.com/fwlink/?LinkId=165676)(Avviso automatico se i processi di SQL Agent sono abilitati o disabilitati) su mssqltips.com  
  
-   Intervento nel blog [Configuring SQL Agent Jobs to Write to Windows Event Log](https://go.microsoft.com/fwlink/?LinkId=220745)(Configurazione dei processi di SQL Agent per la scrittura nel Registro eventi di Windows) su mssqltips.com.  
  
  
