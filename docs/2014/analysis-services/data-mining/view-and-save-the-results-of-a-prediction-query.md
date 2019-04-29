---
title: Visualizzare e salvare i risultati di una Query di stima | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0273919410b5b182b535b805922ec39cdd82d6e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62733739"
---
# <a name="view-and-save-the-results-of-a-prediction-query"></a>Visualizzare e salvare i risultati di una query di stima
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Dopo aver definito una query in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante il generatore delle query di stima, è possibile eseguire la query e visualizzare i risultati passando alla visualizzazione dei risultati della query.  
  
 È possibile salvare i risultati di una query di stima in una tabella inclusa in qualsiasi origine dati definita in un progetto di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . È possibile creare una nuova tabella oppure salvare i risultati della query in una tabella esistente. Se si salvano i risultati in una tabella esistente, è possibile scegliere di sovrascrivere i dati attualmente archiviati nella tabella. Altrimenti, i risultati della query verranno accodati ai dati esistenti nella tabella.  
  
### <a name="run-a-query-and-view-the-results"></a>Eseguire una query e visualizzare i risultati  
  
1.  Sulla barra degli strumenti della scheda **Stima modello di data mining** di Progettazione modelli di data mining in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic su **Risultato** .  
  
     Verrà aperta la visualizzazione dei risultati della query, tramite cui verrà eseguita la query. I risultati verranno visualizzati in una griglia nel visualizzatore.  
  
### <a name="save-the-results-of-a-prediction-query-to-a-table"></a>Salvare i risultati di una query di stima in una tabella  
  
1.  Sulla barra degli strumenti della scheda **Stima modello di data mining** di Progettazione modelli di data mining fare clic su **Salva risultati query**.  
  
     Verrà visualizzata la finestra di dialogo **Salva risultati query di data mining** .  
  
2.  Selezionare un'origine dati nell'elenco **Origine dati** oppure fare clic su **Nuova** per creare una nuova origine dati.  
  
3.  Nella casella **Nome tabella** immettere il nome della tabella. Se la tabella esiste già, selezionare **Sovrascrivi se esistente** per sostituire il contenuto della tabella con i risultati della query. Se non si desidera sovrascrivere il contenuto della tabella, non selezionare questa casella di controllo. I nuovi risultati della query verranno accodati ai dati esistenti nella tabella.  
  
4.  Selezionare una vista origine dati in **Aggiungi a vista origine dati** se si desidera aggiungere la tabella a una vista origine dati.  
  
5.  Fare clic su **Salva**.  
  
    > [!WARNING]  
    >  Se la destinazione non supporta set di righe gerarchici, è possibile aggiungere la parola chiave FALTTENED ai risultati per effettuare il salvataggio come tabella flat.  
  
  
