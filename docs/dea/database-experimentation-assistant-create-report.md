---
title: Creazione di report di analisi
description: Creazione di report di analisi in Database Experimentation Assistant
ms.date: 11/21/2019
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: jtoland
ms.reviewer: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 4d3f057ffcfb1030b473b69f96b7204b3a975613
ms.sourcegitcommit: aaa42f26c68abc2de10eb58444fe6b490c174eab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/21/2019
ms.locfileid: "74307979"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant-sql-server"></a>Creazione di report di analisi in Database Experimentation Assistant (SQL Server)

Dopo aver riprodotto la traccia di origine in entrambi i server di destinazione, è possibile generare un report di analisi in Database Experimentation Assistant (DEA). I report di analisi consentono di ottenere informazioni approfondite sulle implicazioni sulle prestazioni delle modifiche proposte.

## <a name="create-an-analysis-report"></a>Creazione di un report di analisi

In DEA selezionare l'icona di menu. Nel menu espanso selezionare report di **analisi** accanto all'icona dell'elenco di controllo.

![Menu analisi](./media/database-experimentation-assistant-create-report/dea-create-reports-menu.png)

In **report di analisi**selezionare **nuovo report di analisi**.

![Menu nuovo report di analisi](./media/database-experimentation-assistant-create-report/dea-create-reports-new-report.png)

Immettere o selezionare le seguenti informazioni:

- **Nome report**: immettere un nome per il report. Il nome del report viene utilizzato per i database A e B. Esempio:*identificatore univoco*del*nome* + del report *(o B)* + .
- **Nome server**: immettere il nome del computer server che si desidera includere nei database di analisi a, B e.
- **Nome istanza SQL Server**: immettere il nome dell'istanza di SQL Server da utilizzare per il report.
- **Trace for Source Server**: immettere il SQL Server (2008 R2) First trace (. trc).
- **Traccia per server di destinazione**: immettere il SQL Server di destinazione (2014) primo file con estensione trc.

![Pagina nuovo report di analisi](./media/database-experimentation-assistant-create-report/dea-create-reports-inputs.png)

## <a name="generate-a-report"></a>Generare un report

Dopo aver immesso o selezionato le informazioni necessarie nella pagina **nuovo report di analisi** , selezionare **Avvia** per avviare la creazione del report. Se le informazioni immesse sono valide, viene creato il report di analisi. In caso contrario, le caselle di testo contenenti informazioni non valide vengono evidenziate con il rosso. Assicurarsi di immettere i valori corretti e quindi selezionare **Avvia**.

Viene generato un nuovo report di analisi. Il database di analisi segue l' + *identificatore univoco*dell'analisi dello schema di denominazione e del *nome del report specificato dall'utente*.

## <a name="frequently-asked-questions-about-analysis-reports"></a>Domande frequenti sui report di analisi

**D: cosa indica il report di analisi?**

DEA USA i test statistici per analizzare il carico di lavoro e determinare il modo in cui ogni query è stata eseguita dalla destinazione 1 alla destinazione 2. Fornisce informazioni dettagliate sulle prestazioni per ogni query. Per altre informazioni su DEA, [vedere Introduzione](database-experimentation-assistant-get-started.md).

**D: è possibile creare un nuovo report di analisi mentre è in corso la generazione di un altro report?**

No.  Attualmente, per evitare conflitti, è possibile generare un solo report alla volta. Tuttavia, è possibile eseguire più di un'acquisizione e riprodurle nello stesso momento.

**D: è stato eseguito l'aggiornamento di DEA alla versione 2,0. Posso comunque visualizzare e usare i vecchi report?**

Sì. Per visualizzare i report generati in precedenza, è necessario aggiornare lo schema del report. Per altre informazioni, vedere [dea 2,0: aggiornare lo schema del database per il report di analisi in dea](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-updating-db-schema-for-analysis-report-in-the-database-experimentation-assistant/).

**D: è possibile generare un report di analisi usando il prompt dei comandi?**

Sì. È possibile generare un report di analisi al prompt dei comandi. È quindi possibile visualizzare il report nell'interfaccia utente. Per ulteriori informazioni, vedere [eseguire al prompt dei comandi](database-experimentation-assistant-run-command-prompt.md).

## <a name="troubleshoot-analysis-reports"></a>Risolvere i problemi relativi ai report di analisi

**D: quali autorizzazioni di sicurezza sono necessarie per generare e visualizzare un report di analisi nel server?**

L'utente che ha eseguito l'accesso a DEA deve disporre dei diritti di amministratore di ruolo su Analysis Server. Se l'utente fa parte di un gruppo, assicurarsi che il gruppo disponga dei diritti di amministratore di gruppo.

|Possibili errori|Soluzione|  
|---|---|  
|Impossibile connettersi al database. Assicurarsi di disporre dei diritti sysadmin per l'analisi e la visualizzazione dei report.|È possibile che non si disponga dei diritti di accesso o di amministratore di ruolo per il server o il database. Verificare i diritti di accesso e riprovare.|  
|Impossibile generare il **nome del report** sul **nome del server**del server. Per informazioni dettagliate, controllare il report del **nome del report** .|È possibile che non si disponga dei diritti sysadmin necessari per generare un nuovo report. Per visualizzare gli errori dettagliati, selezionare il report con errori e controllare i log in% temp%\\dea.|  
|L'utente corrente non dispone delle autorizzazioni necessarie per eseguire l'operazione. Assicurarsi di disporre dei diritti di amministratore di ruolo per l'esecuzione di tracce e l'analisi dei report.|Non si dispone dei diritti sysadmin necessari per generare un nuovo report.|  

