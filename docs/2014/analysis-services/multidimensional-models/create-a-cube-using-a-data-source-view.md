---
title: Creare un cubo tramite una vista origine dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: bec845a1-d10c-4d45-9acf-0a302adfee47
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84e134854770f0096cc99c94698cfd8d7e3e818a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66076563"
---
# <a name="create-a-cube-using-a-data-source-view"></a>Creare un cubo tramite una vista origine dati
  Utilizzare questo metodo di compilazione di un nuovo cubo se si desidera utilizzare una vista origine dati esistente. Con questo metodo, è possibile specificare la vista origine dati, nonché selezionare le tabelle dei fatti e delle dimensioni che si desidera utilizzare nella vista origine dati. Successivamente è possibile scegliere le dimensioni e le misure che si desidera includere nel cubo.  
  
 Per creare un cubo con un'origine dati, in Esplora soluzioni fare clic con il pulsante destro del mouse su **Cubi** , quindi scegliere **Nuovo cubo**. Verrà aperta la Creazione guidata cubo.  
  
## <a name="selecting-the-build-method"></a>Selezione del metodo di compilazione  
 Nella pagina **Selezione metodo di creazione** della procedura guidata fare clic su **Crea il cubo utilizzando un'origine dei dati**.  
  
 Se si seleziona la casella di controllo **Compilazione automatica** , tramite la procedura guidata vengono analizzate la vista origine dati per configurare il cubo e le relative dimensioni. La procedura guidata consente di identificare le tabelle dei fatti e delle dimensioni, di selezionare le misure da includere nel cubo, nonché di compilare le gerarchie. In ogni pagina della procedura guidata è possibile esaminare e modificare le scelte effettuate tramite tale procedura se è selezionata l'opzione **Compilazione automatica** . **In caso contrario**, tutte queste scelte devono essere effettuate manualmente.  
  
 Se si seleziona **Compilazione automatica**, è possibile fare clic su **Fine** in qualsiasi pagina della procedura guidata per passare all'ultima pagina e accettare le configurazioni predefinite per tutte le pagine restanti. Nell'ultima pagina della procedura guidata è possibile controllare la struttura del cubo prima di terminare tale procedura.  
  
 Se non si sceglie **Compilazione automatica**, è necessario selezionare manualmente le tabelle dei fatti e delle dimensioni. La procedura guidata consente di compilare tutte le dimensioni che si intende creare, tuttavia è necessario utilizzare Progettazione dimensioni per compilare manualmente le gerarchie definite dall'utente nelle dimensioni. Se sono già state create le dimensioni che si desidera utilizzare nel cubo prima di eseguire la Creazione guidata cubo, questo requisito potrebbe essere ininfluente.  
  
## <a name="selecting-the-data-source-view"></a>Selezione della vista origine dati  
 Se si utilizza un'origine dati esistente per creare un cubo, il primo passaggio consiste nella specificazione della vista origine dati su cui basare il cubo. Nella pagina **Selezione vista origine dati** della procedura guidata selezionare una vista origine dati esistente. Nel riquadro di anteprima è possibile visualizzare le tabelle in una vista origine dati selezionata. Per visualizzare lo schema per qualsiasi vista origine dati selezionata, fare clic su **Sfoglia**.  
  
 Se la vista origine dati che si desidera utilizzare non è elencata, nella Creazione guidata cubo fare clic su **Annulla**e aprire la Creazione guidata vista origine dati. È anche possibile fare clic su **Aggiungi nuovo elemento** nel menu **File** per aggiungere una vista origine dati esistente da un altro database o percorso. Per altre informazioni sulla creazione delle viste origine dati, vedere [Viste origine dati in modelli multidimensionali](data-source-views-in-multidimensional-models.md).  
  
> [!NOTE]  
>  In una vista origine dati deve essere contenuta almeno una tabella da elencare in questa pagina. Non è possibile creare un cubo basato su una vista origine dati in cui non è presente una tabella.  
  
