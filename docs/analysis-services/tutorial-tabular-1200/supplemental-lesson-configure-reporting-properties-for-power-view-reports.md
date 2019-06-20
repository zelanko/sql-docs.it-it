---
title: Configurare le proprietà di creazione di report per i report Power View | Microsoft Docs
ms.date: 05/07/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3ee35ac833a1170a688bb9439ed4dd8f6b6d6716
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65403373"
---
# <a name="supplemental-lesson---configure-reporting-properties-for-power-view-reports"></a>Supplementare lezione - configurare le proprietà di creazione di report per i report Power View
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

In questa lezione supplementare si imposteranno le proprietà per il progetto AW Internet Sales dei report. Proprietà di Reporting rendono più semplice per gli utenti di selezionare e visualizzare i dati del modello in Power View. Si imposteranno inoltre le proprietà per nascondere alcune colonne e tabelle, nonché per creare nuovi dati da utilizzare nei grafici.   
  
Tempo stimato per il completamento della lezione: **30 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
Questa lezione supplementare fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività di questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti.  
Per completare questa lezione supplementare specifica, è necessario disporre anche degli elementi seguenti:  
  
-   Il progetto AW Internet Sales (completato con questa esercitazione) pronto per essere distribuito o già distribuito in un server Analysis Services.  
  
  
## <a name="model-properties-that-affect-reporting"></a>Proprietà del modello che influiscono sulla creazione di report  
Quando si crea un modello tabulare, esistono alcune proprietà che è possibile impostare su singole colonne e tabelle per migliorare l'utente di creazione di report in Power View. Inoltre, è possibile creare ulteriori dati del modello per supportare la visualizzazione dei dati e altre funzionalità specifiche del client di creazione report. Di seguito sono riportate alcune delle modifiche che verranno apportate all'esempio Adventure Works Internet Sales Model:  
  
-   **Aggiungere nuovi dati** -aggiunta di nuovi dati in una colonna calcolata con una formula DAX create informazioni sulla data in un formato che è più facile da visualizzare nei grafici.  
  
-   **Nascondere tabelle e colonne inutili per l'utente finale** : con la proprietà **Hidden** è possibile controllare se le tabelle e le relative colonne sono visualizzate nel client di creazione del report. Gli elementi nascosti fanno comunque parte del modello e rimangono disponibili per le query e i calcoli.  
  
-   **Abilitare tabelle con un clic** -per impostazione predefinita, viene eseguita alcuna azione se un utente fa clic su una tabella nell'elenco dei campi. Per modificare questo comportamento in modo che facendo clic su una tabella, questa venga aggiunta al report, è necessario impostare la proprietà Set di campi predefiniti per ogni colonna che si desidera includere nella tabella. Questa proprietà viene impostata nelle colonne della tabella che sarà utilizzata maggiormente dagli utenti finali.  
  
-   **Impostare raggruppamenti ove necessario** : con la proprietà **Keep Unique Rows** è possibile determinare se i valori nella colonna debbano essere raggruppati in base ai valori in un campo diverso, ad esempio un campo dell'identificatore. Per le colonne contenenti valori duplicati, ad esempio nome del cliente (ad esempio, più clienti chiamati John Smith), è importante effettuare raggruppamenti (mantenere righe univoche) nel **identificatore di riga** , in modo da offrire agli utenti finali di risultati corretti.  
  
-   **Impostare tipi e formati di dati** : per impostazione predefinita, in Power View le regole vengono applicate in base al tipo di dati della colonna per determinare se il campo può essere usato come misura. Poiché ogni visualizzazione dati in Power View ha anche regole su cui è possibile inserire misure e non misure, è importante impostare il tipo di dati nel modello oppure sostituire l'impostazione predefinita, per ottenere il comportamento desiderato per l'utente.  
  
-   **Impostare l'ordinamento per colonna** proprietà - i **Ordina per colonna** proprietà specifica se i valori nella colonna devono essere ordinati dai valori in un campo diverso. Ad esempio, nella colonna Month Calendar contenente il nome del mese, effettuare l'ordinamento in base alla colonna Month Number.  
  
