---
title: Abilitare la modalità DirectQuery di Analysis Services in SSMS | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 27e704e6274910e2c9e3f77fe235e02918d95425
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072208"
---
# <a name="enable-directquery-mode-in-ssms"></a>Abilitare la modalità DirectQuery in SSMS
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  È possibile modificare le proprietà di accesso ai dati di un modello tabulare già distribuito abilitando la modalità DirectQuery, con la quale le query vengono eseguite su un'origine dati relazionale di back-end e non sui dati memorizzati nella cache che risiedono in memoria.  
  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], i passaggi per la configurazione di DirectQuery variano in base al livello di compatibilità del modello. Di seguito sono elencati i passaggi validi per tutti i livelli di compatibilità.  
  
 Questo articolo si presuppone di aver creato e convalidato un modello tabulare in memoria a livello di compatibilità 1200 o superiore e solo necessità di abilitare l'accesso DirectQuery e aggiornare le stringhe di connessione. Se si inizia da un livello di compatibilità inferiore, è necessario prima di tutto aggiornarlo manualmente. Per informazioni sulla procedura, vedere [Aggiornare Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md) .  
  
> [!IMPORTANT]  
>  È consigliabile usare [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] anziché Management Studio per alternare le diverse modalità di archiviazione di dati. Quando si usa  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] per cambiare modello e poi si esegue la distribuzione nel server, il modello e il database rimangano sincronizzati. Inoltre, la modifica delle modalità di archiviazione nel modello consente di verificare eventuali errori di convalida. Quando si usa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] come descritto in questo articolo, gli errori di convalida non vengono segnalati.  
  
## <a name="requirements"></a>Requisiti  
 L'abilitazione dell'uso della modalità DirectQuery su un modello tabulare è un processo a più passaggi.  
  
-   Assicurarsi che il modello non disponga di funzionalità che potrebbero causare errori di convalida in modalità DirectQuery e quindi modificare la modalità di archiviazione di dati del modello in memoria per DirectQuery.  
  
     Un elenco di restrizioni di funzionalità è documentato in [la modalità DirectQuery](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).  
  
-   Esaminare la stringa di connessione e le credenziali usate dal database distribuito per recuperare i dati dai database di back-end esterni. Assicurarsi che vi sia una sola connessione e che le relative impostazioni siano adatte per l'esecuzione di query.  
  
     I database tabulari che non sono stati appositamente progettati per DirectQuery potrebbero avere più connessioni che ora devono essere ridotte a una sola, come necessario per la modalità DirectQuery.  
  
     Le credenziali originariamente usate per l'elaborazione dei dati sono ora usate per eseguire query sui dati. Come parte della configurazione di DirectQuery, esaminare ed eventualmente modificare l'account se si usano account diversi per le operazioni dedicate.  
  
     La modalità DirectQuery è l'unico scenario in cui Analysis Services esegue la delega trusted. Se la soluzione richiede la delega per ottenere risultati di query specifiche dell'utente, l'account usato per connettersi al database back-end deve poter delegare l'identità dell'utente che effettua la richiesta e le identità utente devono disporre di autorizzazioni di lettura per il database back-end.  
  
-   Infine, confermare l'operatività della modalità DirectQuery eseguendo una query.  
  
## <a name="step-1-check-the-compatibility-level"></a>Passaggio 1: Controllare il livello di compatibilità  
 Le proprietà che definiscono l'accesso ai dati sono diverse per i diversi livelli di compatibilità. Un passaggio preliminare consiste nel verificare quale sia il livello di compatibilità del database.  
  
1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] connettersi all'istanza che contiene il modello tabulare.  
  
2.  In Esplora oggetti fare doppio clic sul database > **Proprietà** > **Livello di compatibilità**.  
  
     Il valore sarà **SQL Server 2016 (1200)** o un livello precedente come **SQL Server 2012 SP1 o versione successiva (1103)**. Nel passaggio successivo, seguire le istruzioni adatte al livello di compatibilità.  
  
 Quando si modifica un modello tabulare in modalità DirectQuery, la nuova modalità di archiviazione di dati diventa effettiva immediatamente.  
  
## <a name="step-2a-switch-a-tabular-1200-database-to-directquery-mode"></a>Passaggio 2a: Passare un database tabulare 1200 alla modalità DirectQuery  
  
1.  In Esplora oggetti, fare clic sul database > **Proprietà** > **Modello** > **Modalità predefinita**.  
  
2.  Impostare la modalità su **DirectQuery**.  
  
    |||  
    |-|-|  
    |**Valori validi**|**Descrizione**|  
    |**DirectQuery**|Le query vengono eseguite in un database relazionale di back-end, tramite la connessione all'origine dati definita per il modello.<br /><br /> Le query sul modello vengono convertite in query native di database e reindirizzate all'origine dati.<br /><br /> Quando si elabora un modello impostato sulla modalità DirectQuery, vengono compilati e distribuiti solo i metadati. I dati sono esterni al modello e risiedono nei file di database dell'origine dati operativa.|  
    |**Importa**|Le query vengono eseguite nel database tabulare in MDX o DAX.<br /><br /> Quando si elabora un modello impostato sulla modalità di importazione, i dati vengono recuperati da un'origine dati back-end e archiviati su disco. Quando si carica il database, i dati vengono copiati completamente in memoria, consentendo query e scansioni di tabella rapide.<br /><br /> Si tratta della modalità predefinita per i modelli tabulari ed è l'unica modalità per determinate origini dati (non relazionali).|  
  
