---
title: Editor di Query DMX (Analysis Services - Data Mining) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.startpage.dmx.f1
ms.assetid: 7ac877a1-0f29-46b9-9a51-73b02172bef1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3be28b0a402743e4d9c26b346386202127c5f74d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66081572"
---
# <a name="dmx-query-editor-analysis-services---data-mining"></a>Editor di query DMX (Analysis Services - Data mining)
  Utilizzare l'Editor di query DMX per progettare ed eseguire istruzioni scritte nel linguaggio DMX.  
  
## <a name="features"></a>Funzionalità  
  
-   Consente di digitare script nel riquadro di modifica delle query.  
  
-   Per eseguire gli script è possibile premere **F5**o fare clic su **Esegui** sulla barra degli strumenti o scegliere lo stesso comando dal menu **Query** . Se è stata selezionata una parte del codice, viene eseguita solo quella parte. Se non è stata selezionata alcuna parte del codice, viene eseguito tutto il contenuto dell'Editor di query DMX.  
  
-   Consente di visualizzare metadati per cubi e altri oggetti contenuti in un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nel riquadro dei metadati  
  
-   Per informazioni sulla sintassi DMX, selezionare una parola chiave nell'Editor di query DMX, quindi premere **F1**.  
  
-   Per visualizzare la Guida dinamica contenente la sintassi DMX, scegliere **Guida dinamica** dal menu **?** per aprire il componente Guida dinamica. Quando si usa la Guida dinamica, i relativi argomenti vengono visualizzati nella finestra di dialogo **Guida dinamica** mentre si digitano le parole chiave nell'editor di query.  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>Barra degli strumenti degli Editor di SQL Server Analysis Services  
 Quando l'Editor di query DMX è aperto, la barra degli strumenti **Editor di SQL Server Analysis Services** visualizzata contiene i pulsanti elencati nella tabella seguente.  
  
|Nome|Definizione|  
|----------|----------------|  
|**Connect**|Consente di aprire la finestra di dialogo **Connetti al server** per attivare una connessione a un'istanza di Analysis Services.|  
|**Disconnetti**|Consente di disconnettere l'Editor di query DMX da un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Cambia connessione**|Consente di aprire la finestra di dialogo **Connetti al server** per stabilire una connessione a una diversa istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Nuova query con connessione corrente**|Consente di aprire una nuova finestra dell'Editor di query DMX utilizzando le informazioni di connessione contenute nella finestra dell'Editor di query DMX corrente.|  
|**Database disponibili**|Consente di cambiare la connessione a un diverso database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nella stessa istanza.|  
|**Eseguire**|Consente di eseguire il codice selezionato oppure, nel caso in cui non sia stato selezionato alcun codice, di eseguire tutto il codice contenuto nell'Editor di query DMX.|  
|**Analizza**|Consente di controllare la sintassi del codice selezionato. Se non è stato selezionato alcun codice, questa opzione controlla la sintassi dell'intera finestra dell'Editor di query DMX.|  
|**Annulla esecuzione query**|Consente di inviare una richiesta di annullamento al server. Alcune query non possono essere annullate immediatamente, ma è necessario attendere che si verifichi una condizione di annullamento appropriata. Quando vengono annullate, è possibile che si verifichino ritardi durante il rollback delle transazioni.|  
  
## <a name="dmx-query-editor-window"></a>Finestra dell'Editor di query DMX  
 Nell'Editor di query DMX sono disponibili le opzioni elencate nella tabella seguente.  
  