## <a name="hide-tables-from-client-tools"></a>Nascondere le tabelle negli strumenti client  
Poiché nella tabella Product sono già presenti le colonne calcolate Product Category e Product Subcategory, non è necessario che le tabelle Product Category e Product Subcategory siano visibili nelle applicazioni client.  
  
#### <a name="to-hide-the-product-category-and-product-subcategory-tables"></a>Per nascondere le tabelle Product Category e Product Subcategory  
  
1.  In Progettazione modelli fare clic con il pulsante destro del mouse sulla tabella (scheda) **Product Category** e scegliere **Nascondi a strumenti client**.  
  
2.  Fare clic con il pulsante destro del mouse sulla tabella (scheda) **Product Subcategory** e scegliere **Nascondi a strumenti client**.  
  
## <a name="create-new-data-for-charts"></a>Creare nuovi dati per i grafici  
Talvolta potrebbe essere necessario creare nuovi dati nel modello utilizzando le formule DAX. In questa attività si aggiungeranno due nuove colonne calcolate alla tabella Date. In queste colonne saranno disponibili campi di data con un formato pratico per l'utilizzo nei grafici.  
  
#### <a name="to-create-new-data-for-charts"></a>Per creare nuovi dati per i grafici  
  
1.  Scorrere la tabella **Date** fino all'estrema destra e fare clic su **Aggiungi colonna**.  
  
2.  Aggiungere due nuove colonne calcolate utilizzando le seguenti formule presenti nell'apposita barra:  
  
    |Nome colonna|Formula|  
    |---------------|-----------|  
    |Year Quarter|=[Calendar Year] & " Q" & [Calendar Quarter]|  
    |Year Month|=[Calendar Year] & FORMAT([Month],"#00")|  
  
## <a name="default-field-set"></a>Set di campi predefiniti  
Set di campi predefiniti è un elenco predefinito di colonne e misure per una tabella che vengono aggiunti automaticamente a un'area di disegno report quando la tabella viene fatto clic su nell'elenco di campi del report. Essenzialmente, è possibile specificare le colonne, le misure e l'ordinamento dei campi predefiniti che gli utenti desiderano visualizzare quando questa tabella viene mostrata nei report Power View.  Per il modello Internet Sales verranno definiti un set di campi predefiniti e l'ordine delle tabelle Customer, Geography e Product. Sono incluse solo le colonne più comuni che gli utenti desiderano visualizzare durante l'analisi dei dati del modello Adventure Works Internet Sales utilizzando i report Power View.  
  
Per informazioni dettagliate sui Set di campi predefiniti, vedere [configurare Set di campi predefiniti per i report Power View](../tabular-models/power-view-configure-default-field-set-for-reports.md).  
  
#### <a name="to-set-default-field-set-for-tables"></a>Per impostare la finestra di dialogo Set di campi predefiniti per le tabelle  
  
1.  In Progettazione modelli fare clic sulla tabella (scheda) **Customer** .  
  
2.  Nella finestra **Proprietà** , alla voce **Proprietà report**della proprietà **Default Field Set** fare clic su **Fare clic per modificare** per aprire la finestra di dialogo **Set di campi predefiniti** .  
  
3.  Nell'elenco **Campi nella tabella** della finestra di dialogo **Set di campi predefiniti** premere CTRL, selezionare i campi seguenti e fare clic su **Aggiungi**.  
  
    **Data di nascita**, **Customer ID alternativo**, **First Name**, **cognome**.  
  
4.  Nella finestra **Campi predefiniti, nell'ordine** usare i pulsanti Sposta su e Sposta giù per applicare l'ordine seguente:  
  
    **Customer ID alternativo**  
  
    **First Name**  
  
    **Last Name**  
  
    **Birth Date**.  
  
5.  Fare clic su **OK** per chiudere la finestra di dialogo **Set di campi predefiniti** per la tabella **Customer** .  
  
6.  Seguire la stessa procedura per la tabella **Geography** , selezionando i campi seguenti e mettendoli in questo ordine.  
  
    **City**, **State Province Code**, **Country Region Code**.  
  
7.  Infine, seguire la stessa procedura per la tabella **Product** , selezionando i campi seguenti e mettendoli in questo ordine.  
  
    **Product Alternate ID**, **il nome del prodotto**.  
  
