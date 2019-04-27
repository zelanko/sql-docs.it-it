---
title: Sulla barra degli strumenti (scheda esplorazione, Progettazione cubi) (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: a1c6272d-e514-456b-9995-b73fec0112a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 050be457b1b7915e4354e8a0edf2fe79fabf8d67
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62756823"
---
# <a name="toolbar-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>Barra degli strumenti (scheda Esplorazione, Progettazione cubi) (Analysis Services - Dati multidimensionali)
  Usare le funzionalità in **Barra degli strumenti** in Progettazione cubi per eseguire operazioni comuni durante la progettazione o l'esplorazione di un cubo o del relativo oggetto oppure durante la creazione di una query MDX. Le operazioni comuni sia in fase di progettazione che in visualizzazione query includono l'impostazione del contesto utente, l'elaborazione di oggetti e l'impostazione della lingua predefinita.  
  
 La tabella seguente elenca i pulsanti della **Barra degli strumenti** con le relative funzioni.  
  
|Button|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Non abilitato per questo tipo di origine dati.|  
|**Importa**|Consente di importare una query esistente da un file di definizione di report (con estensione rdl) nel file system.|  
|![Passa alla visualizzazione query MDX](media/rsqdicon-commandtypemdx.gif "Passa alla visualizzazione query MDX")|Consente di passare al tipo di comando MDX.|  
|![Aggiorna i dati dei risultati](media/rsqdicon-refresh.gif "Aggiorna i dati dei risultati")|Consente di aggiornare i metadati dall'origine dati.|  
|![Add calculated member](media/rsqdicon-addcalculatedmember.gif "Add calculated member")|Consente di visualizzare la finestra di dialogo **Generatore membri calcolati** ,|  
|![Visualizza/nascondi celle vuote](media/rsqdicon-showemptycells.gif "Visualizza/nascondi celle vuote")|Consente di visualizzare o nascondere le celle vuote nel riquadro Dati. Questa operazione equivale a utilizzare la clausola NON EMPTY in MDX.|  
|![Esecuzione automatica della query](media/rsqdicon-autoexecute.gif "Esecuzione automatica della query")|Consente di eseguire automaticamente la query e di visualizzarne i risultati ogni volta che viene apportata una modifica. I risultati verranno visualizzati nel riquadro Dati.|  
|![Pulsante Mostra aggregazioni](media/rsqdicon-showaggregations.gif "Pulsante Mostra aggregazioni")|Consente di visualizzare le aggregazioni nel riquadro Dati.|  
|![Elimina](media/rsqdicon-delete.gif "Elimina")|Consente di eliminare dalla query la colonna selezionata nel riquadro Dati.|  
|![Icona della finestra di dialogo Parametri query](media/iconqueryparameter.gif "Icona della finestra di dialogo Parametri query")|Consente di visualizzare la finestra di dialogo **Parametri query** . Quando si specificano valori per un parametro di query, viene creato automaticamente un parametro con lo stesso nome.|  
|![Pulsante Prepara query](media/rsqdicon-preparequery.gif "Pulsante Prepara query")|Consente di preparare la query.|  
|![Esecuzione della query](media/rsqdicon-run.gif "Esecuzione della query")|Consente di eseguire la query di e visualizzare i risultati nel riquadro Dati.|  
|![Annullamento della query](media/rsqdicon-cancel.gif "Annullamento della query")|Consente di annullare la query.|  
|![Passa alla modalità progettazione](media/rsqdicon-designmode.gif "Passa alla modalità progettazione")|Consente di passare dalla modalità progettazione alla modalità query e viceversa.|  
  
 In generale, i pulsanti della barra degli strumenti sono identici in **Modalità progettazione** e in **Modalità query**, tuttavia i pulsanti seguenti non sono abilitati in Modalità query:  
  
-   **Modifica come testo**  
  
-   **Aggiungi membro calcolato** (![Add calculated member](media/rsqdicon-addcalculatedmember.gif "Add calculated member"))  
  
-   **Mostra celle vuote** (![Visualizza/nascondi celle vuote](media/rsqdicon-showemptycells.gif "Visualizza/nascondi celle vuote"))  
  
-   **Esecuzione automatica** (![Esecuzione automatica della query](media/rsqdicon-autoexecute.gif "Esecuzione automatica della query"))  
  
-   **Mostra aggregazioni** (![Pulsante Mostra aggregazioni](media/rsqdicon-showaggregations.gif "Pulsante Mostra aggregazioni"))  
  
## <a name="options"></a>Opzioni  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**Process**|Fare clic su questo pulsante per visualizzare la finestra di dialogo **Elabora** ed elaborare il cubo. Per altre informazioni sulla finestra di dialogo **Elabora** vedere [Finestra di dialogo Elabora &#40;Analysis Services - Dati multidimensionali&#41;](process-dialog-box-analysis-services-multidimensional-data.md).|  
|**Cambia utente**|Fare clic per visualizzare la finestra di dialogo **Contesto di sicurezza** e cambiare l'utente e il ruolo usati nella scheda **Esplorazione**. Per altre informazioni sulla finestra di dialogo **Contesto di sicurezza**, vedere [Finestra di dialogo Contesto di sicurezza &#40;Analysis Services - Dati multidimensionali&#41;](security-context-dialog-box-analysis-services-multidimensional-data.md).|  
|**Ristabilire la connessione**|Fare clic su questo pulsante per riconnettere la scheda **Calcoli** all'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e al database contenente il cubo nel caso in cui la sessione per la scheda **Esplorazione** sia stata disconnessa a causa della perdita della connessione o per il verificarsi del timeout.|  
|**Aggiorna**|Fare clic su questo pulsante per aggiornare i riquadri **Metadati** e **Report** .|  
|**Ordinamento crescente**|Fare clic su questo pulsante per ordinare gli elementi di pari livello della riga selezionata nel riquadro **Report** in ordine crescente in base alla lingua specificata in **Lingua**.<br /><br /> **Nota** Questa opzione è attivata solo se nel riquadro **Report** è selezionata una cella.|  
|**Ordinamento decrescente**|Fare clic su questo pulsante per ordinare gli elementi di pari livello della riga selezionata nel riquadro **Report** in ordine decrescente in base alla lingua specificata in **Lingua**.<br /><br /> Nota: Questa opzione è abilitata solo se una cella nel **report** è selezionato il riquadro.|  
|**Filtro automatico**|Fare clic per filtrare automaticamente i risultati nel riquadro **Risultato** .|  
|**Mostra solo prime/ultime**|Selezionare un valore per visualizzare solo il numero o la percentuale di celle superiori o inferiori nel riquadro **Report** in base alla misura selezionata.<br /><br /> Per altre informazioni su questa opzione, vedere [TopCount &#40;MDX&#41;](/sql/mdx/topcount-mdx), [TopPercent &#40;MDX&#41;](/sql/mdx/toppercent-mdx), [BottomCount &#40;MDX&#41;](/sql/mdx/bottomcount-mdx) e [BottomPercent &#40;MDX&#41;](/sql/mdx/bottompercent-mdx).|  
|**Subtotale**|Fare clic su questo pulsante per visualizzare i subtotali.|  
|**I totali di tutti gli elementi**|Fare clic per visualizzare i totali di tutti i membri nel riquadro **Report** .|  
|**Mostra celle vuote**|Fare clic per visualizzare le celle vuote nel riquadro **Report** .|  
|**Cancella risultati**|Fare clic per cancellare i risultati nel riquadro **Report** .|  
|**Comandi e opzioni**|Fare clic su questo pulsante per visualizzare la finestra di dialogo **Comandi e opzioni** e modificare le proprietà avanzate per il controllo Tabella pivot di Microsoft Office 11.0 nel riquadro **Report** . Per altre informazioni sulla finestra di dialogo **Comandi e opzioni** , vedere la documentazione di Microsoft Office.|  
|**Punto di vista**|Consente di selezionare la prospettiva da cui visualizzare i dati e i metadati nei riquadri **Metadati** e **Report** .<br /><br /> Per visualizzare il cubo senza utilizzare una prospettiva, selezionare il nome del cubo.|  
|**Lingua**|Consente di selezionare la lingua con cui visualizzare i dati e i metadati nei riquadri **Metadati** e **Report** .<br /><br /> Per visualizzare il cubo con la lingua predefinita, selezionare **Predefinita**.|  
  
  
