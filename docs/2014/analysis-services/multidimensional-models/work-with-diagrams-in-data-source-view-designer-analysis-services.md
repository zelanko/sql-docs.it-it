---
title: Utilizzare diagrammi in Progettazione vista origine dati (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.diagramorganizerpane.f1
- sql12.asvs.dsvdesigner.findtable.f1
- sql12.asvs.dsvdesigner.diagrampane.f1
helpviewer_keywords:
- data source views [Analysis Services], diagrams
- diagrams [Analysis Services]
ms.assetid: 491fdd22-2326-4f27-a0dd-0a02faae3fd8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0b127b3dac76663e77b7ce0fa4faa76a91628ccc
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52507765"
---
# <a name="work-with-diagrams-in-data-source-view-designer-analysis-services"></a>Utilizzare diagrammi in Progettazione vista origine dati (Analysis Services)
  Un diagramma vista origine dati è una rappresentazione visiva degli oggetti contenuti in tale vista. È possibile utilizzare il diagramma in modo interattivo per aggiungere, nascondere, eliminare o modificare oggetti specifici. Inoltre, è possibile creare più diagrammi nella stessa vista origine dati per concentrare l'attenzione su un subset degli oggetti.  
  
 Per modificare l'area del diagramma visualizzata nel riquadro, fare clic sulla freccia a quattro punte nell'angolo inferiore destro del riquadro e quindi trascinare la casella di selezione sul diagramma di anteprima fino a selezionare l'area da visualizzare nel riquadro.  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
 [Aggiungere un diagramma](#bkmk_add)  
  
 [Modificare o eliminare un diagramma](#bkmk_edit)  
  
 [Ricercare tabelle in un diagramma](#bkmk_findtables)  
  
 [Disporre oggetti in un diagramma](#bkmk_arrangeobjects)  
  
 [Mantenere la disposizione degli oggetti](#bkmk_preserve)  
  
##  <a name="bkmk_add"></a> Aggiungere un diagramma  
 I diagrammi delle viste origine dati vengono creati automaticamente durante la creazione di tale vista. Quando la vista origine dati è disponibile, è possibile creare diagrammi aggiuntivi, rimuoverli o nascondere oggetti specifici per generare una rappresentazione della vista origine dati più gestibile.  
  
 Per creare un nuovo diagramma, fare clic con il pulsante destro del mouse in qualsiasi punto del riquadro **Libreria diagrammi** e scegliere **Nuovo diagramma**.  
  
 Quando si definisce inizialmente una vista origine dati (DSV) in un progetto di Analysis Services, tutte le tabelle e le viste aggiunte alla vista origine dati vengono aggiunti per il \<tutte le tabelle > diagramma. Questo diagramma viene visualizzato nel riquadro Libreria diagrammi di Progettazione vista origine dati, mentre le tabelle di tale diagramma e le relative colonne e relazioni vengono elencate nel riquadro Tabelle e visualizzate graficamente nel riquadro degli schemi. Tuttavia, quando si aggiungere tabelle, viste e query denominate al \<tutte le tabelle > diagramma, il numero degli oggetti nel diagramma rende complessa la visualizzazione relazioni, in particolar modo vengono aggiunte al diagramma, più tabelle dei fatti e delle dimensioni due tabelle sono correlate a più tabelle dei fatti.  
  
 Per semplificare la rappresentazione visiva quando si desidera visualizzare soltanto un subset delle tabelle della vista origine dati, è possibile definire diagrammi secondari, denominati semplicemente diagrammi, costituiti da subset selezionati delle tabelle, delle viste e delle query denominate della vista origine dati. È possibile utilizzare i diagrammi per raggruppare gli elementi nella vista origine dati in base alle esigenze aziendali o ai requisiti delle soluzioni.  
  
 È possibile raggruppare query denominate e tabelle correlate in diagrammi separati per scopi aziendali, nonché per rendere maggiormente comprensibile una vista origine dati contenente un numero elevato di tabelle e query denominate. La stessa tabella o query denominata può essere incluso in più diagrammi, ad eccezione di \<tutte le tabelle > diagramma. Nel \<tutte le tabelle > diagramma, tutti gli oggetti contenuti nella vista origine dati vengono visualizzati una sola volta.  
  
##  <a name="bkmk_edit"></a> Modificare o eliminare un diagramma  
 Quando si utilizza un diagramma, prestare molta attenzione ai comandi utilizzati per l'aggiunta e la rimozione di oggetti. Ad esempio, l'eliminazione di un oggetto da un diagramma ne comporterà l'eliminazione anche dalla vista origine dati. Se si desidera eliminare l'oggetto solo dal diagramma, usare invece **Nascondi tabella** .  
  
 ![Screenshot dell'area di lavoro di diagramma, menu di scelta rapida](../media/ssas-olapdsv-diagram.gif "Screenshot dell'area di lavoro di diagramma, menu di scelta rapida")  
  
 Sebbene sia possibile nascondere gli oggetti singolarmente, restituendoli utilizzando il comando Mostra tabelle correlate vengono restituiti anche tutti gli oggetti correlati al diagramma. Per controllare quali oggetti vengono restituiti all'area di lavoro, trascinarli invece dal riquadro Tabelle.  
  
##  <a name="bkmk_findtables"></a> Ricercare tabelle in un diagramma  
 Se le dimensioni dello schema sono elevate, potrebbe essere difficile scorrere fino a una tabella specifica nel riquadro **Diagramma** . Gli strumenti seguenti semplificano tuttavia la ricerca di una tabella in un diagramma.  
  
-   Scorrere l'elenco di tabelle nel riquadro **Tabelle** .  
  
     Per includere una tabella nel diagramma corrente, trascinare la tabella dal riquadro **Tabelle** a quello del diagramma.  
  
     Per allineare al centro la visualizzazione in una tabella già inclusa nel diagramma, selezionarla nel riquadro **Tabelle** .  
  
-   Indicatore di posizione nella tabella **diagramma** locator riquadro: la tabella è un'icona di freccia a 4 vie che si trova all'intersezione tra le barre di scorrimento orizzontale e verticale nell'angolo inferiore destro del **diagramma** riquadro. Consente di visualizzare un'anteprima del diagramma corrente nel riquadro Diagramma. È possibile utilizzare questa anteprima per modificare la visualizzazione nel riquadro Diagramma in base a qualsiasi posizione nel diagramma.  
  
-   Usare la **trova tabella** della finestra di dialogo-Right click su un'area vuota nel riquadro Diagramma e scegliere **trova tabella**. In alternativa, fare clic sul comando **Trova tabella** sulla barra degli strumenti o nel menu **Vista origine dati** .  
  
     È possibile digitare stringhe e caratteri jolly nella casella Filtro per visualizzare subset delle tabelle presenti nel diagramma.  
  
##  <a name="bkmk_arrangeobjects"></a> Disporre oggetti in un diagramma  
 Sebbene in Progettazione vista origine dati sia possibile definire più diagrammi per rendere una vista origine dati maggiormente comprensibile, i diagrammi contenenti decine di tabelle possono risultare di difficile lettura e la riorganizzazione manuale dei layout delle tabelle potrebbe essere un'operazione laboriosa. In Progettazione vista origine dati, le tabelle del diagramma corrente possono essere riorganizzate automaticamente con un layout rettangolare o diagonale basato sulle relazioni tra tali tabelle.  
  
-   In un layout rettangolare, le linee di relazione vengono tracciate tra le tabelle anziché tra le colonne, in senso orizzontale e verticale.  
  
-   In un layout diagonale, le linee di relazione vengono tracciate nel modo più diretto possibile tra le colonne correlate delle tabelle. Una relazione tra più colonne viene collegata alla prima colonna correlata nella tabella. Se le colonne di una tabella non sono visibili, le linee vengono tracciate verso la parte superiore della tabella.  
  
##  <a name="bkmk_preserve"></a> Mantenere la disposizione degli oggetti  
 Dopo aver disposto manualmente le tabelle nel modo desiderato, l'aggiunta di più tabelle al diagramma può comportare un aggiornamento del diagramma che rimuove tutte le modifiche recenti apportate al layout dell'oggetto.  
  
 Questo comportamento si verifica con più probabilità quando si aggiunge una tabella, poiché causa lo spostamento di altre tabelle nella Libreria diagrammi per consentire l'inserimento di quella nuova. Il diagramma viene quindi ridisegnato per assicurare che tutte le tabelle e le linee di connessione siano rappresentate correttamente. A questo punto è possibile che tutte le modifiche manuali apportate alla posizione di oggetti specifici vadano perse.  
  
 Per evitare il problema, aggiungere tutte le tabelle prima di procedere alle modifiche finali. In tal modo gli oggetti dovrebbero mantenere la relativa posizione nel diagramma quando verrà riaperto.  
  
## <a name="see-also"></a>Vedere anche  
 [Viste origine dati in modelli multidimensionali](data-source-views-in-multidimensional-models.md)   
 [Progettazione vista origine dati &#40;Analysis Services - Dati multidimensionali&#41;](../data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  
