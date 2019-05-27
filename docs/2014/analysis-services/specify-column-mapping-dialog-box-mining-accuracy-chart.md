---
title: Impostazione Mapping (grafico di accuratezza) finestra di dialogo colonne | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.coltotablecolmapping.f1
ms.assetid: 68e9e2d2-173f-4363-a515-fc60bfee3af0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4416a51ea32500d56c209d745065da20bf8010c9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66068415"
---
# <a name="specify-column-mapping-dialog-box-mining-accuracy-chart"></a>Finestra di dialogo Impostazione mapping colonne (Grafico accuratezza modello di data mining)
  Usare la scheda **Impostazione mapping colonne** per selezionare tabelle da un'origine dati esterna ed eseguire il mapping delle colonne a un modello di data mining. È quindi possibile utilizzare i dati esterni per eseguire il test dell'accuratezza di un modello di data mining e visualizzare i risultati nel grafico di accuratezza.  
  
 **Per ulteriori informazioni:** [Test e convalida &#40;Data mining&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>Opzioni  
 **Struttura di data mining**  
 Consente di visualizzare la struttura di data mining selezionata contenente il modello di cui verrà eseguito il test.  
  
 **Seleziona struttura**  
 Fare clic per aprire la finestra di dialogo **Seleziona struttura di data mining** e selezionare una struttura di data mining diversa.  
  
 **Seleziona tabella/e di Input**  
 Consente di visualizzare le tabelle di input selezionate che sono utilizzate per la creazione del grafico di accuratezza. Selezionare la tabella che contiene i dati di test da utilizzare per verificare l'accuratezza dei modelli.  
  
> [!NOTE]  
>  Se il riquadro non contiene alcuna tabella, fare clic su **Seleziona tabella del case** per aggiungere tabelle da una vista origine dati.  
  
 **Rimuovi tabella**  
 Consente di rimuovere la tabella selezionata. Questo pulsante è disabilitato se non è stata selezionata una tabella oppure se nell'elenco **Seleziona tabella/e di input** non ne viene visualizzata alcuna.  
  
 **Seleziona tabella del Case**  
 Fare clic per aprire la finestra di dialogo **Seleziona tabella** e selezionare una vista origine dati.  
  
 **Nota** Questo pulsante viene visualizzato solo se non è stata selezionata una tabella del case. Per attivare il pulsante in modo da selezionare una diversa tabella del case, cancellare l'elenco selezionando tutte le tabelle esistenti e facendo clic su **Rimuovi tabella**.  
  
 **Seleziona tabella nidificata**  
 Consente di aprire la finestra di dialogo **Seleziona tabella** . Questo pulsante viene visualizzato solo se è stata selezionata una tabella del case. Se nella struttura di data mining associata non è inclusa una tabella nidificata, il pulsante è disabilitato.  
  
 **Modifica Join**  
 Consente di aprire la finestra di dialogo **Specifica join nidificato** . Questo pulsante è attivo solo se si seleziona una tabella nidificata.  
  
## <a name="see-also"></a>Vedere anche  
 [Test e convalida le attività e procedure relative alla &#40;Data Mining&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Finestra di progettazione grafico accuratezza di data mining &#40;Data Mining&#41;](mining-accuracy-chart-designer-data-mining.md)  
  
  
