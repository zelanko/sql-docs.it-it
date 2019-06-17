---
title: Configurare le proprietà di creazione di report per i report Power View | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0ffc5f44-17d3-42d4-bc2c-baf3b4485e2d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 812c205c1e612604c0c39a5effb3b9da50308d7a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067955"
---
# <a name="configure-reporting-properties-for-power-view-reports"></a>Configurare le proprietà di creazione di report per i report Power View
  In questa lezione supplementare si imposteranno le proprietà dei report per il progetto Adventure Works Internet Sales Model. Con le proprietà dei report risulta più semplice, per gli utenti finali, selezionare e visualizzare i dati del modello in Power View. Si imposteranno inoltre le proprietà per nascondere alcune colonne e tabelle, nonché per creare nuovi dati da utilizzare nei grafici.  
  
 Dopo aver completato questa lezione e ridistribuito il modello in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] integrata con SharePoint e [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], è possibile creare un'origine dati, specificare le informazioni sulla connessione dati, avviare Power View e progettare report in base al modello.  
  
 In questa lezione non si illustra come creare e utilizzare i report Power View, bensì viene fornita agli autori del modello tabulare un'introduzione alle proprietà e alle impostazioni che influiscono sulla modalità di visualizzazione dei dati del modello in Power View. Per altre informazioni sulla creazione di report di Power View, vedere [esercitazione: Creare un Report di esempio in Power View](https://go.microsoft.com/fwlink/?LinkId=221204).  
  
 Tempo stimato per il completamento della lezione: **30 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questa lezione supplementare fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività di questa lezione supplementare, è necessario avere completato tutte le lezioni precedenti.  
  
 Per completare questa lezione supplementare specifica, è necessario disporre anche degli elementi seguenti:  
  
-   Il modello Adventure Works Internet Sales (completato con questa esercitazione) pronto per essere distribuito o già distribuito in un'istanza di Analysis Services in esecuzione in modalità tabulare.  
  
-   Un sito di SharePoint integrato con [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] in esecuzione in modalità tabulare e [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)], configurato per supportare i report Power View.  
  
-   È necessario disporre di autorizzazioni sufficienti per creare una connessione dati nel sito di SharePoint che punta al modello Adventure Works Internet Sales.  
  
## <a name="model-properties-that-affect-reporting"></a>Proprietà del modello che influiscono sulla creazione di report  
 Quando si crea un modello tabulare, è possibile impostare alcune proprietà in singole colonne e tabelle per migliorare la creazione di report in Power View da parte dell'utente finale. Inoltre, è possibile creare ulteriori dati del modello per supportare la visualizzazione dei dati e altre funzionalità specifiche del client di creazione report. Di seguito sono riportate alcune delle modifiche che verranno apportate all'esempio Adventure Works Internet Sales Model:  
  
-   **Aggiungere nuovi dati** -aggiunta di nuovi dati in una colonna calcolata con una formula DAX create informazioni sulla data in un formato che è più facile da visualizzare nei grafici.  
  
-   **Nascondere tabelle e colonne inutili per l'utente finale** : con la proprietà **Hidden** è possibile controllare se le tabelle e le relative colonne sono visualizzate nel client di creazione del report. Gli elementi nascosti fanno comunque parte del modello e rimangono disponibili per le query e i calcoli.  
  
-   **Abilitare tabelle con un clic** -per impostazione predefinita, viene eseguita alcuna azione se un utente finale fa clic su una tabella nell'elenco dei campi. Per modificare questo comportamento in modo che facendo clic su una tabella, questa venga aggiunta al report, è necessario impostare la proprietà Set di campi predefiniti per ogni colonna che si desidera includere nella tabella. Questa proprietà viene impostata nelle colonne della tabella che sarà utilizzata maggiormente dagli utenti finali.  
  
