---
title: Editor di query MDX (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.startpage.mdx.f1
helpviewer_keywords:
- Query Editor [MDX]
- MDX Query Editor
ms.assetid: 777f2c23-1c1c-4b72-9d19-48a4866551f8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 579af162998ffaa7c9483a6e6d29a87f98e96fac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66077874"
---
# <a name="mdx-query-editor-analysis-services---multidimensional-data"></a>Editor di query MDX (Analysis Services - Dati multidimensionali)
  Utilizzare l'Editor di query MDX per progettare ed eseguire istruzioni e script scritti nel linguaggio MDX (Multidimensional Expressions).  
  
## <a name="features"></a>Funzionalità  
  
-   Consente di digitare gli script nel riquadro dell'editor di query dell'Editor di query MDX.  
  
-   Per eseguire gli script è possibile premere **F5**oppure fare clic su **Esegui** sulla barra degli strumenti oppure scegliere **Esegui** dal menu **Query**. Se è stata selezionata una parte del codice, viene eseguita solo quella parte. Se non è stata selezionata alcuna parte del codice, viene eseguito tutto il contenuto dell'Editor di query MDX.  
  
-   Consente di visualizzare metadati per cubi e altri oggetti contenuti in un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nel riquadro dei metadati.  
  
-   Per informazioni sulla sintassi MDX, selezionare una parola chiave nell'Editor di query MDX, quindi premere **F1**.  
  
-   Per visualizzare la Guida dinamica contenente la sintassi MDX, scegliere **Guida dinamica** dal menu **?** per aprire il componente Guida dinamica. Quando si usa la Guida dinamica, i relativi argomenti vengono visualizzati nella finestra di dialogo **Guida dinamica** mentre si digitano le parole chiave nell'editor di query.  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>Barra degli strumenti degli Editor di SQL Server Analysis Services  
 Quando l'Editor di query MDX è aperto, la barra degli strumenti Editor di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] visualizzata contiene i pulsanti elencati nella tabella seguente.  
  
|Termine|Definizione|  
|----------|----------------|  
|**Connettere**|Consente di aprire la finestra di dialogo **Connetti al server** per stabilire una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Disconnettere**|Consente di disconnettere l'Editor di query MDX da un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Cambia connessione**|Consente di aprire la finestra di dialogo **Connetti al server** per stabilire una connessione a una diversa istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Nuova query con connessione corrente**|Consente di aprire una nuova finestra dell'Editor di query MDX utilizzando le informazioni di connessione contenute nella finestra dell'Editor di query MDX corrente.|  
|**Database disponibili**|Consente di cambiare la connessione a un diverso database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nella stessa istanza.|  
|**Eseguire**|Consente di eseguire il codice selezionato oppure, nel caso in cui non sia stato selezionato alcun codice, di eseguire tutto il codice contenuto nell'Editor di query MDX.|  
|**Analizza**|Consente di controllare la sintassi del codice selezionato. Nel caso in cui non sia stato selezionato alcun codice, viene controllata la sintassi dell'intera finestra dell'Editor di query MDX.|  
|**Annulla esecuzione query**|Consente di inviare una richiesta di annullamento al server. Alcune query non possono essere annullate immediatamente, ma devono attendere una condizione di annullamento adatta. Quando le query vengono annullate, è possibile che si verifichino ritardi durante il rollback delle transazioni.|  
  
## <a name="mdx-query-editor-window"></a>Finestra dell'Editor di query MDX  
 Nell'Editor di query MDX sono disponibili le opzioni elencate nella tabella seguente.  
  
|Termine|Definizione|  
|----------|----------------|  
|**Finestra dell'editor di query**|Consente di digitare le istruzioni e gli script MDX da eseguire tramite l'Editor di query MDX.<br /><br /> Nel menu di scelta rapida dell'editor di query sono disponibili le opzioni seguenti:<br /><br /> **Taglia**: consente di copiare la selezione corrente negli Appunti e di rimuovere la selezione dalla finestra dell'editor di query.<br /><br /> **Copia**: copia la selezione corrente negli Appunti.<br /><br /> **Incolla**: incolla il contenuto degli Appunti nella selezione corrente.<br /><br /> **Connetti**: apre la finestra di dialogo **Connetti al server** per stabilire una connessione a un' [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] istanza di.<br /><br /> **Disconnetti**: disconnette l'editor di query corrente da un' [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] istanza di.<br /><br /> **Disconnetti tutte le query**: disconnette tutti gli editor di query attualmente aperti.<br /><br /> **Cambia connessione**: apre la finestra di dialogo **Connetti al server** per stabilire una connessione a un'istanza [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] diversa.<br /><br /> **Apri server in Esplora oggetti**: apre l' [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] istanza di a cui è connesso l'editor di query corrente nel **Esplora oggetti**.<br /><br /> **Esegui**: esegue il codice selezionato oppure, se non è selezionato alcun codice, esegue l'intero codice nell'editor di query corrente.<br /><br /> **Finestra Proprietà**: consente di **** visualizzare la finestra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] proprietà in per la finestra di query corrente.<br /><br /> **Opzioni query**: consente di visualizzare la finestra di dialogo **Opzioni query** .|  
|**Finestra Metadati**|Consente di visualizzare i metadati per il database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] attualmente connesso.|  
|**Cubo**|Consente di selezionare un cubo nel database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] attualmente connesso per visualizzare i metadati associati al cubo nella scheda **Metadati** .|  
|**Metadati**|Consente di visualizzare i metadati per il cubo selezionato in **Cubo**, inclusi i gruppi di misure e le misure, gli indicatori di prestazioni chiave, le dimensioni, le gerarchie, i livelli, i membri e le proprietà membro. Per recuperare la chiave completa di un oggetto eseguire una delle operazioni seguenti:<br /><br /> Trascinare l'oggetto dalla scheda **Metadati** nel riquadro Query.<br /><br /> Fare clic con il pulsante destro del mouse sull'oggetto e scegliere **Copia**, quindi fare clic con il pulsante destro del mouse nel riquadro Query e scegliere **Incolla**.|  
|**Funzioni**|Consente di visualizzare i metadati per le funzioni MDX disponibili per il database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] come metadati recuperati dal set di righe dello schema MDSCHEMA_FUNCTIONS. Per recuperare la sintassi di una funzione eseguire una delle operazioni seguenti:<br /><br /> Trascinare l'oggetto dalla scheda **Funzioni** nel riquadro Query.<br /><br /> Fare clic con il pulsante destro del mouse sulla funzione e scegliere **Copia**, quindi fare clic con il pulsante destro del mouse nel riquadro Query e scegliere **Incolla**.|  
|**Finestra Risultati**|Consente di visualizzare i risultati di un'istruzione o di uno script MDX in una griglia.|  
|**Finestra Messaggi**|Consente di visualizzare informazioni sulla modalità di esecuzione di un'istruzione o di uno script MDX. Ad esempio, in questa finestra vengono visualizzati gli eventuali errori rilevati durante l'esecuzione o il numero di celle recuperate dopo l'esecuzione.|  
  
  