## <a name="identify-fact-and-dimension-tables"></a>Selezione tabelle dei fatti e delle dimensioni  
 Nella Creazione guidata cubo utilizzare la pagina **Selezione tabelle dei fatti e delle dimensioni** della procedura guidata per selezionare le tabelle dei fatti e delle dimensioni necessarie per creare il cubo. Se è stata selezionata la casella di controllo **Compilazione automatica** per creare il cubo, le tabelle dei fatti o delle dimensioni rilevate dalla procedura guidata vengono selezionate alla prima visualizzazione di questa pagina. Se tramite la procedura guidata viene rilevata una tabella che è sia dei fatti sia delle dimensioni, vengono selezionate entrambe le colonne. Se viene invece rilevata una tabella che non è correlata a nessuno dei due elementi, non viene selezionata alcuna colonna. Se non è necessaria nessuna tabella per la progettazione del cubo, deselezionare le caselle di controllo **Fatti** e **Dimensioni** .  
  
 Se non è stata selezionata la casella di controllo **Compilazione automatica** , è necessario effettuare manualmente tutte le selezioni. Utilizzare la scheda **Tabelle** o **Diagramma** :  
  
-   Nella scheda **Tabelle** sono elencate le tabelle nell'apposito formato. Selezionare la casella di controllo nella colonna **Fatti** o **Diagramma** .  
  
-   Nella scheda **Diagramma** viene visualizzato lo schema della vista origine dati. Le tabelle sono codificate con colori diversi a seconda che si tratti di tabelle dei fatti o delle dimensioni. Fare clic su qualsiasi tabella nello schema, quindi su **Fatti** o **Dimensioni** per selezionare o deselezionare l'impostazione in tale tabella. Utilizzare il pulsante **Zoom** per modificare l'ingrandimento.  
  
> [!NOTE]  
>  Nella scheda **Diagramma** è possibile allargare o ingrandire al massimo la finestra della procedura guidata per visualizzare lo schema.  
  
 Se nella vista origine dati è presente una tabella delle dimensioni temporali, selezionarla nell'elenco **Tabella dimensioni temporali** . Se non vi sono, lasciare  **\<None >** selezionato. Si tratta dell'elemento predefinito dell'elenco. Se si seleziona una tabella come tabella delle dimensioni temporali, tale tabella viene selezionata anche come tabella delle dimensioni nelle schede **Tabelle** e **Diagramma** .  
  
## <a name="defining-time-periods"></a>Definizione dei periodi di tempo  
 Se durante la selezione dei tipi di tabella è stata specificata una tabella delle dimensioni temporali, utilizzare la pagina **Definizione periodi di tempo** della procedura guidata per specificare le colonne della tabella che corrispondono ai periodi di tempo standard. Cercare i periodi standard in **Nome proprietà tempo**. Per ogni riga per cui esiste una colonna corrispondente nella tabella delle dimensioni temporali, scegliere la colonna corretta in **Colonne tabella tempi**. Nella procedura guidata vengono utilizzate le associazioni specificate per creare attributi e suggerire gerarchie temporali utili per i dati. Queste associazioni consentono inoltre di impostare la proprietà **Tipo** per gli attributi corrispondenti nella nuova dimensione temporale. La procedura guidata consente di creare quindi una dimensione temporale basata su una tabella delle dimensioni temporali.  
  
 Dopo aver creato il cubo, è possibile utilizzare la Configurazione guidata funzionalità di Business Intelligence per aggiungere funzionalità avanzate di Business Intelligence per le gerarchie temporali al cubo. In tali funzionalità sono incluse viste per il calcolo dei dati di un periodo rispetto alla data corrente, di un periodo specifico o della media mobile dei dati in un periodo.  
  
## <a name="selecting-dimensions"></a>Selezione delle dimensioni  
 Utilizzare la pagina per **selezionare le dimensioni** della procedura guidata per aggiungere dimensioni esistenti al cubo. Questa pagina verrà visualizzata solo se sono già presenti dimensioni condivise che corrispondono alle tabelle delle dimensioni nel nuovo cubo.  
  
 Per aggiungere dimensioni esistenti, selezionare una o più dimensioni nell'elenco **Dimensioni condivise** e fare clic sul pulsante con la freccia a destra (**>**) per spostarle nell'elenco **Dimensioni cubo** . Fare clic sul pulsante con la doppia freccia (**>>**) per spostare tutte le dimensioni nell'elenco.  
  
 Se una dimensione esistente non viene visualizzata nell'elenco come previsto, è possibile fare clic su **Indietro** e modificare le impostazioni del tipo di tabella per una o più tabelle. Una dimensione esistente deve essere anche correlata ad almeno una delle tabelle dei fatti del cubo per poter essere visualizzata nell'elenco **Dimensioni condivise** .  
  
