---
title: Sviluppo di oggetti personalizzati per Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services]
- custom objects [Integration Services]
ms.assetid: ca1929a6-0ae6-47d7-b65f-08173b143720
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7b621ebd5750d918c22f61ac005b02e1b8bea187
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297220"
---
# <a name="developing-custom-objects-for-integration-services"></a>Sviluppo di oggetti personalizzati per Integration Services

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Quando gli oggetti del flusso di controllo e del flusso di dati inclusi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non soddisfano completamente specifici requisiti, è possibile sviluppare molti tipi di oggetti personalizzati, tra cui:  
  
-   **Attività personalizzate**.  
  
-   **Gestioni connessioni personalizzate**. Consentono la connessione a origini dati esterne attualmente non supportate.  
  
-   **Provider di log personalizzati**. Consentono di registrare eventi dei pacchetti in formati attualmente non supportati.  
  
-   **Enumeratori personalizzati**. Supportano l'iterazione in un set di oggetti o valori in formati attualmente non supportati.  
  
-   **Componenti flusso di dati personalizzati**. Possono essere configurati come origini, trasformazioni o destinazioni.  
  
 Il modello a oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] facilita questo sviluppo personalizzato con classi di base che forniscono un framework coerente e affidabile per l'implementazione personalizzata.  
  
 Se non è necessario riutilizzare la funzionalità personalizzata in più pacchetti, l'attività Script e il componente script offrono tutte le funzionalità di un linguaggio di programmazione gestito con una quantità decisamente minore di codice dell'infrastruttura da scrivere Per altre informazioni, vedere [Confronto tra soluzioni di scripting e oggetti personalizzati](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md).  
  
## <a name="steps-in-developing-a-custom-object-for-integration-services"></a>Passaggi per lo sviluppo di un oggetto personalizzato Integration Services  
 Quando si sviluppa un oggetto personalizzato per l'utilizzo in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], è necessario sviluppare una libreria di classi (DLL) che verrà caricata in fase di progettazione e di esecuzione da Progettazione SSIS e dal runtime di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. I metodi più importanti che è necessario implementare non sono quelli che lo sviluppatore chiama dal codice personalizzato, ma quelli chiamati dal runtime nei momenti appropriati per inizializzare e convalidare i componenti e richiamarne le funzionalità.  
  
 Di seguito sono riportati i passaggi che è necessario completare per lo sviluppo di un oggetto personalizzato:  
  
1.  Creare un nuovo progetto di tipo Libreria di classi nel linguaggio di programmazione gestito preferito.  
  
2.  Ereditare dalla classe di base appropriata, come illustrato nella tabella seguente.  
  
3.  Applicare l'attributo appropriato alla nuova classe, come illustrato nella tabella seguente.  
  
4.  Eseguire l'override dei metodi della classe di base, se necessario, e scrivere codice per la funzionalità personalizzata dell'oggetto.  
  
5.  Facoltativamente, compilare un'interfaccia utente personalizzata per il componente. Per agevolare la distribuzione, è possibile sviluppare l'interfaccia utente come progetto distinto nella stessa soluzione e compilarla come assembly distinto.  
  
6.  Facoltativamente, visualizzare un collegamento a esempi e contenuto della Guida per l'oggetto personalizzato nella **Casella degli strumenti SSIS**.  
  
7.  Compilare, distribuire ed eseguire il debug del nuovo oggetto personalizzato come descritto in [Compilazione, distribuzione e debug di oggetti personalizzati](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md).  
  
## <a name="base-classes-attributes-and-important-methods"></a>Classi di base, attributi e metodi importanti  
 In questa tabella viene fornito un riferimento rapido agli elementi più importanti del modello a oggetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per ogni tipo di oggetto personalizzato che è possibile sviluppare.  
  
|Oggetto personalizzato|Classe di base|Attributo|Metodi importanti|  
|-------------------|----------------|---------------|-----------------------|  
|Attività|<xref:Microsoft.SqlServer.Dts.Runtime.Task>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A>|  
|Gestione connessione|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ReleaseConnection%2A>|  
|Provider di log|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.OpenLog%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A>, <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.CloseLog%2A>|  
|Enumeratore|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator>|<xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute>|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A>|  
|Componente del flusso di dati|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>|<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>|<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>, <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>|  
  
