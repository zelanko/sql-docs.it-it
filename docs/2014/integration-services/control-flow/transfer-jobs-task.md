---
title: Attività Trasferisci processi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferjobstask.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03913242246fcdaf11e9272e827cd8e06951a108
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62829897"
---
# <a name="transfer-jobs-task"></a>Attività Trasferisci processi
  L'attività Trasferisci processi trasferisce uno o più processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent tra istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 È possibile configurare l'attività per il trasferimento di tutti i processi o dei processi specificati. È inoltre possibile indicare se i processi trasferiti devono essere attivati o meno nella destinazione.  
  
 I processi da trasferire potrebbero essere già presenti nella destinazione. È possibile configurare l'attività Trasferisci processi per la gestione dei processi duplicati nei modi seguenti:  
  
-   I processi duplicati vengono sovrascritti.  
  
-   In presenza di processi duplicati l'attività ha esito negativo.  
  
-   I processi duplicati vengono ignorati.  
  
 In fase di esecuzione l'attività Trasferisci processi si connette al server di origine e al server di destinazione utilizzando una o più gestioni connessioni SMO. Le gestioni connessioni SMO vengono configurate separatamente dall'attività Trasferisci processi, che tuttavia vi fa riferimento. Le gestioni connessioni SMO specificano il server e la modalità di autenticazione da adottare per l'accesso al server. Per altre informazioni, vedere [Gestione connessione file](../connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>Trasferimento di processi tra istanze di SQL Server  
 L'attività Trasferisci processi supporta un'origine e una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Non esiste alcuna limitazione relativamente alla versione da utilizzare come origine o destinazione.  
  
## <a name="events"></a>Eventi  
 L'attività Trasferisci processi genera un evento informativo in cui è indicato il numero di processi trasferiti. Genera inoltre un evento di avviso quando un processo viene sovrascritto. Non viene riportato lo stato incrementale del trasferimento, ma solo il completamento 0% e 100%.  
  
## <a name="execution-value"></a>Valore di esecuzione  
 Il valore di esecuzione, definito nella proprietà `ExecutionValue` dell'attività, restituisce il numero di processi trasferiti. Tramite l'assegnazione di una variabile definita dall'utente alla proprietà `ExecValueVariable` dell'attività, le informazioni sul trasferimento dei processi possono essere rese disponibili ad altri oggetti del pacchetto. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Voci di log  
 L'attività Trasferisci processi include le voci di log personalizzate seguenti:  
  
-   TransferJobsTaskStarTransferringObjects   Indica che il trasferimento è iniziato. La voce di log include l'ora di inizio.  
  
-   TransferJobsTaskFinishedTransferringObjects    Indica che il trasferimento è stato completato. La voce di log include l'ora di fine.  
  
 Inoltre, una voce di log per l'evento `OnInformation` indica il numero di processi che sono stati trasferiti e viene scritta una voce di log per l'evento `OnWarning` per ogni processo sovrascritto nella destinazione.  
  
## <a name="security-and-permissions"></a>Sicurezza e autorizzazioni  
 Per poter trasferire processi, l'utente deve essere un membro del ruolo predefinito del server sysadmin o di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nel database msdb, sia nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di origine che in quella di destinazione.  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>Configurazione dell'attività Trasferisci processi  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Trasferisci processi &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor attività Trasferisci processi &#40;pagina Processi&#41;](../transfer-jobs-task-editor-jobs-page.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per informazioni sull'impostazione di queste proprietà a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Attività Integration Services](integration-services-tasks.md)   
 [Flusso di controllo](control-flow.md)  
  
  