## <a name="table-behavior"></a>Comportamento tabella  
Utilizzando le proprietà Comportamento tabella è possibile modificare il comportamento della tabella per diversi tipi di visualizzazioni e comportamenti di raggruppamento per le tabelle utilizzate nei report Power View. In questo modo viene fornita una posizione predefinita migliore per le informazioni di identificazione quali nomi, immagini o titoli nei layout di sezioni, schede e grafici.  
  
Per informazioni dettagliate sulle proprietà comportamento tabella, vedere [configurare le proprietà di comportamento tabella per i report Power View](../tabular-models/power-view-configure-table-behavior-properties-for-reports.md).  
  
#### <a name="to-set-table-behavior"></a>Per impostare il comportamento delle tabelle 
  
1.  In Progettazione modelli fare clic sulla tabella (scheda) **Customer** .  
  
2.  Nella proprietà **Table Behavior** della finestra **Proprietà** selezionare **Fare clic per modificare**per aprire la finestra di dialogo **Comportamento tabella** .  
  
3.  Nel **comportamento tabella** nella finestra di dialogo il **identificatore di riga** casella di riepilogo a discesa, seleziona il **ID cliente** colonna.  
  
4.  Nell'elenco **Mantieni righe univoche** selezionare **Name** e **Last Name**.  
  
    Con questa impostazione di proprietà si specifica che in queste colonne sono disponibili valori che devono essere considerati come univoci anche se duplicati, ad esempio quando due o più dipendenti hanno lo stesso nome.  
  
5.  Nell'elenco a discesa **Etichetta predefinita** selezionare la colonna **Last Name** .  
  
    Con questa impostazione di proprietà si specifica che in questa colonna è disponibile un nome visualizzato per rappresentare i dati della riga.  
  
6.  Ripetere questi passaggi per il **geografia** di tabella, selezionando il **Geography ID** come identificatore di riga e il **City** colonna nel **Mantieni righe univoche**  casella di riepilogo. Non è necessario impostare un'etichetta predefinita per questa tabella.  
  
7.  Ripetere questi passaggi per la **prodotto** di tabella, selezionando il **ID prodotto** come identificatore di riga e il **Product Name** colonna il **mantenere univoco Righe** casella di riepilogo. Per la **etichetta predefinita**, selezionare **Product Alternate ID**.  
  
## <a name="reporting-properties-for-columns"></a>Proprietà report per le colonne  
Per migliorare la creazione di report del modello è possibile impostare diverse proprietà relative alle colonne di base e alla creazione di report specifici. Ad esempio, gli utenti potrebbero non voler visualizzare tutte le colonne in ogni tabella. Proprio come le tabelle Product Category e Product Subcategory è stata nascosta in precedenza, tramite proprietà Hidden di una colonna, è possibile nascondere colonne particolari di una tabella che viene visualizzato in caso contrario. Altre proprietà, ad esempio Formato dati e Ordina per colonna, possono influire anche sulla modalità di visualizzazione dei dati delle colonne nei report. Nell'esempio, alcune di esse vengono impostate in colonne particolari. Le altre colonne per cui non è richiesta alcuna azione non vengono mostrate di seguito.  
  
In questo esempio vengono impostate solo alcune delle diverse proprietà di colonne. Per altre informazioni sulla colonna proprietà report, vedere [le proprietà delle colonne](../tabular-models/column-properties-ssas-tabular.md).  
  
#### <a name="to-set-properties-for-columns"></a>Per impostare le proprietà per le colonne  
  
1.  In Progettazione modelli fare clic sulla tabella (scheda) **Customer** .  
  
2.  Fare clic sul **ID cliente** per visualizzare le proprietà della colonna nella colonna il **proprietà** finestra.  
  
3.  Nella finestra **Proprietà** impostare la proprietà **Hidden** su True. Il **Customer ID** colonna quindi disattivata in Progettazione modelli.  
  
