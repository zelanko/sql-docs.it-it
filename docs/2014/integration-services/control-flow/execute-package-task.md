---
title: Attività Esegui pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executepackagetask.f1
helpviewer_keywords:
- Execution Package task [Integration Services]
- child packages
- parent packages [Integration Services]
ms.assetid: 042d4ec0-0668-401c-bb3a-a25fe2602eac
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 59b623076e86f3bacf5ae8c6e24b48774e33f670
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62831910"
---
# <a name="execute-package-task"></a>Attività Esegui pacchetto
  L'attività Esegui pacchetto permette di estendere le funzionalità aziendali di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] consentendo ai pacchetti di eseguire altri pacchetti nell'ambito di un flusso di lavoro.  
  
 È possibile utilizzare l'attività Esegui pacchetto per gli scopi seguenti:  
  
-   Suddivisione del flusso di lavoro di pacchetti complessi. Questa attività consente di suddividere il flusso di lavoro in più pacchetti, più semplici da leggere, testare e gestire. Se ad esempio si caricano dati in uno schema star, sarà possibile compilare un pacchetto a parte per il popolamento delle singole dimensioni e della tabella dei fatti.  
  
-   Riutilizzo di parti di pacchetti. È possibile riutilizzare parti del flusso di lavoro di un pacchetto in altri pacchetti. È ad esempio possibile compilare un modulo di estrazione dati che può essere chiamato da pacchetti diversi. Ogni pacchetto che chiama il modulo di estrazione può quindi eseguire operazioni diverse di ripulitura, filtraggio o aggregazione dei dati.  
  
-   Raggruppamento di unità di lavoro. Le unità di lavoro possono essere incapsulate in pacchetti separati ed è possibile crearne un join come componenti transazionali al flusso di lavoro di un pacchetto padre. Il pacchetto padre esegue ad esempio i pacchetti accessori e, in base all'esito positivo o negativo dell'esecuzione di questi ultimi, esegue il commit o il rollback della transazione.  
  
-   Controllo della sicurezza dei pacchetti. Gli autori dei pacchetti hanno l'esigenza di accedere solo a una parte di una soluzione composta da più pacchetti. Suddividendo un pacchetto in più pacchetti è possibile offrire un livello di sicurezza superiore, perché a ogni autore è possibile concedere l'accesso ai soli pacchetti interessati.  
  
 Un pacchetto che esegue altri pacchetti è detto in genere pacchetto padre, mentre i pacchetti eseguiti dal flusso di lavoro di un pacchetto padre sono detti pacchetti figlio.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include attività per l'esecuzione delle operazioni del flusso di lavoro, ad esempio l'esecuzione di eseguibili e file batch. Per altre informazioni, vedere [Attività Esegui processo](execute-process-task.md).  
  
## <a name="running-packages"></a>Esecuzione di pacchetti  
 L'attività Esegui pacchetto consente di eseguire i pacchetti figlio contenuti nello stesso progetto in cui è contenuto il pacchetto padre. Per selezionare un pacchetto figlio dal progetto, impostare la proprietà **ReferenceType** su **Riferimento al progetto**e quindi impostare la proprietà **PackageNameFromProjectReference** .  
  
