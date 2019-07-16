---
title: Gerarchie nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d4e16aa049dbebd6a5d3d9e7f996748cabb3c236
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68162835"
---
# <a name="hierarchies"></a>Gerarchie
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Nei modelli tabulari le gerarchie sono metadati che consentono di definire le relazioni tra due o più colonne di una tabella. Le gerarchie possono essere visualizzate separatamente dalle altre colonne in un elenco di campi client per la creazione di report, semplificando l'esplorazione e l'inserimento di tali gerarchie in un report.  
  
##  <a name="bkmk_benefits"></a> Vantaggi  
 Nelle tabelle sono incluse decine, se non addirittura centinaia, di colonne con nomi insoliti senza nessun ordine apparente. Questa situazione può comportare una visualizzazione non ordinata negli elenchi di campi del client di creazione report, rendendo difficile per gli utenti il rilevamento e l'inclusione dei dati in un report. Le gerarchie possono consentire una visualizzazione semplice e intuitiva di una struttura dei dati altrimenti complessa.  
  
 In una tabella Date è ad esempio possibile creare una gerarchia Calendar. Anno di calendario verrà utilizzato come livello padre superiore, con Mese, Settimana e Anno inclusi come livelli figlio (Anno di calendario->Mese->Settimana->Giorno). In questa gerarchia viene illustrata una relazione logica da Calendar Year a Day. Un utente client può quindi selezionare l'anno di calendario in un elenco dei campi per includere tutti i livelli in una tabella pivot oppure espandere la gerarchia e selezionare solo livelli particolari da includere nella tabella pivot.  
  
 Poiché ogni livello di una gerarchia è una rappresentazione di una colonna di una tabella, il livello può essere rinominato. Sebbene non sia esclusiva delle gerarchie (qualsiasi colonna può essere rinominata in un modello tabulare), la ridenominazione dei livelli della gerarchia può rendere più semplificare l'individuazione e l'inclusione di livelli in un report. La ridenominazione di un livello non consente di ridenominare la colonna a cui fa riferimento, bensì rende semplicemente più identificabile il livello. In questo esempio gerarchia Calendar Year, nella tabella Date in vista dati, le colonne: CalendarYear, CalendarMonth, CalendarWeek e CalendarDay sono state rinominate Calendar Year, Month, settimana e giorno per renderle più facilmente identificabili. La ridenominazione dei livelli consente inoltre di fornire coerenza nei report, poiché gli utenti dovranno probabilmente modificare di meno i nomi delle colonne per renderle più leggibili nelle tabelle pivot, nei grafici e così via.  
  
 Le gerarchie possono essere incluse nelle prospettive. Le prospettive consentono di definire subset visualizzabili di un modello in grado di offrire punti di vista mirati, specifici di un'attività aziendale o di un'applicazione del modello. Una prospettiva può ad esempio fornire agli utenti un elenco visualizzabile (gerarchia) dei soli elementi di dati necessari a soddisfare specifici requisiti di creazione di report. Per altre informazioni, vedere [prospettive](../../analysis-services/tabular-models/perspectives-ssas-tabular.md).  
  
 Le gerarchie non sono pensate per essere utilizzate come meccanismo di sicurezza, ma piuttosto come strumento per migliorare l'esperienza utente. Tutte le impostazioni di sicurezza di una determinata gerarchia vengono ereditate dal modello sottostante. Le gerarchie non possono consentire l'accesso agli oggetti del modello se l'utente non dispone già del relativo diritto di accesso. È quindi necessario risolvere la sicurezza del database modello prima di poter fornire l'accesso agli oggetti del modello tramite una gerarchia. I ruoli di sicurezza possono essere utilizzati per proteggere i metadati e i dati del modello. Per altre informazioni, vedere [ruoli](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
##  <a name="bkmk_define"></a> Defining hierarchies  
 Per creare e gestire gerarchie è possibile utilizzare Progettazione modelli in Vista diagramma. La creazione e la gestione di gerarchie non sono supportate in Progettazione modelli in Vista dati. Per visualizzare Progettazione modelli in Vista diagramma fare clic sul menu **Modello** , scegliere **Vista modelli**, quindi fare clic su **Vista diagramma**.  
  
 Per creare una gerarchia, fare clic con il pulsante destro del mouse su una colonna che si desidera specificare come livello padre, quindi fare clic su **Crea gerarchia**. È possibile selezionare qualsiasi numero di colonne (all'interno di un'unica tabella) da includere oppure aggiungere in un secondo momento le colonne come livelli figlio facendo clic e trascinando le colonne nel livello padre. In caso di selezione di più colonne, la relativa posizione viene scelta automaticamente secondo un ordine basato sulla cardinalità. È possibile modificare l'ordine facendo clic e trascinando una colonna (livello) in un ordine diverso oppure utilizzando i controlli per la navigazione Su e Giù del menu di scelta rapida. Quando si aggiunge una colonna come livello figlio, è possibile utilizzare il rilevamento automatico trascinando la colonna nel livello padre.  
  
 Una colonna può essere visualizzata in più gerarchie. Nelle gerarchie non possono essere inclusi oggetti diversi da colonne quali misure o indicatori KPI. Una gerarchia può essere basata sulle colonne all'interno di un'unica tabella. Se si effettua una selezione multipla di una misura con una o più colonne oppure se si selezionano colonne da più tabelle, il comando **Crea gerarchia** sarà disabilitato nel menu di scelta rapida. Per aggiungere una colonna da un'altra tabella, utilizzare la funzione RELATED DAX per aggiungere una colonna calcolata che fa riferimento alla colonna dalla tabella correlata. Nella funzione viene usata la sintassi seguente: `=RELATED(TableName[ColumnName])`. Per ulteriori informazioni, vedere la funzione RELATED.  
  
 Per impostazione predefinita, le nuove gerarchie vengono denominate hierarchy1, hierarchy2 e così via. È necessario modificare i nomi delle gerarchie per riflettere la natura della relazione padre-figlio, rendendole più identificabili agli utenti.  
  
 Dopo aver creato le gerarchie, è possibile utilizzare la funzionalità Analizza in Excel per eseguire un test sulla loro efficacia. Per altre informazioni, vedere [analizza in Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
##  <a name="bkmk_related_tasks"></a> Related tasks  
  
|Attività|Descrizione|  
|----------|-----------------|  
|[Creare e gestire gerarchie](../../analysis-services/tabular-models/create-and-manage-hierarchies-ssas-tabular.md)|Viene descritto come creare e gestire gerarchie utilizzando Progettazione modelli in Vista diagramma.|  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione di modelli tabulari](../../analysis-services/tabular-models/tabular-model-designer-ssas.md)   
 [Prospettive](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Roles](../../analysis-services/tabular-models/roles-ssas-tabular.md)  
  
  