4.  Ripetere questi passaggi, impostando le seguenti proprietà di colonna e di creazione report per ogni tabella specificata. Per tutte le altre proprietà mantenere le impostazioni predefinite.  
  
    Nota: Per tutte le colonne di date, assicurarsi che **tipo di dati** viene **data**.  
  
    **Customer**  
  
    |colonna|Proprietà|Value|  
    |----------|------------|---------|  
    |ID geografico|Hidden|True|  
    |Birth Date|Formato dati|Short Date|  
  
    **Data**  
  
    > [!NOTE]  
    > Poiché la tabella Date è stata selezionata come tabella data dei modelli, usando il contrassegno come impostazioni tabella data, nella lezione 7: Contrassegna come tabella data, la colonna Date nella tabella Date come colonna da utilizzare come identificatore univoco, la proprietà identificatore di riga per la colonna Date verrà automaticamente impostata su True e non può essere modificato. Quando si utilizzano funzioni di Business Intelligence per le gerarchie temporali nelle formule DAX, è necessario specificare una tabella relativa alla data. In questo modello sono state create diverse misure utilizzando funzioni di Business Intelligence per le gerarchie temporali per calcolare i dati di vendita per diversi periodi, ad esempio i trimestri precedente e corrente, nonché per essere utilizzati negli indicatori KPI. Per altre informazioni su come specificare una tabella data, vedere [specificare contrassegna come tabella data per l'uso con Intelligence tempo](../tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md).  
  
    |colonna|Proprietà|Value|  
    |----------|------------|---------|  
    |Date|Formato dati|Short Date|  
    |Day Number of Week|Hidden|True|  
    |Day Name|Sort By Column|Day Number of Week|  
    |Day of Week|Hidden|True|  
    |Day of Month|Hidden|True|  
    |Day of Year|Hidden|True|  
    |Month Name|Sort By Column|Month|  
    |Month|Hidden|True|  
    |Month Calendar|Hidden|True|  
    |Fiscal Quarter|Hidden|True|  
    |Fiscal Year|Hidden|True|  
    |Fiscal Semester|Hidden|True|  
  
    **Geography**  
  
    |colonna|Proprietà|Value|  
    |----------|------------|---------|  
    |ID geografico|Hidden|True|  
    |ID territorio vendita|Hidden|True|  
  
    **Product**  
  
    |colonna|Proprietà|Value|  
    |----------|------------|---------|  
    |ID prodotto|Hidden|True|  
    |Product Alternate ID|Etichetta predefinita|True|  
    |ID di sottocategoria di prodotto|Hidden|True|  
    |Product Start Date|Formato dati|Short Date|  
    |Product End Date|Formato dati|Short Date|  
  
    **Internet Sales**  
  
    |colonna|Proprietà|Value|  
    |----------|------------|---------|  
    |ID prodotto|Hidden|True|  
    |ID cliente|Hidden|True|  
    |ID di innalzamento di livello|Hidden|True|  
    |ID di tipo valuta|Hidden|True|  
    |ID territorio vendita|Hidden|True|  
    |Order Quantity|tipo di dati<br /><br />Formato dati<br /><br />Cifre decimali|Decimal Number<br /><br />Numero decimale<br /><br />0|  
    |Order Date|Formato dati|Short Date|  
    |Due Date|Formato dati|Short Date|  
    |Ship Date|Formato dati|Short Date|  
  
## <a name="redeploy-the-adventure-works-internet-sales-tabular-model"></a>Ridistribuire il modello tabulare Adventure Works Internet Sales  
Poiché il modello è stato modificato, è necessario ridistribuirlo.  
  
#### <a name="to-redeploy-the-adventure-works-internet-sales-tabular-model"></a>Per ridistribuire il modello tabulare Adventure Works Internet Sales  
  
-   In SSDT scegliere il **compilare** menu e quindi fare clic su **Distribuisci Adventure Works Internet Sales Model**.  
  
    Si aprirà la finestra di dialogo **Distribuisci** in cui sono indicati lo stato della distribuzione dei metadati e ogni tabella inclusa nel modello.  
  
## <a name="next-steps"></a>Passaggi successivi  
È ora possibile usare Excel per visualizzare i dati del modello. Assicurarsi che agli account di Analysis Services e Reporting Services nel sito di SharePoint siano associate le autorizzazioni di lettura per l'istanza di Analysis Services in cui è stato distribuito il modello.  
  
  
  
  
