---
title: Gerarchie (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e3e50e89-f85d-485b-a271-1e0550520212
author: minewiskan
ms.author: owend
ms.openlocfilehash: 823d35b71fca52b2f1892d6e7dbfc940688f0ae6
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938872"
---
# <a name="hierarchies-ssas-tabular"></a>Gerarchie (SSAS tabulare)
  Nei modelli tabulari le gerarchie sono metadati che consentono di definire le relazioni tra due o più colonne di una tabella. Le gerarchie possono essere visualizzate separatamente dalle altre colonne in un elenco di campi client per la creazione di report, semplificando l'esplorazione e l'inserimento di tali gerarchie in un report.  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi](#bkmk_benefits)  
  
-   [Definizione di gerarchie](#bkmk_define)  
  
-   [Attività correlate](#bkmk_related_tasks)  
  
##  <a name="benefits"></a><a name="bkmk_benefits"></a> Vantaggi  
 Nelle tabelle sono incluse decine, se non addirittura centinaia, di colonne con nomi insoliti senza nessun ordine apparente. Questa situazione può comportare una visualizzazione non ordinata negli elenchi di campi del client di creazione report, rendendo difficile per gli utenti il rilevamento e l'inclusione dei dati in un report. Le gerarchie possono consentire una visualizzazione semplice e intuitiva di una struttura dei dati altrimenti complessa.  
  
 In una tabella Date è ad esempio possibile creare una gerarchia Calendar. Anno di calendario verrà utilizzato come livello padre superiore, con Mese, Settimana e Anno inclusi come livelli figlio (Anno di calendario->Mese->Settimana->Giorno). In questa gerarchia viene illustrata una relazione logica da Calendar Year a Day. Un utente client può quindi selezionare l'anno di calendario in un elenco dei campi per includere tutti i livelli in una tabella pivot oppure espandere la gerarchia e selezionare solo livelli particolari da includere nella tabella pivot.  
  
 Poiché ogni livello di una gerarchia è una rappresentazione di una colonna di una tabella, il livello può essere rinominato. Sebbene non sia esclusiva delle gerarchie (qualsiasi colonna può essere rinominata in un modello tabulare), la ridenominazione dei livelli della gerarchia può rendere più semplificare l'individuazione e l'inclusione di livelli in un report. La ridenominazione di un livello non consente di ridenominare la colonna a cui fa riferimento, bensì rende semplicemente più identificabile il livello. Nell'esempio della gerarchia Calendar Year nella tabella Date in Vista dati, le colonne CalendarYear, CalendarMonth, CalendarWeek e CalendarDay sono state rinominate Calendar Year, Calendar Month, Calendar Week e Calendar Day per renderle più facilmente identificabili. La ridenominazione dei livelli consente inoltre di fornire coerenza nei report, poiché gli utenti dovranno probabilmente modificare di meno i nomi delle colonne per renderle più leggibili nelle tabelle pivot, nei grafici e così via.  
  
 Le gerarchie possono essere incluse nelle prospettive. Le prospettive consentono di definire subset visualizzabili di un modello in grado di offrire punti di vista mirati, specifici di un'attività aziendale o di un'applicazione del modello. Una prospettiva può ad esempio fornire agli utenti un elenco visualizzabile (gerarchia) dei soli elementi di dati necessari a soddisfare specifici requisiti di creazione di report. Per altre informazioni, vedere [Prospettive &#40;SSAS tabulare&#41;](perspectives-ssas-tabular.md).  
  
 Le gerarchie non sono pensate per essere utilizzate come meccanismo di sicurezza, ma piuttosto come strumento per migliorare l'esperienza utente. Tutte le impostazioni di sicurezza di una determinata gerarchia vengono ereditate dal modello sottostante. Le gerarchie non possono consentire l'accesso agli oggetti del modello se l'utente non dispone già del relativo diritto di accesso. È quindi necessario risolvere la sicurezza del database modello prima di poter fornire l'accesso agli oggetti del modello tramite una gerarchia. I ruoli di sicurezza possono essere utilizzati per proteggere i metadati e i dati del modello. Per altre informazioni, vedere [Ruoli &#40;SSAS tabulare&#41;](roles-ssas-tabular.md).  
  
##  <a name="defining-hierarchies"></a><a name="bkmk_define"></a>Definizione di gerarchie  
 Per creare e gestire gerarchie è possibile utilizzare Progettazione modelli in Vista diagramma. La creazione e la gestione di gerarchie non sono supportate in Progettazione modelli in Vista dati. Per visualizzare Progettazione modelli in Vista diagramma fare clic sul menu **Modello** , scegliere **Vista modelli**, quindi fare clic su **Vista diagramma**.  
  
 Per creare una gerarchia, fare clic con il pulsante destro del mouse su una colonna che si desidera specificare come livello padre, quindi fare clic su **Crea gerarchia**. È possibile selezionare qualsiasi numero di colonne (all'interno di un'unica tabella) da includere oppure aggiungere in un secondo momento le colonne come livelli figlio facendo clic e trascinando le colonne nel livello padre. In caso di selezione di più colonne, la relativa posizione viene scelta automaticamente secondo un ordine basato sulla cardinalità. È possibile modificare l'ordine facendo clic e trascinando una colonna (livello) in un ordine diverso oppure utilizzando i controlli per la navigazione Su e Giù del menu di scelta rapida. Quando si aggiunge una colonna come livello figlio, è possibile utilizzare il rilevamento automatico trascinando la colonna nel livello padre.  
  
 Una colonna può essere visualizzata in più gerarchie. Nelle gerarchie non possono essere inclusi oggetti diversi da colonne quali misure o indicatori KPI. Una gerarchia può essere basata sulle colonne all'interno di un'unica tabella. Se si effettua una selezione multipla di una misura con una o più colonne oppure se si selezionano colonne da più tabelle, il comando **Crea gerarchia** sarà disabilitato nel menu di scelta rapida. Per aggiungere una colonna da un'altra tabella, utilizzare la funzione RELATED DAX per aggiungere una colonna calcolata che fa riferimento alla colonna dalla tabella correlata. Nella funzione viene usata la sintassi seguente: `=RELATED(TableName[ColumnName])`. Per ulteriori informazioni, vedere la funzione RELATED.  
  
 Per impostazione predefinita, le nuove gerarchie vengono denominate hierarchy1, hierarchy2 e così via. È necessario modificare i nomi delle gerarchie per riflettere la natura della relazione padre-figlio, rendendole più identificabili agli utenti.  
  
 Dopo aver creato le gerarchie, è possibile utilizzare la funzionalità Analizza in Excel per eseguire un test sulla loro efficacia. Per altre informazioni, vedere la sezione [Analizzare in Excel &#40;SSAS tabulare&#41;](analyze-in-excel-ssas-tabular.md).  
  
##  <a name="related-tasks"></a><a name="bkmk_related_tasks"></a> Attività correlate  
  
|Attività|Descrizione|  
|----------|-----------------|  
|[Creare e gestire gerarchie &#40;SSAS tabulare&#41;](hierarchies-ssas-tabular.md)|Viene descritto come creare e gestire gerarchie utilizzando Progettazione modelli in Vista diagramma.|  
  
## <a name="see-also"></a>Vedere anche  
 [Progettazione di modelli tabulari &#40;SSAS tabulare&#41;](../tabular-model-designer-ssas-tabular.md)   
 [Prospettive &#40;SSAS tabulare&#41;](perspectives-ssas-tabular.md)   
 [Ruoli &#40;SSAS tabulare&#41;](roles-ssas-tabular.md)  
  
  
