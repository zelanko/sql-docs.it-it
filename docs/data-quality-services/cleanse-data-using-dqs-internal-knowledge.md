---
title: Pulizia dei dati mediante le informazioni interne di DQS
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.dqproject.interactivecleansing.f1
- sql13.dqs.dqproject.map.f1
- sql13.dqs.dqproject.correction.f1
- sql13.dqs.dqproject.export.f1
ms.assetid: c96b13ad-02a6-4646-bcc7-b4a8d490f5cc
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 280149ccb0e94b1ca7bcca75616ec5353f41e62b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255695"
---
# <a name="cleanse-data-using-dqs-internal-knowledge"></a>Pulizia dei dati mediante le informazioni interne di DQS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritto come eseguire la pulizia dei dati utilizzando un progetto Data Quality in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). La pulizia dei dati viene eseguita sui dati di origine utilizzando una Knowledge Base incorporata in DQS e confrontando tali dati con un set di dati di alta qualità. Per altre informazioni, vedere [Compilazione di una Knowledge Base](../data-quality-services/building-a-knowledge-base.md).  
  
 La pulizia dei dati viene eseguita in quattro fasi: una fase di *mapping* , nel corso della quale viene identificata l'origine dati da pulire e ne viene eseguito il mapping ai domini richiesti in una Knowledge Base; una fase di *pulizia computerizzata* , in cui DQS applica la Knowledge Base ai dati da pulire e propone/effettua modifiche ai dati di origine; una fase di *pulizia interattiva* , che consente agli amministratori dei dati di analizzare, accettare o rifiutare le modifiche ai dati; infine, la fase di *esportazione* che consente di esportare i dati puliti. Ognuno di questi processi viene eseguito in una pagina separata della procedura guidata relativa all'attività di pulizia, consentendo all'utente di spostarsi da una pagina a un'altra al fine di rieseguire il processo, completare un processo di pulizia specifico e tornare nuovamente a una sua fase specifica. DQS fornisce statistiche sui dati di origine e sui risultati della pulizia che consentono di prendere decisioni informate sulla pulizia dei dati.  
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
###  <a name="Prerequisites"></a>Prerequisiti  
  
-   È necessario avere specificato valori soglia adatti per l'attività di pulizia. Per informazioni su questa operazione, vedere [Configurazione dei valori soglia per le attività di pulizia e di individuazione delle corrispondenze](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   È necessario che in [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] sia disponibile una Knowledge Base DQS con cui confrontare i dati di origine ed eseguirne la pulizia. La Knowledge Base deve inoltre contenere informazioni sul tipo di dati da pulire. Se si vogliono pulire dati di origine che contengono indirizzi in Italia, ad esempio, è necessario aver creato una Knowledge Base in base a dati di esempio di alta qualità per indirizzi italiani.  
  
