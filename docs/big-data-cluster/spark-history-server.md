---
title: Diagnosi/debug delle applicazioni Spark
titleSuffix: SQL Server big data clusters
description: Usare il Server cronologia Spark per eseguire il debug e diagnosticare le applicazioni Spark in esecuzione nei cluster di SQL Server 2019 dei big Data.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 6bc310fc856a9f2fe4a100770a5af2eed6a189e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66782101"
---
# <a name="debug-and-diagnose-spark-applications-on-sql-server-big-data-clusters-in-spark-history-server"></a>Debug e diagnosticare le applicazioni Spark nei cluster di big data di SQL Server in Server cronologia Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo fornisce indicazioni su come usare il Server cronologia Spark estesi per eseguire il debug e diagnosticare le applicazioni Spark in un cluster di big data 2019 Server SQL (anteprima). Queste funzionalità di debug e diagnosi vengono incorporate nel Server cronologia Spark e con tecnologia Microsoft. L'estensione include schede di dati e scheda graph e diagnosi. Nella scheda dati, gli utenti possono controllare i dati di input e outpui del processo Spark. Nella scheda graph, gli utenti possono controllare il flusso di dati e riprodurre il grafico del processo. Nella scheda diagnostica utente può fare riferimento a un'asimmetria dei dati, mancata sincronizzazione dell'ora e analisi dell'utilizzo di Executor.

## <a name="get-access-to-spark-history-server"></a>Ottenere l'accesso a Server cronologia Spark

L'esperienza utente di Spark cronologia server di origine aprire è stata migliorata con le informazioni, che includono dati specifici del processo e la visualizzazione interattiva dei flussi di dati e grafico processo per cluster di big data. 

### <a name="open-the-spark-history-server-web-ui-by-url"></a>Aprire il sito Web Server cronologia Spark dell'interfaccia utente dall'URL
Aprire il Server cronologia Spark passando all'URL seguente, sostituire `<Ipaddress>` e `<Port>` con informazioni specifiche del cluster di big data. Sono possibile fare riferimento altre informazioni: [Distribuire il cluster di big data di SQL Server](quickstart-big-data-cluster-deploy.md)

```
https://<Ipaddress>:<Port>/gateway/default/sparkhistory
```

Web Server cronologia Spark dell'interfaccia utente sarà simile a:

![Server cronologia Spark](./media/apache-azure-spark-history-server/spark-history-server.png)


## <a name="data-tab-in-spark-history-server"></a>Scheda di dati nel Server cronologia Spark
Selezionare l'ID di processo, quindi scegliere **dati** nel menu degli strumenti per ottenere la visualizzazione dei dati.

+ Controllare la **input**, **Outputs**, e **operazioni su tabella** selezionando le schede separatamente.

    ![Schede di dati Server cronologia Spark](./media/apache-azure-spark-history-server/sparkui-data-tabs.png)

+ Copiare tutte le righe facendo clic sul pulsante **copia**.

    ![Copiare tutte le righe](./media/apache-azure-spark-history-server/sparkui-data-copy.png)

+ Salvare tutti i dati come file con estensione CSV facendo clic sul pulsante **csv**.

    ![Salvare i dati come file CSV](./media/apache-azure-spark-history-server/sparkui-data-save.png)

+ Ricerca immettendo parole chiave nel campo **ricerca**, il risultato della ricerca verrà visualizzati immediatamente.

    ![Eseguire una ricerca con parole chiave](./media/apache-azure-spark-history-server/sparkui-data-search.png)

+ Fare clic sull'intestazione di colonna per ordinare tabelle, fare clic sul segno più per espandere una riga per visualizzare altri dettagli o fare clic sul segno meno per comprimere una riga.

    ![Funzionalità della tabella di dati](./media/apache-azure-spark-history-server/sparkui-data-table.png)

