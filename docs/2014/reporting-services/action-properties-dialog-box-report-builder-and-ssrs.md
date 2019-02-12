---
title: Finestra di dialogo Proprietà azione (Generatore Report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.shared.action.f1
- "10413"
- "10504"
- sql12.rtp.rptdesigner.calculatedseriesproperties.action.f1
- sql12.rtp.rptdesigner.pictureproperties.action.f1
- sql12.rtp.rptdesigner.actionproperties.f1
- sql12.rtp.rptdesigner.charttitleproperties.action.f1
- "10133"
- "10052"
- "10147"
- sql12.rtp.rptdesigner.chartproperties.action.f1
- "10122"
- sql12.rtp.rptdesigner.serieslabelproperties.action.f1
- sql12.rtp.rptdesigner.textboxproperties.action.f1
- "10162"
- "10168"
- sql12.rtp.rptdesigner.textproperties.action.f1
- sql12.rtp.rptdesigner.placeholderproperties.action.f1
- "10250"
- "10129"
- "10244"
- sql12.rtp.rptdesigner.seriesproperties.action.f1
ms.assetid: 2c5d915b-4f97-42cf-b8f1-49ca3ff3d0f9
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 63c9b4e601faad155d6f843b6ccef2f1cac7698a
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017983"
---
# <a name="action-properties-dialog-box-report-builder-and-ssrs"></a>Finestra di dialogo Proprietà azione (Generatore report e SSRS)
  È possibile utilizzare la finestra di dialogo **Azione** per abilitare opzioni dei collegamenti ipertestuali per un grafico, un misuratore e gli elementi della mappa che supportano i collegamenti. Definire un'azione in modo che un utente possa fare clic sul report e collegarsi a un URL, a un report diverso nello stesso server di report o in un sito di SharePoint integrato con un server di report oppure a un percorso diverso nello stesso report.  
  
## <a name="options"></a>Opzioni  
 **Abilita come azione**  
 Selezionare un'opzione per indicare l'azione da eseguire quando l'utente fa clic sull'elemento.  
  
 **None**  
 Selezionare questa opzione per indicare che all'elemento non è associata alcuna azione.  
  
 **Vai al report**  
 Scegliere questa opzione per creare un collegamento a un report drill-through disponibile in un server di report. Le opzioni aggiuntive elencate di seguito vengono visualizzate quando si seleziona **Vai al report**.  
  
 **Specificare un report**  
 Digitare o selezionare il nome del report che si desidera utilizzare come report drill-through. I report drill-through devono trovarsi sullo stesso server di report di questo report.  
  
 Per un report pubblicato in un server di report configurato per la modalità nativa, utilizzare un percorso completo o relativo senza l'estensione del nome di file. Se il report è archiviato nella stessa cartella del report corrente, è sufficiente utilizzare il nome del report. Se il report si trova in una cartella diversa nello stesso server di report, utilizzare un percorso relativo o completo. Un percorso relativo inizia dalla cartella corrente e risale la gerarchia di cartelle, ad esempio ../Cartella2/Report1. Un percorso completo inizia da /, la cartella Home, ad esempio /Report/Report1.  
  
 Per un report pubblicato in un server di report configurato per la modalità integrata SharePoint, utilizzare un URL completo, inclusa l'estensione del nome di file (RDL). Ad esempio, http://*\<NomeServerSharePoint > /\<sito >*/Documents/Report1.rdl. I percorsi relativi non sono supportati.  
  
 Per altre informazioni, vedere [Specifica di percorsi di elementi esterni &#40;Generatore report e SSRS&#41;](report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md) nella [documentazione di Generatore report](https://go.microsoft.com/fwlink/?LinkId=154494) nel sito msdn.microsoft.com.  
  
 **Utilizzare i parametri seguenti per eseguire il report**  
 Aggiungere un elenco di parametri da passare al report drill-through. I nomi dei parametri devono corrispondere ai parametri definiti per il report di destinazione. Utilizzare i pulsanti **Aggiungi** ed **Elimina** per aggiungere e rimuovere parametri e le frecce SU e GIÙ per ordinare l'elenco di parametri.  
  
 **Aggiungi**  
 Consente di aggiungere un nuovo parametro da passare al report drill-through.  
  
 **Elimina**  
 Consente di eliminare un parametro per il report drill-through.  
  
 **Freccia in su**  
 Consente di spostare il parametro di una posizione verso l'alto nell'elenco.  
  
 **Freccia GIÙ**  
 Consente di spostare il parametro di una posizione verso il basso nell'elenco.  
  
 **Name**  
 Digitare il testo che corrisponde al nome di un parametro definito nel report drill-through.  
  
 **Valore**  
 Digitare o selezionare un valore da passare per il parametro denominato nel report drill-through. Fare clic sul pulsante **Espressione** (*fx*) per modificare l'espressione.  
  
 **Omit**  
 Selezionare questa opzione per impedire l'esecuzione del parametro. Per impostazione predefinita, questa casella di controllo è deselezionata e non è attiva. Per selezionare la casella di controllo, fare clic sul pulsante **Espressione** (*fx*) e digitare **True** o creare un'espressione. La casella di controllo viene selezionata quando si fa clic su **OK** nella finestra di dialogo **Espressione** .  
  
 **Vai al segnalibro**  
 Selezionare questa opzione per definire un collegamento a un segnalibro nel report corrente. L'opzione aggiuntiva elencata di seguito viene visualizzata quando si seleziona **Vai al segnalibro**.  
  
 **Seleziona un segnalibro**  
 Digitare o selezionare l'ID del segnalibro del report a cui passare quando viene fatto clic sul collegamento. Fare clic sul pulsante Espressione (**fx**) per modificare l'espressione. L'ID del segnalibro può essere un ID statico oppure un'espressione che restituisce l'ID di un segnalibro. L'espressione può includere un campo contenente un ID del segnalibro.  
  
 Per creare un collegamento a un segnalibro, è innanzitutto necessario impostare la proprietà Bookmark di un elemento del report. Per impostare la proprietà Bookmark, selezionare un elemento del report e nel riquadro Proprietà digitare un valore o un'espressione per l'ID del segnalibro, ad esempio SalesChart o 5TopSales.  
  
 **Vai a URL**  
 Selezionare questa opzione per definire un collegamento a una pagina Web. Digitare o selezionare l'URL di una pagina Web o un'espressione che restituisca l'URL di una pagina Web. Fare clic sul pulsante **Espressione** (*fx*) per modificare l'espressione. L'espressione può includere un campo contenente un URL. L'opzione aggiuntiva elencata di seguito viene visualizzata quando si seleziona **Vai a URL**.  
  
 **Selezionare un URL**  
 Digitare o immettere l'URL dell'elemento. Per un elemento pubblicato in un server di report configurato per la modalità nativa, utilizzare un percorso completo o relativo. Ad esempio, http://*\<nomeserver >*  /Images/Image1.jpg. Per un elemento pubblicato in un server di report configurato in modalità integrata SharePoint, utilizzare un URL completo (ad esempio, http://*\<NomeServerSharePoint > /\<sito >*  /documenta/immagini / Image1).  
  
## <a name="see-also"></a>Vedere anche  
 [Grafici &#40;Generatore report e SSRS&#41;](report-design/charts-report-builder-and-ssrs.md)   
 [Guida di Generatore report per finestre di dialogo, riquadri e procedure guidate](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Parametri report &#40;Generatore report e Progettazione report&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [Aggiungere un sottoreport e parametri &#40;Generatore report e SSRS&#41;](report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [Ordinamento interattivo, mappe documento e collegamenti &#40;Generatore report e SSRS&#41;](report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)  
  
  