-   Se i dati di origine da pulire si trovano in un file di Excel, è necessario che Microsoft Excel sia installato nel computer [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . In caso contrario, non sarà possibile selezionare il file di Excel nella fase di mapping. I file creati da Microsoft Excel potranno presentare l'estensione xlsx, xls o csv. Se viene utilizzata la versione a 64 bit di Excel, sono supportati solo i file di Excel 2003 (xls), mentre non sono supportati file di Excel 2007 o 2010 (xlsx). Se si utilizza una versione a 64 bit di Excel 2007 o 2010, salvare il file come file xls o csv o installare una versione a 32 bit di Excel.  
  
###  <a name="Security"></a>Sicurezza  
  
####  <a name="Permissions"></a>Autorizzazioni  
 Per eseguire la pulizia dei dati è necessario disporre del ruolo dqs_kb_editor o dqs_kb_operator nel database DQS_MAIN.  
  
##  <a name="Create"></a>Creazione di un progetto Data Quality per la pulizia dei dati  
 Per eseguire l'operazione di pulizia dei dati è necessario utilizzare un progetto Data Quality. Per creare un progetto Data Quality per la pulizia dei dati:  
  
1.  Seguire i passaggi 1-3 nell'argomento [Creare un progetto Data Quality](../data-quality-services/create-a-data-quality-project.md).  
  
2.  Nel passaggio 3.d, selezionare l'attività **Pulizia** .  
  
3.  Fare clic su **Crea** per creare un progetto Data Quality per la pulizia dei dati.  
  
 Viene creato un progetto Data Quality per la pulizia dei dati e viene aperta la pagina **Mappa** della procedura guidata Data Quality per la pulizia dei dati.  
  
##  <a name="Mapping"></a>Fase di mapping  
 Nella fase di mapping è possibile specificare la connessione ai dati di origine da pulire ed eseguire il mapping delle colonne dei dati di origine ai domini appropriati nella Knowledge Base selezionata.  
  
1.  Nella pagina **Mappa** della procedura guidata Data Quality per la pulizia dei dati, selezionare i dati di origine da pulire: **SQL Server** o **File di Excel**:  
  
    1.  **SQL Server**: selezionare **DQS_STAGING_DATA** come database di origine se sono stati copiati i dati di origine in questo database, quindi selezionare la tabella o vista appropriata contenente i dati di origine. In alternativa, selezionare il database di origine e la tabella o vista appropriata. Il database di origine deve essere presente nella stessa istanza di SQL Server di [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] per essere visualizzato nell'elenco a discesa **Database** .  
  
    2.  **File di Excel**: fare clic su **Sfoglia**e selezionare il file di Excel contenente i dati da pulire. Per selezionare un file di Excel, è necessario che Microsoft Excel sia installato nel computer [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . In caso contrario, il pulsante **Sfoglia** non sarà disponibile e verrà visualizzata una notifica sotto questa casella di testo in cui non è installato Microsoft Excel. Lasciare inoltre selezionata la casella di controllo **Utilizza la prima riga come intestazione** se la prima riga del file di Excel contiene dati dell'intestazione.  
  
2.  In **Mapping**, eseguire il mapping delle colonne di dati nei dati di origine ai domini appropriati della Knowledge Base selezionando una colonna di origine dall'elenco a discesa nella **Colonna di origine** , quindi selezionando un dominio dall'elenco a discesa nella colonna **Dominio** della stessa riga. Ripetere questo passaggio per eseguire il mapping di tutte le colonne nei dati di origine ai domini appropriati nella Knowledge Base. Se necessario, è possibile fare clic sull'icona **Aggiungi un mapping colonne** per aggiungere righe alla tabella di mapping.  
  
    > [!NOTE]  
    >  È possibile eseguire il mapping dei dati di origine a un dominio DQS per eseguire la pulizia dei dati solo se il tipo di dati di origine è supportato in DQS e corrisponde al tipo di dati del dominio DQS. Per informazioni sui tipi di dati di origine supportati, vedere [Tipi di dati di SQL Server e SSIS supportati per i domini DQS](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
3.  Fare clic sull'icona **Anteprima origine dati** per visualizzare i dati nella tabella o vista di SQL Server selezionata o nel foglio di lavoro di Excel selezionato.  
  
4.  Fare clic su **Visualizza/Seleziona domini compositi** per visualizzare un elenco dei domini compositi di cui è stato eseguito il mapping a una colonna di origine. Questo pulsante è disponibile solo se si dispone di almeno di un dominio composito di cui è stato eseguito il mapping a una colonna di origine.  
  
5.  Fare clic su **Avanti** per procedere alla fase di pulizia computerizzata (pagina**Pulisci** ).  
  
##  <a name="ComputerAssisted"></a>Fase di pulizia computerizzata  
 In questa fase viene eseguito un processo automatico di pulizia dei dati tramite il quale i dati di origine vengono analizzati rispetto ai domini di cui è stato eseguito il mapping nella Knowledge Base e vengono apportate o proposte delle modifiche dei dati.  
  
1.  Nella pagina **Pulisci** della procedura guidata Data Quality, fare clic su **Avvia** per eseguire il processo di pulizia computerizzato. DQS utilizza algoritmi e livelli di confidenza avanzati basati sui livelli di soglia specificati per l'analisi dei dati da confrontare alla Knowledge Base selezionata e procedere quindi alla loro pulizia. Per altre informazioni sulla pulizia assistita da computer in DQS, vedere [Pulizia assistita da computer](../data-quality-services/data-cleansing.md#ComputerAssisted) in [Pulizia dei dati](../data-quality-services/data-cleansing.md).  
  
    > [!IMPORTANT]  
    >  -   Una volta completata l'analisi dei dati, il pulsante **Avvia** viene sostituito dal pulsante **Riavvia** . Se i risultati dall'analisi precedente non sono stati ancora salvati, facendo clic su **Riavvia** si causerà la perdita di tali dati non salvati. Durante l'esecuzione dell'analisi, non lasciare la pagina o il processo di analisi verrà interrotto.  
    > -   Se la Knowledge Base utilizzata per il progetto di pulizia è stata aggiornata e pubblicata dopo l'ora di creazione del progetto di pulizia stesso, quando si fa clic su **Avvia** verrà richiesto se utilizzare la Knowledge Base più recente per la pulizia. Ciò può verificarsi se si è creato un progetto Data Quality utilizzando una Knowledge Base, si è chiuso il progetto di pulizia in esecuzione facendo clic su **Chiudi**, quindi si è riaperto il progetto Data Quality in un secondo tempo per effettuare la pulizia. Nel frattempo, la Knowledge Base utilizzata nel progetto di pulizia è stata aggiornata e pubblicata.  
    >   
    >      Analogamente, se la Knowledge Base utilizzata per il progetto di pulizia è stata aggiornata e pubblicata dopo l'ultima esecuzione della pulizia computerizzata, quando si fa clic su **Riavvia** verrà chiesto se utilizzare la Knowledge Base più recente per la pulizia.  
    >   
    >      In entrambi i casi, fare clic su **Sì** per utilizzare la Knowledge Base aggiornata per la pulizia computerizzata. Inoltre, se è presente qualsiasi conflitto tra i mapping correnti e la Knowledge Base aggiornata (ad esempio domini eliminati o modifiche al tipo di dati del dominio) viene richiesto anche di correggere i mapping correnti per utilizzare la Knowledge Base aggiornata. Facendo clic su **Sì** si passa alla pagina **Mappa** in cui è possibile correggere i mapping prima di continuare con la pulizia computerizzata.  
  
2.  Durante la fase di pulizia computerizzata, è possibile attivare il profiler facendo clic sulla scheda **Profiler** e visualizzare i dati di profiling e le notifiche in tempo reale. Per altre informazioni, vedere [Statistiche del profiler](#Profiler).  
  
3.  Se non si è soddisfatti dei risultati, fare clic su **Indietro** per tornare alla pagina **Mappa** , modificare uno o più mapping come desiderato, tornare alla pagina **Pulisci** , quindi fare clic su **Riavvia**.  
  
4.  Una volta completato il processo di pulizia computerizzata, fare clic su **Avanti** per procedere alla fase di pulizia interattiva (pagina**Gestisci e visualizza risultati** ).  
  
##  <a name="Interactive"></a>Fase di pulizia interattiva  
 Nella fase di pulizia interattiva, è possibile visualizzare le modifiche proposte da DQS e decidere se implementarle o meno, approvandole o rifiutandole. Nel riquadro sinistro della pagina **Gestisci e visualizza risultati** , tramite DQS viene mostrato un elenco di tutti i domini di cui si è eseguito il mapping precedentemente nella fase di mapping, insieme al numero di valori analizzati nei dati di origine rispetto a ciascun dominio durante la fase di pulizia computerizzata. Nel riquadro destro della pagina **Gestisci e visualizza risultati** , in base al rispetto delle regole di dominio, alle regole relative agli errori di sintassi e ad algoritmi avanzati, tramite DQS i dati vengono suddivisi in categorie in cinque schede, utilizzando il *livello di confidenza*. Il livello di confidenza indica il livello di certezza da parte di DQS in relazione a una correzione o suggerimento e si basa sui valori soglia seguenti:  
  
-   **Soglia di correzione automatica**: qualsiasi valore con un livello di confidenza al di sopra di questa soglia viene corretto automaticamente da DQS. L'amministratore dei dati può tuttavia ignorare la modifica durante la pulizia interattiva. È possibile specificare il valore soglia di correzione automatica nella scheda **Impostazioni generali** della schermata **Configurazione** . Per altre informazioni, vedere [Configurazione dei valori soglia per le attività di pulizia e di individuazione delle corrispondenze](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   **Soglia di suggerimento automatico**: qualsiasi valore con un livello di confidenza al di sopra di questa soglia, ma al di sotto della soglia di correzione automatica, viene suggerito come valore di sostituzione. In DQS la modifica viene apportata solo se approvata dall'amministratore dei dati. È possibile specificare il valore soglia di suggerimento automatico nella scheda **Impostazioni generali** della schermata **Configurazione** . Per altre informazioni, vedere [Configurazione dei valori soglia per le attività di pulizia e di individuazione delle corrispondenze](../data-quality-services/configure-threshold-values-for-cleansing-and-matching.md).  
  
-   **Altro**: qualsiasi valore al di sotto del valore soglia di suggerimento automatico viene lasciato invariato da DQS.  
  
 In base al livello di confidenza, i valori vengono visualizzati nelle cinque schede seguenti:  
  
|TAB|Description|  
|---------|-----------------|  
|**Suggerito**|Mostra i valori del dominio per il quale tramite DQS sono stati trovati valori suggeriti che dispongono di un livello di confidenza più elevato del valore *soglia di suggerimento automatico* , ma inferiore al valore *soglia di correzione automatica* .<br /><br /> Nella colonna **Correggi in** vengono visualizzati i valori suggeriti rispetto al valore originale. È possibile fare clic sul pulsante di opzione nella colonna **Approva** o **Rifiuta** rispetto a un valore nella griglia superiore per accettare o rifiutare il suggerimento per tutte le istanze di tale valore. In questo caso, il valore accettato viene spostato nella scheda **Con correzione** e il valore respinto viene spostato nella scheda **Non validi** .|  
|**Nuovo**|Consente di visualizzare il dominio valido per il quale DQS non dispone di informazioni sufficienti e pertanto non è possibile eseguirne il mapping a qualsiasi altra scheda. Inoltre, questa scheda contiene anche valori con un livello di confidenza inferiore al valore *soglia di suggerimento automatico* , ma sufficientemente elevato per essere contrassegnati come validi.<br /><br /> Se il valore è ritenuto corretto, fare clic sul pulsante di opzione nella colonna **Approva** . Altrimenti, fare clic sul pulsante di opzione nella colonna **Rifiuta** . Il valore accettato viene spostato nella scheda **corretti** e il valore rifiutato passa alla scheda **non valida** . È anche possibile digitare manualmente il valore corretto come sostituzione del valore originale nella colonna **Correggi** in rispetto al valore, quindi fare clic sul pulsante di opzione nella colonna **approva** per accettare la modifica. In questo caso, il valore viene spostato nella scheda **Con correzione** .|  
|**Non valido**|Mostra i valori del dominio contrassegnati come non validi nel dominio della Knowledge Base o i valori che non hanno superato una regola di dominio. Questa scheda contiene inoltre i valori rifiutati dall'utente in qualsiasi delle altre quattro schede.<br /><br /> Se il valore è ritenuto corretto, tuttavia, è possibile fare clic sul pulsante di opzione nella colonna **Approva** . Il valore accettato viene spostato nella scheda **corretta** . È anche possibile digitare manualmente il valore corretto come sostituzione del valore originale nella colonna **Correggi** in rispetto al valore, quindi fare clic sul pulsante di opzione nella colonna **approva** per accettare la modifica. In questo caso, il valore viene spostato nella scheda **Con correzione** .|  
|**Corretto**|Visualizza i valori di dominio corretti da DQS durante il processo automatico di pulizia, nel caso in cui sia stata trovata una correzione per il valore con un livello di confidenza superiore al valore soglia di correzione automatica.<br /><br /> Nella colonna **Correggi in** vengono visualizzati i valori con correzione rispetto al valore originale. Per impostazione predefinita, il pulsante di opzione nella colonna **Approva** per il valore viene selezionato. Se necessario, è possibile rifiutare la correzione proposta facendo clic sul pulsante di opzione nella colonna **Rifiuta** per spostarlo nella scheda **Non validi** o digitare manualmente il valore corretto nella colonna **Correggi in** , quindi fare clic sul pulsante di opzione nella colonna **Approva** per accettare la modifica e spostare il valore nella scheda **Con correzione** .|  
|**Corretto**|Mostra i valori di dominio che sono risultati corretti, Ad esempio, un valore corrispondente a un valore di dominio. Questa scheda contiene anche valori approvati dall'utente facendo clic sul pulsante di opzione nella colonna **Approva** nelle schede **Nuovi** e **Non validi** .<br /><br /> Per impostazione predefinita, il pulsante di opzione nella colonna **Approva** è selezionato per ciascun valore. Se tuttavia si ritiene che un valore in questa scheda sia errato, è possibile fare clic sul pulsante di opzione nella colonna **Rifiuta** per quel valore e spostarlo nella scheda **Non validi** oppure digitare manualmente il valore corretto con cui sostituirlo nella colonna **Correggi in** , quindi fare clic sul pulsante di opzione nella colonna **Approva** per accettare la modifica e spostarlo nella scheda **Con correzione** .|  
  
 Per pulire i dati in modo interattivo:  
  
1.  Nella pagina **Gestisci e visualizza risultati** della procedura guidata Data Quality per la pulizia dei dati, fare clic su un nome di dominio nel riquadro sinistro.  
  
2.  Rivedere i valori di dominio nelle cinque schede e intraprendere le azioni appropriate come illustrato in precedenza.  
  
    -   Nel riquadro superiore destro vengono visualizzate le informazioni seguenti per ciascun valore nel dominio selezionato: il valore originale, il numero di istanze (record), una casella per specificare un altro valore (corretto), il livello di confidenza (non disponibile per i valori nella scheda **Corretti** ), il motivo per l'azione DQS sul valore, l'opzione per approvare e rifiutare le correzioni e i suggerimenti per il valore.  
  
        > [!TIP]  
        >  È possibile approvare o rifiutare tutti i valori nel dominio selezionato nel riquadro superiore destro facendo clic rispettivamente sull'icona **Approva tutti i termini** o **Rifiuta tutti i termini** . Alternativamente, è possibile fare clic con il pulsante destro del mouse su un valore nel dominio selezionato e scegliere **Accetta tutto** o **Rifiuta tutto** dal menu di scelta rapida.  
  
    -   Nel riquadro inferiore vengono visualizzate occorrenze singole del valore di dominio selezionato nel riquadro superiore destro. Nel superiore destro vengono visualizzate le informazioni seguenti: una casella per specificare un altro valore (corretto), il livello di confidenza (non disponibile per i valori nella scheda **Corretti** ), il motivo per l'azione DQS sul valore, l'opzione per approvare e rifiutare le correzioni, i suggerimenti per il valore e il valore originale.  
  
3.  Se è stata abilitata la funzionalità **Correttore ortografico** per un dominio durante la sua creazione, vengono visualizzati dei caratteri di sottolineatura rossi ondulati insieme a quei valori di dominio identificati come potenziali errori. La sottolineatura viene visualizzata per l'intero valore. Se ad esempio "New York" è stato erroneamente digitato "Neu York", la sottolineatura rossa verrà visualizzata sotto "Neu York" e non solo sotto "Neu". Se si fa clic con il pulsante destro del mouse sul valore, verranno visualizzate le correzioni suggerite. Se sono presenti più di 5 suggerimenti, è possibile fare clic su **Ulteriori suggerimenti** nel menu di scelta rapida per visualizzare quelli rimanenti. Così come avviene per la visualizzazione degli errori, i suggerimenti rappresentano sostituzioni per l'intero valore. Il suggerimento visualizzato per l'esempio precedente sarà ad esempio "New York" e non solo "New". È possibile scegliere uno dei suggerimenti o aggiungere al dizionario una voce da visualizzare per quel valore. I valori vengono archiviati nel dizionario a livello di account utente. Quando si seleziona un suggerimento dal menu di scelta rapida del correttore ortografico, tale suggerimento viene aggiunto alla colonna **Correggi in** . Se si seleziona un suggerimento nella colonna **Correggi in** , tuttavia, il valore nella colonna viene sostituito dal suggerimento selezionato.  
  
     La funzionalità di correzione ortografica è abilitata per impostazione predefinita nella fase di pulizia interattiva. È possibile disabilitare il correttore ortografico nella fase di pulizia interattiva facendo clic sull'icona **Abilita/Disabilita correttore ortografico** o facendo clic con il pulsante destro del mouse nell'area dei valori di dominio e scegliendo **Correttore ortografico** dal menu di scelta rapida. Per abilitarlo nuovamente, seguire la stessa procedura.  
  
    > [!NOTE]  
    >  La funzionalità di correzione ortografica è disponibile solo nel riquadro superiore (valori di dominio). Non è inoltre possibile abilitare o disabilitare il correttore ortografico per domini compositi. Per i domini figlio di tipo stringa abilitati per la funzionalità di correzione ortografica in un dominio composito, tale funzionalità viene abilitata per impostazione predefinita durante la fase di pulizia interattiva.  
  
4.  Durante la fase di pulizia interattiva, è possibile attivare il profiler facendo clic sulla scheda **Profiler** e visualizzare i dati di profiling e le notifiche in tempo reale. Per altre informazioni, vedere [Statistiche del profiler](#Profiler).  
  
5.  Dopo avere rivisto tutti i valori di dominio, fare clic su **Avanti** per procedere alla fase di esportazione.  
  
##  <a name="Export"></a>Fase di esportazione  
 Nella fase di esportazione si specificano i parametri per indicare quali dati puliti esportare e in quale ubicazione.  
  
1.  Nella pagina **Esporta** della procedura guidata Data Quality per la pulizia dei dati, selezionare il tipo di destinazione per l'esportazione dei dati puliti: **SQL Server**, **File CSV**o **File di Excel**.  
  
    > [!IMPORTANT]  
    >  Se si utilizza la versione a 64 bit di Excel, non è possibile esportare i propri dati puliti in un file di Excel. È possibile eseguire l'esportazione solo in un database di SQL Server o in un file con estensione csv.  
  
    1.  **SQL Server**: selezionare **DQS_STAGING_DATA** come database di destinazione se si desidera esportare i dati qui, quindi specificare un nome di tabella che verrà creato per archiviare i dati esportati. Altrimenti, se si desidera esportare i dati in un database diverso, sceglierlo e specificare un nome di tabella che verrà creata per archiviare i dati esportati. Il database di destinazione deve essere presente nella stessa istanza di SQL Server di [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] per essere visualizzato nell'elenco a discesa **Database** .  
  
    2.  **File CSV**: fare clic su **Sfoglia**e specificare il nome e il percorso del file con estensione CSV in cui si desidera esportare i dati puliti. È anche possibile digitare il nome per il file csv insieme al percorso completo in cui si desidera esportare i dati puliti, Ad esempio, "c:\ExportedData.csv". Il file viene salvato nel computer in cui è installato [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] .  
  
    3.  **File di Excel**: fare clic su **Sfoglia**e specificare il nome e il percorso del file di Excel in cui si desidera esportare i dati puliti. È anche possibile digitare il nome per il file di Excel insieme al percorso completo in cui si desidera esportare i dati puliti, Ad esempio, "c:\ExportedData.xlsx". Il file viene salvato nel computer in cui è installato [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] .  
  
2.  Selezionare la casella di controllo **Standardizzare output** per standardizzare l'output in base al formato selezionato per il dominio. Ad esempio, modificare il valore stringa in caratteri maiuscoli o cambiare al maiuscolo l'iniziale della parola. Per informazioni sulla specifica del formato di output di un dominio, vedere l'elenco **Formato output in** in [Imposta proprietà del dominio](../data-quality-services/set-domain-properties.md).  
  
3.  Selezionare quindi l'output dei dati: esportare solo i dati puliti o i dati puliti insieme alle informazioni relative alla pulizia.  
  
    -   **Solo dati**: fare clic sul pulsante di opzione per esportare solo i dati puliti.  
  
    -   **Dati e informazioni pulizia**: fare clic sul pulsante di opzione per esportare i dati seguenti per ogni dominio:  
  
        -   >_Source di dominio: il valore originale nel dominio. ** \<**  
  
        -   >_Output di dominio: i valori puliti nel dominio. ** \<**  
  
        -   >_Reason di dominio: il motivo specificato per la correzione del valore. ** \<**  
  
        -   >_Confidence di dominio: il livello di confidenza per tutti i termini corretti. ** \<** Viene visualizzato come valore decimale equivalente al valore percentuale corrispondente. Un livello di confidenza del 95% viene ad esempio visualizzato come 0,9500000.  
  
        -   >_Status di dominio: stato del valore del dominio dopo la pulizia dei dati. ** \<** Ad esempio **Suggeriti**, **Nuovi**, **Non validi**, **Con correzione**o **Corretti**.  
  
        -   **Stato record**: oltre a avere un campo di stato per ogni dominio mappato **(\<NomeDominio>_Status**), il campo **stato record** Visualizza lo stato di un record. Se uno stato del dominio nel record è *Nuovi* o *Corretti*, il valore di **Stato record** viene impostato su *Corretti*. Se uno stato del dominio nel record è *Suggeriti*, *Non validi*o *Con correzione*, il valore di **Stato record** viene impostato sul rispettivo valore. Ad esempio, se uno stato del dominio nel record è *Suggeriti*, il valore di **Stato record** viene impostato su *Suggeriti*.  
  
            > [!NOTE]  
            >  Se si utilizza un servizio dati di riferimento per l'operazione di pulizia, sono disponibili dati aggiuntivi sui valori di dominio per l'esportazione. Per altre informazioni, vedere [Pulire i dati mediante le informazioni dei dati di riferimento &#40;esterni&#41;](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md).  
  
4.  Fare clic su **Esporta** per esportare i dati nella destinazione selezionata. Se si è selezionato  
  
    -   **SQL Server** come destinazione dei dati, nel database selezionato verrà creata una nuova tabella con il nome specificato.  
  
    -   **File CSV** come destinazione dei dati, verrà creato un file CSV nel percorso nel [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] computer con il nome file specificato in precedenza nella casella nome **file CSV** .  
  
    -   **File di Excel** come destinazione dei dati, verrà creato un file di Excel nel percorso nel [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] computer con il nome file specificato in precedenza nella casella **nome file di Excel** .  
  
5.  Fare clic su **Fine** per chiudere il progetto Data Quality.  
  
##  <a name="Profiler"></a>Statistiche Profiler  
 La scheda **Profiler** fornisce statistiche che indicano la qualità dei dati di origine. Il profiling consente di valutare il livello di efficacia dell'attività di pulizia dei dati e potenzialmente di determinare in quale misura tale attività è stata in grado di migliorare la qualità dei dati.  
  
 La scheda **Profiler** fornisce le statistiche seguenti per i dati di origine, per campo e dominio:  
  
-   **Record**: il numero di record del campione di dati analizzati per l'attività di pulizia dei dati  
  
-   **Record corretti**: il numero di record trovati corretti  
  
-   **Record corretti**: numero di record corretti  
  
-   **Record suggeriti**: numero di record suggeriti  
  
-   **Record non validi**: numero di record non validi  
  
 Le statistiche relative ai campi includono:  
  
-   **Field**: nome del campo nei dati di origine  
  
-   **Dominio**: nome del dominio di cui viene eseguito il mapping al campo  
  
-   **Valori corretti**: numero di valori di dominio corretti  
  
-   **Valori suggeriti**: il numero di valori di dominio suggeriti  
  
-   **Completezza**: la completezza di ogni campo di origine di cui è stato eseguito il mapping per l'attività di pulizia  
  
-   **Accuratezza**: l'accuratezza di ogni campo di origine di cui è stato eseguito il mapping per l'attività di pulizia  
  
 Il profiling DQS fornisce due dimensioni della qualità dei dati: *completezza* (l'entità della presenza dei dati) e *accuratezza* (la misura entro cui i dati possono essere utilizzati per gli scopi previsti). Se il profiling suggerisce che un campo è relativamente incompleto, è necessario rimuoverlo dalla Knowledge Base di un progetto Data Quality. È possibile che il profiling non fornisca statistiche di completezza affidabili per i domini compositi. Se sono necessarie statistiche di completezza, utilizzare domini singoli anziché domini compositi. Se si desidera utilizzare domini compositi, è consigliabile creare una Knowledge Base con domini singoli di cui eseguire il profiling per determinare la completezza, quindi creare un altro dominio con un dominio composito per il processo di pulizia. Ad esempio, il profiling potrebbe mostrare una completezza del 95% per record relativi a indirizzi, utilizzando un dominio composito, ma potrebbe esservi un livello di incompletezza molto più alto per una delle colonne, ad esempio una colonna relativa al codice postale (CAP). In questo esempio, è necessario misurare la completezza della colonna del CAP con un solo dominio. Il profiling fornirà probabilmente statistiche di accuratezza affidabili per i domini compositi perché è possibile misurare l'accuratezza di più colonne allo stesso tempo. Il valore di questi dati sta nell'aggregazione composta, pertanto è consigliabile misurarne l'accuratezza con un dominio composito.  
  
 Se non si utilizza un servizio dati di riferimento, le statistiche di accuratezza richiederanno probabilmente un maggior livello di interpretazione. Se si utilizza un servizio dati di riferimento per la pulizia dei dati, si otterrà un certo livello di attendibilità nelle statistiche di accuratezza. Per altre informazioni sulla pulizia dei dati mediante il servizio dati di riferimento, vedere [Pulire i dati mediante le informazioni dei dati di riferimento & #40; esterni & #41;](../data-quality-services/cleanse-data-using-reference-data-external-knowledge.md).  
  
### <a name="cleansing-notifications"></a>Notifiche relative alla pulizia  
 Le condizioni seguenti danno luogo a notifiche:  
  
-   Non sono presenti correzioni o suggerimenti per un campo. Potrebbe essere necessario rimuovere tale campo dal mapping, eseguire prima l'individuazione delle informazioni oppure utilizzare una Knowledge Base diversa.  
  
-   È presente un numero relativamente basso di correzioni o suggerimenti per un campo. Potrebbe essere necessario rimuovere tale campo dal mapping, eseguire prima l'individuazione delle informazioni oppure utilizzare una Knowledge Base diversa.  
  
-   Il livello di accuratezza del campo è molto basso. Potrebbe essere necessario verificare il mapping o considerare l'esecuzione dell'individuazione delle informazioni.  
  
 Per ulteriori informazioni sul profiling, vedere [Profiling di dati e notifiche in DQS](../data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
  