## <a name="providing-links-to-samples-and-help-content"></a>Collegamenti a esempi e contenuto della Guida  
 Per visualizzare un collegamento nella **Casella degli strumenti SSIS** a esempi e contenuto della Guida per un oggetto personalizzato scritto in codice gestito, usare le proprietà seguenti.  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.SamplesTag%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpCollection%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DTSPipelineComponentAttribute.HelpKeyword%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.SamplesTag%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpCollection%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DTSTaskAttribute.HelpKeyword%2A>  
  
 Per visualizzare un collegamento a esempi e contenuto della Guida per un oggetto personalizzato scritto in codice nativo, aggiungere voci nel file (con estensione rgs) dello script del Registro di sistema per SamplesTag, HelpKeyword e HelpCollection. Di seguito è riportato un esempio.  
  
 `val HelpKeyword = s 'sql11.dts.designer.executepackagetask.F1'`  
  
 `val SamplesTag = s 'ExecutePackageTask'`  
  
## <a name="providing-a-custom-user-interface"></a>Sviluppo di un'interfaccia utente personalizzata  
 Per consentire agli utenti dell'oggetto personalizzato di configurarne le proprietà, può essere necessario sviluppare anche un'interfaccia utente personalizzata. Nei casi in cui un'interfaccia utente personalizzata non sia strettamente necessaria, è possibile scegliere di crearne una per fornire un'interfaccia più intuitiva rispetto all'editor predefinito.  
  
 In un progetto o assembly di interfaccia utente personalizzata sono in genere incluse due classi: una classe che implementa un'interfaccia [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per le interfacce utente per il tipo specifico di oggetto personalizzato e il Windows Form che l'interfaccia visualizza per raccogliere informazioni dall'utente. Le interfacce che si implementano includono solo alcuni metodi e un'interfaccia utente personalizzata non è difficile da sviluppare.  
  
> [!NOTE]  
>  Molti provider di log di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] hanno un'interfaccia utente personalizzata che implementa <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> e sostituisce la casella di testo **Configurazione** con un elenco a discesa filtrato di gestioni connessioni disponibili. Tuttavia, le interfacce utente personalizzate per i provider di log personalizzati non sono implementate in questa versione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. L'impostazione di un valore per la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute.UITypeName%2A> di <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> non ha alcun effetto.  
  
 Nella tabella seguente viene fornito un riferimento rapido alle interfacce che è necessario implementare quando si sviluppa un'interfaccia utente personalizzata per ogni tipo di oggetto personalizzato. Viene inoltre illustrato ciò che l'utente visualizza se si sceglie di non sviluppare un'interfaccia utente personalizzata per l'oggetto oppure se l'oggetto non viene collegato alla relativa interfaccia utente tramite la proprietà **UITypeName** nell'attributo dell'oggetto. Anche se il potente editor avanzato può essere soddisfacente per un componente del flusso di dati personalizzato, la finestra delle proprietà è una soluzione meno semplice da utilizzare per attività e gestioni connessioni e un enumeratore Foreach personalizzato non può essere configurato senza un form personalizzato.  
  
|Oggetto personalizzato|Classe di base per l'interfaccia utente|Comportamento di modifica predefinito senza un'interfaccia utente personalizzata|  
|-------------------|-----------------------------------|----------------------------------------------------------------------|  
|Attività|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsTaskUI>|Solo finestra delle proprietà|  
|Gestione connessione|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsConnectionManagerUI>|Solo finestra delle proprietà|  
|Provider di log|<xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI><br /><br /> (non implementato in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)])|Casella di testo nella colonna **Configurazione**|  
|Enumeratore|<xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumeratorUI>|Solo finestra delle proprietà. L'area Configurazione enumeratore dell'editor è vuota.|  
|Componente del flusso di dati|<xref:Microsoft.SqlServer.Dts.Pipeline.Design.IDtsComponentUI>|Editor avanzato|  
  
## <a name="external-resources"></a>Risorse esterne  
  
-   Intervento nel blog, [Il processo di compilazione della soluzione per Visual Studio restituisce un avviso sulla dipendenza indiretta dall'assembly .NET Framework a causa dei riferimenti SSIS](https://go.microsoft.com/fwlink/?LinkId=215662), su blogs.msdn.com.  
  
## <a name="see-also"></a>Vedere anche  
 [Persistenza degli oggetti personalizzati](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [Compilazione, distribuzione e debug di oggetti personalizzati](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
  
  