+ Scaricare un singolo file facendo clic sul pulsante **Download parziale** che posizionare a destra, quindi il file selezionato viene scaricato alla posizione locale. Se il file non esiste più, si aprirà una nuova scheda per visualizzare i messaggi di errore.

    ![Download di una riga di dati](./media/apache-azure-spark-history-server/sparkui-data-download-row.png)

+ Copia percorso completo o relativo, selezionando il **Copia percorso completo**, **Copia percorso relativo** vengono espanse dal menu di download. Per i file di archiviazione di azure data lake, **aperto in Azure Storage Explorer** avvierà Azure Storage Explorer. E individuare la cartella esatta durante l'accesso.

    ![Copiare un percorso completo o relativo](./media/apache-azure-spark-history-server/sparkui-data-copy-path.png)

+ Scegliere il numero di tabella seguente per passare pagine quando troppo molte righe per visualizzare in un'unica pagina. 

    ![Pagina di dati](./media/apache-azure-spark-history-server/sparkui-data-page.png)

+ Passare il puntatore sul punto interrogativo accanto a dati da visualizzare la descrizione comando, oppure fare clic sul punto interrogativo per ottenere altre informazioni.

    ![Dati altre info](./media/apache-azure-spark-history-server/sparkui-data-more-info.png)

+ Inviare commenti e suggerimenti con problemi facendo **fornire commenti e suggerimenti**.

    ![commenti e suggerimenti di Graph](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)

## <a name="graph-tab-in-spark-history-server"></a>Scheda grafico nel Server cronologia Spark

Selezionare l'ID di processo, quindi scegliere **Graph** dal menu dello strumento per ottenere la visualizzazione grafico del processo.

+ Panoramica del processo per controllare, il grafico del processo generato. 

+ Per impostazione predefinita, mostrerà tutti i processi e potrebbe essere filtrata dal **ID processo**.

    ![ID processo del grafico](./media/apache-azure-spark-history-server/sparkui-graph-jobid.png)

+ È necessario lasciare **lo stato di avanzamento** come valore predefinito. Utente può controllare il flusso di dati selezionando **Read** o * * Written * * * nell'elenco a discesa dei **Display**.

    ![visualizzazione del grafico](./media/apache-azure-spark-history-server/sparkui-graph-display.png)

    La visualizzazione del nodo grafico in colore che mostra la mappa termica.

    ![mappa termica del grafico](./media/apache-azure-spark-history-server/sparkui-graph-heatmap.png)

+ Riprodurre il processo facendo il **riproduzione** pulsante e arrestare in qualsiasi momento facendo clic sul pulsante Arresta. La visualizzazione di attività a colori per visualizzare lo stato di diversi durante la riproduzione:

    + Verde per ha avuto esito positivo: Il processo è stata completata.
    + Arancione per ripetuti: Istanze di attività non riuscite ma che non influiscono sul risultato finale del processo. Queste attività erano duplicati o ripetere le istanze che può essere completata in un secondo momento.
    + Blu per esecuzione: L'attività è in esecuzione.
    + Bianco per l'attesa o ignorate: L'attività è in attesa di esecuzione o la fase è ignorato.
    + Non è riuscita rosso per: L'attività non è riuscita.

    ![esempio di colore grafico, in esecuzione](./media/apache-azure-spark-history-server/sparkui-graph-color-running.png)
 
    La visualizzazione fase ignorata in bianco.
    ![esempio di colore del grafico, skip](./media/apache-azure-spark-history-server/sparkui-graph-color-skip.png)

    ![esempio di colore Graph, non è riuscita](./media/apache-azure-spark-history-server/sparkui-graph-color-failed.png)
 
    > [!NOTE]
    > È consentita la riproduzione per ogni processo. Per processo incompleto. la riproduzione non è supportata.


+ Scorre il mouse per ingrandire in ingresso/uscita grafico del processo oppure fare clic su **adatta alla** per renderla adatta allo schermo.
 
    ![zoom del grafico in base alle](./media/apache-azure-spark-history-server/sparkui-graph-zoom2fit.png)

