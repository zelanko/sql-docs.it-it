---
title: Creare report di analisi nel Database sperimentazione Assistant per gli aggiornamenti di SQL Server
description: Creare report di analisi nel Database sperimentazione Assistente
ms.custom: ''
ms.date: 10/22/2018
ms.prod: sql
ms.prod_service: dea
ms.suite: sql
ms.technology: dea
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: HJToland3
ms.author: ajaykar
ms.reviewer: mathoma
manager: jroth
ms.openlocfilehash: ff0a31fc4d825966fefafc11d8780862634f1937
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794483"
---
# <a name="create-analysis-reports-in-database-experimentation-assistant"></a>Creare report di analisi nel Database sperimentazione Assistant

Dopo che riprodurre la traccia di origine su entrambi i server di destinazione, è possibile generare un report di analisi nel Database sperimentazione Assistant DEA (). I report di analisi consentono di ottenere informazioni dettagliate sulle implicazioni sulle prestazioni delle modifiche proposte.

## <a name="create-an-analysis-report"></a>Creare un report di analisi

In DEA, selezionare l'icona di menu. Nel menu espanso, selezionare **report di analisi** accanto all'icona di elenco di controllo.

![Menu Analysis](./media/database-experimentation-assistant-create-report/dea-create-reports-menu.png)

Sotto **report di analisi**, selezionare **nuovo report di analisi**.

![Menu Nuovo Report di analisi](./media/database-experimentation-assistant-create-report/dea-create-reports-new-report.png)

Immettere o selezionare le informazioni seguenti:

- **Nome del report**: Immettere un nome per il report. Il nome del report viene usato sia per il database B e. Esempio: *(A o B)*  + *nome del report* + *identificatore univoco*. 
- **Nome server**: Immettere il nome del computer del server che si desidera includere in A, B e i database di analisi.
- **Nome dell'istanza SQL Server**: Immettere il nome dell'istanza di SQL Server da utilizzare per il report.
- **Traccia per il server di origine**: Immettere il file di traccia (trc) prima di SQL Server (2008 R2).
- **Traccia per il server di destinazione**: Immettere la destinazione SQL Server (2014) primo file trc.

![Pagina nuovo report di analisi](./media/database-experimentation-assistant-create-report/dea-create-reports-inputs.png)

## <a name="generate-a-report"></a>Generare un report

Dopo aver immesso o selezionato le informazioni necessarie sul **nuovo report di analisi** pagina, selezionare **avviare** per avviare la creazione di report. Se le informazioni immesse sono valide, viene creato il report di analisi. In caso contrario, le caselle di testo contenenti informazioni non valide sono evidenziate in rosso. Assicurarsi di immettere i valori corretti e quindi selezionare **avviare**. 

Viene generato un nuovo report di analisi. Il database di analisi segue lo schema di denominazione Analysis + *nome report specificato dall'utente* + *identificatore univoco*.

## <a name="frequently-asked-questions-about-analysis-reports"></a>Domande frequenti sui report di analisi

### <a name="what-does-my-analysis-report-tell-me"></a>Come può il report di analisi?
    
DEA Usa test statistici per analizzare il carico di lavoro e determinare come ogni query è stata eseguita dalla destinazione 1 e 2 di destinazione. Fornisce dettagli sulle prestazioni per ogni query. Altre informazioni su DEA negli [iniziare a usare](database-experimentation-assistant-get-started.md).
    
### <a name="can-i-create-a-new-analysis-report-while-another-report-is-being-generated"></a>È possibile creare un nuovo report di analisi durante la generazione di un altro report?
    
No.  Attualmente, è possibile generare un solo report alla volta per evitare conflitti. Tuttavia, è possibile eseguire più di una sola acquisizione e riproduzione nello stesso momento.

### <a name="i-upgraded-dea-to-version-20-can-i-still-view-and-use-my-old-reports"></a>DEA aggiornamento alla versione 2.0. È possibile comunque visualizzare e utilizzare report personali precedente?
    
