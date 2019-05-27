---
title: Modificare la visualizzazione dei risultati di traccia | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 860a80dc-bac0-4ef0-bf7f-7a9b430d7aa3
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 780772f7703e4499c13eb9373ccad4252097b536
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66089443"
---
# <a name="modify-the-trace-results-view"></a>Modificare la visualizzazione dei risultati della traccia
  In questo argomento viene descritto come modificare la vista dei risultati di traccia di una sessione di Eventi estesi in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] eseguendo le attività seguenti.  
  
1.  [Aggiungere o rimuovere colonne](#AddRemoveColumns)  
  
2.  [Creare, modificare o eliminare colonne unite](#ChangeColumns)  
  
3.  [Ordinare i risultati](#SortResults)  
  
4.  [Raggruppare i risultati](#GroupResults)  
  
5.  [Aggregare i risultati](#AggregateResults)  
  
6.  [Filtrare i risultati](#Filter)  
  
7.  [Cercare il testo nelle colonne](#Search)  
  
8.  [Modificare le impostazioni di visualizzazione](#ChangeDisplay)  
  
##  <a name="AddRemoveColumns"></a> Aggiungere o rimuovere colonne  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia.  
  
    > [!NOTE]  
    >  È possibile anche con il pulsante destro fare clic sul nome della sessione e quindi selezionare **Controlla dati dinamici**.  
  
2.  Nella finestra dei risultati della traccia, fare doppio clic sull'intestazione di colonna e quindi selezionare **Scegli colonne**.  
  
3.  Nella sezione **Colonne disponibili** della finestra di dialogo **Scegli colonne** selezionare i nomi delle colonne che si desidera aggiungere, quindi fare clic su pulsante della freccia DESTRA.  
  
    > [!NOTE]  
    >  Per impostazione predefinita, le colonne sono disposte in base al nome. Per visualizzare le colonne in base all'evento, fare clic su **Disponi per evento**.  
  
     Per rimuovere colonne, nella sezione **Colonne selezionate** selezionare le colonne che si desidera rimuovere, quindi fare clic sulla freccia a sinistra.  
  
4.  Per modificare la visualizzazione dell'ordine delle colonne, nella sezione **Colonne selezionate** fare clic rispettivamente su **Sposta su** o **Sposta giù** . Non è possibile spostare più righe.  
  
5.  Fare clic su **OK**.  
  
##  <a name="ChangeColumns"></a> Creare, modificare o eliminare colonne unite  
  
#### <a name="to-create-merged-columns"></a>Per creare colonne unite  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia.  
  
    > [!NOTE]  
    >  È possibile anche con il pulsante destro fare clic sul nome della sessione e quindi selezionare **Controlla dati dinamici**.  
  
2.  Nella finestra dei risultati della traccia fare clic con il pulsante destro del mouse sull'intestazione di colonna, quindi fare clic su **Scegli colonne**.  
  
3.  Nella finestra di dialogo **Scegli colonne** fare clic su **Nuova**.  
  
4.  Nella casella **Nome colonna unita** della finestra di dialogo **Nuova colonna unita** immettere un nome per le colonne unite.  
  
5.  Nel **colonne originali da unire** selezionare due o più colonne da unire nell'elenco a discesa.  
  
    > [!NOTE]  
    >  Eventi estesi supporta solo l'unione di un massimo di cinque colonne.  
  
6.  Fare clic su **OK**.  
  
#### <a name="to-edit-merged-columns"></a>Per modificare colonne unite  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia.  
  
    > [!NOTE]  
    >  È possibile anche con il pulsante destro fare clic sul nome della sessione e quindi selezionare **Controlla dati dinamici**.  
  
2.  Nella finestra dei risultati della traccia fare clic con il pulsante destro del mouse sull'intestazione di colonna, quindi fare clic su **Scegli colonne**.  
  
3.  Nella finestra di dialogo **Scegli colonne** fare clic su **Modifica**.  
  
4.  Per modificare il nome della colonna unita, nella casella **Nome colonna unita** della finestra di dialogo **Nuova colonna unita** immettere il nuovo nome.  
  
     Per modificare le colonne che si desidera unire, nella **colonne originali da unire** , selezionare le colonne da unire nell'elenco a discesa e quindi fare clic su **OK**.  
  
#### <a name="to-delete-merged-columns"></a>Per eliminare colonne unite  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia.  
  
    > [!NOTE]  
    >  È possibile anche con il pulsante destro fare clic sul nome della sessione e quindi selezionare **Controlla dati dinamici**.  
  
2.  Nella finestra dei risultati della traccia fare clic con il pulsante destro del mouse sull'intestazione di colonna, quindi fare clic su **Scegli colonne**.  
  
3.  Nella finestra di dialogo **Scegli colonne** selezionare il nome della colonna unita da eliminare, quindi scegliere **Elimina**.  
  
##  <a name="SortResults"></a> Ordinare i risultati  
  
#### <a name="to-sort-the-results-in-ascending-or-descending-order"></a>Per ordinare i risultati in ordine crescente o decrescente  
  
-   Aprire un file XEL per visualizzare i risultati della traccia.  
  
    > [!NOTE]  
    >  È anche possibile fare clic sul nome della sessione, selezionare **Controlla dati dinamici**, quindi fare clic sui **arresta Feed di dati** pulsante sulla barra degli strumenti.  
  
-   Nella finestra dei risultati della traccia fare clic con il pulsante destro del mouse sull'intestazione di colonna che si desidera ordinare. Selezionare **Ordinamento crescente** o **Ordinamento decrescente** per ordinare le colonne rispettivamente in ordine crescente o decrescente.  
  
     In caso di raggruppamento di colonne, il relativo ordinamento comporta l'esecuzione della stessa operazione esclusivamente per i dati all'interno del gruppo.  
  
##  <a name="GroupResults"></a> Raggruppare i risultati  
  
#### <a name="to-group-the-results-by-a-single-column"></a>Per raggruppare i risultati per una sola colonna  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia.  
  
    > [!NOTE]  
    >  È anche possibile fare clic sul nome della sessione, selezionare **Controlla dati dinamici**, quindi fare clic sui **arresta Feed di dati** pulsante sulla barra degli strumenti eventi estesi.  
  
2.  Nella finestra dei risultati della traccia, fare doppio clic su intestazione di colonna si desidera raggruppare e quindi fare clic su **Raggruppa per questa colonna**.  
  
#### <a name="to-group-the-results-by-multiple-columns"></a>Per raggruppare i risultati per più colonne  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia.  
  
    > [!NOTE]  
    >  È anche possibile fare clic sul nome della sessione, selezionare **Controlla dati dinamici**, quindi fare clic sui **arresta Feed di dati** pulsante sulla barra degli strumenti.  
  
2.  Fare clic sul pulsante **Raggruppamento** sulla barra degli strumenti Eventi estesi.  
  
3.  Nella casella **Colonne disponibili** della finestra di dialogo **Raggruppamento** selezionare le colonne che si desidera raggruppare, quindi fare clic sul pulsante della freccia DESTRA.  
  
     Per modificare l'ordine di raggruppamento, nella sezione **Colonne raggruppate per** fare clic sulle frecce SU o GIÙ.  
  
     Per rimuovere colonne dal raggruppamento, nella casella **Colonne raggruppate per** selezionare le colonne che si desidera rimuovere, quindi fare clic sulla freccia a sinistra.  
  
4.  Fare clic su **OK**.  
  
##  <a name="AggregateResults"></a> Aggregare i risultati  
 Eventi estesi supporta cinque funzioni di aggregazione:  
  
-   Sum  
  
-   Min  
  
-   Max  
  
-   Media  
  
-   Count  
  
 Sum, Min, Max e Average possono essere utilizzate solo con le colonne numeriche disponibili. Count è il numero di valori non Null esistente per la colonna selezionata nel gruppo.  
  
#### <a name="to-aggregate-results"></a>Per aggregare i risultati  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia.  
  
    > [!NOTE]  
    >  È anche possibile fare clic sul nome della sessione, selezionare **Controlla dati dinamici**, quindi fare clic sui **arresta Feed di dati** pulsante sulla barra degli strumenti.  
  
    > [!NOTE]  
    >  L'aggregazione viene eseguita su un gruppo, pertanto è necessario raggruppare i risultati prima di effettuare l'aggregazione.  
  
2.  Fare clic sul pulsante **Aggregazione** sulla barra degli strumenti Eventi estesi.  
  
     Verrà visualizzata la finestra di dialogo **Aggregazione** in cui vengono mostrate le colonne disponibili per l'aggregazione.  
  
3.  Sotto **tipo di aggregazione**, selezionare in che modo si desidera aggregare la colonna corrispondente nell'elenco a discesa.  
  
4.  Nel **Ordina aggregazione per** , selezionare la colonna che si desidera ordinare in base dall'elenco a discesa.  
  
5.  Selezionare l'opzione **In ordine crescente** per ordinare il risultato dell'aggregazione in ordine crescente.  
  
6.  Selezionare l'opzione **In ordine decrescente** per ordinare il risultato dell'aggregazione in ordine decrescente.  
  
7.  Fare clic su **OK**.  
  
##  <a name="Filter"></a> Filtrare i risultati  
 È possibile applicare filtri per limitare i risultati della traccia visualizzati nella finestra di traccia. Nel filtro di visualizzazione sono inclusi un filtro temporale e un filtro avanzato. È possibile utilizzare il filtro temporale per filtrare i risultati della traccia in base al timestamp dell'evento e il filtro avanzato per costruire condizioni di filtro utilizzando i campi e le azioni dell'evento. Esiste una relazione AND logica tra i filtri temporale e avanzato.  
  
#### <a name="to-create-a-filter"></a>Per creare un filtro  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia.  
  
    > [!NOTE]  
    >  È possibile anche con il pulsante destro fare clic sul nome della sessione e quindi selezionare **Controlla dati dinamici**.  
  
2.  Nella finestra dei risultati della traccia selezionare i risultati che si desidera filtrare, quindi nella barra degli strumenti Eventi estesi fare clic sul pulsante **Filtri** .  
  
3.  Nella finestra di dialogo **Filtri** selezionare **Imposta filtro temporale** per impostare il filtro temporale trascinando le barre del dispositivo di scorrimento per impostare la sequenza temporale. Si noti che quando si spostano le barre del dispositivo di scorrimento, il valore dell'ora nell'apposita casella cambia di conseguenza. È possibile immettere l'ora anche nelle caselle dell'ora o selezionarla dall'elenco a discesa. Si noti che quando si immette l'ora, il dispositivo di scorrimento tempo a sinistra si sposterà di conseguenza.  
  
4.  Nella sezione **Filtri aggiuntivi** applicare i criteri di filtro, quindi fare clic su **Applica**. Una volta completata la creazione del filtro, fare clic su **OK**.  
  
 Una situazione speciale si crea quando un campo relativo all'evento ha lo stesso nome di un'azione. Un esempio potrebbe essere session_id. Ci sono diversi eventi che includono il campo session_id ed è anche possibile aggiungere l'azione session_id. Entrambe le informazioni vengono raccolte, ma la griglia di visualizzazione del profiler di Eventi estesi utilizza la logica indicata di seguito.  
  
-   Solo una copia della colonna (session_id in questo caso) viene mostrata nella visualizzazione della griglia.  
  
-   Se i campi e l'azione esistono nei dati, viene mostrato il valore del campo.  
  
-   Se nei dati è presente solo il campo o l'azione, viene visualizzato il campo o l'azione.  
  
-   Se non è presente né l'azione né il campo, viene visualizzato NULL.  
  
##  <a name="Search"></a> Cercare il testo nelle colonne  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia.  
  
    > [!NOTE]  
    >  È possibile anche con il pulsante destro fare clic sul nome della sessione e quindi selezionare **Controlla dati dinamici**.  
  
2.  Fare clic sul pulsante **Trova** sulla barra degli strumenti Eventi estesi.  
  
3.  Nella casella **Trova** della finestra di dialogo **Trova in eventi estesi** immettere il testo che si desidera cercare.  
  
     È possibile selezionare una delle ultime 20 stringhe di ricerca nell'elenco a discesa.  
  
4.  Nel **Cerca in** selezionare il percorso in cui cercare il testo specificato nell'elenco a discesa. Per la ricerca, utilizzare le opzioni seguenti:  
  
    -   **Colonne della tabella**. Utilizzare questa opzione per eseguire ricerche in tutte le colonne visibili nella finestra di traccia.  
  
    -   **Dettagli**. Usare questa opzione per eseguire ricerche in tutte le colonne (promosse e non promosse) nella finestra di traccia selezionate prima di aprire la **trova in eventi estesi** nella finestra di dialogo.  
  
    -   **\<Nome di colonna di evento >**. Utilizzare questa opzione per eseguire ricerche in una colonna specifica dell'evento dall'elenco a discesa.  
  
5.  Utilizzare le opzioni seguenti per specificare la modalità con cui si desidera definire la ricerca:  
  
    1.  **Maiuscole/minuscole**. Utilizzare questa opzione per visualizzare i risultati della ricerca del testo immesso nella casella **Trova** corrispondenti sia in termini di contenuto sia in termini di applicazione della distinzione tra maiuscole e minuscole.  
  
    2.  **Parola intera**. Utilizzare questa opzione per visualizzare solo i risultati della ricerca del testo immesso che corrispondono a parole intere.  
  
    3.  **Cerca in alto**. Utilizzare questa opzione per eseguire la ricerca dalla posizione del cursore fino all'inizio dei risultati.  
  
    4.  **Usa**. Utilizzare questa opzione per interpretare le espressioni regolari e i caratteri speciali immessi nella casella **Trova** . Tra i caratteri speciali sono inclusi i caratteri jolly (*) e (?) per rappresentare uno o più caratteri. Le espressioni regolari sono notazioni speciali utilizzate per definire i criteri del testo di ricerca.  
  
6.  Fare clic su **Trova successivo** per cercare il successivo testo immesso nella casella **Trova** .  
  
##  <a name="ChangeDisplay"></a> Modificare le impostazioni di visualizzazione  
 È possibile salvare le informazioni sulle colonne (ordine delle colonne, colonna di unione e larghezza delle colonne) e sul filtro di un risultato di traccia in un file di impostazioni di visualizzazione degli eventi estesi (con estensione viewsetting). Dopo aver salvato il file, è possibile applicarlo ai risultati della traccia per modificare la vista.  
  
#### <a name="to-change-the-display-settings"></a>Per modificare le impostazioni di visualizzazione  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia.  
  
    > [!NOTE]  
    >  È possibile anche con il pulsante destro fare clic sul nome della sessione e quindi selezionare **Controlla dati dinamici**.  
  
2.  Nella finestra dei risultati della traccia, dal menu o sulla barra degli strumenti degli eventi estesi scegliere **Impostazioni di visualizzazione**.  
  
3.  Selezionare una delle opzioni seguenti nell'elenco a discesa:  
  
    -   **Salva con nome**. Consente di salvare le informazioni sulle colonne e sul filtro di un risultato di traccia in un file con estensione viewsetting.  
  
    -   **Apri**. Consente di aprire un file con estensione viewsetting esistente.  
  
    -   **Apri recente**. Consente di aprire un file con estensione viewsetting salvato recentemente.  
  
  
