---
title: Pulizia dei dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e67136cc-f8c6-4cb3-ba0b-c966c636256c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 465d20f425a479f173ed5a9c2b5f5ec96ec7f707
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65480812"
---
# <a name="data-cleansing"></a>Data Cleansing
  La pulizia dei dati è il processo di analisi della qualità dei dati in un'origine dati, con l'approvazione o il rifiuto manuale dei suggerimenti del sistema e la conseguente modifica dei dati. La pulizia dei dati in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) include un processo assistito da computer, che analizza la conformità dei dati alle informazioni in una Knowledge Base, e un processo interattivo, che consente all'amministratore dei dati di rivedere e modificare i risultati del processo assistito da computer per assicurarsi che la pulizia dei dati risponda esattamente alle aspettative.  
  
 L'amministratore dei dati può anche eseguire la pulizia dei dati durante il processo di creazione dei pacchetti di Integration Services. In questo caso, l'amministratore dei dati utilizza il [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)] che permette di eseguire automaticamente la pulizia dei dati tramite una Knowledge Base esistente. Per altre informazioni, vedere [Trasformazione DQS Cleansing](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md).  
  
 La funzionalità di pulizia dei dati in DQS offre i vantaggi seguenti:  
  
-   Identifica dati incompleti o errati nell'origine dati (file di Excel o database SQL Server), quindi effettua le correzioni o avvisa in caso di dati non validi.  
  
-   Fornisce un processo a due passaggi per pulire i dati: *assistito da computer* e *interattivo*. Nel processo assistito da computer vengono utilizzate le informazioni di una Knowledge Base DQS per elaborare automaticamente i dati e vengono suggerite sostituzioni/correzioni. Nel passaggio interattivo successivo l'amministratore dei dati può approvare, rifiutare o modificare le modifiche proposte da DQS nel corso della pulizia assistita da computer.  
  
-   Standardizza e arricchisce dati dei clienti tramite valori e regole di dominio e dati di riferimento. Un esempio può essere la standardizzazione del termine "Lgo" in "Largo" o l'arricchimento dei dati con l'inserimento di elementi mancanti modificando "1 Microsoft way Redmond 98006" in "1 Microsoft Way, Redmond, WA 98006, Stati Uniti".  
  
-   Fornisce all'utente un'interfaccia simile a una procedura guidata semplice, intuitiva e coerente per spostarsi all'interno di dati e controllare errori in set di dati molto grandi.  
  
 Nella figura seguente viene illustrata la modalità di pulizia dei dati in DQS:  
  
 ![Processo di pulizia dei dati in DQS](../../2014/data-quality-services/media/dqs-cleansingprocess.gif "Processo di pulizia dei dati in DQS")  
  
##  <a name="ComputerAssisted"></a>Pulizia assistita da computer  
 Tramite il processo di pulizia dei dati DQS la Knowledge Base viene applicata ai dati da pulire e vengono proposte modifiche ai dati. L'amministratore dei dati può accedere a ogni modifica proposta, valutando e correggendo le modifiche. Per eseguire la pulizia dei dati, l'amministratore dei dati effettua le operazioni seguenti:  
  
1.  Creare un progetto Data Quality, selezionare una Knowledge Base rispetto alla quale analizzare e pulire i dati di origine e selezionare l'attività **Pulizia** . La stessa Knowledge Base può essere utilizzata per più progetti Data Quality.  
  
2.  Specificare la tabella/vista di database o un file di Excel che contiene i dati di origine da pulire. Il database o il file di Excel può corrispondere o meno a quello utilizzato per l'individuazione delle informazioni.  
  
    > [!NOTE]  
    >  Se si seleziona la stessa origine dati per le attività di individuazione delle informazioni e di pulizia, non si verificheranno modifiche ai dati. Si consiglia di eseguire l'individuazione delle informazioni su dati di esempio e successivamente pulire i dati di origine rispetto alle informazioni compilate durante l'attività di individuazione delle informazioni.  
  
3.  Eseguire il mapping dei campi dati da pulire ai domini singoli/composti appropriati nella Knowledge Base. Se si esegue il mapping di un campo a un dominio composito, il mapping avviene tra il campo e il dominio composito e non i domini singoli nel dominio composito. Inoltre, la pulizia dei dati per il campo di cui è stato eseguito il mapping viene effettuata in base alle regole specificate per il dominio composito e non per i domini singoli nel dominio composito. Per ulteriori informazioni sui domini compositi, vedere [DQS Knowledge Bases and Domains](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md).  
  
