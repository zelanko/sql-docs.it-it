---
title: Editor attività Trasferisci processi (pagina processi) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferjobstask.jobs.f1
helpviewer_keywords:
- Transfer Jobs Task Editor
ms.assetid: e72b1dc7-8cda-4ee6-abb5-d438370f04df
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 43066d036a23a063c218234b3a346bf89560994f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66054986"
---
# <a name="transfer-jobs-task-editor-jobs-page"></a>Editor attività Trasferisci processi (pagina Processi)
  Utilizzare la pagina **Processi** della finestra di dialogo **Editor attività Trasferisci processi** per specificare le proprietà relative alla copia di uno o più processi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent tra due istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Per ulteriori informazioni sull'attività Trasferisci processi, vedere [Transfer Jobs Task](control-flow/transfer-jobs-task.md).  
  
> [!NOTE]  
>  Per accedere ai processi nel server di origine, l'utente deve essere un membro almeno del ruolo predefinito del database **SQLAgentUserRole** nel server. Per creare processi nel server di destinazione, l'utente deve essere un membro del ruolo predefinito del server **sysadmin** o di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent. Per altre informazioni sui ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent e sulle relative autorizzazioni, vedere [Ruoli di database predefiniti di SQL Server Agent](../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="options"></a>Opzioni  
 **SourceConnection**  
 Selezionare una gestione connessione SMO nell'elenco o fare clic su **\<Nuova connessione...>** per creare una nuova connessione al server di origine.  
  
 **DestinationConnection**  
 Selezionare una gestione connessione SMO nell'elenco o fare clic su **Nuova connessione...>\<** per creare una nuova connessione al server di destinazione.  
  
 **TransferAllJobs**  
 Indicare se l'attività deve copiare dal server di origine nel server di destinazione tutti i processi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent o solo quelli specificati.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**True**|Copia tutti i processi.|  
|**False**|Copia solo i processi specificati.|  
  
 **JobsList**  
 Fare clic sul pulsante con i puntini di sospensione **(...)** per selezionare i processi da copiare. È necessario selezionare almeno un processo.  
  
> [!NOTE]  
>  Prima di selezionare i processi da copiare, specificare la proprietà **SourceConnection** .  
  
 Quando la proprietà **TransferAllJobs** è impostata su **True** , l'opzione **JobsList**non è disponibile.  
  
 **IfObjectExists**  
 Indicare la modalità con cui l'attività deve gestire i processi che hanno lo stesso nome di processi già esistenti nel server di destinazione.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**FailTask**|L'attività viene interrotta se nel server di destinazione esistono processi con lo stesso nome.|  
|**Overwrite**|L'attività sovrascrive i processi con lo stesso nome che si trovano nel server di destinazione.|  
|**Skip**|L'attività ignora i processi con lo stesso nome che si trovano nel server di destinazione.|  
  
 **EnableJobsAtDestination**  
 Specificare se i processi copiati nel server di destinazione devono essere attivati.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**True**|Attiva i processi nel server di destinazione.|  
|**False**|Disabilita i processi nel server di destinazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Attività di Integration Services](control-flow/integration-services-tasks.md)   
 [Editor attività Trasferisci processi &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Pagina Espressioni](expressions/expressions-page.md)   
 [Gestione connessione SMO](connection-manager/smo-connection-manager.md)  
  
  