**D: non è possibile connettersi al computer che esegue SQL Server**

- Verificare che il nome del computer in cui è in esecuzione SQL Server sia valido. Per confermare, provare a connettersi al server usando SQL Server Management Studio (SSMS).
- Verificare che la configurazione del firewall non blocchi le connessioni al computer in cui è in esecuzione SQL Server.
- Verificare che l'utente disponga dei diritti utente necessari.

È possibile visualizzare altri dettagli nei log in% temp%\\dea. Se il problema persiste, contattare il team del prodotto.

**D: viene visualizzato un errore durante la generazione di un report di analisi**

L'accesso a Internet è necessario la prima volta che si genera un report di analisi dopo l'installazione di DEA. Per scaricare i pacchetti necessari per l'analisi statistica, è necessario l'accesso a Internet.

Se si verifica un errore durante la creazione del report, nella pagina stato viene visualizzato il passaggio specifico in cui la generazione dell'analisi non è riuscita. È possibile visualizzare altri dettagli nei log in% temp%\\dea. Verificare di disporre di una connessione valida al server con i diritti utente necessari, quindi riprovare. Se il problema persiste, contattare il team del prodotto.

|Possibili errori|Soluzione|  
|---|---|  
|RInterop ha raggiunto un errore all'avvio. Controllare i registri di RInterop e riprovare.|DEA richiede l'accesso a Internet per scaricare i pacchetti R dipendenti. Controllare i registri RInterop in% temp\\% RINTEROP e dea log in% temp\\% dea. Se RInterop è stato inizializzato in modo errato o è stato inizializzato senza i pacchetti R corretti, è possibile che venga visualizzata l'eccezione "non è stato possibile generare il nuovo report di analisi" dopo il passaggio InitializeRInterop nei log di DEA.<br><br>I registri RInterop possono anche visualizzare un errore simile a "non è disponibile alcun pacchetto jsonlite". Se il computer non ha accesso a Internet, è possibile scaricare manualmente il pacchetto R jsonlite necessario:<br><br><li>Passare alla cartella% UserProfile%\\DEARPackages nel file System del computer. Questa cartella è costituita dai pacchetti usati da R per DEA.</li><br><li>Se la cartella jsonlite non è presente nell'elenco dei pacchetti installati, è necessario disporre di un computer con accesso a Internet per scaricare la versione\_di rilascio di jsonlite [https://cran.r-project.org/web/packages/jsonlite/index.html](https://cran.r-project.org/web/packages/jsonlite/index.html)1.4. zip da.</li><br><li>Copiare il file zip nel computer in cui si sta eseguendo DEA.  Estrarre la cartella jsonlite e copiarla in% UserProfile%\\DEARPackages. Questo passaggio installa automaticamente il pacchetto jsonlite in R. La cartella deve essere denominata **jsonlite** e il contenuto deve trovarsi direttamente all'interno della cartella, non a un livello inferiore.</li><br><li>Chiudere DEA, riaprire e provare a eseguire di nuovo l'analisi.</li><br>È anche possibile usare RGUI. Passare a **pacchetti** > **Installa da zip**. Passare al pacchetto scaricato in precedenza e installare.<br><br>Se RInterop è stato inizializzato e configurato correttamente, verrà visualizzato il "installazione del pacchetto R dipendente jsonlite" nei log di RInterop.|  
|Impossibile connettersi all'istanza di SQL Server, verificare che il nome del server sia corretto e verificare l'accesso richiesto per l'utente che ha eseguito l'accesso.|È possibile che non si disponga dei diritti di accesso o utente per il server o che il nome del server non sia corretto.|
|Timeout del processo RInterop. Controllare i registri DEA e RInterop, arrestare il processo RInterop in Gestione attività, quindi riprovare.<br><br>o<br><br>RInterop è in stato di errore. Arrestare il processo RInterop in Gestione attività, quindi riprovare.|Per confermare l'errore, controllare\\i log in% Temp% RInterop. Rimuovere il processo RInterop da Gestione attività prima di riprovare. Se il problema persiste, contattare il team del prodotto.|

**D: il report è stato generato, ma i dati sembrano mancanti**

Controllare il database nel computer di analisi che esegue SQL Server per verificare che i dati esistano. Verificare che il database di analisi esista e controllarne le tabelle. Ad esempio, controllare le tabelle seguenti: TblBatchesA, TblBatchesB e TblSummaryStats.

Se i dati non sono presenti, è possibile che i dati non siano stati copiati correttamente o che il database sia danneggiato. Se mancano solo alcuni dati, i file di traccia creati in acquisizione o riproduzione potrebbero non avere acquisito accuratamente il carico di lavoro. Se i dati sono presenti, controllare i file di log in% temp\\% dea per verificare se sono stati registrati errori. Quindi, riprovare a generare il report di analisi.

Altre domande o commenti e suggerimenti? Inviare commenti e suggerimenti tramite lo strumento DEA scegliendo l'icona smile nell'angolo in basso a sinistra. 

## <a name="see-also"></a>Vedere anche

- Per informazioni su come visualizzare il report di analisi, vedere [visualizzare i report](database-experimentation-assistant-view-report.md).
