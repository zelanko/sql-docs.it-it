---
title: Guida sensibile al contesto di Gestione Utilità | Microsoft Docs
ms.custom: ''
ms.date: 08/19/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: reference
f1_keywords:
- sql13.swb.ue.navigation.f1
- sql13.SWB.UE.dac.details.F1
- sql13.SQB.UE.dac.details.F1
- utility details
helpviewer_keywords:
- Utility
- management
- data-tier application
ms.assetid: 8697e4a4-4f59-4cda-af71-7de86005bd4a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1dd8c492c2353793ad195cea9606a89c502dc5f1
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68024493"
---
# <a name="utility-explorer-f1-help"></a>Guida sensibile al contesto di Gestione Utilità
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Le sezioni seguenti includono informazioni sulle funzionalità di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e sulle operazioni associate.  
  
  ## <a name="utility-dashboard-sql-server-utility"></a>Dashboard Utilità (Utilità SQL Server)
 Per visualizzare i dati inclusi nel dashboard Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], nell'albero Gestione Utilità selezionare il nodo principale, con l'etichetta "Utilità<Nome_PuntoDiControlloUtilità">\\(NomeComputer\PuntoDiControlloUtilità)". Il dashboard include i dati di riepilogo e i dettagli relativi a tutte le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e a tutte le applicazioni di livello dati nell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per aggiornare dati nel dashboard, fare clic con il pulsante destro del mouse sul nodo principale nell'albero Esplora utilità e selezionare **Aggiorna**.  
  
 Per altre informazioni su come creare un punto di controllo dell'utilità, vedere [Creare un punto di controllo dell'Utilità SQL Server &#40;Utilità SQL Server&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md). Per altre informazioni su come aggiungere un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] all'utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Registrare un'istanza di SQL Server &#40;Utilità SQL Server&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md).  
 
  
### <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 Integrità istanze gestite  
 Lo stato di integrità per le istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene visualizzato sul lato sinistro del riquadro contenuto di Esplora utilità.  
  
 I parametri relativi all'integrità dell'istanza gestita sono i seguenti:  
  
-   Utilizzo CPU per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Utilizzo del file di database.  
  
-   Utilizzo dello spazio del volume di archiviazione.  
  
-   Utilizzo della CPU per il computer.  
  
-   Per ogni parametro esistono le tre categorie di stato seguenti:  
  
-   Adeguatamente utilizzato - Numero di istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non stanno violando criteri di utilizzo delle risorse.  
  
-   Sottoutilizzato - Numero di risorse gestite che stanno violando criteri di sottoutilizzo delle risorse.  
  
-   Sovrautilizzato - Numero di risorse gestite che stanno violando criteri di sovrautilizzo delle risorse.  
  