+ Passare il mouse sul nodo grafico per visualizzare la descrizione comando quando sono presenti le attività non riuscite, fare clic sul palco per aprire la pagina di fase.

    ![descrizione comando del grafico](./media/apache-azure-spark-history-server/sparkui-graph-tooltip.png)

+ Nella scheda graph processo fasi disporrà della descrizione comando e icona piccola visualizzata se sono presenti attività soddisfa le seguenti condizioni:
    + Asimmetria dei dati: leggere i dati delle dimensioni > dimensioni di tutte le attività all'interno di questa fase di lettura dei dati Media * 2 e i dati letti dimensione > 10 MB
    + Sfasamento dell'ora: tempo di esecuzione > tempo di esecuzione medio di tutte le attività all'interno di questa fase * 2 e il tempo di esecuzione > 2 minuti

    ![icona dello sfasamento del Graph](./media/apache-azure-spark-history-server/sparkui-graph-skew-icon.png)

+ Il nodo grafico del processo visualizzerà le informazioni seguenti di ogni fase:
    + ID.
    + Nome o descrizione.
    + Numero totale di attività.
    + Dati letti: la somma delle dimensioni di input e shuffle dimensioni di lettura.
    + Scrittura di dati: la somma delle dimensioni di output e la sequenza casuale di dimensione di scrittura.
    + Tempo di esecuzione: il tempo tra l'ora di inizio del primo tentativo e l'ora di completamento dell'ultimo tentativo.
    + Conteggio delle righe: la somma dei record di input, record di output, riprodurre in modo casuale i record di lettura e scrittura record di riproduzione casuale.
    + Stato di avanzamento.

    > [!NOTE]
    > Per impostazione predefinita, il nodo grafico del processo verrà visualizzate le informazioni dall'ultimo tentativo di ogni fase (ad eccezione di tempo di esecuzione fase), ma durante il grafico di riproduzione nodo consentirà di visualizzare le informazioni di ogni tentativo.

    > [!NOTE]
    > Per le dimensioni dei dati di lettura e scrittura viene usato 1 MB = 1000 KB = 1000 * 1000 byte.

+ Inviare commenti e suggerimenti con problemi facendo **fornire commenti e suggerimenti**.

    ![commenti e suggerimenti di Graph](./media/apache-azure-spark-history-server/sparkui-graph-feedback.png)


## <a name="diagnosis-tab-in-spark-history-server"></a>Scheda diagnosi nel Server cronologia Spark
Selezionare l'ID di processo, quindi scegliere **diagnosi** nel menu degli strumenti per ottenere il processo di visualizzazione di diagnosi. La scheda diagnostica include **asimmetria dei dati**, **sfasamento dell'ora**, e **analisi dell'utilizzo dell'Executor**.
    
+ Verificare i **asimmetria dei dati**, **sfasamento dell'ora**, e **analisi dell'utilizzo dell'Executor** selezionando le schede, rispettivamente.

    ![Schede di diagnosi](./media/apache-azure-spark-history-server/sparkui-diagnosis-tabs.png)

### <a name="data-skew"></a>Asimmetria dei dati
Fare clic su **asimmetria dei dati** corrispondente della scheda vengono visualizzate attività differente in base ai parametri specificati. 

+ **Specificare i parametri** -la prima sezione Visualizza i parametri, che consentono di rilevare differenze dei dati. La regola predefinita è: Dati attività letti è maggiori di tre volte in cui i dati di attività medio di lettura e i dati attività letti sono superiore a 10 MB. Se si desidera definire una regola personalizzata per le attività asimmetriche, è possibile scegliere i parametri, il **fase asimmetrica**, e **inclinare Char** sezione verrà aggiornata di conseguenza. 

