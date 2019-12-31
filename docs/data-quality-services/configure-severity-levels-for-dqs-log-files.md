---
title: Configurare livelli di gravità per i file di log DQS
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.admin.config.log.f1
helpviewer_keywords:
- severity levels
- log files,severity levels
- dqs log files,severity levels
- logging,severity levels
- configure severity levels
ms.assetid: 66ffcdec-4bf7-4dd5-a221-fd9baefeeef4
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 4215cda5bfc82f0c6d195f336a1099309ab18154
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255644"
---
# <a name="configure-severity-levels-for-dqs-log-files"></a>Configurare livelli di gravità per i file di log DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritto come configurare i livelli di gravità per le varie attività e i vari moduli di [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) tramite il [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. I livelli di gravità definiscono l'intensità degli eventi che si verificano in DQS. Gli eventi DQS dispongono dei livelli di gravità seguenti, in ordine di gravità decrescente:  
  
-   **Fatale**: errori di runtime critici che potrebbero provocare risultati gravi/imprevisti.  
  
-   **Errore**: altri errori di Runtime.  
  
-   **Avviso: avvisi**sugli eventi che potrebbero generare un errore.  
  
-   **Info**: informazioni sugli eventi generali che non sono errori o avvisi. Ad esempio, un processo DQS avviato.  
  
-   **Debug**: informazioni dettagliate sull'evento.  
  
 Quando si configurano i livelli di gravità per varie attività e i vari moduli DQS, si filtrano le informazioni che si desidera registrare e scrivere nel file di log DQS per la rispettiva attività o modulo DQS. Se ad esempio si imposta il livello di gravità di un'attività DQS su **Avviso**, verranno registrati solo i messaggi di avviso e quelli con livello di gravità maggiore (Errore ed Errore irreversibile) associati all'attività DQS.  
  
##  <a name="BeforeYouBegin"></a>Prima di iniziare  
  
###  <a name="Security"></a>Sicurezza  
  
####  <a name="Permissions"></a>Autorizzazioni  
 Per configurare le impostazioni di gravità del log, è necessario disporre del ruolo dqs_administrator per il database DQS_MAIN.  
  
##  <a name="ConfigureActivity"></a>Configurare i livelli di gravità a livello di attività  
 In DQS è possibile configurare le impostazioni di gravità del log per le attività seguenti: gestione del dominio, individuazione delle informazioni, criteri di corrispondenza, pulizia dei dati, corrispondenza dei dati e servizi dati di riferimento. A tale scopo, procedere come segue:  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] fare clic su **Configurazione**.  
  
3.  Fare quindi clic sulla scheda **Impostazioni log** . Sono elencate le seguenti attività DQS per le quali è possibile selezionare un livello di gravità: **Gestione dominio**, **Individuazione informazioni**, **progetto di pulizia (ad esempio, RDS)**, **criteri di corrispondenza e progetto corrispondente** **e Servizi Desktop remoto.**  
  
4.  Selezionare il livello di gravità che si desidera registrare per un'attività DQS. È possibile selezionare uno tra i valori seguenti: **Errore irreversibile**, **Errore**, **Avviso**, **Informazioni**e **Debug**. Se ad esempio si desidera che nei file di log DQS vengano scritti solo i messaggi di errore irreversibile per l'attività di individuazione delle informazioni, selezionare **Errore irreversibile** nell'elenco a discesa dell'attività **Individuazione informazioni** .  
  
    > [!NOTE]  
    >  Per impostazione predefinita, è selezionato **Errore** per ognuna delle attività. Ciò significa che i messaggi di errore ed errore irreversibile verranno scritti nei file di log DQS per ogni attività per impostazione predefinita.  
  
5.  Fare clic su **Chiudi**.  
  
##  <a name="ConfigureModule"></a>Configurare i livelli di gravità a livello di modulo (avanzate)  
 La sezione **Avanzate** della scheda **Impostazioni log** consente di configurare le impostazioni di gravità del log a livello di modulo. I moduli sono assembly di sistema DQS che implementano varie funzionalità all'interno di una funzionalità in DQS. Ad esempio, l'attività di gestione del dominio contiene varie funzionalità quali la definizione di regole di dominio, la definizione di condizioni della regola, la definizione di regole tra domini per i domini compositi e così via.  
  
 Talvolta, il livello di granularità a livello di attività non è sufficiente. Può essere necessario esaminare un problema che si è verificato in un particolare modulo all'interno di un'attività. È possibile pertanto configurare i livelli di gravità del log a livello di modulo per isolare e tenere traccia del problema con maggiore precisione.  
  
 L'impostazione di gravità del log specificata a livello di attività determina l'impostazione di gravità del log di tutti i moduli che costituiscono l'attività. Tuttavia, in caso di conflitto tra le impostazioni di gravità del log a livello di attività e a livello di modulo, vengono considerate le impostazioni di gravità a livello di modulo.  
  
> [!NOTE]
>  -   Per impostazione predefinita, il modulo **Microsoft.Ssdqs.Core.Startup** viene preconfigurato nella sezione **Avanzate** con il livello di gravità impostato su **Informazioni**. Ciò consente di registrare gli eventi con il livello di gravità Informazioni e con un livello maggiore (Avviso, Errore ed Errore irreversibile) correlati all'avvio e all'arresto dei servizi DQS.  
> -   È consigliabile configurare i livelli di gravità del log a livello di modulo solo se si è un utente DQS avanzato con familiarità con gli assembly di sistema DQS.  
  
 Per configurare i livelli di gravità del log a livello di modulo:  
  
1.  Nella scheda **Impostazioni log** fare clic sulla freccia in giù accanto ad **Avanzate** per visualizzare l'area.  
  
2.  Nella griglia visualizzata selezionare un nome del modulo dall'elenco a discesa nella colonna **Modulo** .  
  
3.  Selezionare quindi un livello di gravità per il modulo dall'elenco a discesa nella colonna **Gravità** . È possibile selezionare uno tra i valori seguenti: **Errore irreversibile**, **Errore**, **Avviso**, **Informazioni**e **Debug**.  
  
     Ad esempio, all'interno dell'attività di gestione del dominio, è possibile impostare un livello di granularità diverso per la funzionalità di definizione di una regola di dominio rispetto all'attività di gestione del dominio selezionando il modulo **Microsoft.Ssdqs.DomainRules.Define** e selezionando un livello di gravità del log diverso. Analogamente, è possibile impostare un livello di granularità diverso per la funzionalità di definizione di una regola tra domini selezionando il modulo **Microsoft.Ssdqs.DomainRules.Condition.CrossDomain** e selezionando un livello di gravità del log diverso.  
  
4.  Ripetere i passaggi 2 e 3 per altri moduli, se necessario. È inoltre possibile aggiungere o eliminare righe nella griglia facendo clic sulle icone **Aggiungi modulo** e **Rimuovi modulo** .  
  
5.  Fare clic su **Chiudi**.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le impostazioni avanzate per i file di log DQS](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)  
  
  