4.  Eseguire il processo di pulizia assistita da computer facendo clic su **Avvia** nella pagina **Pulisci**.  
  
 Il processo di pulizia dei dati consente di trovare la corrispondenza migliore tra un'istanza di dati e valori noti del dominio di dati. Con il processo vengono applicate le informazioni sulla qualità dei dati a tutti i dati di origine, a differenza del processo di individuazione delle informazioni che viene eseguito su una percentuale dei dati di esempio.  
  
 Il processo assistito da computer consente di visualizzare le informazioni sulla qualità dei dati nel [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] che verrà utilizzato per il processo interattivo di pulizia. Oltre al rispetto delle regole relative agli errori di sintassi, in DQS vengono utilizzati anche dati di riferimento e algoritmi avanzati per la classificazione dei dati in base a un *livello di confidenza*. Il livello di confidenza indica il grado di certezza in DQS in relazione alla correzione o al suggerimento. Il livello di confidenza è basato sui seguenti valori soglia:  
  
-   Un valore *soglia di correzione automatica* sopra la quale tramite DQS viene suggerita e apportata una modifica, a meno che questa non venga rifiutata dall'amministratore dei dati. È possibile specificare il valore soglia di correzione automatica nella scheda **Impostazioni generali** della schermata **Configurazione** . Per altre informazioni, vedere [Configurazione dei valori soglia per le attività di pulizia e di individuazione delle corrispondenze](../../2014/data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   Un valore *soglia di suggerimento automatico* sotto la soglia di correzione automatica, sopra la quale tramite DQS viene suggerita e apportata una modifica, se l'amministratore dei dati la approva. È possibile specificare il valore soglia di suggerimento automatico nella scheda **Impostazioni generali** della schermata **Configurazione** . Per altre informazioni, vedere [Configurazione dei valori soglia per le attività di pulizia e di individuazione delle corrispondenze](../../2014/data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
 Qualsiasi valore con un livello di confidenza inferiore al valore soglia di suggerimento automatico viene lasciato invariato da DQS a meno che l'amministratore dei dati specifichi una modifica.  
  
##  <a name="Interactive"></a>Pulizia interattiva  
 In base al processo di pulizia assistito da computer, all'amministratore dei dati vengono fornite le informazioni necessarie per prendere una decisione sulla modifica dei dati. DQS consente di suddividere i dati in categorie nelle cinque schede seguenti:  
  
-   **Suggeriti**: valori per i quali sono stati trovati suggerimenti con un livello di confidenza superiore al valore *soglia di suggerimento automatico* ma inferiore al valore *soglia di correzione automatica* . È necessario analizzare questi valori e approvarli o rifiutarli nel modo appropriato.  
  
-   **Nuovi**: valori validi per i quali DQS non dispone di informazioni sufficienti (suggerimento) e pertanto non è possibile eseguirne il mapping a qualsiasi altra scheda. Inoltre, questa scheda contiene anche valori con un livello di confidenza inferiore al valore *soglia di suggerimento automatico* , ma sufficientemente elevato per essere contrassegnati come validi.  
  
-   **Non validi**: valori contrassegnati come non validi nel dominio della Knowledge base o valori che non hanno superato una regola di dominio o dati di riferimento. Questa scheda conterrà anche valori rifiutati dall'utente nelle altre quattro schede durante il processo di pulizia interattiva.  
  
-   Con **correzione**: valori corretti da DQS durante il processo automatico di pulizia, nel caso in cui sia stata trovata una correzione per il valore con un livello di confidenza superiore al valore *soglia di correzione automatica* . Questa scheda conterrà anche valori per i quali l'utente ha specificato un valore corretto nella colonna **Correggi in** durante la pulizia interattiva e che ha quindi approvato facendo clic sul pulsante di opzione nella colonna **Approva** in una delle altre quattro schede.  
  
-   **Corretti**: valori trovati corretti. Ad esempio, un valore corrispondente a un valore di dominio. Se richiesto, è possibile eseguire l'override della pulizia DQS rifiutando i valori in questa scheda o specificando una parola alternativa nella colonna **Correggi in** e facendo clic quindi sul pulsante di opzione nella colonna **Accetta** . Questa scheda conterrà anche valori approvati dall'utente durante la pulizia interattiva facendo clic sul pulsante di opzione nella colonna **Approva** nelle schede **Nuovi** o **Non validi** .  
  
> [!NOTE]  
>  Nelle schede **Suggeriti**, **Con correzione**e **Corretti** viene visualizzato il valore iniziale per un dominio, se applicabile, nella colonna **Correggi in** rispetto al relativo valore del dominio.  
  
 L'amministratore dei dati utilizza il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] per visualizzare le modifiche proposte da DQS e decidere se implementarle o meno. Può verificare che i valori designati da DQS come corretti siano effettivamente corretti. Può verificare che le modifiche già apportate da DQS, con un livello di confidenza elevato, debbano essere effettivamente apportate. Può decidere se approvare le modifiche suggerite automaticamente. Infine, può rivedere i valori che non sono stati modificati, in caso desideri apportare una modifica non individuata tramite il processo assistito da computer.  
  
 Tramite DQS le modifiche effettuate dall'amministratore dei dati vengono unite ai risultati della pulizia dei dati assistita da computer. Queste modifiche vengono mantenute con il progetto, ma non vengono aggiunte alla Knowledge Base. Durante la pulizia dei dati, la Knowledge Base associata è di sola lettura.  
  
 Quando il processo di pulizia dei dati è stato completato, è possibile scegliere di esportare i dati elaborati in una nuova tabella in un database SQL Server, un file con estensione csv o un file di Excel. I dati di origine su cui viene eseguita la pulizia vengono mantenuti nello stato originale. L'amministratore dei dati può utilizzare i dati puliti separatamente per correggere i dati di origine effettivi.  
  
 Nella figura seguente viene illustrata la modalità di pulizia dei dati con l'applicazione [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] :  
  
 ![Pulizia dei dati nel client Data Quality](../../2014/data-quality-services/media/dqs-cleansingindqsclient.gif "Pulizia dei dati nel client Data Quality")  
  
##  <a name="Leading"></a>Correzione del valore iniziali  
 La correzione del valore iniziale si applica ai valori di dominio con sinonimi, quando l'utente desidera utilizzare uno dei sinonimi come valore iniziale, anziché altri, per rappresentare il valore in modo coerente. Ad esempio, "New York", "NYC" e "Grande mela" sono sinonimi e l'utente vuole usare "New York" come valore iniziale, anziché "NYC" e "Grande mela". DQS supporta la correzione del valore iniziale durante il processo di pulizia per consentire di standardizzare i dati. La correzione del valore iniziale viene effettuata solo se il dominio è stato opportunamente abilitato al momento della creazione. Per impostazione predefinita, tutti i domini sono abilitati per la correzione del valore iniziale a meno che sia stata deselezionata la casella di controllo **Utilizza valori iniziali** durante la creazione di un dominio. Per ulteriori informazioni su questa casella di controllo, vedere [Set Domain Properties](../../2014/data-quality-services/set-domain-properties.md).  
  
##  <a name="Standardize"></a>Standardizzare i dati puliti  
 È possibile scegliere se esportare i dati puliti nel formato standardizzato basato sul formato di output definito per i domini. Durante la creazione di un dominio, è possibile selezionare la formattazione che verrà applicata alla restituzione dei valori dei dati nel dominio. Per ulteriori informazioni sulla specifica dei formati di output per un dominio, vedere l'elenco **Formato output in** in [Set Domain Properties](../../2014/data-quality-services/set-domain-properties.md).  
  
 Durante l'esportazione dei dati puliti nella pagina **Esporta** della procedura guidata di pulizia del progetto Data Quality, va specificato se si desidera che i dati puliti vengano esportati nel formato standardizzato selezionando la casella di controllo **Standardizzare output** . Per impostazione predefinita, i dati puliti vengono esportati nel formato standardizzato, cioè la casella di controllo è selezionata. Per altre informazioni sull’esportazione dei dati puliti, vedere [Pulizia dei dati mediante le informazioni interne di DQS](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
##  <a name="Related"></a> Attività correlate  
  
|Descrizione dell'attività|Argomento|  
|----------------------|-----------|  
|Viene descritto come configurare valori soglia per l'attività di pulizia.|[Configurazione dei valori soglia per le attività di pulizia e di individuazione delle corrispondenze](../../2014/data-quality-services/configure-threshold-values-for-cleansing-and-matching.md)|  
|Viene descritto come pulire i dati utilizzando le informazioni incorporate in DQS.|[Pulire i dati mediante DQS &#40;informazioni interne sulla&#41;](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md)|  
|Viene descritto come pulire i dati utilizzando le informazioni del servizio dati di riferimento.|[Pulire i dati usando dati di riferimento &#40;conoscenza&#41; esterna](../../2014/data-quality-services/cleanse-data-using-reference-data-external-knowledge.md)|  
|Viene descritto come pulire un dominio composito.|[Pulire i dati in un dominio composito](../../2014/data-quality-services/cleanse-data-in-a-composite-domain.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Progetti Data Quality &#40;&#41;DQS](../../2014/data-quality-services/data-quality-projects-dqs.md)   
 [Corrispondenza di dati](../../2014/data-quality-services/data-matching.md)  
  
  