> [!NOTE]  
>  L'opzione **ReferenceType** è di sola lettura e viene impostata su **Riferimento esterno** se il progetto in cui è contenuto il pacchetto non è stato convertito nel modello di distribuzione del progetto. Per altre informazioni sulla conversione, vedere [Distribuire progetti nel server Integration Services](../deploy-projects-to-integration-services-server.md).  
  
 L'attività Esegui pacchetto può eseguire sia pacchetti archiviati nel database msdb di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che pacchetti archiviati nel file system. L'attività usa una gestione connessione OLE DB per connettersi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o una gestione connessione file per l'accesso al file system. Per altre informazioni, vedere [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md) e [File Connection Manager](../connection-manager/flat-file-connection-manager.md).  
  
 Poiché l'attività Esegui pacchetto consente anche di eseguire un piano di manutenzione database, è possibile gestire sia pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)] che piani di manutenzione database nella stessa soluzione di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Un piano di manutenzione database è simile a un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] , ma può includere solo attività di manutenzione del database e viene sempre archiviato nel database msdb.  
  
 Se si sceglie un pacchetto archiviato nel file system, sarà necessario specificare il nome e il percorso del pacchetto. Il pacchetto può risiedere in qualunque posizione del file system e non deve necessariamente trovarsi nella stessa cartella del pacchetto padre.  
  
 Il pacchetto figlio può essere eseguito nel processo del pacchetto padre o in un processo a parte. L'esecuzione del pacchetto figlio in un processo a parte richiede più memoria, ma offre maggiore flessibilità. Se ad esempio il processo figlio non riesce, il processo padre potrà continuare l'esecuzione.  
  
 Talvolta può essere tuttavia necessario che l'esito dei pacchetti padre e figlio venga determinato come per una singola unità oppure si desidera evitare l'overhead di un processo aggiuntivo. Se ad esempio un processo figlio non riesce e nel processo padre la fase successiva dell'elaborazione dipende dal completamento del processo figlio, è preferibile eseguire il pacchetto figlio nello stesso processo del pacchetto padre.  
  
 Per impostazione predefinita, la proprietà ExecuteOutOfProcess dell'attività Esegui pacchetto è impostata su `False`, e il pacchetto figlio viene eseguito nello stesso processo del pacchetto padre. Se si imposta questa proprietà su `True`, il pacchetto figlio viene eseguito in un processo separato. In questo modo è possibile che l'avvio del pacchetto figlio sia rallentato. Inoltre, se si imposta la proprietà su `True`, non è possibile eseguire il debug del pacchetto in un'installazione di soli strumenti. È necessario installare [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Per altre informazioni, vedere [Installazione di Integration Services](../install-windows/install-integration-services.md).  
  
## <a name="extending-transactions"></a>Estensione delle transazioni  
 Poiché la transazione utilizzata dal pacchetto padre può essere estesa al pacchetto figlio, è possibile eseguire in un'unica operazione il commit o il rollback di tutte le operazioni eseguite dai due pacchetti. È ad esempio possibile eseguire il commit o il rollback degli inserimenti nel database eseguiti dal pacchetto padre a seconda dell'esito degli inserimenti nel database eseguiti dal pacchetto figlio e viceversa. Per altre informazioni, vedere [Transazioni ereditate](../inherited-transactions.md).  
  
## <a name="propagating-logging-details"></a>Propagazione dei dettagli di registrazione  
 Il pacchetto figlio eseguito dall'attività Esegui pacchetto invia sempre i dettagli di registrazione al pacchetto padre, anche se non è configurato per l'utilizzo della registrazione. I dettagli ricevuti dal pacchetto figlio verranno tuttavia registrati solo se l'attività Esegui pacchetto è configurata per l'utilizzo della registrazione. Per altre informazioni, vedere [registrazione di Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md).  
  
## <a name="passing-values-to-child-packages"></a>Passaggio di valori ai pacchetti figlio  
 I pacchetti figlio utilizzano in genere valori ricevuti dal pacchetto chiamante, che normalmente è il pacchetto padre. L'utilizzo di valori ricevuti da un pacchetto padre può essere utile negli scenari seguenti:  
  
-   Parti di un flusso di lavoro più grande sono assegnate a pacchetti diversi. È ad esempio possibile creare un pacchetto che scarica dati durante la notte, li riepiloga, assegna i valori di riepilogo alle variabili appropriate e quindi le passa a un altro pacchetto per un'ulteriore elaborazione dei dati.  
  
-   Il pacchetto padre coordina dinamicamente le attività in un pacchetto figlio. Il pacchetto padre determina ad esempio il numero dei giorni del mese corrente e lo assegna a una variabile, di modo che il pacchetto figlio esegua una determinata attività per il numero di volte indicato da tale valore.  
  