## <a name="step-2b-switch-a-tabular-1100-1103-database-to-directquery-mode"></a>Passaggio 2b: Passare un database tabulare 1100-1103 alla modalità DirectQuery  
  
1.  In Esplora oggetti fare clic sul database > **Proprietà** > **Database** > **DirectQueryMode**.  
  
2.  Impostare la modalità su **DirectQuery**.  
  
     Le proprietà della modalità predefinita sono le seguenti:  
  
    |||  
    |-|-|  
    |**Valori validi**|**Descrizione**|  
    |**InMemory**|Le query usano solo i dati memorizzati nella cache, in memoria.|  
    |**InMemorywithDirectQuery**|le query usano la cache per impostazione predefinita, salvo diversa indicazione nella stringa di connessione del client.<br /><br /> Si tratta di una modalità ibrida in cui le partizioni sono configurate singolarmente per l'uso in memoria o in DirectQuery.|  
    |**DirectQuery**|le query usano solo l'origine dati relazionale.|  
    |**DirectQuerywithInMemory**|le query usano l'origine dati relazionale per impostazione predefinita, salvo diversa indicazione nella stringa di connessione del client.<br /><br /> Si tratta di una modalità ibrida in cui le partizioni sono configurate singolarmente per l'uso in memoria o in DirectQuery.|  
  
 **Archiviazione ibrida dei dati**  
  
 Quando si usa una combinazione di accesso in memoria e basato su disco, la cache è ancora disponibile e può essere usata per le query. In una modalità ibrida sono disponibili molte opzioni:  
  
-   Quando la cache e l'origine dati relazionale sono entrambe disponibili, è possibile impostare il metodo di connessione preferito, ma sarà il client a stabilire in definitiva quale origine verrà utilizzata, tramite la proprietà della stringa di connessione DirectQueryMode.  
  
-   È anche possibile configurare le partizioni nella cache in modo che quella primaria usata per la modalità DirectQuery non venga mai elaborata e faccia sempre riferimento all'origine relazionale. Sono disponibili molti modi per utilizzare le partizioni allo scopo di ottimizzare la progettazione dei modelli e la creazione di report. Per altre informazioni, vedere [definire le partizioni nei modelli DirectQuery](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md).  
  
-   Dopo avere distribuito il modello, è possibile modificare il metodo di connessione preferito. È ad esempio possibile utilizzare una modalità ibrida per i test e passare alla modalità **Solo DirectQuery** unicamente dopo avere testato accuratamente eventuali report o query che utilizzano il modello. Per altre informazioni, vedere [Impostare o modificare il metodo di connessione preferito per DirectQuery](http://msdn.microsoft.com/library/f10d5678-d678-4251-8cce-4e30cfe15751).  
  
## <a name="step-3-check-the-connection-properties-on-the-database"></a>Passaggio 3: Controllare le proprietà di connessione nel database  
 In base all'impostazione della configurazione della connessione all'origine dati, il passaggio a DirectQuery potrebbe modificare il contesto di sicurezza della connessione. Dopo aver modificato la modalità di accesso ai dati, esaminare le proprietà della rappresentazione e della stringa di connessione per verificare che l'account di accesso sia valido per le connessioni in corso al database back-end.  
  
 Esaminare la sezione **Configurare Analysis Services per la delega trusted** in [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md) per informazioni sulla delega di un'identità utente per gli scenari di DirectQuery.  
  
1.  In Esplora oggetti espandere **Connessioni** e fare doppio clic su una connessione per visualizzarne le proprietà.  
  
     Per i modelli DirectQuery deve essere definita una sola connessione per il database e l'origine dati deve essere relazionale e di un tipo di database supportato. Visualizzare [origini dati supportate](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md).  
  
2.  **Stringa di connessione** deve specificare il server, il nome del database e il metodo di autenticazione usati nelle operazioni di DirectQuery. Se si usa l'autenticazione di SQL Server, è possibile specificare qui l'account di accesso al database.  
  
3.  L'opzione**Impostazioni di rappresentazione** viene usata per l'autenticazione di Windows. Le opzioni valide per i modelli tabulari in modalità DirectQuery sono le seguenti:  
  
    -   **Usa account del servizio**. Scegliere questa opzione se l'account del servizio Analysis Services dispone di autorizzazioni di lettura per il database relazionale.  
  
    -   **Usa nome utente e password specifici**. Specificare un account utente di Windows che disponga di autorizzazioni di lettura per il database relazionale.  
  
 Si noti che queste credenziali vengono utilizzate unicamente per rispondere alle query sull'archivio dati relazionale. Non corrispondono alle credenziali utilizzate per l'elaborazione della cache di un modello ibrido.  
  
 La rappresentazione non può essere utilizzata se il modello viene utilizzato solo in memoria. L'impostazione **ImpersonateCurrentUser**non è valida, a meno che il modello non utilizzi la modalità DirectQuery.  
  
## <a name="step-4-validate-directquery-access"></a>Passaggio 4: Convalidare l'accesso DirectQuery  
  
1.  Avviare una traccia con SQL Server Profiler o XEvent in Management Studio, connesso al database relazionale su SQL Server.  
  
     Se si usano Oracle or Teradata, adottare gli strumenti di traccia adeguati a queste piattaforme di database.  
  
2.  In Management Studio, immettere ed eseguire una semplice query MDX, ad esempio `select <some measure> on 0 from model.`.  
  
3.  Nella traccia, l'esecuzione della query viene evidenziata nel database relazionale.  
  
## <a name="see-also"></a>Vedere anche  
 [Livello di compatibilità](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Origini dati supportate](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [Eventi estesi](../../relational-databases/extended-events/extended-events.md)   

  
  
