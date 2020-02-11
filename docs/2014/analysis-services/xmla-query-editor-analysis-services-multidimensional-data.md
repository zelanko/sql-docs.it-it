---
title: Editor di query XMLA (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.editor.xmla.f1
helpviewer_keywords:
- XMLA Query Editor
- Query Editor [XMLA]
ms.assetid: 14623019-7839-4038-9d12-2f8953d2ec04
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1939ea9e1de7b0b7858ad09ad26bc3b4fbf008c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66065305"
---
# <a name="xmla-query-editor-analysis-services---multidimensional-data"></a>Editor di query XMLA (Analysis Services - Dati multidimensionali)
  Utilizzare l'Editor di query XMLA per progettare ed eseguire istruzioni e script scritti nel linguaggio MDX (XMLA).  
  
## <a name="features"></a>Funzionalità  
  
-   È possibile digitare gli script nel riquadro dell'editor di query XMLA.  
  
-   Per eseguire gli script è possibile premere **F5**oppure fare clic su **Esegui** sulla barra degli strumenti oppure scegliere **Esegui** dal menu **Query**. Se è stata selezionata una parte del codice, viene eseguita solo quella parte. Se non è stata eseguita alcuna selezione, verrà eseguito tutto il contenuto dell'editor di query XMLA.  
  
-   Consente di visualizzare metadati per cubi e altri oggetti contenuti in un database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nel riquadro dei metadati.  
  
-   Per informazioni sulla sintassi XMLA, selezionare una parola chiave nell'editor di query XMLA e quindi premere **F1**.  
  
-   Per la Guida dinamica relativa alla sintassi XMLA, scegliere **Guida dinamica** dal menu **?** per aprire il componente. Quando si usa la Guida dinamica, i relativi argomenti vengono visualizzati nella finestra di dialogo **Guida dinamica** mentre si digitano le parole chiave nell'editor di query.  
  
## <a name="sql-server-analysis-services-editors-toolbar"></a>Barra degli strumenti degli Editor di SQL Server Analysis Services  
 Quando l'editor di query XMLA è aperto, sulla barra degli strumenti **Editor di SQL Server Analysis Services** sono disponibili i pulsanti seguenti.  
  
|Termine|Definizione|  
|----------|----------------|  
|**Connettere**|Consente di aprire la finestra di dialogo **Connetti al server** per stabilire una connessione a un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Disconnettere**|Consente di disconnettere l'editor di query XMLA da un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Cambia connessione**|Consente di aprire la finestra di dialogo **Connetti al server** per stabilire una connessione a una diversa istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Nuova query con connessione corrente**|Consente di aprire una nuova finestra dell'editor di query XMLA utilizzando le stesse informazioni di connessione della finestra dell'editor di query XMLA corrente.|  
|**Database disponibili**|Consente di cambiare la connessione a un diverso database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] nella stessa istanza.|  
|**Eseguire**|Consente di eseguire il codice selezionato o, se non è selezionata alcuna parte specifica del codice, di eseguire tutto il codice contenuto nell'editor di query XMLA.|  
|**Analizza**|Consente di controllare la sintassi del codice selezionato. Se non è selezionata alcuna parte di codice, consente di controllare la sintassi di tutto il contenuto della finestra dell'editor di query XMLA.|  
|**Annulla esecuzione query**|Consente di inviare una richiesta di annullamento al server. Alcune query non possono essere annullate immediatamente, ma devono attendere una condizione di annullamento adatta. Quando le query vengono annullate, è possibile che si verifichino ritardi durante il rollback delle transazioni.|  
  
## <a name="xmla-query-editor-window"></a>Finestra dell'editor di query XMLA  
 Nell'editor di query XMLA sono disponibili le opzioni seguenti:  
  
|Termine|Definizione|  
|----------|----------------|  
|**Finestra dell'editor di query**|Consente di digitare istruzioni e script XMLA da eseguire mediante l'editor di query XMLA.<br /><br /> Nel menu di scelta rapida dell'editor di query sono disponibili le opzioni seguenti:<br /><br /> **Taglia**: consente di copiare la selezione corrente negli Appunti e di rimuovere la selezione dalla finestra dell'editor di query.<br />**Copia**: copia la selezione corrente negli Appunti.<br />**Incolla**: incolla il contenuto degli Appunti nella selezione corrente.<br />**Connetti**: apre la finestra di dialogo **Connetti al server** per stabilire una connessione a un' [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] istanza di.<br />**Disconnetti**: disconnette l'editor di query corrente da un' [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] istanza di.<br />**Disconnetti tutte le query**: disconnette tutti gli editor di query aperti.<br />**Cambia connessione**: apre la finestra di dialogo **Connetti al server** per stabilire una connessione a un'istanza [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] diversa.<br />**Apri server in Esplora oggetti**: apre l' [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] istanza di a cui è connesso l'editor di query corrente nel **Esplora oggetti**.<br />**Esegui**: esegue il codice selezionato oppure, se non è selezionato alcun codice, esegue l'intero codice nell'editor di query corrente.<br />**Finestra Proprietà**: consente di **** visualizzare la finestra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] proprietà in per la finestra di query corrente.<br />**Opzioni query**: consente di visualizzare la finestra di dialogo **Opzioni query** .|  
|**Finestra Risultati**|Consente di visualizzare i risultati di un'istruzione o di uno script XMLA in formato testo.|  
|**Finestra Messaggi**|Consente di visualizzare informazioni sull'esecuzione di un'istruzione o di uno script XMLA. Ad esempio, in questa finestra vengono visualizzati gli eventuali errori rilevati durante l'esecuzione o il numero di celle recuperate dopo l'esecuzione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Editor di query MDX &#40;Analysis Services Dati multidimensionali&#41;](mdx-query-editor-analysis-services-multidimensional-data.md)   
 [Editor di query DMX &#40;Analysis Services-Data mining&#41;](dmx-query-editor-analysis-services-data-mining.md)   
 [Editor di query e di testo &#40;SQL Server Management Studio&#41;](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)   
 [Tasti di scelta rapida di SQL Server Management Studio](../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
  
  