-   Dati non disponibili - I dati per le istanze gestite di SQL Server non sono disponibili perché l'istanza di SQL Server è appena stata inclusa e la prima operazione di raccolta dati non è stata completata o perché si è verificato un problema con l'istanza gestita di SQL Server durante la raccolta e il caricamento dei dati nel punto di controllo dell'utilità.  
  
 Le informazioni di stato dettagliate per ogni parametro di integrità sono elencate negli indicatori scorrevoli. La frazione a destra degli indicatori scorrevoli mostra il numero di istanze gestite incluso in ogni categoria di stato.  
  
 Per creare una visualizzazione filtrata di un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un'applicazione del livello dati, fare clic sul collegamento per una categoria di utilizzo accanto al relativo indicatore scorrevole nel dashboard dell'utilità. Ad esempio, se si fa clic su **CPU istanza sovrautilizzata** nel riquadro **Contenuto Esplora utilità** , SSMS crea una visualizzazione elenco filtrata delle istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che dispongono di una CPU sovrautilizzata in base alle impostazioni dei criteri correnti.  
  
 Si noti che quando si fa clic su un collegamento per una categoria di utilizzo, al nodo corrispondente nel riquadro di navigazione Esplora utilità viene aggiunto **(filtrato)** , ovvero **Istanze gestite** viene etichettato **Istanze gestite (filtrato)** . Per visualizzare le impostazioni del filtro, fare clic con il pulsante destro del mouse sul nodo nel riquadro di navigazione e selezionare **Filtro**, quindi fare clic su **Impostazioni filtro**. Per cancellare le impostazioni del filtro, fare clic con il pulsante destro del mouse sul nodo nel riquadro di navigazione e selezionare **Filtro**, quindi fare clic su **Rimuovi filtro**.  
  
 Per altre informazioni sulla visualizzazione dello stato di integrità per singole istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o per visualizzare o modificare impostazioni di configurazione dei criteri, vedere [Dettagli di istanze gestite &#40;Utilità SQL Server&#41;](https://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2).  
  
 Riepilogo utilità  
 Consente di visualizzare il numero di istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il numero di applicazioni di livello dati gestite dall'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Integrità applicazione del livello dati  
 Lo stato di integrità per le applicazioni di livello dati viene visualizzato sul lato destro del riquadro contenuto di Esplora utilità.  
  
 I parametri relativi all'integrità dell'applicazione del livello dati sono i seguenti:  
  
-   Utilizzo CPU per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Utilizzo del file di database.  
  
-   Utilizzo dello spazio del volume di archiviazione.  
  
-   Utilizzo della CPU per il computer.  
  
 Per ogni parametro esistono le tre categorie di stato seguenti:  
  
-   Adeguatamente utilizzato - Numero di applicazioni di livello dati che non stanno violando i criteri di utilizzo delle risorse.  
  
-   Sovrautilizzato - Numero di applicazioni di livello dati che non stanno violando i criteri di sovrautilizzo delle risorse.  
  
-   Sottoutilizzato - Numero di applicazioni di livello dati che non stanno violando i criteri di sottoutilizzo delle risorse.  
  
-   Dati non disponibili - I dati per le applicazioni di livello dati non sono disponibili perché l'istanza gestita di SQL Server che contiene l'applicazione del livello dati non sta registrando dati.  
  
 Le informazioni di stato dettagliate per ogni parametro di integrità sono elencate negli indicatori scorrevoli. La frazione a destra degli indicatori scorrevoli mostra il numero di applicazioni di livello dati incluso in ogni categoria di stato. Per altre informazioni sulla visualizzazione dello stato di integrità per le singole applicazioni di livello dati o per visualizzare o modificare le impostazioni di configurazione dei criteri, vedere [Dettagli di applicazioni di livello dati distribuite &#40;Utilità SQL Server&#41;](https://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
 Cronologia di utilizzo dello spazio di archiviazione utilità  
 La cronologia di utilizzo viene mostrata in un grafico temporale nella parte inferiore del dashboard utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si noti che i dati relativi all'ora mostrano la data e l'ora locale del punto di controllo utilità utilizzando il tipo di dati datetime. Per altre informazioni, vedere l'argomento [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) . Quando si utilizza il modello a oggetti dell'utilità, si noti che SSMS utilizza il tipo di dati datetimeoffset. Per altre informazioni, vedere l'argomento [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Utilizzare i pulsanti di opzione a sinistra dell'area di visualizzazione per modificare il periodo del report per il grafico.  
  
 Le opzioni disponibili per l'intervallo del report sono:  
  
-   1 giorno, visualizzato in intervalli di 15 minuti.  
  
-   1 settimana, visualizzata in intervalli di 1 giorno.  
  
-   1 mese, visualizzato in intervalli di 1 settimana.  
  
-   1 anno, visualizzato in intervalli di 1 mese.  
  
 Dopo avere apportato modifiche all'intervallo scelto per il report, i dati verranno aggiornati automaticamente.  
  
 Utilizzo di spazio di archiviazione utilità  
 Nella parte inferiore destra del dashboard, il grafico a torta relativo all'utilizzo dello spazio di archiviazione restituisce la percentuale di spazio utilizzato rispetto allo spazio disponibile nei volumi che si trovano in computer contenenti istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. I dati contenuti in questa visualizzazione vengono aggiornati ogni 15 minuti.  
 
 ## <a name="deployed-data-tier-application-details-sql-server-utility"></a>Dettagli delle applicazioni livello dati distribuite (Utilità SQL Server)
  Le informazioni incluse nella vista Applicazioni livello dati distribuite di Gestione Utilità forniscono dati di utilizzo relativi a singole applicazioni livello dati, cronologia dell'utilizzo della CPU, dettagli sull'utilizzo dello spazio di archiviazione a livello di file e la possibilità di visualizzare e aggiornare le soglie dei criteri. È possibile controllare le soglie dei criteri a livello di applicazione del livello dati per utilizzo della CPU, file di database e file di log. È inoltre possibile visualizzare dettagli delle proprietà per le singole applicazioni di livello dati.  
  
### <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 Vista Elenco  
 La visualizzazione Elenco nel riquadro superiore include dati sulle singole applicazioni di livello dati. Le icone di stato di integrità forniscono lo stato riepilogativo per ogni applicazione del livello dati in base alle categorie di utilizzo:  
  
-   Segno di spunta verde - ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") - Numero di applicazioni livello dati che non violano i criteri di utilizzo delle risorse. Le risorse sono utilizzate adeguatamente.  
  
-   Freccia in giù verde - ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") - Le risorse sono sottoutilizzate.  
  
-   Freccia in su rossa - ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_up_arrow") - Le risorse sono sovrautilizzate.  
  
 La sequenza di colonne nella visualizzazione Elenco può essere modificata trascinando le colonne verso destra o verso sinistra. È possibile aggiungere o eliminare colonne nella visualizzazione Elenco facendo clic con il pulsante destro del mouse sulle intestazioni di colonna e selezionando o deselezionando le colonne desiderate. Anche il menu di scelta rapida fornisce opzioni per l'ordinamento. È inoltre possibile attivare l'ordinamento facendo clic all'inizio di un nome di colonna.  
  
 Per accedere alle opzioni di filtro per la visualizzazione Elenco di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , fare clic con il pulsante destro del mouse sul nodo **Applicazioni livello dati distribuite** nel riquadro di spostamento Esplora utilità e selezionare **Filtro**. Dopo l'implementazione delle impostazioni di filtro, il nodo **Deployed Data-tier Applications** (Applicazioni livello dati distribuite) in Esplora utilità sarà identificato dall'etichetta **Deployed Data-tier Applications (filtered)** (Applicazioni livello dati distribuite - con filtro). Per altre informazioni, vedere [Impostazioni filtro &#40;Esplora oggetti ed Esplora utilità&#41;](https://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2).  
  
 Per impostazione predefinita, nelle colonne seguenti sono visualizzate informazioni sullo stato di integrità relative a ogni applicazione del livello dati.  
  
-   Nome - Nome dell'applicazione del livello dati.  
  
-   CPU applicazione - Consente di visualizzare lo stato di integrità di utilizzo del processore per questa applicazione del livello dati. Lo stato di integrità per questo parametro è determinato in base al set dei criteri di utilizzo della CPU per l'applicazione del livello dati e all'impostazione di configurazione per i criteri di valutazione di risorse volatili. Per altre informazioni, vedere [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Per visualizzare la cronologia di utilizzo del processore per questa applicazione livello dati o per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo CPU**.  
  
-   CPU computer - Consente di visualizzare lo stato di integrità di utilizzo del processore del computer. Lo stato di integrità per questo parametro è determinato in base al set dei criteri di utilizzo della CPU per il computer e all'impostazione di configurazione per i criteri di valutazione di risorse volatili. Per altre informazioni, vedere [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Per visualizzare la cronologia di utilizzo del processore per questa applicazione livello dati o per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo CPU**.  
  
-   Spazio file - Consente di visualizzare un riepilogo dello stato di integrità di utilizzo spazio file per ogni applicazione del livello dati.  
  
    -   Segno di spunta verde - Lo stato di integrità per tutti i filegroup e il gruppo file di log non è né sovrautilizzato né sottoutilizzato.  
  
    -   Freccia in giù verde - Lo stato di integrità di almeno un filegroup o gruppo file di log è sottoutilizzato, nessun filegroup o gruppo di file di log è sovrautilizzato.  
  
    -   Freccia in su rossa - Lo stato di integrità di almeno un filegroup o il gruppo file di log è sovrautilizzato. Si noti che se il database si trova in stato di "emergenza", lo stato di integrità visualizzerà lo spazio sovrautilizzato del file di log.  
  
     Per visualizzare o modificare i limiti dei criteri di spazio per i file, fare clic sulla scheda **Utilizzo spazio di archiviazione** .  
  
-   Spazio volume - Consente di visualizzare un riepilogo di stati di integrità di utilizzo dello spazio volume per tutti i volumi che contengono database appartenenti all'applicazione del livello di dati selezionata. Se lo stato di integrità di qualsiasi file di database è sovrautilizzato, lo stato di integrità dello spazio file sarà riportato nella visualizzazione Elenco come sovrautilizzato. Se lo stato di integrità di qualsiasi volume è sottoutilizzato, e nessun volume è sovrautilizzato, lo stato di integrità del volume sarà riportato nella visualizzazione Elenco come sottoutilizzato. In caso contrario, lo stato di integrità del volume sarà riportato nella visualizzazione Elenco come utilizzato adeguatamente. Per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo spazio di archiviazione** .  
  
-   Tipo criteri - Indica se i criteri predefiniti "Globale" o i criteri personalizzati "Sostituzione" sono attivi per l'applicazione del livello di dati.  
  
-   Nome istanza - Consente di visualizzare il nome dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospita l'applicazione del livello di dati.  
  
 Altre colonne che è possibile visualizzare utilizzando il menu di scelta rapida nell'area dell'intestazione di colonna della visualizzazione Elenco:  
  
-   Nome database  
  
-   Data di distribuzione  
  
-   Attendibile: (True o False)  
  
-   Regole di confronto  
  
-   Livello di compatibilità: (ad esempio Versione100)  
  
-   Crittografia abilitata: (True o False)  
  
-   Modello di recupero: (Con registrazione minima, Con registrazione completa o Con registrazione minima delle operazioni bulk)  
  
-   Ultima ora registrata: questa colonna restituisce la data e l'ora locale del punto di controllo utilità usando il tipo di dati datetime. Per altre informazioni, vedere l'argomento [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) . Quando si utilizza il modello a oggetti dell'utilità, si noti che SSMS utilizza il tipo di dati datetimeoffset. Per altre informazioni, vedere l'argomento [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Scheda Utilizzo CPU  
 La scheda Utilizzo CPU mostra grafici affiancati con dati cronologici relativi all'applicazione del livello dati e all'utilizzo della CPU del computer.  
  
 Il grafico consente di visualizzare la cronologia di utilizzo del processore per l'intervallo specificato nei pulsanti di opzione sul lato destro dell'area di visualizzazione. Per modificare l'intervallo visualizzato e aggiornare il set di dati, selezionare un pulsante di opzione dall'elenco.  
  
 Sono disponibili le opzioni di intervallo seguenti:  
  
-   1 giorno, visualizzato in intervalli di 15 minuti.  
  
-   1 settimana, visualizzata in intervalli di 1 giorno.  
  
-   1 mese, visualizzato in intervalli di 1 settimana.  
  
-   1 anno, visualizzato in intervalli di 1 mese.  
  
 Scheda Utilizzo spazio di archiviazione  
 La scheda Utilizzo spazio di archiviazione include una visualizzazione albero con i dettagli relativi all'utilizzo dello spazio di archiviazione per file di database e file di log che appartengono all'applicazione del livello dati selezionata nella visualizzazione Elenco. Si noti che i dati relativi all'ora mostrano la data e l'ora locale del punto di controllo utilità utilizzando il tipo di dati datetime. Per altre informazioni, vedere l'argomento [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) . Quando si utilizza il modello a oggetti dell'utilità, si noti che SSMS utilizza il tipo di dati datetimeoffset. Per altre informazioni, vedere l'argomento [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 È possibile raggruppare la visualizzazione in base al filegroup o al volume. Per utilizzare la visualizzazione albero filegroup, selezionare il pulsante di opzione **Filegroup** nella selezione **Raggruppa file per:** .  
  
 I dati visualizzati nel grafico della cronologia di utilizzo dello spazio di archiviazione variano a seconda del nodo selezionato nella visualizzazione albero:  
  
-   Selezionare il nodo del gruppo di file per visualizzare un grafico dello spazio file utilizzato da tutti i file di dati che appartengono al gruppo di file selezionato.  
  
-   Selezionare il nodo del file di log per visualizzare un grafico dello spazio file utilizzato da tutti i file di log che appartengono al database selezionato.  
  
-   Selezionare il nodo del database per visualizzare un grafico che aggiunge lo spazio file utilizzato da tutti i file di dati e file di log che appartengono al database selezionato.  
  
 Per visualizzare lo stato di utilizzo dello spazio di archiviazione per i singoli file, fare clic sul segno più accanto a un nome di file nella visualizzazione albero.  
  
 Le icone di stato di integrità forniscono informazioni immediate sullo stato di ogni filegroup rispetto alle soglie dei criteri:  
  
-   Segno di spunta verde - Lo spazio file per almeno un file di dati nel filegroup non è né sovrautilizzato né sottoutilizzato.  
  
-   Freccia in giù verde - Lo spazio file per almeno un file di dati nel filegroup è sottoutilizzato e nessun file nel filegroup è sovrautilizzato.  
  
-   Freccia in su rossa - Lo spazio file per tutti i file di dati nel filegroup è sovrautilizzato. Si noti che se il database si trova in stato di "emergenza", lo stato di integrità visualizzerà lo spazio sovrautilizzato del file di log.  
  
 Per visualizzare i file in base al volume, selezionare il pulsante di opzione **Volume** nella selezione **Raggruppa file per:** . Il grafico della cronologia di utilizzo dello spazio di archiviazione consente di visualizzare lo spazio file utilizzato da tutti i file di dati e da tutti i file di log nel volume di archiviazione. Espandere l'albero per visualizzare i dettagli relativi ai singoli file di dati e file di log del database.  
  
 Le icone di stato sono utilizzate per fornire informazioni sullo stato di ogni volume:  
  
-   Segno di spunta verde - Le risorse sono utilizzate adeguatamente.  
  
-   Freccia in giù verde - Le risorse sono sottoutilizzate.  
  
-   Freccia in su rossa - Le risorse sono sovrautilizzate.  
  
 Il misuratore accanto a ogni nome file nella scheda Utilizzo spazio di archiviazione rappresenta la quantità di spazio utilizzata dal file rispetto alla capacità effettiva del file. Il valore percentuale visualizzato accanto al misuratore rappresenta la percentuale di spazio utilizzata dal file rispetto alla capacità effettiva del file. Le descrizioni comandi forniscono dati utilizzati per calcolare percentuali per ogni volume e per ogni file rispetto alla capacità effettiva.  
  
 Se il file non è configurato per l'aumento automatico, la capacità effettiva corrisponderà alla quantità di spazio allocata per il file. Se il file è configurato per l'aumento automatico, la capacità effettiva corrisponderà alla somma della quantità di spazio attualmente allocata per il file più la quantità di spazio libero attualmente disponibile sul volume.  
  
 È possibile configurare i criteri dello spazio di archiviazione per i file di dati e per i file di log. Per visualizzare o modificare le soglie dei criteri di utilizzo dello spazio di archiviazione per i file, fare clic sul collegamento **Criteri file** nella parte inferiore del riquadro Utilizzo spazio di archiviazione. Per visualizzare o modificare le soglie dei criteri di utilizzo dello spazio di archiviazione per un volume di archiviazione, fare clic sul collegamento **Criteri volume** nella parte inferiore del riquadro Utilizzo spazio di archiviazione.  
  
 Per sostituire le soglie di criteri predefinite, fare clic sul pulsante di opzione **Sostituisci criteri predefiniti**, specificare i valori per i limiti superiori e inferiori, quindi fare clic su **OK**.  
  
 Per altre informazioni sulla modifica di valori di tolleranza per le violazioni dei criteri, vedere [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU&#40;Utilità SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 Scheda Dettagli proprietà  
 I dettagli delle proprietà elencati per le applicazioni del livello dati includono le categorie seguenti:  
  
-   Nome database  
  
-   Data di distribuzione  
  
-   Attendibile: (True o False)  
  
-   Regole di confronto  
  
-   Livello di compatibilità: (ad esempio Versione100)  
  
-   Crittografia abilitata: (True o False)  
  
-   Modello di recupero: (Con registrazione minima, Con registrazione completa o Con registrazione minima delle operazioni bulk)  
  
-   Ultima ora registrata: questa colonna restituisce la data e l'ora locale del punto di controllo utilità usando il tipo di dati datetime. Per altre informazioni, vedere l'argomento [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) . Quando si utilizza il modello a oggetti dell'utilità, si noti che SSMS utilizza il tipo di dati datetimeoffset. Per altre informazioni, vedere l'argomento [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) .

## <a name="managed-instance-details-sql-server-utility"></a>Dettagli di istanze gestite (Utilità SQL Server)
 Le informazioni incluse nella vista Istanze gestite di Esplora utilità forniscono dati di utilizzo per singole istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cronologia di utilizzo della CPU, dettagli sull'utilizzo dello spazio di archiviazione a livello di file e la possibilità di visualizzare e aggiornare le soglie dei criteri. È possibile controllare le soglie dei criteri a livello di volumi di archiviazione e a livello di istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per un computer e per file di database e file di log. È inoltre possibile visualizzare dettagli delle proprietà per singole istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 Vista Elenco  
 La visualizzazione Elenco nel riquadro superiore include dati relativi a singole stanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elencate nelle righe per NomeComputer/NomeIstanza.  
  
 Le icone di stato di integrità forniscono lo stato riepilogativo per ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in base alla categoria di utilizzo:  
  
-   Segno di spunta verde - ![](../../relational-databases/manage/media/well-utilized.gif "Well_utilized") - Numero di istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non violano i criteri di utilizzo delle risorse. Le risorse sono utilizzate adeguatamente.  
  
-   Freccia in giù verde - ![](../../relational-databases/manage/media/utility-down-arrow.gif "Utility_down_arrow") - Le risorse sono sottoutilizzate.  
  
-   Freccia in su rossa - ![](../../relational-databases/manage/media/utility-up-arrow.gif "Utility_up_arrow") - Le risorse sono sovrautilizzate.  
  
 La sequenza di colonne nella visualizzazione Elenco può essere modificata trascinando le colonne verso destra o verso sinistra. È possibile aggiungere o eliminare colonne nella visualizzazione Elenco facendo clic con il pulsante destro del mouse sulle intestazioni di colonna e selezionando o deselezionando le colonne desiderate. Anche il menu di scelta rapida fornisce opzioni per l'ordinamento. È inoltre possibile attivare l'ordinamento facendo clic all'inizio di un nome di colonna.  
  
 Per accedere alle opzioni di filtro per la visualizzazione Elenco dell’utilità, fare clic con il pulsante destro del mouse sul nodo **Istanze gestite** nel riquadro di spostamento Esplora utilità, quindi selezionare **Filtro**. Dopo l'implementazione delle impostazioni del filtro, il nodo **Istanze gestite** in Gestione Utilità verrà identificato dall'etichetta **Istanze gestite (filtrato)** . Per altre informazioni, vedere [Impostazioni filtro &#40;Esplora oggetti ed Esplora utilità&#41;](https://msdn.microsoft.com/library/4aab04bc-e1ab-4d4b-ab74-b287fc805bc2).  
  
 Per impostazione predefinita, nelle colonne seguenti sono visualizzate informazioni sullo stato di integrità relative a ogni istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   CPU istanza - Consente di visualizzare lo stato di integrità di utilizzo del processore allocato a questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Lo stato di integrità per questo parametro è determinato in base al set dei criteri di utilizzo della CPU per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e all'impostazione di configurazione per i criteri di valutazione di risorse volatili. Per altre informazioni, vedere [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Per visualizzare la cronologia di utilizzo del processore per questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo CPU**.  
  
-   CPU computer - Consente di visualizzare lo stato di integrità di utilizzo del processore del computer. Lo stato di integrità per questo parametro è determinato in base al set dei criteri di utilizzo della CPU per il computer e all'impostazione di configurazione per i criteri di valutazione di risorse volatili. Per altre informazioni, vedere [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Per visualizzare la cronologia di utilizzo del processore per questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo CPU**.  
  
-   Spazio file - Consente di visualizzare un riepilogo dello stato di integrità di utilizzo dello spazio file per tutti i database che appartengono all'istanza selezionata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se lo stato di integrità di qualsiasi database è sovrautilizzato, lo stato di integrità dello spazio file sarà riportato nella visualizzazione Elenco come sovrautilizzato. Se lo stato di integrità di qualsiasi database è sottoutilizzato, e non sono presenti database sovrautilizzati, lo stato di integrità dello spazio file sarà riportato nella visualizzazione Elenco come sottoutilizzato. In caso contrario, lo stato di integrità dello spazio file sarà riportato nella visualizzazione Elenco come utilizzato adeguatamente. Per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo spazio di archiviazione** .  
  
-   Spazio volume - Consente di visualizzare un riepilogo dello stato di integrità di utilizzo dello spazio volume per tutti i volumi che contengono database appartenenti all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]selezionata. Se lo stato di integrità di qualsiasi file di database è sovrautilizzato, lo stato di integrità dello spazio file sarà riportato nella visualizzazione Elenco come sovrautilizzato. Se lo stato di integrità di qualsiasi volume è sottoutilizzato, e nessun volume è sovrautilizzato, lo stato di integrità del volume sarà riportato nella visualizzazione Elenco come sottoutilizzato. In caso contrario, lo stato di integrità del volume sarà riportato nella visualizzazione Elenco come utilizzato adeguatamente. Per visualizzare o modificare i limiti dei criteri, fare clic sulla scheda **Utilizzo spazio di archiviazione** .  
  
-   Tipo criteri - Indica se i criteri predefiniti "Globale" o i criteri personalizzati "Sostituzione" sono attivi per l'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Altre colonne che è possibile visualizzare utilizzando il menu di scelta rapida nell'area dell'intestazione di colonna della visualizzazione Elenco:  
  
-   Nome processore:  
  
-   Velocità processore (MHz):  
  
-   Conteggio processore:  
  
-   Memoria fisica (MB):  
  
-   Versione del sistema operativo:  
  
-   Versione di SQL Server:  
  
-   Edizione di SQL Server:  
  
-   Raggruppato: (True o False)  
  
-   Directory di backup:  
  
-   Regole di confronto:  
  
-   Distinzione maiuscole/minuscole: (True o False)  
  
-   Language:  
  
-   Ultima ora registrata: questa colonna restituisce la data e l'ora locale del punto di controllo utilità usando il tipo di dati datetime. Per altre informazioni, vedere l'argomento [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) . Quando si utilizza il modello a oggetti dell'utilità, si noti che SSMS utilizza il tipo di dati datetimeoffset. Per altre informazioni, vedere l'argomento [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 Scheda Utilizzo CPU  
 La scheda Utilizzo CPU mostra grafici affiancati con dati cronologici relativi all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e all'utilizzo della CPU del computer.  
  
 Il grafico consente di visualizzare la cronologia di utilizzo del processore per l'intervallo specificato nei pulsanti di opzione sul lato destro dell'area di visualizzazione. Per modificare l'intervallo visualizzato e aggiornare il set di dati, selezionare un pulsante di opzione dall'elenco.  
  
 Sono disponibili le opzioni di intervallo seguenti:  
  
-   1 giorno, visualizzato in intervalli di 15 minuti.  
  
-   1 settimana, visualizzata in intervalli di 1 giorno.  
  
-   1 mese, visualizzato in intervalli di 1 settimana.  
  
-   1 anno, visualizzato in intervalli di 1 mese.  
  
 Scheda Utilizzo spazio di archiviazione  
 La scheda Utilizzo spazio di archiviazione include una visualizzazione albero con dettagli relativi allo spazio di archiviazione. Si noti che i dati relativi all'ora mostrano la data e l'ora locale del punto di controllo utilità utilizzando il tipo di dati datetime. Per altre informazioni, vedere l'argomento [datetime (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=164071) . Quando si utilizza il modello a oggetti dell'utilità, si noti che SSMS utilizza il tipo di dati datetimeoffset. Per altre informazioni, vedere l'argomento [datetimeoffset (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=141713) .  
  
 È possibile raggruppare la visualizzazione in base al database o al volume. Per usare la visualizzazione albero del database, selezionare il pulsante di opzione **Database** nella selezione **Raggruppa file per:** . Per visualizzare lo stato di utilizzo dello spazio di archiviazione per i singoli file di database, fare clic sul segno più accanto a un nome di database nella visualizzazione albero. I file di database elencati includono tutti i sistemi e i database utente che appartengono all'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionata nella visualizzazione Elenco.  
  
 La struttura ad albero corrisponde alla gerarchia di archiviazione. Il nodo radice nella visualizzazione albero corrisponde al database. Il livello successivo della visualizzazione albero contiene un nodo o nodi filegroup che appartengono al database e un nodo del file di log per i log che appartengono al database. Il livello successivo contiene i file di dati che appartengono al filegroup.  
  
 I dati visualizzati nel grafico della cronologia di utilizzo dello spazio di archiviazione variano a seconda del nodo selezionato nella visualizzazione albero:  
  
-   Selezionare il nodo del gruppo di file per visualizzare un grafico dello spazio file utilizzato da tutti i file di dati che appartengono al gruppo di file selezionato.  
  
-   Selezionare il nodo del file di log per visualizzare un grafico dello spazio file utilizzato da tutti i file di log che appartengono al database selezionato.  
  
-   Selezionare il nodo del database per visualizzare un grafico che aggiunge lo spazio file utilizzato da tutti i file di dati e file di log che appartengono al database selezionato.  
  
 Le icone di stato di integrità forniscono informazioni immediate sullo stato di file di database, filegroup e file di log:  
  
 Per i database:  
  
-   Segno di spunta verde - Lo stato di integrità di tutti i filegroup e file di log non è né sovrautilizzato né sottoutilizzato.  
  
-   Freccia in giù verde - Lo stato di integrità di almeno un filegroup o file di log è sottoutilizzato, nessuno stato di integrità è sovrautilizzato.  
  
-   Freccia in su rossa - Lo stato di integrità di almeno un filegroup o file di log è sovrautilizzato.  
  
 Per filegroup e file di log:  
  
-   Segno di spunta verde - Lo spazio file per tutti i file nel filegroup non è né sovrautilizzato né sottoutilizzato.  
  
-   Freccia in giù verde - Lo spazio file per almeno un file nel filegroup è sottoutilizzato e nessun file nel filegroup è sovrautilizzato.  
  
-   Freccia in su rossa - Lo spazio file per tutti i file di dati nel filegroup è sovrautilizzato.  
  
 Per visualizzare i file in base al volume, selezionare il pulsante di opzione **Volume** nella selezione **Raggruppa file per:** . Il grafico della cronologia di utilizzo dello spazio di archiviazione consente di visualizzare lo spazio file utilizzato da tutti i file di dati e da tutti i file di log nel volume di archiviazione. Espandere l'albero per visualizzare i dettagli relativi ai singoli file di dati e file di log del database.  
  
 Le icone di stato sono utilizzate per fornire informazioni sullo stato di ogni volume:  
  
-   Segno di spunta verde - Le risorse sono utilizzate adeguatamente.  
  
-   Freccia in giù verde - Le risorse sono sottoutilizzate.  
  
-   Freccia in su rossa - Le risorse sono sovrautilizzate.  
  
 Il misuratore accanto a ogni nome file nella scheda Utilizzo spazio di archiviazione rappresenta la quantità di spazio utilizzata dal file rispetto alla capacità effettiva del file. Il valore percentuale visualizzato accanto al misuratore rappresenta la percentuale di spazio utilizzata dal file rispetto alla capacità effettiva del file. Le descrizioni comandi forniscono dati utilizzati per calcolare percentuali per ogni volume e per ogni file rispetto alla capacità effettiva.  
  
 Se il file non è configurato per l'aumento automatico, la capacità effettiva corrisponderà alla quantità di spazio allocata per il file. Se il file è configurato per l'aumento automatico, la capacità effettiva corrisponderà alla somma della quantità di spazio attualmente allocata per il file più la quantità di spazio libero attualmente disponibile sul volume.  
  
 È possibile configurare i criteri dello spazio di archiviazione per i file di dati e per i file di log. Per visualizzare o modificare le soglie dei criteri di utilizzo dello spazio di archiviazione per i file, fare clic sul collegamento **Criteri file** nella parte inferiore del riquadro Utilizzo spazio di archiviazione. Per visualizzare o modificare le soglie dei criteri di utilizzo dello spazio di archiviazione per un volume di archiviazione, fare clic sul collegamento **Criteri volume** nella parte inferiore del riquadro Utilizzo spazio di archiviazione.  
  
 Per sostituire le soglie di criteri predefinite, fare clic sul pulsante di opzione **Sostituisci criteri predefiniti**, specificare i valori per i limiti superiori e inferiori, quindi fare clic su **OK**.  
  
 Per altre informazioni sulla modifica di valori di tolleranza per le violazioni dei criteri, vedere [Ridurre le segnalazioni non significative nei criteri di utilizzo della CPU&#40;Utilità SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
 Scheda Dettagli proprietà  
 I dettagli delle proprietà elencati per le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] includono le categorie seguenti:  
  
-   Nome processore:  
  
-   Velocità processore (MHz):  
  
-   Conteggio processore:  
  
-   Memoria fisica (MB):  
  
-   Versione del sistema operativo:  
  
-   Versione di SQL Server:  
  
-   Edizione di SQL Server:  
  
-   Raggruppato: (True o False)  
  
-   Directory di backup:  
  
-   Regole di confronto:  
  
-   Distinzione maiuscole/minuscole: (True o False)  
  
-   Language:  

## <a name="utility-administration-sql-server-utility"></a>Amministrazione utilità (Utilità SQL Server)
Utilizzare le schede Amministrazione utilità per gestire le impostazioni di criteri, sicurezza e data warehouse per un'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni sui concetti di Utilità [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vedere [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
### <a name="uielement-list"></a>Elenco degli elementi di interfaccia
 **Scheda Criteri** - Utilizzare la scheda Criteri per visualizzare o specificare criteri di monitoraggio globali.  
  
 Consente di impostare i criteri di monitoraggio globali dell'applicazione del livello dati. Per espandere l'elenco dei valori disponibili per questa opzione, fare clic sulla freccia accanto al nome dei criteri o fare clic sul titolo dei criteri.  
 Se un'applicazione sta esaurendo la capacità del processore - Per modificare questi criteri, usare il controllo a destra della descrizione dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   Il valore massimo predefinito per l'utilizzo del processore è 70%.  
  
-   Il valore minimo predefinito per l'utilizzo del processore è 0%.  
  
 Se un'applicazione sta esaurendo lo spazio file - Per modificare i criteri per l'uso dello spazio dei file di dati o file di log, usare il controllo a destra della descrizione dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   Il valore massimo predefinito per l'utilizzo dello spazio file è 70%.  
  
-   Il valore minimo predefinito per l'utilizzo dello spazio file è 0%.  
  
 Consente di impostare i criteri di monitoraggio globali dell'applicazione istanza gestita di SQL Server. Per espandere l'elenco dei valori disponibili per questa opzione, fare clic sulla freccia accanto al nome dei criteri o fare clic sul titolo dei criteri.  
 Se un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sta esaurendo la capacità del processore - Per modificare questi criteri, usare il controllo a destra della descrizione dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   Il valore massimo predefinito per l'utilizzo del processore dell'istanza è 70%.  
  
-   Il valore minimo predefinito per l'utilizzo del processore dell'istanza è 0%.  
  
 Se un'istanza gestita di un computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sta esaurendo la capacità del processore - Per modificare questi criteri, usare il controllo a destra della descrizione dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   Il valore massimo predefinito per l'utilizzo del processore del computer è 70%.  
  
-   Il valore minimo predefinito per l'utilizzo del processore del computer è 0%.  
  
 Se un'istanza gestita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sta esaurendo lo spazio file - Per modificare i criteri per l'uso dello spazio dei file di dati o file di log, usare il controllo a destra della descrizione dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   Il valore massimo predefinito per l'utilizzo dello spazio file è 70%.  
  
-   Il valore minimo predefinito per l'utilizzo dello spazio file è 0%.  
  
 Se un'un'istanza gestita di un computer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sta esaurendo lo spazio del volume di archiviazione - Per modificare questi criteri, usare il controllo a destra della descrizione dei criteri, quindi fare clic su **Applica**. È inoltre possibile ripristinare i valori predefiniti o annullare le modifiche utilizzando i pulsanti nella parte inferiore della visualizzazione.  
  
-   Il valore massimo predefinito per l'utilizzo dello spazio del volume del computer è 70%.  
  
-   Il valore minimo predefinito per l'utilizzo dello spazio del volume del computer è 0%.  
  
 Riduzione dei disturbi di violazione dei criteri da risorse estremamente volatili. Per espandere i controlli per questa caratteristica, fare clic sulla freccia in giù sul lato destro della visualizzazione.  
 Per altre informazioni, vedere [Riduzione delle segnalazioni non significative nei criteri di utilizzo della CPU &#40;Utilità SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md)  
  
 
**Scheda Sicurezza** - Consente di visualizzare i nomi degli account di accesso con le autorizzazioni necessarie per amministrare o leggere dal punto di controllo dell'utilità.  
  
 Seleziona gli account di accesso del punto di controllo dell'utilità che verranno aggiunti al ruolo Utility Reader.  
 Il privilegio Utility Reader consente all'account utente di:  
  
-   Connettersi all'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Vedere tutti i punti di visualizzazione in Esplora utilità di SSMS.  
  
-   Vedere le impostazioni nel nodo Amministrazione utilità in Esplora utilità di SSMS.  
  
 Gli amministratori dell'utilità possono includere e rimuovere istanze di SQL Server in utilità di SQL Server e modificare criteri su istanze gestite e impostazioni di amministrazione sul punto di controllo dell'utilità.  
  
 Per essere un amministratore di utilità, è necessario avere privilegi sysadmin sull'istanza di SQL Server. Per aggiungere o modificare gli account utente per il punto di controllo dell'utilità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilizzare Esplora oggetti di SSMS per aggiungere l'utente agli account di accesso al server dell'istanza punto di controllo dell'utilità di SQL Server. Per altre informazioni, vedere [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md).  
  
 
Scheda **Data warehouse** - Consente di visualizzare i dettagli relativi alla configurazione per il data warehouse di gestione dell'utilità.  
  
 Conservazione dei dati  
 Specifica il periodo di mantenimento dei dati per informazioni sull'utilizzo raccolte per istanze gestite di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il periodo di mantenimento predefinito è di 1 anno. Il valore minimo è di 1 mese. Il valore massimo supportato è 2 anni.  
  
 Informazioni di configurazione data warehouse dell'utilità  
 Le impostazioni di configurazione seguenti non sono configurabili in questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Nome del data warehouse di gestione dell'utilità (UMDW): Sysutility_mdw_\<GUID>_DATA.  
  
-   Frequenza di caricamento del set di raccolta: ogni 15 minuti.  
  
 La directory dell'utilità UMDW è configurabile: \<Unità di sistema>:\Programmi\Microsoft SQL Server\MSSQL10_50.<Nome_UCP>\MSSQL\Data\\, dove \<Unità di sistema> è in genere l'unità C:\. Il file di log UMDW_\<GUID>_LOG si trova nella stessa directory.  
  
> **NOTA** È possibile modificare la posizione del file data warehouse di gestione dell'utilità (UMDW) sysutility_mdw utilizzando i comandi collega/scollega o l'istruzione ALTER DATABASE. È consigliabile utilizzare l'istruzione ALTER DATABASE. Per altre informazioni, vedere [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md).  
  
 Ritorna ai valori predefiniti  
 Per ripristinare i valori predefiniti delle impostazioni in questa scheda, fare clic sul pulsante **Ripristina impostazioni predefinite** , quindi fare clic su **Applica**.  
 
  
## <a name="reference"></a>Informazioni di riferimento  
 [Creare un punto di controllo dell'Utilità SQL Server &#40;Utilità SQL Server&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md)  
  
 [Effettuare la connessione a Utilità SQL Server.](../../relational-databases/manage/connect-to-a-sql-server-utility.md)  
  
 [Registrare un'istanza di SQL Server &#40;Utilità SQL Server&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md)  
  
 [Configurare i criteri di integrità &#40;Utilità SQL Server&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)  
  
 [Monitoraggio di istanze di SQL Server in Utilità SQL Server](../../relational-databases/manage/monitor-instances-of-sql-server-in-the-sql-server-utility.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e funzionalità di Utilità SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Attività e funzionalità di Utilità SQL Server](https://msdn.microsoft.com/library/f5f47c2a-38ea-40f8-9767-9bc138d14453)  
  
  