-   **Impostare raggruppamenti ove necessario** : con la proprietà **Keep Unique Rows** è possibile determinare se i valori nella colonna debbano essere raggruppati in base ai valori in un campo diverso, ad esempio un campo dell'identificatore. Per le colonne contenenti valori duplicati, ad esempio la colonna con il nome del cliente, in cui possono essere presenti più clienti di nome Diego Sages, è importante raggruppare i dati, mantenendo righe univoche, nel campo **Identificatore di riga** per offrire agli utenti finali i risultati corretti.  
  
-   **Impostare tipi e formati di dati** : per impostazione predefinita, in Power View le regole vengono applicate in base al tipo di dati della colonna per determinare se il campo può essere usato come misura. Poiché a ogni visualizzazione dei dati in Power View sono anche applicate regole relative al posizionamento di misure e non misure, è importante impostare il tipo di dati nel modello oppure sostituire l'impostazione predefinita per ottenere il comportamento voluto per l'utente finale.  
  
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
    |-----------------|-------------|  
    |Year Quarter|=[Calendar Year] & " Q" & [Calendar Quarter]|  
    |Year Month|=[Calendar Year] & FORMAT([Month],"#00")|  
  
## <a name="default-field-set"></a>Set di campi predefiniti  
 Set di campi predefiniti è un elenco predefinito di colonne e misure per una tabella che vengono aggiunte automaticamente all'area di disegno di un report Power View quando si seleziona la tabella nell'elenco di campi del report. Essenzialmente, è possibile specificare le colonne, le misure e l'ordinamento dei campi predefiniti che gli utenti desiderano visualizzare quando questa tabella viene mostrata nei report Power View.  Per il modello Internet Sales verranno definiti un set di campi predefiniti e l'ordine delle tabelle Customer, Geography e Product. Sono incluse solo le colonne più comuni che gli utenti desiderano visualizzare durante l'analisi dei dati del modello Adventure Works Internet Sales utilizzando i report Power View.  
  
 Per informazioni dettagliate su Set di campi predefiniti, vedere [Configurare il set di campi predefiniti per i report Power View &#40;SSAS tabulare&#41;](tabular-models/power-view-configure-default-field-set-for-reports.md) nella documentazione online di SQL Server.  
  
#### <a name="to-set-default-field-set-for-tables"></a>Per impostare la finestra di dialogo Set di campi predefiniti per le tabelle  
  
1.  In Progettazione modelli fare clic sulla tabella (scheda) **Customer**.  
  
2.  Nella finestra **Proprietà** , alla voce **Proprietà report**della proprietà **Default Field Set** fare clic su **Fare clic per modificare** per aprire la finestra di dialogo **Set di campi predefiniti** .  
  
3.  Nell'elenco **Campi nella tabella** della finestra di dialogo **Set di campi predefiniti** premere CTRL, selezionare i campi seguenti e fare clic su **Aggiungi**.  
  
     **Birth Date**, **Customer Alternate Id**, **First Name**, **Last Name**.  
  
4.  Nella finestra **Campi predefiniti, nell'ordine** usare i pulsanti Sposta su e Sposta giù per applicare l'ordine seguente:  
  
     **Customer Alternate Id**  
  
     **First Name**  
  
     **Last Name**  
  
     **Birth Date**.  
  
5.  Fare clic su **OK** per chiudere la finestra di dialogo **Set di campi predefiniti** per la tabella **Customer** .  
  
6.  Seguire la stessa procedura per la tabella **Geography** , selezionando i campi seguenti e mettendoli in questo ordine.  
  
     **Città**, **State Province Code**, **stato indicativo di paese**.  
  
7.  Infine, seguire la stessa procedura per la tabella **Product** , selezionando i campi seguenti e mettendoli in questo ordine.  
  
     **Product Alternate Id**, **Product Name**.  
  
## <a name="table-behavior"></a>Comportamento tabella  
 Utilizzando le proprietà Comportamento tabella è possibile modificare il comportamento della tabella per diversi tipi di visualizzazioni e comportamenti di raggruppamento per le tabelle utilizzate nei report Power View. In questo modo viene fornita una posizione predefinita migliore per le informazioni di identificazione quali nomi, immagini o titoli nei layout di sezioni, schede e grafici.  
  
 Per informazioni dettagliate sull'impostazione delle proprietà che determinano il comportamento della tabella, vedere [Configurare le proprietà Comportamento tabella per i report Power View &#40;SSAS tabulare&#41;](tabular-models/power-view-configure-table-behavior-properties-for-reports.md) nella documentazione online di SQL Server.  
  
#### <a name="to-set-table-behavior-for-tables"></a>Per impostare la finestra di dialogo Comportamento tabella per le tabelle  
  
1.  In Progettazione modelli fare clic sulla tabella (scheda) **Customer** .  
  
2.  Nella proprietà **Table Behavior** della finestra **Proprietà** selezionare **Fare clic per modificare**per aprire la finestra di dialogo **Comportamento tabella** .  
  
3.  Nell'elenco a discesa **Identificatore di riga** della finestra di dialogo **Comportamento tabella** selezionare la colonna **Customer Id** .  
  
4.  Nell'elenco **Mantieni righe univoche** selezionare **Name** e **Last Name**.  
  
     Con questa impostazione di proprietà si specifica che in queste colonne sono disponibili valori che devono essere considerati come univoci anche se duplicati, ad esempio quando due o più dipendenti hanno lo stesso nome.  
  
5.  Nell'elenco a discesa **Etichetta predefinita** selezionare la colonna **Last Name** .  
  
     Con questa impostazione di proprietà si specifica che in questa colonna è disponibile un nome visualizzato per rappresentare i dati della riga.  
  
6.  Ripetere questi passaggi per la tabella **Geography** selezionando la colonna **Geography Id** come identificatore di riga e la colonna **City** dall'elenco **Mantieni righe univoche** . Non è necessario impostare un'etichetta predefinita per questa tabella.  
  
7.  Ripetere questi passaggi per la tabella **Product** , selezionando la colonna **Product Id** come identificatore di riga e la colonna **Product Name** dall'elenco **Mantieni righe univoche** . Per **Etichetta predefinita**selezionare **Product Alternate Id**.  
  
## <a name="reporting-properties-for-columns"></a>Proprietà report per le colonne  
 Per migliorare la creazione di report del modello è possibile impostare diverse proprietà relative alle colonne di base e alla creazione di report specifici. Ad esempio, gli utenti potrebbero non voler visualizzare tutte le colonne in ogni tabella. Proprio come le tabelle Product Category e Product Subcategory è stata nascosta in precedenza, tramite proprietà Hidden di una colonna, è possibile nascondere colonne particolari di una tabella che viene visualizzato in caso contrario. Altre proprietà, ad esempio Formato dati e Ordina per colonna, possono influire anche sulla modalità di visualizzazione dei dati delle colonne nei report. Nell'esempio, alcune di esse vengono impostate in colonne particolari. Le altre colonne per cui non è richiesta alcuna azione non vengono mostrate di seguito.  
  
 In questo esempio vengono impostate solo alcune delle diverse proprietà di colonne. Per altre informazioni dettagliate sulle proprietà di creazione di report relativi alle colonne, vedere [Scheda Proprietà colonne &#40;SSAS tabulare&#41;](tabular-models/properties-ssas-tabular.md) nella documentazione online di SQL Server.  
  
#### <a name="to-set-properties-for-columns"></a>Per impostare le proprietà per le colonne  
  
1.  In Progettazione modelli fare clic sulla tabella (scheda) **Customer** .  
  
2.  Fare clic sulla colonna **Customer Id** per visualizzare le proprietà della colonna nella finestra **Proprietà** .  
  
3.  Nella finestra **Proprietà** impostare la proprietà **Hidden** su True. La colonna **Customer Id** viene disattivata in Progettazione modelli.  
  
4.  Ripetere questi passaggi, impostando le seguenti proprietà di colonna e di creazione report per ogni tabella specificata. Per tutte le altre proprietà mantenere le impostazioni predefinite.  
  
     **Customer**  
  
    |colonna|Proprietà|Value|  
    |------------|--------------|-----------|  
    |Geography Id|Hidden|True|  
    |Birth Date|Formato dati|Short Date|  
  
     **Data**  
  
    > [!NOTE]  
    >  Poiché la tabella Date è stata selezionata come tabella data dei modelli, usando il contrassegno come impostazioni tabella data, nella lezione 7: Contrassegna come tabella data, la colonna Date nella tabella Date come colonna da utilizzare come identificatore univoco, la proprietà identificatore di riga per la colonna Date verrà automaticamente impostata su True e non può essere modificato. Quando si utilizzano funzioni di Business Intelligence per le gerarchie temporali nelle formule DAX, è necessario specificare una tabella relativa alla data. In questo modello sono state create diverse misure utilizzando funzioni di Business Intelligence per le gerarchie temporali per calcolare i dati di vendita per diversi periodi, ad esempio i trimestri precedente e corrente, nonché per essere utilizzati negli indicatori KPI. Per altre informazioni su come specificare una tabella con data, vedere [Specificare Contrassegna come tabella data per l'utilizzo con funzionalità di Business Intelligence per le gerarchie temporali &#40;SSAS tabulare&#41;](tabular-models/specify-mark-as-date-table-for-use-with-time-intelligence-ssas-tabular.md) documentazione online di SQL Server.  
  
    |colonna|Proprietà|Value|  
    |------------|--------------|-----------|  
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
    |------------|--------------|-----------|  
    |Geography Id|Hidden|True|  
    |ID territorio vendita|Hidden|True|  
  
     **Product**  
  
    |colonna|Proprietà|Value|  
    |------------|--------------|-----------|  
    |Product Id|Hidden|True|  
    |Product Alternate Id|Etichetta predefinita|True|  
    |Product Subcategory Id|Hidden|True|  
    |Product Start Date|Formato dati|Short Date|  
    |Product End Date|Formato dati|Short Date|  
    |Large Photo|Hidden|True|  
  
     **Internet Sales**  
  
    |colonna|Proprietà|Value|  
    |------------|--------------|-----------|  
    |Product Id|Hidden|True|  
    |Customer Id|Hidden|True|  
    |Promotion Id|Hidden|True|  
    |Currency Id|Hidden|True|  
    |ID territorio vendita|Hidden|True|  
    |Order Quantity|tipo di dati<br /><br /> Formato dati<br /><br /> Cifre decimali|Decimal Number<br /><br /> Numero decimale<br /><br /> 0|  
    |Order Date|Tipo di dati|Short Date|  
    |Due Date|Tipo di dati|Short Date|  
    |Ship Date|Tipo di dati|Short Date|  
  
## <a name="redeploy-the-adventure-works-internet-sales-tabular-model"></a>Ridistribuire il modello tabulare Adventure Works Internet Sales  
 Poiché il modello è stato modificato, è necessario ridistribuirlo. Verranno essenzialmente ripetute le attività eseguite in [lezione 14: Distribuire](lesson-13-deploy.md).  
  
#### <a name="to-redeploy-the-adventure-works-internet-sales-tabular-model"></a>Per ridistribuire il modello tabulare Adventure Works Internet Sales  
  
-   In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] fare clic sul menu **Compila** e scegliere **Deploy Adventure Works Internet Sales Model** (Distribuisci Adventure Works Internet Sales Model).  
  
     Si aprirà la finestra di dialogo **Distribuisci** in cui sono indicati lo stato della distribuzione dei metadati e ogni tabella inclusa nel modello.  
  
## <a name="next-steps"></a>Passaggi successivi  
 A questo punto è possibile usare Power View per visualizzare i dati del modello. Assicurarsi che agli account di Analysis Services e Reporting Services nel sito di SharePoint siano associate le autorizzazioni di lettura per l'istanza di Analysis Services in cui è stato distribuito il modello.  
  
 Per creare un'origine dati del report di Reporting Services che fa riferimento al modello, vedere la pagina relativa al [tipo di connessione al modello di tabella (SSRS)](https://msdn.microsoft.com/library/hh270317%28v=SQL.110%29.aspx).  
  
  