|Nome|Definizione|  
|----------|----------------|  
|**Finestra dell'editor di query**|Consente di digitare le istruzioni e gli script MDX da eseguire tramite l'Editor di query MDX.<br /><br /> Nel menu di scelta rapida dell'editor di query sono disponibili le opzioni seguenti:<br /><br /> **Taglia**: Consente di copiare la selezione corrente negli Appunti e di rimuovere la selezione dalla finestra dell'editor di query.<br /><br /> **Copia**: Consente di copiare la selezione corrente negli Appunti.<br /><br /> **Incolla**: Consente di incollare il contenuto degli Appunti nella selezione corrente.<br /><br /> **Connetti**: Consente di aprire la finestra di dialogo **Connetti al server** per stabilire una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br /><br /> **Disconnetti**: Consente di disconnettere l'editor di query corrente da un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .<br /><br /> **Disconnetti tutte le query**: Consente di disconnettere tutti gli editor di query aperti.<br /><br /> **Cambia connessione**: Consente di aprire la finestra di dialogo **Connetti al server** per stabilire una connessione a una diversa istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].<br /><br /> **Apri server in Esplora oggetti**: Consente di aprire l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a cui è connesso l'editor di query corrente in **Esplora oggetti**.<br /><br /> **Esegui**: Consente di eseguire il codice selezionato o, se non è selezionata alcuna parte specifica del codice, di eseguire tutto il codice contenuto nell'editor di query corrente.<br /><br /> **Finestra Proprietà**: Consente di visualizzare la finestra **Proprietà** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per la finestra della query corrente.<br /><br /> **Opzioni query**: Consente di visualizzare la finestra di dialogo **Opzioni query** .|  
|**Finestra metadati**|Consente di visualizzare i metadati per il database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] attualmente connesso.|  
|**Cube**|Consente di selezionare un cubo nel database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] attualmente connesso per visualizzare i metadati associati al cubo nella scheda **Metadati** .|  
|**Metadati**|Consente di visualizzare i metadati per il cubo selezionato in **Cubo**, inclusi i gruppi di misure e le misure, gli indicatori di prestazioni chiave, le dimensioni, le gerarchie, i livelli, i membri e le proprietà membro. Per recuperare la chiave completa di un oggetto eseguire una delle operazioni seguenti:<br /><br /> Trascinare l'oggetto dalla scheda **Metadati** nel riquadro Query.<br /><br /> Oppure:<br /><br /> Fare clic con il pulsante destro del mouse sull'oggetto e scegliere **Copia**, quindi fare clic con il pulsante destro del mouse nel riquadro Query e scegliere **Incolla**.|  
|**Funzioni**|Consente di visualizzare i metadati per le funzioni DMX disponibili per il database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] come metadati recuperati dal set di righe dello schema DMSCHEMA_MINING_FUNCTIONS.<br /><br /> Per recuperare la sintassi di una funzione eseguire una delle operazioni seguenti:<br /><br /> Trascinare l'oggetto dalla scheda **Funzioni** nel riquadro Query.<br /><br /> Oppure:<br /><br /> Fare clic con il pulsante destro del mouse sulla funzione e scegliere **Copia**, quindi fare clic con il pulsante destro del mouse nel riquadro Query e scegliere **Incolla**.|  
|**Finestra dei risultati**|Consente di visualizzare i risultati di un'istruzione DMX in una griglia.|  
|**Finestra dei messaggi**|Consente di visualizzare informazioni sulla modalità di esecuzione di un'istruzione DMX. Ad esempio, in questa finestra vengono visualizzati gli eventuali errori rilevati durante l'esecuzione o il numero di celle recuperate dopo l'esecuzione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Guida di riferimento a DMX &#40;Data Mining Extensions&#41;](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Editor di Query MDX &#40;Analysis Services - dati multidimensionali&#41;](mdx-query-editor-analysis-services-multidimensional-data.md)   
 [Editor di Query XMLA &#40;Analysis Services - dati multidimensionali&#41;](xmla-query-editor-analysis-services-multidimensional-data.md)   
 [Progettazione query e gli editor di testo &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [Scelte rapide da tastiera SQL Server Management Studio](../ssms/sql-server-management-studio-keyboard-shortcuts.md)   
 [Personalizzare menu e tasti di scelta rapida](../ssms/customize-menus-and-shortcut-keys.md)   
 [Codifica con colori negli editor di query](../relational-databases/scripting/color-coding-in-query-editors.md)  
  
  
