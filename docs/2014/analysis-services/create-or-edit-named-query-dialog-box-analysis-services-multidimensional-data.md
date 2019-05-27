---
title: Creare o modificare la finestra di dialogo Query denominata (Analysis Services - dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.createnamedquery.f1
helpviewer_keywords:
- Create Named Query dialog box
ms.assetid: 8e192ad6-a0b1-4e21-bb3f-087c93e62941
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97f01b0bbf3d1ddc54ea4db2b771723e12d168d7
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66086807"
---
# <a name="create-or-edit-named-query-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Crea query denominata o Modifica query denominata (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Crea/Modifica query denominata** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per creare o modificare una query denominata in **Progettazione vista origine dati**. Una query denominata può essere gestita come una tabella ed essere utilizzata come base per altri oggetti [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Per visualizzare la finestra di dialogo **Crea/Modifica query denominata** , è possibile:  
  
-   Fare clic su **Nuova query denominata** nel riquadro **Barra degli strumenti** di **Progettazione vista origine dati**.  
  
-   Fare clic con il pulsante destro del mouse nel riquadro **Diagramma** di **Progettazione vista origine dati** e scegliere **Nuova query denominata**.  
  
-   Fare clic con il pulsante destro del mouse sul nome di una query denominata nel riquadro **Diagramma** o **Tabelle** di **Progettazione vista origine dati** e scegliere **Modifica query denominata**.  
  
 La query immessa deve essere un comando di query valido per il provider sottostante. La query viene preparata con il provider sottostante per la convalida e per l'identificazione delle colonne restituite. Sono previste due viste per la finestra di dialogo:  
  
-   Generatore query Visual Database Tools (VDT)  
  
     Per tutti gli utenti, nella vista Generatore query Visual Database Tools è disponibile un set di strumenti di interfaccia utente che consente di costruire e testare visivamente una query SQL.  
  
-   Generatore query generico  
  
     La visualizzazione Generatore query generico offre agli utenti esperti un'interfaccia utente più semplice e diretta per la costruzione e la verifica di una query SQL.  
  
## <a name="options"></a>Opzioni  
 **Name**  
 Consente di digitare il nome della query.  
  
 **Descrizione**  
 Consente di digitare una descrizione facoltativa della query.  
  
 **Data Source**  
 Consente di specificare l'origine dei dati per la query.  
  
 **Definizione della query**  
 Questa opzione mette a disposizione una barra degli strumenti e riquadri in cui è possibile definire e testare la query, a seconda della vista selezionata.  
  
 **Barra degli strumenti**  
 La barra degli strumenti consente di gestire i set di dati, selezionare i riquadri da visualizzare e controllare le varie funzioni di query.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**Passa a Generatore Query generico**|Selezionare questo comando per visualizzare solo le opzioni disponibili nella vista Generatore query generico. Verranno visualizzate solo le opzioni seguenti.<br />**Riquadro SQL**<br />**Riquadro risultati**<br />**Barra degli strumenti**, contenente solo **Passa a Generatore query Visual Database Tools** ed **Esegui**<br /><br /> <br /><br /> Nota: Questa opzione viene visualizzata solo se **passa a Generatore Query Visual Database Tools** sia selezionata.|  
|**Passa a Generatore Query Visual Database Tools**|Selezionare questo comando per visualizzare tutte le opzioni disponibili nella vista Generatore query Visual Database Tools.<br /><br /> Nota: Questa opzione viene visualizzata solo se **passa a Generatore Query generico** sia selezionata.|  
|**Mostra/Nascondi riquadro diagramma**|Consente di visualizzare o nascondere il riquadro **diagramma**.<br /><br /> **Nota** Questa opzione viene visualizzata solo se si seleziona **Passa a Generatore query Visual Database Tools** .|  
|**Mostra/Nascondi riquadro griglia**|Mostra o nasconde il **riquadro griglia**.<br /><br /> Nota: Questa opzione viene visualizzata solo se **passa a Generatore Query Visual Database Tools** sia selezionata.|  
|**Mostra/Nascondi riquadro SQL**|Mostra o nasconde il **riquadro SQL**.<br /><br /> Nota: Questa opzione viene visualizzata solo se **passa a Generatore Query Visual Database Tools** sia selezionata.|  
|**Mostra/Nascondi riquadro risultati**|Consente di visualizzare o nascondere il **Riquadro risultati**.<br /><br /> Nota: Questa opzione viene visualizzata solo se **passa a Generatore Query Visual Database Tools** sia selezionata.|  
|**Esegui**|Consente di eseguire la query. I risultati verranno visualizzati nel **riquadro dei risultati**.|  
|**Verifica istruzione SQL**|Consente di verificare l'istruzione SQL nella query.<br /><br /> Nota: Questa opzione viene visualizzata solo se **passa a Generatore Query Visual Database Tools** sia selezionata.|  
|**Ordinamento crescente**|Consente di disporre in ordine crescente le righe di output della colonna selezionata nel **riquadro. griglia**<br /><br /> Nota: Questa opzione viene visualizzata solo se **passa a Generatore Query Visual Database Tools** sia selezionata.|  
|**Ordinamento decrescente**|Consente di disporre in ordine decrescente le righe di output della colonna selezionata nel **riquadro griglia**.<br /><br /> Nota: Questa opzione viene visualizzata solo se **passa a Generatore Query Visual Database Tools** sia selezionata.|  
|**Rimuovi filtro**|Consente di rimuovere i criteri di ordinamento, se applicabili, per la riga selezionata nel **riquadro griglia**.<br /><br /> Nota: Questa opzione viene visualizzata solo se **passa a Generatore Query Visual Database Tools** sia selezionata.|  
|**Usa Group By**|Consente di aggiungere funzionalità di raggruppamento alla query.<br /><br /> Nota: Questa opzione viene visualizzata solo se **passa a Generatore Query Visual Database Tools** sia selezionata.|  
|**Aggiungi tabella**|Consente di visualizzare la finestra di dialogo **Aggiungi tabella** per aggiungere una nuova tabella o vista alla query. Per altre informazioni sulla finestra di dialogo **Aggiungi tabella**, vedere [Finestra di dialogo Aggiungi tabella &#40;Analysis Services - Dati multidimensionali&#41;](add-table-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Nota: Questa opzione viene visualizzata solo se **passa a Generatore Query Visual Database Tools** sia selezionata.|  
  
 **Riquadro Diagramma**  
 Consente di visualizzare gli oggetti a cui fa riferimento la query sotto forma di diagramma. Nel diagramma vengono visualizzate le tabelle incluse nella query e indicate le relative modalità di unione in join. Selezionare o deselezionare la casella di controllo accanto a una colonna nella tabella per aggiungere o rimuovere la colonna dall'output della query.  
  
 Quando si aggiungono tabelle alla query, vengono creati join tra le tabelle in base alle chiavi della tabella. Per aggiungere un join, trascinare un campo da una tabella in un campo di un'altra tabella. Per gestire un join, fare clic su di esso con il pulsante destro del mouse.  
  
 Fare clic con il pulsante destro del mouse sul **riquadro Diagramma** per aggiungere o rimuovere tabelle, selezionare tutte le tabelle e visualizzare o nascondere i riquadri.  
  
> [!NOTE]  
>  I contenuti del **riquadro Diagramma**, del **riquadro Griglia**e del **riquadro SQL** sono sincronizzati, pertanto le modifiche apportate in un riquadro vengono aggiornate anche negli altri due riquadri.  
  
> [!IMPORTANT]  
>  Questa finestra di dialogo non supporta la modifica dei tipi di query.  
  
 **Riquadro griglia**  
 Consente di visualizzare gli oggetti a cui fa riferimento la query in una griglia. È possibile utilizzare questo riquadro per aggiungere o rimuovere colonne da un query e modificare le impostazioni per ogni colonna.  
  
> [!NOTE]  
>  I contenuti del **riquadro Diagramma**, del **riquadro Griglia**e del **riquadro SQL** sono sincronizzati, pertanto le modifiche apportate in un riquadro vengono aggiornate anche negli altri due riquadri.  
  
 **Riquadro SQL**  
 Consente di visualizzare la query come istruzione SQL. Digitare un testo per modificare l'istruzione SQL per la query.  
  
> [!NOTE]  
>  I contenuti del **riquadro Diagramma**, del **riquadro Griglia**e del **riquadro SQL** sono sincronizzati, pertanto le modifiche apportate in un riquadro vengono aggiornate anche negli altri due riquadri.  
  
 **Riquadro risultati**  
 Consente di visualizzare i risultati della query quando si fa clic su **Esegui** nel riquadro **Barra degli strumenti** .  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Definire query denominate in una vista origine dati &#40;Analysis Services&#41;](multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)  
  
  
