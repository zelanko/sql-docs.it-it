---
title: Precaricare la cache (SSRS) | Microsoft Docs
ms.date: 05/14/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- cache [Reporting Services]
- preloading cache
ms.assetid: 152a1051-8aa5-4c01-bc85-f8be8971b0cd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6b2be1e020354f47aa21dc83f17ff6169bcf2d72
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "66174996"
---
# <a name="preload-the-cache"></a>Precaricare la cache  
  Per precaricare la cache per un set di dati condiviso, è possibile creare un piano di aggiornamento della cache per il set di dati stesso.  
  
 Di seguito vengono indicate le due modalità di precaricamento della cache.  
  
1.  Creazione di un piano di aggiornamento della cache per il report Questo è il metodo preferito.  
  
2.  Utilizzo di una sottoscrizione guidata dai dati per il precaricamento della cache con istanze di report con parametri. Questo metodo consente di precaricare la cache solo in versioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] precedenti a [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. Per altre informazioni, vedere [Memorizzazione dei report nella cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md).  
  
 Per memorizzare nella cache un report o un set di dati condiviso, è necessario che siano soddisfatte le condizioni seguenti:  
  
-   Il set di dati condiviso o il report deve essere abilitato per la memorizzazione nella cache.  
  
-   Le origini dati condivise per il set di dati condiviso o il report devono essere configurate per l'utilizzo di credenziali archiviate o di nessuna credenziale.  
  
-   È necessario che il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia in esecuzione.  
  
## <a name="to-preload-the-cache-by-creating-a-cache-refresh-plan"></a>Per precaricare la cache creando un piano di aggiornamento della cache  
  
1. Avviare il [portale Web di un server di report](../../reporting-services/web-portal-ssrs-native-mode.md "Portale Web di un server di report").  
  
2. Selezionare **Esplora** dalla schermata iniziale e spostarsi nella gerarchia di cartelle per individuare l'elemento che si vuole memorizzare nella cache.  
  
3. Selezionare i puntini di sospensione nell'angolo superiore destro dell'elemento e quindi selezionare **Gestisci** dal menu a discesa.  
  
4. Selezionare la scheda **Cache** nel menu verticale a sinistra.  
  
5. Per attivare la memorizzazione nella cache per un set di dati, selezionare il pulsante di opzione **Memorizzare nella cache copie di questo set di dati e usarle quando disponibili**. Verrà visualizzata la sezione **Scadenza della cache** al di sotto. Selezionare uno dei pulsanti di opzione seguenti:

    - **Scadenza della cache dopo x minuti** (immettere il numero desiderato di minuti per x).
    - **Scadenza della cache in base a una pianificazione**.  Reporting Services rende disponibili pianificazioni condivise e pianificazioni specifiche dei report per controllare l'elaborazione, la coerenza dei contenuti e le prestazioni della distribuzione dei report. Per altre informazioni, vedere [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md "Create, Modify, and Delete Schedules"). Sono disponibili diverse opzioni per creare una pianificazione, in questo caso per la scadenza della cache: Selezionare una delle due opzioni di pianificazione seguenti:  
      - Pulsante di opzione **Pianificazione condivisa** e quindi selezionare una pianificazione nella casella di testo a discesa **Selezionare una pianificazione condivisa**. Per altre informazioni, vedere [Schedules](../../reporting-services/subscriptions/schedules.md "Pianificazioni").  
      - Pulsante di opzione **Pianificazione in base al report**, quindi selezionare il collegamento **Modifica pianificazione** se necessario per visualizzare la pagina *Dettagli pianificazione*.  

         ![Pagina dei dettagli della pianificazione della scadenza della cache del portale Web per i set di dati](../../reporting-services/report-server/media/preload-the-cache/web-portal-dataset-cache-schedule-details.png "Pagina dei dettagli della pianificazione della cache del set di dati")

          In questa pagina è possibile selezionare:
         - Il tipo di pianificazione:
           - **Ora** - Esegui la pianificazione ogni: specificare ore e minuti e l'ora di inizio.
           - **Giorno** - Selezionare una delle tre opzioni seguenti:  
              - **Nei giorni seguenti**: (Dom, Lun, Mar, Mer, Gio, Ven, Sat).
              - **Ogni giorno feriale**
              - **Ripeti dopo il numero di giorni seguente** - Specificare un numero.  
           - **Settimana** - Specificare entrambe le opzioni seguenti:
              - **Ripeti dopo il numero di settimane seguente:** - Specificare un numero.  
              - **Nei giorni** - Selezionare i giorni della settimana per l'esecuzione.  
           - **Mese** - Selezionare i mesi per l'esecuzione, scegliendo le opzioni seguenti:
              - **Nella settimana del mese**:  
                 - selezionare Prima, Seconda, Terza, Quarta o Ultima nella casella a discesa.  
                 - **Giorno della settimana**: selezionare una o più delle caselle di controllo Lun, Mar, Mer, Gio, Ven, Sab, Dom.  
                 - **Nei giorni di calendario** - Immettere il numero effettivo del giorno del mese separato da virgole, o un intervallo di giorni separati da un trattino o qualsiasi combinazione di entrambi (ad esempio 1,3-5).  
           - **Una volta** - Una singola occorrenza.  
         - **Ora di inizio** - Ora del giorno per l'avvio della pianificazione.  
         - **Date di inizio e fine** - Specificare la data di inizio e facoltativamente la data di fine della pianificazione.
         - Selezionare **Applica** per salvare la pianificazione.  
           > [!NOTE]
           > Se per l'elemento la memorizzazione nella cache non è abilitata, verrà richiesto di abilitarla. Per abilitare la memorizzazione nella cache, selezionare **OK**.  

         - Selezionare **Crea piano di aggiornamento della cache** per creare/salvare il piano della cache.  
         La pagina **Piani di aggiornamento della cache** verrà visualizzata sullo schermo. Da qui è possibile:
           - Aggiungere un nuovo piano di aggiornamento della cache.
           - Creare un nuovo piano di aggiornamento della cache da un piano esistente.
           - Aggiornare la pagina dei piani di aggiornamento della cache.
           - Eliminare un piano.
           - Cercare un piano in base al nome.

         Se non è ancora stato salvato alcun piano di aggiornamento della cache, l'elenco sarà vuoto e "Aggiungi" sarà l'unica opzione disponibile. Selezionare **+ Nuovo piano di aggiornamento della cache** per aggiungerne uno nuovo. Verrà visualizzata la pagina **Nuovo piano di aggiornamento della cache**.  
           - Digitare una **Descrizione** nella prima casella di testo per assegnare un nome al piano di aggiornamento.  
           - Selezionare uno dei seguenti pulsanti di opzione in **Aggiornare la cache in base alla pianificazione seguente**  
             - **Pianificazione condivisa** - Selezionare una pianificazione condivisa nella casella a discesa adiacente. 
             - **Pianificazione in base al report** - Modificare la pianificazione come indicato nel passaggio 2.2 precedente selezionando il collegamento **Modifica pianificazione** se si vuole, per visualizzare la pagina *Dettagli pianificazione*. 
             - Selezionare **Crea piano di aggiornamento della cache** per salvare il piano, in caso di aggiunta, o **Applica** in caso di modifica del piano.  
      Si tornerà alla pagina **Piani di aggiornamento della cache** aggiornata.
  
## <a name="to-preload-the-cache-with-a-user-specific-report-by-using-a-data-driven-subscription"></a>Per precaricare la cache con un report specifico dell'utente tramite una sottoscrizione guidata dai dati

1. Avviare il [portale Web di un server di report](../../reporting-services/web-portal-ssrs-native-mode.md "Portale Web di un server di report").  
2. Selezionare **Esplora** dalla schermata iniziale e spostarsi nella gerarchia di cartelle per individuare il report che si vuole sottoscrivere.  
3. Fare clic con il pulsante destro del mouse sul report e scegliere **Sottoscrivi** dal menu a discesa. Verrà visualizzata la pagina **Nuove sottoscrizioni**.  
4. Immettere una descrizione per la sottoscrizione nella casella di testo **Descrizione**.  
5. Per il pulsante di opzione **Tipo di sottoscrizione** vengono visualizzate due opzioni:  
   - **Sottoscrizione standard** - Per generare e fornire un solo report
   - **Sottoscrizione guidata dai dati** - Per generare e fornire un solo report per ogni riga di un set di dati. Questa è l'opzione da selezionare per precaricare la cache.
6. Nella sezione **Pianificazione** selezionare uno dei pulsanti di opzione seguenti:
   - **Pianificazione condivisa** - Selezionare una pianificazione condivisa nella casella a discesa.  
   - **Pianificazione in base al report** - Modificare la pianificazione come indicato nel passaggio 2.2 precedente selezionando il collegamento **Modifica pianificazione** se si vuole, per visualizzare la pagina *Dettagli pianificazione*.  
7. Nella sezione **Destinazione** vengono visualizzate le opzioni seguenti in una casella a discesa:
    - **Condivisione file di Windows**
    - **Posta elettronica**
    - **Provider recapito Null** - Per questa attività, selezionare un provider di recapito Null.  
8. Nella sezione **Set di dati** modificare o creare un set di dati per questa sottoscrizione del report selezionando il pulsante **Modifica set di dati**.  
9. Nella pagina **Modifica set di dati** nella sezione **Origine dati** scegliere l'origine dati che contiene i valori dei parametri del report e le opzioni di recapito. Le scelte disponibili sono:  
   - **Origine dati condivisa** - Selezionare i puntini di sospensione e selezionare un'origine dati condivisa dalla cartella *Origine dati condivisa*.
   - **Origine dati personalizzata** - Scelta più probabile. Si tratta dell'opzione che sarà necessario scegliere, a meno che qualcuno non abbia già completato i passaggi seguenti per crearla come origine dati condivisa.  
     - Specificare il tipo di connessione, la stringa di connessione e le credenziali per l'accesso all'origine dei dati che contiene i dati relativi ai sottoscrittori. L'esempio seguente illustra una stringa di connessione usata per la connessione a un database di SQL Server denominato Subscribers.  
  
   ```T-SQL
   data source=<servername>;initial catalog=Subscribers  
   ```
  
10. Nella sezione **Query** specificare la query che recupera i dati del sottoscrittore desiderato.  Ad esempio:  
  
    ```T-SQL  
    Select * from RptSubscribers  
    ```
  
    Se lo si desidera, aumentare il periodo di timeout per le query che richiedono un'elaborazione prolungata.  
  
11. Selezionare **Convalida**. È necessario convalidare la query prima di proseguire. Quando viene visualizzato il messaggio **La convalida è riuscita**, verrà visualizzato un elenco di campi di set di dati sotto il pulsante **Convalida**. Selezionare **Applica** per creare l'origine dati personalizzata.  
  
12. Si torna alla pagina **Nuova sottoscrizione**.  Nella sezione **Parametri report** specificare i valori per gli eventuali parametri del report visualizzati.  

13. Selezionare **Crea sottoscrizione**.  
  
14. Verrà visualizzata la pagina **Sottoscrizioni** che mostra la nuova sottoscrizione guidata dai dati. Da questa pagina è possibile abilitare la sottoscrizione quando si è pronti selezionando la casella di controllo alla sua sinistra e selezionando poi il pulsante **Abilita**. ![Pulsante Abilita della pagina Sottoscrizioni](../../reporting-services/report-server/media/preload-the-cache/subscriptions-page-enable-button.png "Pulsante Abilita nella pagina Sottoscrizioni")

15. Specificare quando viene elaborata la sottoscrizione. Non scegliere **Quando i dati del report vengono aggiornati nel server di report**. Questa impostazione è solo per gli snapshot. Se si vuole usare una pianificazione preesistente, selezionare **In base a una pianificazione condivisa**.  
  
     In alternativa, per creare una pianificazione personalizzata selezionare **In base a una pianificazione creata per questa sottoscrizione** e quindi selezionare **Avanti**. Configurare la pianificazione e quindi selezionare **Fine**.  
  
    > [!NOTE]  
    > Perché i sottoscrittori possano ricevere il report più recente, è necessario che la pianificazione configurata dall'utente sia coerente con la pianificazione di recapito del report che è stata definita per i sottoscrittori. Per altre informazioni, vedere [Portale Web di un server di report](../../reporting-services/web-portal-ssrs-native-mode.md  "Portale Web di un server di report").  
  
16. Configurare le opzioni di esecuzione del report come segue. Nella pagina del report selezionare la scheda **Proprietà**.  
  
17. Nel riquadro a sinistra selezionare la scheda **Esecuzione**.  
  
18. Nella pagina scegliere **Esegui il rendering del report con i dati più recenti**.  
  
19. Selezionare una delle due opzioni della cache e configurare la scadenza come segue:  
  
    - Per impostare la scadenza della copia memorizzata nella cache dopo un determinato periodo di tempo, selezionare **Memorizza nella cache una copia temporanea del report. La copia del report scadrà dopo il numero di minuti seguente.** Digitare il numero di minuti alla scadenza del report.  
  
    - Per impostare la scadenza della copia memorizzata nella cache in base a una pianificazione, selezionare **Memorizza nella cache una copia temporanea del report. La scadenza della copia è determinata dalla pianificazione seguente.** Per impostare una pianificazione per la scadenza del report, selezionare **Configura** oppure selezionare una pianificazione condivisa.  
  
20. Selezionare **Applica**.
  
## <a name="see-also"></a>Vedere anche  

 [Sottoscrizioni guidate dai dati](../../reporting-services/subscriptions/data-driven-subscriptions.md)  
 [Creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](../../reporting-services/create-a-data-driven-subscription-ssrs-tutorial.md)  
 [Prestazioni, snapshot, memorizzazione nella cache &#40;Reporting Services&#41;](../../reporting-services/report-server/performance-snapshots-caching-reporting-services.md)  
 [Impostare le proprietà di elaborazione dei report](../../reporting-services/report-server/set-report-processing-properties.md)  
 [Memorizzazione dei report nella cache &#40;SSRS&#41;](../../reporting-services/report-server/caching-reports-ssrs.md)  
 [Utilizzo dei set di dati condivisi](../../reporting-services/work-with-shared-datasets-web-portal.md)  
  
