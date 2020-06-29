---
title: Attività Trasferisci stored procedure master | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfermasterspstask.f1
helpviewer_keywords:
- Transfer Master Stored Procedures task [Integration Services]
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c6356c0ba1a1f9423bffdc704ae9f9f1ab2dd1a4
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438088"
---
# <a name="transfer-master-stored-procedures-task"></a>Attività Trasferisci stored procedure master
  L'attività Trasferisci stored procedure master trasferisce una o più stored procedure definite dall'utente tra i database **master** di istanze diverse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per trasferire una stored procedure dal database **master** , è necessario che il proprietario stored della procedure sia un dbo.  
  
 È possibile configurare l'attività Trasferisci stored procedure master per il trasferimento di tutte le stored procedure o delle stored procedure specificate. Questa attività non esegue la copia delle stored procedure di sistema.  
  
 È possibile che le stored procedure master da trasferire siano già presenti nella destinazione. È tuttavia possibile configurare l'attività Trasferisci stored procedure master per la gestione di eventuali stored procedure esistenti nei modi seguenti:  
  
-   Le stored procedure esistenti vengono sovrascritte.  
  
-   In presenza di stored procedure duplicate l'attività ha esito positivo.  
  
-   Le stored procedure duplicate vengono ignorate.  
  
 In fase di esecuzione l'attività Trasferisci stored procedure master si connette al server di origine e al server di destinazione utilizzando due gestioni connessioni SMO. Le gestioni connessioni SMO vengono configurate separatamente dall'attività Trasferisci stored procedure master, che tuttavia vi fa riferimento. Le gestioni connessioni SMO specificano il server e la modalità di autenticazione da utilizzare per l'accesso al server. Per altre informazioni, vedere [Gestione connessione file](../connection-manager/smo-connection-manager.md).  
  
## <a name="transferring-stored-procedures-between-instances-of-sql-server"></a>Trasferimento di stored procedure tra istanze di SQL Server  
 L'attività Trasferisci stored procedure master supporta un'origine e una destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="events"></a>Eventi  
 L'attività genera un evento informativo in cui è indicato il numero di stored procedure trasferite. Genera inoltre un evento di avviso quando una stored procedure viene sovrascritta.  
  
 Non viene riportato lo stato incrementale del trasferimento, ma solo il completamento 0% e 100%.  
  
## <a name="execution-value"></a>Valore di esecuzione  
 Il valore di esecuzione, definito nella proprietà `ExecutionValue` dell'attività, restituisce il numero di stored procedure trasferite. Tramite l'assegnazione di una variabile definita dall'utente alla proprietà `ExecValueVariable` dell'attività, le informazioni sul trasferimento di stored procedure master possono essere rese disponibili ad altri oggetti del pacchetto. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](../use-variables-in-packages.md).  
  
## <a name="log-entries"></a>Voci di log  
 L'attività Trasferisci stored procedure master include le voci di log personalizzate seguenti:  
  
-   TransferStoredProceduresTaskStartTransferringObjects  Indica che il trasferimento è iniziato. La voce di log include l'ora di inizio.  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  Indica che il trasferimento è stato completato. La voce di log include l'ora di fine.  
  
 Inoltre, una voce di log per l'evento `OnInformation` indica il numero di stored procedure che sono state trasferite e viene scritta una voce di log per l'evento `OnWarning` per ogni stored procedure sovrascritta nella destinazione.  
  
## <a name="security-and-permissions"></a>Sicurezza e autorizzazioni  
 L'utente deve disporre dell'autorizzazione per la visualizzazione dell'elenco di stored procedure nel database **master** dell'origine ed essere un membro del ruolo del server amministratore di sistema o disporre dell'autorizzazione per la creazione di stored procedure nel database **master** del server di destinazione.  
  
## <a name="configuration-of-the-transfer-master-stored-procedures-task"></a>Configurazione dell'attività Trasferisci stored procedure master  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Trasferisci stored procedure master &#40;pagina Generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Editor attività Trasferisci stored procedure master &#40;pagina Stored procedure&#41;](../transfer-master-stored-procedures-task-editor-stored-procedures-page.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### <a name="configuring-the-transfer-master-stored-procedures-task-programmatically"></a>Configurazione dell'attività Trasferisci stored procedure master a livello di codice  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Attività Trasferisci oggetti SQL Server](transfer-sql-server-objects-task.md)   
 [Attività Integration Services](integration-services-tasks.md)   
 [Flusso di controllo](control-flow.md)  
  
  