## <a name="selecting-measures"></a>Selezione di misure  
 Utilizzare la pagina **Selezione misure** della procedura guidata per selezionare le misure che si desidera includere nel cubo. Ogni tabella contrassegnata come tabella dei fatti viene visualizzata come gruppo di misure in questo elenco e ogni colonna non chiave numerica viene visualizzata come una misura dell'elenco. Per impostazione predefinita vengono selezionate tutte le misure in ogni gruppo di misure. È possibile deselezionare la casella di controllo accanto alle misure che non si desidera includere nel cubo. Per rimuovere tutte le misure di un relativo gruppo dal cubo, deselezionare la casella di controllo **Gruppi di misure/Misure** .  
  
 I nomi di misure elencati in **Gruppi di misure/Misure** riflettono i nomi delle colonne. È possibile fare clic sulla cella contenente un nome per modificarlo.  
  
 Per visualizzare i dati per una misura, fare clic con il pulsante destro del mouse su una qualsiasi delle righe della misura nell'elenco, quindi scegliere **Visualizza dati di esempio**. In questo modo verrà aperto **Visualizzatore dati di esempio** e verranno visualizzati i primi 1000 record della tabella dei fatti corrispondenti.  
  
## <a name="reviewing-new-dimensions"></a>Verifica delle nuove dimensioni  
 Utilizzare la pagina **Verifica nuove dimensioni** della procedura guidata per verificare le strutture delle dimensioni create da tale procedura. Le dimensioni sono elencate nella visualizzazione albero **Dimensioni nuove** di questa pagina della procedura guidata e possono essere verificate nei modi seguenti:  
  
-   Espandere una qualsiasi dimensione per verificare i relativi attributi e gerarchie.  
  
-   Espandere la cartella **Attributi** di una qualsiasi dimensione per visualizzare gli attributi nella dimensione.  
  
-   Espandere la cartella **Gerarchia** di una qualsiasi dimensione per visualizzare le gerarchie nella dimensione.  
  
-   Espandere una qualsiasi gerarchia per visualizzare i relativi livelli.  
  
> [!NOTE]  
>  È possibile allargare o ingrandire al massimo la finestra della procedura guidata per una visualizzazione migliore dell'albero.  
  
 Per rimuovere un qualsiasi oggetto nell'albero dal cubo, deselezionare la casella di controllo accanto a tale oggetto. La deselezione rimuove anche tutti gli oggetti sotto l'oggetto. Le dipendenze tra oggetti sono imposte, pertanto se si rimuove un attributo, vengono rimossi anche i livelli di gerarchia che dipendono dall'attributo. Ad esempio, deselezionando una casella di controllo accanto a una gerarchia vengono deselezionate le caselle di controllo accanto a tutti i livelli nella gerarchia e vengono rimossi sia i livelli sia le gerarchie. Non è possibile rimuovere l'attributo chiave per una dimensione.  
  
 È possibile rinominare qualsiasi dimensione, attributo, gerarchia o livello facendo clic il nome oppure facendo clic con il nome e quindi sul menu di scelta rapida facendo clic **rinominare \<oggetto >**, dove  **\< Oggetto >** viene **dimensione**, **attributo**, oppure **livello**.  
  
 Non esiste necessariamente una relazione uno-a-uno tra il numero di tabelle delle dimensioni definito nella pagina **Selezione tabelle dei fatti e delle dimensioni** della procedura guidata e il numero di dimensioni elencate in questa pagina. A seconda delle relazioni tra tabelle nella vista origine dati, nella procedura guidata possono essere utilizzate due o più tabelle per compilare una dimensione, ad esempio come richiesto da uno schema snowflake.  
  
## <a name="completing-the-cube-wizard"></a>Completamento della Creazione guidata cubo  
 Nella pagina **Completamento procedura guidata** della procedura guidata è possibile visualizzare i gruppi di misure, le misure e le dimensioni nel nuovo cubo. Nella casella **Nome cubo** digitare un nome per il cubo. Successivamente, se il cubo creato soddisfa le proprie esigenze, fare clic su **Fine**. Fare clic su **Indietro** per tornare a una pagina precedente della procedura guidata e apportare modifiche.  
  
  
