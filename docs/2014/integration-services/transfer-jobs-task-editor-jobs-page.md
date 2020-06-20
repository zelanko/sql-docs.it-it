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
ms.openlocfilehash: 0c430f08b4a86c981df5138c7f78e76b54e7de28
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972836"
---
# <a name="transfer-jobs-task-editor-jobs-page"></a>Editor attività Trasferisci processi (pagina Processi)
  Utilizzare la pagina **Processi** della finestra di dialogo **Editor attività Trasferisci processi** per specificare le proprietà relative alla copia di uno o più processi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent tra due istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Per ulteriori informazioni sull'attività Trasferisci processi, vedere [Transfer Jobs Task](control-flow/transfer-jobs-task.md).  
  
> [!NOTE]  
>  Per accedere ai processi nel server di origine, l'utente deve essere un membro almeno del ruolo predefinito del database **SQLAgentUserRole** nel server. Per creare processi nel server di destinazione, l'utente deve essere un membro del ruolo predefinito del server **sysadmin** o di uno dei ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent. Per altre informazioni sui ruoli predefiniti del database di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent e sulle relative autorizzazioni, vedere [Ruoli di database predefiniti di SQL Server Agent](../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## <a name="options"></a>Opzioni  
 **SourceConnection**  
 Selezionare una gestione connessione SMO nell'elenco oppure fare clic su **\<New connection...>** per creare una nuova connessione al server di origine.  
  
 **DestinationConnection**  
 Selezionare una gestione connessione SMO nell'elenco oppure fare clic su **\<New connection...>** per creare una nuova connessione al server di destinazione.  
  
 **TransferAllJobs**  
 Indicare se l'attività deve copiare dal server di origine nel server di destinazione tutti i processi di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent o solo quelli specificati.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Description|  
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
  
|valore|Description|  
|-----------|-----------------|  
|**FailTask**|L'attività viene interrotta se nel server di destinazione esistono processi con lo stesso nome.|  
|**Sovrascrivere**|L'attività sovrascrive i processi con lo stesso nome che si trovano nel server di destinazione.|  
|**Ignora**|L'attività ignora i processi con lo stesso nome che si trovano nel server di destinazione.|  
  
 **EnableJobsAtDestination**  
 Specificare se i processi copiati nel server di destinazione devono essere attivati.  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Description|  
|-----------|-----------------|  
|**True**|Attiva i processi nel server di destinazione.|  
|**False**|Disabilita i processi nel server di destinazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Attività Integration Services](control-flow/integration-services-tasks.md)   
 [Editor attività Trasferisci processi &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Pagina espressioni](expressions/expressions-page.md)   
 [Gestione connessione SMO](connection-manager/smo-connection-manager.md)  
  
  
