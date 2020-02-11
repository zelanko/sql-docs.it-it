---
title: Analysis Services interfaccia utente di progettazione query MDX (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10012"
helpviewer_keywords:
- query designers, Analysis Services
ms.assetid: 7e288eee-2d37-485e-a6a0-dbba5e041e26
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b1d0a5738384a738c3e0882d16bbffb0f2a4d00a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68891552"
---
# <a name="analysis-services-mdx-query-designer-user-interface-report-builder"></a>Interfaccia utente di Progettazione query MDX di Analysis Services (Generatore report)
  Generatore report fornisce una finestra Progettazione query con interfaccia grafica per la compilazione di query MDX (Multidimensional Expression) per un' [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] origine dati. Nella finestra Progettazione query con interfaccia grafica MDX sono disponibili due modalità: progettazione e query. In ogni modalità è disponibile un riquadro dei metadati dal quale è possibile trascinare membri dei cubi selezionati per compilare una query MDX che recupera dati quando il report viene elaborato.  
  
> [!IMPORTANT]  
>  Gli utenti accedono alle origini dati quando creano ed eseguono query. È necessario concedere autorizzazioni minime per le origini dati, ad esempio autorizzazioni di sola lettura.  
  
 Nelle sezioni seguenti vengono descritti i pulsanti della barra degli strumenti e i riquadri di Progettazione query per ogni modalità della finestra Progettazione query con interfaccia grafica.  
  
## <a name="graphical-mdx-query-designer-in-design-mode"></a>Progettazione query MDX in modalità progettazione  
 Quando si modifica una query MDX per un set di dati del report, la finestra Progettazione query MDX con interfaccia grafica verrà aperta in modalità progettazione.  
  
 Nella figura seguente vengono etichettati i riquadri per la modalità progettazione.  
  
 ![Progettazione query MDX di Analysis Services, visualizzazione progettazione](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqd-dsawas-mdx-designmode.gif "Progettazione query MDX di Analysis Services, visualizzazione progettazione")  
  
 Nella tabella seguente vengono elencati i riquadri disponibili in questa modalità:  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Pulsante Seleziona cubo (**...**)|Consente di visualizzare il cubo attualmente selezionato.|  
|Riquadro dei metadati|Consente di visualizzare un elenco gerarchico di misure, indicatori di prestazioni chiave (KPI) e dimensioni definiti sul cubo selezionato.|  
|Riquadro Membri calcolati|Consente di visualizzare i membri calcolati attualmente definiti disponibili per l'utilizzo nella query.|  
|Riquadro Filtro|Consente di scegliere dimensioni e gerarchie correlate per filtrare i dati a livello di origine e limitare i dati restituiti al report.|  
|Riquadro Dati|Consente di visualizzare le intestazioni di colonna per il set di risultati quando si trascinano gli elementi dal riquadro metadati e dal riquadro Membri calcolati. Consente di aggiornare automaticamente il set di risultati se viene selezionato il pulsante **Esecuzione automatica** . .|  
  
 È possibile trascinare dimensioni, misure e indicatori di prestazioni chiave (KPI) dal riquadro metadati e membri calcolati dal riquadro Membro calcolato nel riquadro Dati. Nel riquadro Filtro è possibile selezionare dimensioni e gerarchie correlate e impostare espressioni di filtro per limitare i dati disponibili per la query. Se l'interruttore **esecuzione** automatica (![esecuzione automatica della query](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-autoexecute.gif "Esecuzione automatica della query")) sulla barra degli strumenti è selezionato, progettazione query esegue la query ogni volta che si rilascia un oggetto metadati nel riquadro dati. È possibile eseguire manualmente la query utilizzando il pulsante **Esegui** (![Esegui query](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-run.gif "Esecuzione della query")) sulla barra degli strumenti.  
  
 Quando si crea una query MDX in questa modalità, le seguenti proprietà aggiuntive vengono incluse automaticamente nella query:  
  
 **Proprietà del membro** MEMBER_CAPTION, MEMBER_UNIQUE_NAME  
  
 **Proprietà delle celle** VALORE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS  
  
 Per specificare le proprietà aggiuntive personalizzate, è necessario modificare manualmente la query MDX in modalità query.  
  
> [!NOTE]  
>  Per ulteriori informazioni su MDX e per informazioni generale sulla finestra Progettazione query MDX, vedere "Editor di query MDX (Analysis Services - Dati multidimensionali)" nella [documentazione online di SQL Server](https://go.microsoft.com/fwlink/?linkid=98335). Tuttavia, per visualizzare in un report i dati da una query MDX, è necessario compilare la query tramite la finestra Progettazione query MDX disponibile in Generatore report. L'importazione di una query con estensione mdx da un file non è supportata.  
  
### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>Barra degli strumenti di Progettazione query MDX in modalità progettazione  
 I pulsanti della barra degli strumenti di Progettazione query consentono di progettare query MDX utilizzando l'interfaccia grafica. Nella tabella seguente vengono elencati i pulsanti con le relative funzioni.  
  
|Pulsante|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Non abilitato per questo tipo di origine dati.|  
|**Importa**|Consente di importare una query esistente da un file di definizione di report (con estensione rdl) nel file system.|  
|![Passaggio alla visualizzazione query MDX](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-commandtypemdx.gif "Passaggio alla visualizzazione query MDX")|Consente di passare al tipo di comando MDX.|  
|![Aggiornamento dei dati dei risultati](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-refresh.gif "Aggiornamento dei dati dei risultati")|Consente di aggiornare i metadati dall'origine dati.|  
|![Aggiungi membro calcolato](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-addcalculatedmember.gif "Aggiungi membro calcolato")|Consente di visualizzare la finestra di dialogo **Generatore membri calcolati** ,|  
|![Mostra/Nascondi celle vuote](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-showemptycells.gif "Mostra/Nascondi celle vuote")|Consente di visualizzare o nascondere le celle vuote nel riquadro Dati. Questa operazione equivale a utilizzare la clausola NON EMPTY in MDX.|  
|![Esecuzione automatica della query](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-autoexecute.gif "Esecuzione automatica della query")|Consente di eseguire automaticamente la query e di visualizzarne i risultati ogni volta che viene apportata una modifica. I risultati verranno visualizzati nel riquadro Dati.|  
|![Pulsante Mostra aggregazioni](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-showaggregations.gif "Pulsante Mostra aggregazioni")|Consente di visualizzare le aggregazioni nel riquadro Dati.|  
|![Elimina](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-delete.gif "Delete")|Consente di eliminare dalla query la colonna selezionata nel riquadro Dati.|  
|![Icona della finestra di dialogo Parametri query](https://docs.microsoft.com/analysis-services/analysis-services/media/iconqueryparameter.gif "Icona della finestra di dialogo Parametri query")|Consente di visualizzare la finestra di dialogo **Parametri query** . Quando si specificano valori per un parametro di query, viene creato automaticamente un parametro di report con lo stesso nome. Il valore del parametro di query viene impostato su un'espressione che fa riferimento al parametro di report.|  
|![Pulsante Prepara query](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-preparequery.gif "Pulsante Prepara query")|Consente di preparare la query.|  
|![Eseguire la query](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-run.gif "Esecuzione della query")|Consente di eseguire la query di e visualizzare i risultati nel riquadro Dati.|  
|![Annulla la query](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-cancel.gif "Annullamento della query")|Consente di annullare la query.|  
|![Passa alla modalità progettazione](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-designmode.gif "Passare alla modalità progettazione")|Consente di passare dalla modalità progettazione alla modalità query e viceversa.|  
  
## <a name="graphical-mdx-query-designer-in-query-mode"></a>Progettazione query MDX in modalità query  
 Per modificare la finestra Progettazione query con interfaccia grafica attivando la modalità **Query** , fare clic sul pulsante **Modalità progettazione** sulla barra degli strumenti.  
  
 Nella figura seguente vengono etichettati i riquadri per la modalità query.  
  
 ![Progettazione query MDX di Analysis Services, visualizzazione query](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqd-dsawas-mdx-querymode.gif "Progettazione query MDX di Analysis Services, visualizzazione query")  
  
 Nella tabella seguente vengono elencati i riquadri disponibili in questa modalità:  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Pulsante Seleziona cubo (**...**)|Consente di visualizzare il cubo attualmente selezionato.|  
|Riquadro Metadati/Funzioni/Modelli|Consente di visualizzare un elenco gerarchico di misure, indicatori di prestazioni chiave (KPI) e dimensioni definiti sul cubo selezionato.|  
|Riquadro query|Consente di visualizzare il testo della query.|  
|Riquadro Risultati|Consente di visualizzare i risultati dell'esecuzione della query.|  
  
 Nel riquadro Metadati vengono visualizzate le schede **Metadati**, **Funzioni**e **Modelli**. Dalla scheda **Metadati** è possibile trascinare dimensioni, gerarchie, indicatori di prestazioni chiave (KPI) e misure nel riquadro Query MDX. Dalla scheda **Funzioni** è possibile trascinare funzioni nel riquadro Query MDX. Dalla scheda **Modelli** è possibile aggiungere modelli MDX al riquadro Query MDX. Quando si esegue la query, nel riquadro Risultati verranno visualizzati i risultati per la query MDX.  
  
 È possibile estendere la query MDX predefinita generata in modalità progettazione per includere proprietà del membro e della cella aggiuntive. Quando si esegue la query, questi valori non vengono visualizzati nel set di risultati, ma vengono passati nuovamente con la raccolta dei campi del set di dati e possono essere utilizzati in un report.  
  
### <a name="graphical-query-designer-toolbar-in-query-mode"></a>Barra degli strumenti della finestra Progettazione query con interfaccia grafica in modalità query  
 I pulsanti della barra degli strumenti di Progettazione query consentono di progettare query MDX utilizzando l'interfaccia grafica.  
  
 I pulsanti della barra degli strumenti sono identici in modalità progettazione e in modalità query, ma i pulsanti seguenti non sono abilitati in modalità query:  
  
-   **Modifica come testo**  
  
-   **Aggiungi membro calcolato** (![Aggiungi membro calcolato](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-addcalculatedmember.gif "Aggiungi membro calcolato"))  
  
-   **Mostra celle vuote** (![Mostra/Nascondi celle vuote](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-showemptycells.gif "Mostra/Nascondi celle vuote"))  
  
-   **Esecuzione** automatica (![esecuzione automatica della query](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-autoexecute.gif "Esecuzione automatica della query"))  
  
-   **Mostra aggregazioni** (![pulsante Mostra aggregazioni](https://docs.microsoft.com/analysis-services/analysis-services/media/rsqdicon-showaggregations.gif "Pulsante Mostra aggregazioni"))  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione query &#40;Generatore report&#41;](../../2014/reporting-services/query-designers-report-builder.md)  
  
  