+ **Asimmetria fase** -nella seconda sezione vengono visualizzate le fasi, che sono asimmetrici attività che soddisfano i criteri specificati in precedenza. Se è presente più di un'attività asimmetriche in una fase, la tabella fase asimmetrica viene visualizzato solo l'attività più differente (ad esempio, i dati più grande di asimmetria dei dati). 

    ![Sezione2 asimmetria dei dati](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section2.png)

+ **Una differenza del grafico** : quando è selezionata una riga nella tabella di gestione temporanea di inclinazione, verrà visualizzato il grafico inclinazione ulteriori dettagli di distribuzioni di attività basati su dati letti e tempo di esecuzione. Le attività asimmetriche vengono contrassegnate in rosso e le normali attività vengano contrassegnate in blu. Per considerazioni relative alle prestazioni, il grafico visualizza solo le attività di esempio fino a 100. Nel pannello in basso a destra vengono visualizzati i dettagli dell'attività.

    ![Sezione3 asimmetria dei dati](./media/apache-azure-spark-history-server/sparkui-diagnosis-dataskew-section3.png)

### <a name="time-skew"></a>Mancata sincronizzazione dell'ora
Il **sfasamento dell'ora** scheda vengono visualizzate attività asimmetriche basate sul tempo di esecuzione di attività. 

+ **Specificare i parametri** -la prima sezione Visualizza i parametri, che consentono di rilevare lo sfasamento dell'ora. I criteri predefiniti per il rilevamento dello sfasamento di orario è: tempo di esecuzione di attività è maggiore di tre volte del tempo medio di esecuzione e il tempo di esecuzione di attività è maggiore di 30 secondi. È possibile modificare i parametri in base alle esigenze. Il **fase asimmetrica** e **inclinare grafico** visualizzare le informazioni sulle attività e fasi corrispondente allo stesso modo il **asimmetria dei dati** scheda riportato sopra.

+ Fare clic su **sfasamento dell'ora**, quindi incluso nel risultato filtrato **fase asimmetrica** sezione in base ai parametri impostati nella sezione **specifica parametri di**. Fare clic su un elemento **fase asimmetrica** sezione, quindi, il grafico corrispondente viene redatto in sezione3 e i dettagli dell'attività vengono visualizzati nel pannello in basso a destra.

    ![Sezione2 dello sfasamento dell'ora](./media/apache-azure-spark-history-server/sparkui-diagnosis-timeskew-section2.png)

### <a name="executor-usage-analysis"></a>Analisi dell'utilizzo dell'executor
Visualizza la il grafico sull'utilizzo di Executor di Spark esecutore effettivo in esecuzione e allocazione lo stato del processo.  

+ Fare clic su **analisi dell'utilizzo dell'Executor**, quindi è in versione bozza quattro curve tipi sull'utilizzo di executor. Includano **allocata executor**, **executor in esecuzione**, **inattività executor**, e **numero massimo di istanze di Executor**. Riguardanti gli executor allocati, ogni "Executor aggiunto" o "Executor rimosse" evento aumenterà o diminuirà executor allocato. È possibile controllare "Event Timeline" nella scheda "Jobs" per il confronto di più.

    ![Scheda executor](./media/apache-azure-spark-history-server/sparkui-diagnosis-executors.png)

+ Fare clic sull'icona del colore per selezionare o deselezionare il contenuto corrispondente in tutte le bozze.

    ![Selezionare grafico](./media/apache-azure-spark-history-server/sparkui-diagnosis-select-chart.png)


## <a name="known-issues"></a>Problemi noti
Il Server cronologia Spark ha i seguenti problemi noti:

+ Attualmente, funziona solo per cluster Spark 2.3.

+ Non visualizzerà dati di input/output usando RDD nella scheda dati.

## <a name="next-steps"></a>Passaggi successivi

* [Gestire le risorse per un cluster Spark in HDInsight](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-resource-manager)
* [Configurare le impostazioni di Spark](https://docs.microsoft.com/azure/hdinsight/spark/apache-spark-settings)
