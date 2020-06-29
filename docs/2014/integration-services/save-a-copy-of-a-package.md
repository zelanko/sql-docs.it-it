---
title: Salvare una copia di un pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 21482a20-e420-4452-b7eb-8f9fa1929f31
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9d68eac95885b6c40d607237eeb51050a9c6130f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422538"
---
# <a name="save-a-copy-of-a-package"></a>Salvataggio di una copia di un pacchetto
  Questa procedura descrive come salvare una copia di un pacchetto nel file system, nell'archivio pacchetti o nel database **msdb** in [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando si specifica il percorso di salvataggio della copia del pacchetto, è inoltre possibile modificarne il nome.  
  
 L'archivio pacchetti può includere sia il database **msdb** che le cartelle del file system, solo **msdb**, oppure solo le cartelle del file system. In **msdb**i pacchetti vengono salvati nella tabella **sysssispackages** . Tale tabella include una colonna **folderid** che identifica la cartella logica alla quale il pacchetto appartiene. Le cartelle logiche consentono di raggruppare i pacchetti salvati in **msdb** , nello stesso modo in cui le cartelle del file system consentono di raggruppare i pacchetti salvati nel file system. Le righe della tabella **sysssispackagefolders** di **msdb** definiscono le cartelle.  
  
 Se **msdb** non è definito come parte dell'archivio pacchetti, è possibile continuare ad associare i pacchetti a cartelle logiche esistenti se si seleziona SQL Server nell'opzione **Percorso pacchetto** .  
  
> [!NOTE]  
>  Affinché sia possibile salvarne una copia, il pacchetto deve essere aperto in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
### <a name="to-save-a-copy-of-a-package"></a>Per salvare una copia di un pacchetto  
  
1.  In Esplora soluzioni fare doppio clic sul pacchetto di cui si desidera salvare una copia.  
  
2.  Nel menu **file** fare clic su **Salva copia di \<package file> con nome**.  
  
3.  Nella finestra di dialogo **Salva copia del pacchetto** selezionare la posizione di un pacchetto dall'elenco **Posizione pacchetto**.  
  
4.  Se la posizione è **SQL Server** o **Archivio pacchetti SSIS**, specificare il nome di un server.  
  
5.  Se si esegue il salvataggio in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], specificare il tipo di autenticazione e, se si utilizza l'autenticazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , specificare un nome utente e una password.  
  
6.  Per specificare il percorso del pacchetto, digitarlo oppure fare clic sul pulsante Sfoglia **(...)** per specificare il percorso del pacchetto. Il nome predefinito del pacchetto è Pacchetto. In alternativa, modificare il nome del pacchetto in base alle proprie esigenze.  
  
     Se per l'opzione **Percorso pacchetto** si seleziona **SQL Server** , il percorso del pacchetto sarà composto dalle cartelle logiche di **msdb** più il nome del pacchetto. Ad esempio, se il pacchetto DownloadMonthlyData è associato alla cartella Finance della cartella MSDB (il nome predefinito della cartella logica radice di **msdb**), il percorso del pacchetto denominato DownloadMonthlyData sarà MSDB/Finance/DownloadMonthlyData.  
  
     Se per l'opzione **Percorso pacchetto** si seleziona **Archivio pacchetti SSIS** , il percorso del pacchetto corrisponderà alla cartella gestita dal servizio Integration Services. Ad esempio, se il pacchetto UpdateDeductions si trova nella cartella HumanResources all'interno della cartella del file system gestita dal servizio, il percorso del pacchetto sarà /File System/HumanResources/UpdateDeductions. Analogamente, se il pacchetto PostResumes è associato alla cartella HumanResources della cartella MSDB, il percorso del pacchetto sarà MSDB/HumanResources/PostResumes.  
  
     Se per l'opzione **Percorso pacchetto** si seleziona **File system** , il percorso del pacchetto corrisponderà alla posizione nel file system più il nome del file. Ad esempio, se il nome del pacchetto è UpdateDemographics, il relativo percorso sarà C:\HumanResources\Quarterly\UpdateDemographics.dtsx.  
  
7.  Controllare il livello di protezione del pacchetto.  
  
8.  Facoltativamente, fare clic sul pulsante Sfoglia **(...)** nella casella **livello di protezione** per modificare il livello di protezione.  
  
    -   Nella finestra di dialogo **Livello di protezione pacchetto** selezionare un livello di protezione diverso.  
  
    -   Fare clic su **OK**.  
  
9. Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services &#40;pacchetti&#41; SSIS](../../2014/integration-services/integration-services-ssis-packages.md)   
 [Configurazione del servizio Integration Services &#40;servizio SSIS&#41;](service/integration-services-service-ssis-service.md)  
  
  
