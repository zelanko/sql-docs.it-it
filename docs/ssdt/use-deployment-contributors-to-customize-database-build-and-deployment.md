---
title: Personalizzare la compilazione e la distribuzione del database tramite collaboratori alla compilazione e distribuzione | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: fe2064bb-e01e-4a12-9f12-a99aa9a5203f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3952706cebfd5f26f68e2dd103de1cb19c46bd05
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65101964"
---
# <a name="customize-database-build-and-deployment-by-using-build-and-deployment-contributors"></a>Personalizzare la compilazione e la distribuzione del database tramite collaboratori alla compilazione e distribuzione
Visual Studio fornisce punti di estendibilità che è possibile utilizzare per modificare il comportamento delle azioni di compilazione e distribuzione per i progetti di database.  
  
## <a name="available-extensibility-points"></a>Punti di estendibilità disponibili  
È possibile creare un'estensione per i punti di estendibilità, come illustrato nella tabella seguente:  
  
|**Azione**|**Tipo di collaboratore**|**Note**|  
|--------------|------------------------|-------------|  
|Compilazione|BuildContributor|Questo tipo di estensione viene eseguito quando il progetto SQL viene compilato dopo che il modello di progetto è stato completamente convalidato. Il collaboratore alla compilazione può accedere al modello completato, oltre a tutte le proprietà dell'attività di compilazione e a qualsiasi argomento personalizzato.|  
|Distribuzione|DeploymentPlanModifier|Questo tipo di estensione viene eseguito quando il progetto SQL viene distribuito, come parte della pipeline di distribuzione, dopo che il piano di distribuzione è stato generato ma prima che venga eseguito. È possibile utilizzare DeploymentPlanModifier per modificare il piano di distribuzione aggiungendo o rimuovendo passaggi. I collaboratori alla distribuzione possono accedere al piano di distribuzione, ai risultati del confronto e ai modelli di origine e destinazione.|  
|Distribuzione|DeploymentPlanExecutor|Questo tipo di estensione viene eseguito quando il piano di distribuzione viene eseguito e fornisce accesso in sola lettura al piano di distribuzione. DeploymentPlanExectutor esegue azioni in base al piano di distribuzione.|  
  
### <a name="supported-extensibility-scenarios"></a>Scenari di estendibilità supportati  
È possibile implementare i collaboratori alla compilazione o distribuzione per consentire gli scenari di esempio seguenti:  
  
-   **Generare la documentazione dello schema durante una compilazione del progetto**: per supportare questo scenario, implementare un elemento [BuildContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx) ed eseguire l'override del metodo OnExecute per generare la documentazione dello schema. È possibile creare un file targets che definisce gli argomenti predefiniti che controllano se l'estensione viene eseguita e per specificare il nome del file di output.  
  
-   **Generare un report delle differenze quando un progetto SQL viene distribuito**: per supportare questo scenario, implementare [DeploymentPlanExecutor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanexecutor.aspx) che genera il file XML quando viene distribuito il progetto SQL.  
  
-   **Modificare il piano di distribuzione per modificare quando viene effettuato lo spostamento dei dati**: per supportare questo scenario, implementare [DeploymentPlanModifier](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentplanmodifier.aspx) ed eseguire l'iterazione del piano di distribuzione. Per ogni SqlTableMigrationStep nel piano, esaminare il risultato del confronto per determinare se il passaggio deve essere eseguito o ignorato.  
  
-   **Copiare i file nel dacpac generato quando viene distribuito un progetto SQL**: per supportare questo scenario, implementare un collaboratore alla distribuzione ed eseguire l'override del metodo OnEstablishDeploymentConfiguration per specificare quali file sono contrassegnati come DeploymentExtensionConfiguration dal sistema del progetto. Questi file devono essere copiati nella cartella di output e aggiunti all'interno del dacpac generato. È anche possibile modificare il collaboratore per unire più file in un nuovo file copiato nella cartella di output e aggiunto al manifesto di distribuzione. Durante la distribuzione, è possibile implementare il metodo OnApplyDeploymentConfiguration per estrarre questi file da dacpac e prepararli per l'utilizzo nel metodo OnExecute.  
  
È inoltre possibile esporre coppie personalizzate di argomenti nome/valore dal collaboratore scritti nel file progetto di database. È possibile utilizzare questi argomenti per consentire al collaboratore di estrarre informazioni da MSBuild o per consentire all'utente finale del collaboratore di personalizzare il comportamento. Ad esempio, è possibile consentire agli utenti di specificare il nome di un file di input o di output.  
  
## <a name="common-tasks"></a>Attività comuni  
  
|**Attività comuni**|**Contenuto di supporto**|  
|--------------------|--------------------------|  
|**Altre informazioni sui punti di estendibilità:** altre informazioni sulle classi di base usate per implementare i collaboratori alla compilazione e alla distribuzione.|[BuildContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.buildcontributor.aspx)<br /><br />[DeploymentContributor](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.deployment.deploymentcontributor.aspx)|  
|**Creare collaboratori di esempio:** informazioni sui passaggi necessari per creare un collaboratore alla compilazione o alla distribuzione. Se si utilizzano queste procedure dettagliate, è necessario:<br /><br />- Creare un collaboratore alla compilazione che genera un report in cui sono elencati tutti gli elementi del modello.<br />- Creare un collaboratore alla distribuzione che modifica il piano di distribuzione prima che venga eseguito.<br />- Creare un collaboratore alla distribuzione che genera un report di distribuzione quando si distribuisce un progetto SQL.<br /><br />È possibile creare tutti i collaboratori in un unico assembly o tra più assembly, a seconda di come si desidera che i collaboratori vengano distribuiti al team.|[Procedura dettagliata: Estendere la compilazione del progetto di database per generare statistiche del modello](../ssdt/walkthrough-extend-database-project-build-to-generate-model-statistics.md)<br /><br />[Procedura dettagliata: Estendere la distribuzione del progetto di database per modificare il piano di distribuzione](../ssdt/walkthrough-extend-database-project-deployment-to-modify-the-deployment-plan.md)<br /><br />[Procedura dettagliata: Estendere la distribuzione del progetto di database per analizzare il piano di distribuzione](../ssdt/walkthrough-extend-database-project-deployment-to-analyze-the-deployment-plan.md)|  
  
## <a name="see-also"></a>Vedere anche  
[Definire condizioni personalizzate per unit test SQL](https://msdn.microsoft.com/library/jj860449(v=vs.103).aspx)  
  