Sì. Per visualizzare i report generati in precedenza, è necessario aggiornare lo schema del report. Per altre informazioni, vedere [DEA 2.0: Aggiorna schema di database per report di analisi in DEA](https://blogs.msdn.microsoft.com/datamigration/2017/03/24/dea-2-0-updating-db-schema-for-analysis-report-in-the-database-experimentation-assistant/).
    
### <a name="can-i-generate-an-analysis-report-by-using-the-command-prompt"></a>È possibile generare un report di analisi tramite il prompt dei comandi?
    
Sì. È possibile generare un report di analisi al prompt dei comandi. È quindi possibile visualizzare il report nell'interfaccia utente. Per altre informazioni, vedere [prompt dei comandi eseguire](database-experimentation-assistant-run-command-prompt.md).
    
## <a name="troubleshoot-analysis-reports"></a>Risolvere i problemi di report di analisi

###  <a name="what-security-permissions-do-i-need-to-generate-and-view-an-analysis-report-on-my-server"></a>Le autorizzazioni di sicurezza è necessario generare e visualizzare un report di analisi nella mio server?
    
L'utente che è connesso a DEA deve avere diritti sysadmin per analysis server. Se l'utente fa parte di un gruppo, assicurarsi che il gruppo con diritti sysadmin.

|Possibili errori|Soluzione|  
|---|---|  
|Impossibile connettersi al database. Assicurarsi di avere i diritti sysadmin per l'analisi e visualizzazione dei report.|Non si dispone di diritti di accesso o sysadmin per server o nel database. Verificare i diritti di accesso e riprovare.|  
|Non è possibile generare **nome del Report** nel server **nome Server**. Per informazioni dettagliate, vedere la **Nome Report** report.|Non si dispone dei diritti sysadmin necessari per generare un nuovo report. Per visualizzare gli errori dettagliati, selezionare il report scadute e controllare i registri in % temp %\\DEA.|  
|L'utente corrente non ha le autorizzazioni necessarie per eseguire l'operazione. Assicurarsi di avere i diritti sysadmin per l'esecuzione di traccia e analisi dei report.|Non hai i diritti sysadmin necessari per generare un nuovo report.|  

### <a name="i-cant-connect-to-the-computer-running-sql-server"></a>Non è possibile connettersi al computer che esegue SQL Server
    
- Verificare che il nome del computer che esegue SQL Server sia valido. Per confermare, provare a connettersi al server usando SQL Server Management Studio (SSMS).
- Verificare che la configurazione del firewall non blocca le connessioni al computer che esegue SQL Server.
- Verificare che l'utente disponga dei diritti utente necessari. 

È possibile visualizzare più dettagli nei log in % temp %\\DEA. Se il problema persiste, contattare il team del prodotto.

### <a name="i-see-an-error-when-i-generate-an-analysis-report"></a>Viene visualizzato un errore quando è possibile generare un report di analisi
    
L'accesso a Internet è necessario la prima volta che si genera un report di analisi dopo aver installato DEA. L'accesso a Internet è necessario per scaricare i pacchetti necessari per l'analisi statistica.

Se si verifica un errore durante la creazione di report, la pagina di avanzamento viene illustrato il passaggio specifico in corrispondenza del quale la generazione di analisi non riuscita. È possibile visualizzare più dettagli nei log in % temp %\\DEA. Verificare di avere una connessione valida al server con diritti utente necessari e quindi ripetere. Se il problema persiste, contattare il team del prodotto.

|Possibili errori|Soluzione|  
|---|---|  
|RInterop ha restituito un errore all'avvio. Controllare i registri RInterop e riprovare.|DEA richiede l'accesso a internet per scaricare i pacchetti R dipendenti. Controllare i log di RInterop in % temp %\\RInterop e DEA registri in % temp %\\DEA. Se RInterop è stata inizializzata in modo non corretto o se inizializzata senza i pacchetti R corretti, si può vedere l'eccezione "Non è stato possibile generare nuovo report di analisi" dopo il passaggio InitializeRInterop nei log DEA.<br><br>I log RInterop anche potrebbero mostrare un errore simile a "non vi è alcun pacchetto jsonlite disponibile". Se il computer non dispone dell'accesso a internet, è possibile scaricare manualmente il pacchetto richiesto jsonlite R:<br><br><li>Passare a % userprofile %\\DEARPackages cartella nel file system del computer. Questa cartella è costituito da pacchetti usati da R per DEA.</li><br><li>Se la cartella jsonlite è presente nell'elenco dei pacchetti installati, è necessario un computer con accesso a internet per scaricare la versione finale di jsonlite\_1.4.zip dal [ https://cran.r-project.org/web/packages/jsonlite/index.html ](https://cran.r-project.org/web/packages/jsonlite/index.html).</li><br><li>Copiare il file con estensione zip nel computer in cui si esegue DEA.  Estrarre la cartella jsonlite e copiarli in % userprofile %\\DEARPackages. Questo passaggio installa automaticamente il pacchetto jsonlite in R. La cartella deve essere denominata **jsonlite** e deve essere il contenuto direttamente all'interno della cartella, non un livello sotto.</li><br><li>Chiudere DEA, riaprire e l'analisi di riprovare.</li><br>È anche possibile usare il RGUI. Passare a **pacchetti** > **installare dal file zip**. Passare al pacchetto scaricato in precedenza e installare.<br><br>Se RInterop è stato inizializzato e configurato correttamente, dovrebbe essere "Installing dipendenti R pacchetto jsonlite" nei log RInterop.|  
|Non è possibile connettersi all'istanza di SQL Server, assicurarsi che il nome del server sia corretto e verificare la presenza dell'accesso necessario per l'utente connesso.|Si potrebbe non avere accesso o diritti utente per il server o il nome del server potrebbero non essere corretto.| 
|Timeout del processo RInterop. Controllare i registri DEA e RInterop, arrestare il processo RInterop in Gestione attività e quindi riprovare.<br><br>o Gestione configurazione<br><br>RInterop è in stato di errore. Arrestare il processo RInterop in Gestione attività e quindi riprovare.|Vedere i log in % temp %\\RInterop per confermare l'errore. Rimuovere il processo RInterop da Gestione attività prima di riprovare. Se il problema persiste, contattare il team del prodotto.| 

### <a name="the-report-is-generated-but-data-appears-to-be-missing"></a>Viene generato il report, ma vengono visualizzati dati mancanti
    
Controllare il database nel computer che esegue SQL Server per verificare l'esistano di dati analisi. Controllare che sia presente il database di analisi e controllare le relative tabelle. Ad esempio, controllare queste tabelle: TblBatchesA TblBatchesB e TblSummaryStats.

Se i dati non esistono, i dati non siano stati copiati correttamente o il database potrebbe essere danneggiato. Se solo alcuni dati sono mancanti, i file di traccia creato nell'acquisizione o replay potrebbe non avere acquisito il carico di lavoro in modo accurato. Se i dati sono presenti, controllare i file di log in % temp %\\DEA per vedere se sono stati registrati errori. Quindi, riprovare a generare il report di analisi.

Altre domande o commenti e suggerimenti? Inviare commenti e suggerimenti tramite lo strumento DEA scegliendo l'icona smile nell'angolo inferiore sinistro.  

## <a name="next-steps"></a>Passaggi successivi

- Per informazioni su come visualizzare il report di analisi, vedere [visualizzare i report](database-experimentation-assistant-view-report.md).

- Per un'introduzione di 19 minuti DEA e dimostrazione, guardare il video seguente:

  > [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-the-Database-Experimentation-Assistant/player]
