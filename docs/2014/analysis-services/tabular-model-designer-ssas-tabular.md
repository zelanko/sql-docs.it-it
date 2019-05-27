---
title: Progettazione di modelli tabulari (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.BIDTOOLSET.TOPLEVSEMMODUIENTRY.F1
ms.assetid: 45735c57-2a95-4e45-8994-7242df6c9c5f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 223a8a300a4f3000512f8d75dfb7595cb52abc08
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66067831"
---
# <a name="tabular-model-designer-ssas-tabular"></a>Progettazione di modelli tabulari (SSAS tabulare)
  La progettazione di modelli tabulari fa parte di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], integrato con Microsoft [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 2010 o versione successiva, con modelli di tipi di progetto aggiuntivi espressamente per lo sviluppo di soluzioni di modelli tabulari professionali.  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi](#bkmk_benefits)  
  
-   [Modelli di progetto](#bkmk_proj_temp)  
  
-   [Windows e i menu](#bkmk_wind_men)  
  
-   [Visual Studio Integration](#bkmk_vsint)  
  
##  <a name="bkmk_benefits"></a> Vantaggi  
 Quando si installa [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], i nuovi modelli di progetto per la creazione di modelli tabulari vengono aggiunti ai tipi di progetto disponibili. Dopo aver creato un nuovo progetto di modello tabulare utilizzando uno dei modelli, è possibile iniziare la creazione di modelli utilizzando gli appositi strumenti e procedure guidate.  
  
 Oltre ai nuovi modelli e strumenti per la creazione di soluzioni di modelli multidimensionali e tabulari professionali, nell'ambiente di [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] sono disponibili funzionalità di debug e ciclo di vita di progetti che assicurano la creazione delle soluzioni BI più efficienti per l'organizzazione. Per ulteriori informazioni su [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], vedere la pagina relativa all' [introduzione a Visual Studio](https://go.microsoft.com/fwlink/?LinkId=206389).  
  
##  <a name="bkmk_proj_temp"></a> Modelli di progetto  
 Quando si installa [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], ai tipi di progetto di Business Intelligence vengono aggiunti i modelli relativi al progetto di modello tabulare seguenti:  
  
 **Progetto tabulare di Analysis Services**  
 Questo modello può essere utilizzato per creare un nuovo progetto di modello tabulare vuoto.  
  
 **Importa da server (tabulare)**  
 Questo modello può essere utilizzato per creare un nuovo progetto di modello tabulare estraendo i metadati da un modello tabulare esistente in Analysis Services.  
  
 **Importare da PowerPivot**  
 Questo modello viene utilizzato per creare un nuovo progetto di modello tabulare estraendo i metadati e i dati da un file [!INCLUDE[ssGeminiClient](../includes/ssgeminiclient-md.md)] .  
  
> [!NOTE]  
>  Per i progetti di modello tabulare viene richiesta l'esecuzione in locale o in rete di un'istanza del server Analysis Services in modalità tabulare.  
  
##  <a name="bkmk_wind_men"></a> Finestre e menu  
 Nell'ambiente di creazione di modelli tabulari di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] sono inclusi gli elementi seguenti:  
  
### <a name="designer-window"></a>Finestra di progettazione  
 La finestra di progettazione viene utilizzata per creare modelli tabulari fornendo una rappresentazione visiva del modello. Quando si apre il file Model.bim, il modello viene visualizzato nella finestra di progettazione. È possibile creare un modello nella finestra di progettazione utilizzando due modalità di visualizzazione diverse:  
  
 **Vista dati**  
 Nella Vista dati sono visualizzate le tabelle in formato griglia tabulare. Le misure possono essere definite anche utilizzando la relativa griglia che può essere visualizzata per ogni tabella solo nella Vista dati.  
  
 **Visualizzazione Diagramma**  
 Nella Vista diagramma sono visualizzate le tabelle, con le relative relazioni, in formato grafico. È possibile filtrare colonne, misure, gerarchie e indicatori KPI, nonché scegliere di visualizzare il modello utilizzando una prospettiva definita.  
  
 La maggior parte delle attività di creazione dei modelli può essere effettuata con entrambe le viste.  
  
### <a name="solution-explorer"></a>Esplora soluzioni  
 Nella finestra Esplora soluzioni viene presentata la soluzione attiva come contenitore logico per un progetto di modello tabulare e gli elementi associati. Nel progetto di modelli (con estensione smproj) sono contenuti solo un oggetto References (vuoto) e il file Model.bim. È possibile aprire elementi di progetto per modificarli ed effettuare altre attività di gestione direttamente da questa vista.  
  
 In genere, nelle soluzioni di modelli tabulari è contenuto un solo progetto; tuttavia in una soluzione possono essere inclusi anche altri progetti, ad esempio un progetto Integration Services o Reporting Services. È possibile aggiungere un qualsiasi numero di file a condizione che non siano dello stesso tipo dei file del progetto di modello tabulare, che la proprietà Azione di compilazione sia impostata su Nessuna o che la proprietà Copia nella directory di output sia impostata su Non copiare.  
  
 Per visualizzare Esplora soluzioni, fare clic sul menu **Visualizza** , quindi su **Esplora soluzioni**.  
  
### <a name="properties-window"></a>Finestra Proprietà  
 Nella finestra Proprietà sono elencate le proprietà dell'oggetto selezionato. Gli oggetti seguenti dispongono di proprietà che possono essere visualizzate e modificate nella finestra Proprietà:  
  
-   Model.bim  
  
-   Tabella  
  
-   colonna  
  
-   Misura  
  
 Le proprietà del progetto consentono solo di visualizzare il nome e la cartella del progetto nella finestra Proprietà. Ai progetti sono inoltre associate opzioni di distribuzione aggiuntive e impostazioni del server di distribuzione che è possibile specificare utilizzando una finestra di dialogo delle proprietà modale. Per visualizzare queste proprietà, in **Esplora soluzioni**fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Proprietà**.  
  
 Nei campi della finestra Proprietà sono incorporati diversi controlli che si aprono quando si fa clic su di essi. Il tipo di controllo di modifica dipende dalla proprietà specifica. Nei controlli sono inclusi caselle di modifica, elenchi a discesa e collegamenti a finestre di dialogo personalizzate. Le proprietà visualizzate in grigio sono di sola lettura.  
  
 Per visualizzare la finestra **Proprietà** , fare clic sul menu **Visualizza** , quindi su **Finestra Proprietà**.  
  
### <a name="error-list"></a>Elenco errori  
 Nella finestra Elenco errori sono contenuti i messaggi sullo stato del modello:  
  
-   Notifiche sulle procedure consigliate di sicurezza.  
  
-   Requisiti per l'elaborazione dati.  
  
-   Informazioni sugli errori semantici per le colonne calcolate, le misure e filtri di riga per i ruoli. Per le colonne calcolate, è possibile fare doppio clic sul messaggio di errore per passare all'origine dell'errore.  
  
-   Errori di convalida della modalità DirectQuery.  
  
 Per impostazione predefinita, l' **Elenco errori** non viene visualizzato a meno che non venga restituito un errore. Tuttavia, la finestra **Elenco errori** può essere visualizzata in qualsiasi momento. Per visualizzare la finestra **Elenco errori** , fare clic sul menu **Visualizza** , quindi su **Elenco errori**.  
  
### <a name="output"></a>Output  
 Le informazioni sulla compilazione e sulla distribuzione vengono visualizzate nella finestra **Output** , oltre che nella finestra di dialogo dello stato di avanzamento modale. Per visualizzare la finestra **Output** , fare clic sul menu **Visualizza** , quindi su Output.  
  
### <a name="menu-items"></a>Voci di menu  
 Quando si installa [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], vengono aggiunte ulteriori voci di menu specifiche per la creazione di modelli tabulari alla barra dei menu di Visual Studio. Il menu **Modello** può essere utilizzato per avviare l'Importazione guidata dati, visualizzare connessioni esistenti, elaborare dati dell'area di lavoro ed elaborare l'area di lavoro del modello in [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel. Il menu **Tabella** viene utilizzato per creare e gestire relazioni tra tabelle, creare e gestire misure nonché per specificare impostazioni della tabella di dati, opzioni di calcolo ed altre proprietà della tabella. Con il menu **Colonna** è possibile aggiungere ed eliminare colonne in una tabella, nascondere e visualizzare colonne, nonché specificare altre proprietà della colonna quali i tipi di dati e i filtri. È possibile compilare e distribuire soluzioni di modelli tabulari dal menu **Compila** . Le funzioni Copia/Incolla sono incluse nel menu **Modifica** .  
  
 Oltre a queste voci di menu, vengono aggiunte ulteriori impostazioni alle opzioni di Analysis Services accessibili tramite le voci del menu Strumenti.  
  
### <a name="toolbar"></a>Barra degli strumenti  
 La barra degli strumenti di Analysis Services consente un accesso rapido e semplice ai comandi per la creazione di modelli utilizzati più frequentemente.  
  
##  <a name="bkmk_vsint"></a> Visual Studio Integration  
 **Controllo del codice sorgente**  
 I progetti di Analysis Services sono integrati con il plug-in del controllo del codice sorgente selezionato. Se Visual Studio è stato configurato in modo che venga utilizzato il controllo del codice sorgente, è possibile utilizzare l'archiviazione in Esplora Soluzioni o l'estrazione. Per configurare l'utilizzo di Team Foundation Server, vedere [Configurare Visual Studio con Team Foundation Version Control](https://msdn.microsoft.com/library/ms253064.aspx). Sono supportati anche molti plug-in del controllo del codice sorgente di terze parti.  
  
 **Tipi di carattere**  
 Nei modelli tabulari viene usato il tipo di carattere ambiente di [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] per controllare i tipi di carattere nella visualizzazione. Può essere necessario modificare questo tipo di carattere se quello predefinito di [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] non dispone di tutti i caratteri Unicode necessari per la lingua in uso. Per modificare i tipi di carattere, fare clic sul menu **Strumenti** , quindi su **Opzioni**e infine su **Tipi di carattere e colori**.  
  
 **Tasti di scelta rapida**  
 I tasti di scelta rapida di Analysis Services possono essere configurati o mappati di nuovo tramite Strumenti->Opzioni ->finestra di dialogo Tastiera. Alcuni tasti di scelta rapida [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] globali, ad esempio quelli di compilazione, salvataggio, debug, nuovo progetto e così via, sono supportati nel contesto di progettazione di modelli tabulari. Altri collegamenti specifici della progettazione di modelli tabulari sono disponibili nel contesto di Analysis Services.  
  
## <a name="see-also"></a>Vedere anche  
 [Progetti di modello tabulare &#40;SSAS tabulare&#41;](tabular-models/tabular-model-projects-ssas-tabular.md)   
 [Proprietà &#40;SSAS tabulare&#41;](tabular-models/properties-ssas-tabular.md)  
  
  
