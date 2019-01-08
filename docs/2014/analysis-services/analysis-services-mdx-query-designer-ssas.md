---
title: Progettazione Query MDX (SSAS) di Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.asmdxquerydes.f1
ms.assetid: a2fb0b79-802a-4dac-bd9a-32dfe2e8c4d4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b0f76c8df695dcb4e49c707409243b6f1aa1d28e
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53357280"
---
# <a name="analysis-services-mdx-query-designer-ssas"></a>Progettazione query MDX di Analysis Services (SSAS)
  Progettazione query MDX (Multidimensional Expression) di Analysis Services offre un'interfaccia utente grafica per semplificare la creazione di query MDX per un'origine dati [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Nella finestra Progettazione query con interfaccia grafica MDX sono disponibili due modalità: progettazione e query. In ogni modalità è disponibile un riquadro dei metadati da cui è possibile trascinare membri dei cubi selezionati per compilare una query MDX per il recupero dei dati che si desidera utilizzare.  
  
> [!IMPORTANT]  
>  Gli utenti accedono alle origini dati quando creano ed eseguono query. È necessario concedere autorizzazioni minime per le origini dati, ad esempio autorizzazioni di sola lettura.  
>   
>  Le credenziali dell'utente corrente, non quelle specificate nella pagina Impostazioni di rappresentazione, vengono utilizzate per la connessione all'origine dati quando viene eseguita una query.  
  
 Nelle sezioni seguenti vengono descritti i pulsanti della barra degli strumenti e i riquadri di Progettazione query per ogni modalità della finestra Progettazione query con interfaccia grafica.  
  
## <a name="graphical-mdx-query-designer-in-design-mode"></a>Progettazione query MDX in modalità progettazione  
 Quando si modifica una query MDX, Progettazione query MDX con interfaccia grafica viene aperta in modalità progettazione.  
  
 Nella figura seguente vengono etichettati i riquadri per la modalità progettazione.  
  
 ![Progettazione query MDX di Analysis Services in visualizzazione Progettazione](media/rsqd-dsawas-mdx-designmode.gif "Progettazione query MDX di Analysis Services in visualizzazione Progettazione")  
  
 Nella tabella seguente vengono elencati i riquadri disponibili in questa modalità:  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Pulsante Seleziona cubo (**...**)|Consente di visualizzare il cubo attualmente selezionato.|  
|Riquadro dei metadati|Consente di visualizzare un elenco gerarchico di misure, indicatori di prestazioni chiave (KPI) e dimensioni definiti sul cubo selezionato.|  
|Riquadro Membri calcolati|Consente di visualizzare i membri calcolati attualmente definiti disponibili per l'utilizzo nella query.|  
|Riquadro Filtro|Consente di scegliere dimensioni e gerarchie correlate per filtrare i dati a livello di origine e limitare i dati restituiti.|  
|Riquadro Dati|Consente di visualizzare le intestazioni di colonna per il set di risultati quando si trascinano gli elementi dal riquadro metadati e dal riquadro Membri calcolati. Consente di aggiornare automaticamente il set di risultati se viene selezionato il pulsante **Esecuzione automatica** .|  
  
 È possibile trascinare dimensioni, misure e indicatori di prestazioni chiave (KPI) dal riquadro metadati e membri calcolati dal riquadro Membro calcolato nel riquadro Dati. Nel riquadro Filtro è possibile selezionare dimensioni e gerarchie correlate e impostare espressioni di filtro per limitare i dati disponibili per la query. Se l'interruttore **Esecuzione automatica** (![Esecuzione automatica della query](media/rsqdicon-autoexecute.gif "Esecuzione automatica della query")) sulla barra degli strumenti è selezionato, Progettazione query esegue la query ogni volta che si rilascia un oggetto di metadati nel riquadro Dati. È possibile eseguire manualmente la query usando il pulsante **Esegui** (![Esecuzione della query](media/rsqdicon-run.gif "Esecuzione della query")) sulla barra degli strumenti.  
  
 Quando si crea una query MDX in questa modalità, le seguenti proprietà aggiuntive vengono incluse automaticamente nella query:  
  
 **Proprietà membro** MEMBER_CAPTION, MEMBER_UNIQUE_NAME  
  
 **Proprietà cella** VALUE, BACK_COLOR, FORE_COLOR, FORMATTED_VALUE, FORMAT_STRING, FONT_NAME, FONT_SIZE, FONT_FLAGS  
  
 Per specificare le proprietà aggiuntive personalizzate, è necessario modificare manualmente la query MDX in modalità query.  
  
 L'importazione di una query con estensione mdx da un file non è supportata.  
  
> [!NOTE]  
>  Per altre informazioni su MDX e per informazioni generali sulla finestra Progettazione query MDX, vedere "Editor di query MDX (Analysis Services - Dati multidimensionali)" nella [documentazione online di SQL Server](https://go.microsoft.com/fwlink/?linkid=98335).  
  
### <a name="graphical-mdx-query-designer-toolbar-in-design-mode"></a>Barra degli strumenti di Progettazione query MDX in modalità progettazione  
 I pulsanti della barra degli strumenti di Progettazione query consentono di progettare query MDX utilizzando l'interfaccia grafica. Nella tabella seguente vengono elencati i pulsanti con le relative funzioni.  
  
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
  
## <a name="graphical-mdx-query-designer-in-query-mode"></a>Progettazione query MDX in modalità query  
 Per modificare la finestra Progettazione query con interfaccia grafica attivando la modalità **Query** , fare clic sul pulsante **Modalità progettazione** sulla barra degli strumenti.  
  
 Nella figura seguente vengono etichettati i riquadri per la modalità query.  
  
 ![Progettazione query MDX di Analysis Services in visualizzazione Query](media/rsqd-dsawas-mdx-querymode.gif "Progettazione query MDX di Analysis Services in visualizzazione Query")  
  
 Nella tabella seguente vengono elencati i riquadri disponibili in questa modalità:  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Pulsante Seleziona cubo (**...**)|Consente di visualizzare il cubo attualmente selezionato.|  
|Riquadro Metadati/Funzioni/Modelli|Consente di visualizzare un elenco gerarchico di misure, indicatori di prestazioni chiave (KPI) e dimensioni definiti sul cubo selezionato.|  
|Riquadro query|Consente di visualizzare il testo della query.|  
|Riquadro Risultati|Consente di visualizzare i risultati dell'esecuzione della query.|  
  
 Nel riquadro Metadati vengono visualizzate le schede **Metadati**, **Funzioni**e **Modelli**. Dalla scheda **Metadati** è possibile trascinare dimensioni, gerarchie, indicatori di prestazioni chiave (KPI) e misure nel riquadro Query MDX. Dalla scheda **Funzioni** è possibile trascinare funzioni nel riquadro Query MDX. Dalla scheda **Modelli** è possibile aggiungere modelli MDX al riquadro Query MDX. Quando si esegue la query, nel riquadro Risultati verranno visualizzati i risultati per la query MDX.  
  
 È possibile estendere la query MDX predefinita generata in modalità progettazione per includere proprietà del membro e della cella aggiuntive. Quando si esegue la query, questi valori non vengono visualizzati nel set di risultati, ma vengono passati nuovamente con la raccolta dei campi del set di dati e possono essere utilizzati.  
  
### <a name="graphical-query-designer-toolbar-in-query-mode"></a>Barra degli strumenti della finestra Progettazione query con interfaccia grafica in modalità query  
 I pulsanti della barra degli strumenti di Progettazione query consentono di progettare query MDX utilizzando l'interfaccia grafica.  
  
 I pulsanti della barra degli strumenti sono identici in modalità progettazione e in modalità query, ma i pulsanti seguenti non sono abilitati in modalità query:  
  
-   **Modifica come testo**  
  
-   **Aggiungi membro calcolato** (![Add calculated member](media/rsqdicon-addcalculatedmember.gif "Add calculated member"))  
  
-   **Mostra celle vuote** (![Visualizza/nascondi celle vuote](media/rsqdicon-showemptycells.gif "Visualizza/nascondi celle vuote"))  
  
-   **Esecuzione automatica** (![Esecuzione automatica della query](media/rsqdicon-autoexecute.gif "Esecuzione automatica della query"))  
  
-   **Mostra aggregazioni** (![Pulsante Mostra aggregazioni](media/rsqdicon-showaggregations.gif "Pulsante Mostra aggregazioni"))  
  
  
