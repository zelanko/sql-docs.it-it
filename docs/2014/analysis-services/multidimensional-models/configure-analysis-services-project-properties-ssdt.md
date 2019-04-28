---
title: Configurare proprietà di progetto di Analysis Services (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- VS.TOOLSOPTIONSPAGES.BUSINESS_INTELLIGENCE_DESIGNERS.ANALYSIS_SERVICES_DESIGNERS.GENERAL
helpviewer_keywords:
- projects [Analysis Services], properties
ms.assetid: d9786c66-7d8c-48e3-950d-3f25044b4ce2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb5490f023a2529d102d9ca505092b7f2bc28fec
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726825"
---
# <a name="configure-analysis-services-project-properties-ssdt"></a>Configurare proprietà di progetti di Analysis Services (SSDT)
  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene definito con determinate proprietà predefinite che influiscono sulla compilazione e sulla distribuzione del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Per modificare le proprietà del progetto, fare clic con il pulsante destro del mouse sul progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , quindi scegliere **Proprietà**. In alternativa, è possibile fare clic su **Proprietà** nel menu Progetto.  
  
## <a name="property-description"></a>Descrizione proprietà  
 Nella tabella seguente viene descritta ogni proprietà di progetto, viene elencato il relativo valore predefinito e vengono fornite informazioni sulla modifica del valore.  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|Edizione server di compilazione/distribuzione|Edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzata per sviluppare il progetto|Specifica l'edizione del server in cui verranno distribuiti i progetti. In caso di collaborazione su un progetto con più sviluppatori, gli sviluppatori devono conoscere l'edizione del server per determinare le funzionalità da incorporare nel progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Edizione server di compilazione/distribuzione|Versione utilizzata per sviluppare i progetti.|Specifica la versione del server in cui verranno distribuiti i progetti.|  
|Compila/Output|/bin|Percorso relativo per l'output del processo di compilazione del progetto|  
|Compila/Rimuovi password|True|Specifica l'eventuale rimozione delle password note dalle stringhe di connessione scritte nella directory di output durante il processo di compilazione. Rimuovendo le password viene incrementato il livello di sicurezza. Se vengono rimosse, le password dovranno essere immesse quando il progetto distribuito viene elaborato per consentire l'accesso di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ai dati di origine.|  
|Debug/Oggetto di avvio|\<Oggetto attivo >|Determina l'oggetto che viene avviato all'avvio del debug.|  
|Distribuzione/Modalità di distribuzione|Distribuisci solo modifiche|Per impostazione predefinita, vengono distribuite soltanto le modifiche agli oggetti di progetto (a condizione che non siano state apportate altre modifiche agli oggetti direttamente all'esterno del progetto). È inoltre possibile scegliere di distribuire tutti gli oggetti di progetto durante ogni distribuzione. Per prestazioni ottimali, utilizzare Distribuisci solo modifiche.|  
|Distribuzione/Opzione di elaborazione|Impostazione predefinita|Per impostazione predefinita, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] determina il tipo di elaborazione necessario quando vengono distribuite le modifiche agli oggetti. Ciò garantisce in genere tempi di distribuzione più rapidi. È inoltre possibile, tuttavia, scegliere di eseguire con ogni distribuzione l'elaborazione completa o nessuna elaborazione.|  
|Distribuzione/Distribuzione transazionale|False|Per impostazione predefinita, la distribuzione degli oggetti modificati o di tutti gli oggetti non è transazionale con l'elaborazione degli oggetti distribuiti. La distribuzione può avere esito positivo ed essere persistente anche in caso di esito negativo dell'elaborazione. Questa impostazione predefinita può essere modificata in modo da incorporare la distribuzione e l'elaborazione in una singola transazione.|  
|Server di distribuzione/destinazione|localhost|Per impostazione predefinita, gli oggetti di database all'interno del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] verranno distribuiti nell'istanza predefinita di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sul computer locale su cui viene usato [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] . Modificare questa impostazione predefinita per specificare un'istanza denominata sul computer locale o qualsiasi istanza su qualsiasi computer remoto per cui si dispone dell'autorizzazione necessaria per creare oggetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Distribuzione/Database|\<Nome progetto >|Per impostazione predefinita, il nome del database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in cui verrà creata un'istanza degli oggetti del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] durante la distribuzione corrisponde al nome del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al momento della relativa definizione. Modificare questa proprietà per cambiare il nome del database nell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specificata dalla proprietà Server.|  
  
## <a name="property-configurations"></a>Configurazioni delle proprietà  
 Le proprietà vengono definite in base alla configurazione. Le configurazioni di progetto consentono agli sviluppatori di utilizzare un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con impostazioni di compilazione, debug e distribuzione diverse senza modificare direttamente i file di progetto XML sottostanti.  
  
 Un progetto viene inizialmente creato con una singola configurazione, denominata Development. È possibile creare configurazioni aggiuntive e passare da una configurazione a un'altra mediante Gestione configurazione.  
  
 Finché non vengono create configurazioni aggiuntive, tutti gli sviluppatori utilizzano questa configurazione comune. Tuttavia, durante le diverse fasi di sviluppo - del progetto, ad esempio durante le attività iniziali di sviluppo e test di un progetto - sviluppatori diversi verrà può usare origini dati diverse e distribuire il progetto in server diversi per scopi diversi. Le configurazioni consentono di mantenere tali impostazioni diverse in file di configurazione diversi.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilare progetti di Analysis Services &#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)   
 [Distribuire progetti di Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