-   Un pacchetto figlio deve accedere ai dati derivati dinamicamente dal pacchetto padre. Ad esempio, il pacchetto padre estrae dati da una tabella e carica il set di righe in una variabile, quindi il pacchetto figlio esegue ulteriori elaborazioni su tali dati.  
  
 È possibile utilizzare i metodi seguenti per passare valori a un pacchetto figlio:  
  
-   **Configurazioni di pacchetto**  
  
     [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] offre un tipo di configurazione, cioè Variabile pacchetto padre, per il passaggio dei valori dal pacchetto padre a quello figlio. Tale configurazione è compilata in base al pacchetto figlio e utilizza una variabile del pacchetto padre. Viene quindi eseguito il mapping della configurazione a una variabile nel pacchetto figlio o alla proprietà di un oggetto nel pacchetto figlio. La variabile può anche essere utilizzata negli script eseguiti dall'attività Script o dal componente script.  
  
-   **Parametri**  
  
     È possibile configurare l'attività Esegui pacchetto per eseguire il mapping delle variabili o dei parametri del pacchetto padre o dei parametri del progetto ai parametri del pacchetto figlio. Il progetto deve utilizzare il modello di distribuzione del progetto e il pacchetto figlio deve essere contenuto nello stesso progetto in cui è contenuto il pacchetto padre. Per altre informazioni, vedere [Editor attività Esegui pacchetto](../execute-package-task-editor.md).  
  
    > [!NOTE]  
    >  Se il parametro del pacchetto figlio non è sensibile e ne viene eseguito il mapping a un parametro padre sensibile, non sarà possibile completare l'esecuzione del pacchetto figlio.  
    >   
    >  Sono supportate le seguenti condizioni di mapping:  
    >   
    >  -   Viene eseguito il mapping del parametro del pacchetto figlio sensibile a un parametro padre sensibile  
    > -   Viene eseguito il mapping del parametro del pacchetto figlio sensibile a un parametro padre non sensibile  
    > -   Viene eseguito il mapping del parametro del pacchetto figlio non sensibile a un parametro padre non sensibile  
  
 La variabile del pacchetto padre può essere definita nell'ambito dell'attività Esegui pacchetto o in un contenitore padre, ad esempio il pacchetto. Se sono presenti più variabili con lo stesso nome, verrà utilizzata quella definita nell'ambito dell'attività Esegui pacchetto oppure quella con ambito più vicino all'attività.  
  
 Per altre informazioni, vedere [Utilizzare i valori di variabili e parametri in un pacchetto figlio](../use-the-values-of-variables-and-parameters-in-a-child-package.md).  
  
### <a name="accessing-parent-package-variables"></a>Accesso alle variabili del pacchetto padre  
 Utilizzando l'attività Script è possibile consentire ai pacchetti figlio di accedere alle variabili del pacchetto padre. Quando si immette il nome della variabile del pacchetto padre nella pagina **Script** di **Editor attività Script**, non includere **User:** nel nome della variabile. In caso contrario, il pacchetto figlio non individua la variabile quando si esegue il pacchetto padre. Per altre informazioni sull'utilizzo dell'attività Script per accedere alle variabili del pacchetto padre, vedere questo post di blog, [SSIS: Accesso alle variabili in un pacchetto padre](https://andyleonard.blog/2015/08/ssis-design-pattern-access-parent-variables-from-a-child-package-in-the-ssis-catalog/).  
  
## <a name="configuring-the-execute-package-task"></a>Configurazione dell'attività Esegui pacchetto  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività Esegui pacchetto](../execute-package-task-editor.md)  
  
-   [Pagina Espressioni](../expressions/expressions-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>Attività correlate  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Intervento nel blog concernente [SSIS: Esecuzione dei pacchetti figlio in-process o out-of-process? ](https://go.microsoft.com/fwlink/?LinkId=220819), sul sito Web consultingblogs.emc.com.  
  
-   Intervento nel blog concernente [SSIS: Accesso alle variabili in un pacchetto padre](https://andyleonard.blog/2015/08/ssis-design-pattern-access-parent-variables-from-a-child-package-in-the-ssis-catalog/), su andyleonard.blog. 
  
  
