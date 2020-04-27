---
title: 'Lezione 2: pulizia dei dati fornitore mediante la Knowledge Base Suppliers | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 215c14de-fc3f-46de-a022-bf69b9ea2a96
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: b99676a9f51bf76dc9db294365a5a628dd25fa2e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "65488478"
---
# <a name="lesson-2-cleansing-supplier-data-using-the-suppliers-knowledge-base"></a>Lezione 2: Pulizia dei dati fornitore tramite la Knowledge Base Suppliers
  In questa lezione vengono puliti i dati del fornitore in un file di Excel utilizzando la Knowledge base **Suppliers** creata nella prima lezione. La pulizia dei dati in DQS comprende un **processo computerizzato** che analizza il modo in cui i dati sono conformi alle informazioni in una Knowledge base e un **processo interattivo** che consente di esaminare e modificare i risultati del processo assistito da computer. Tramite la funzionalità di pulizia dei dati vengono identificati i dati errati nell'origine dati e, successivamente, vengono corretti o vengono forniti suggerimenti di correzione. Vengono inoltre standardizzati e arricchiti i dati dei clienti utilizzando i valori di dominio, i valori iniziali per sinonimi, le regole di dominio, le relazioni basate su termini e i dati di riferimento. È possibile approvare o rifiutare in modo interattivo le modifiche proposte dal processo computerizzato. Per ulteriori informazioni, vedere [pulizia dei dati](https://msdn.microsoft.com/library/gg524800.aspx) .  
  
 Nel processo computerizzato vengono utilizzati i seguenti valori soglia che è possibile configurare utilizzando l'apposita opzione nella pagina principale del client DQS.  
  
-   **Punteggio minimo per suggerimenti:** Punteggio minimo o livello di confidenza utilizzato da DQS per suggerire la sostituzione di un valore.  
  
-   **Punteggio minimo per correzioni automatiche:** Punteggio minimo o livello di confidenza utilizzato da DQS per correggere automaticamente un valore.  
  
 Per informazioni dettagliate su come configurare queste impostazioni, vedere [configurare i valori soglia per la pulizia e la corrispondenza](https://msdn.microsoft.com/library/hh510415.aspx) .  
  
 In questa lezione vengono effettuate le attività seguenti per pulire i dati di input utilizzando la Knowledge Base Suppliers.  
  
1.  Creare un progetto Data Quality per la pulizia, selezionare la Knowledge Base Suppliers come quella da utilizzare per analizzare e pulire i dati di origine in un file di Excel e selezionare l'attività di pulizia.  
  
2.  Eseguire il mapping delle colonne di Excel che si desidera pulire ai domini DQS singoli/composti appropriati nella Knowledge Base.  
  
3.  Eseguire l'attività di pulizia computerizzata. Tramite il processo computerizzato vengono visualizzate informazioni sulla qualità dei dati nel client Data Quality che possono essere utilizzate per pulire i dati in modo interattivo.  
  
4.  Visualizzare e gestire i risultati dell'attività di pulizia. È possibile esaminare i valori rilevati dal processo computerizzato come corretti, errati ma a cui è stata apportata una correzione, errati con un suggerimento di modifica o non validi. È possibile approvare o rifiutare in modo interattivo le modifiche correggendo o eseguendo l'override dei suggerimenti forniti dal processo computerizzato mediante il campo Correggi in.  
  
5.  Esportare i risultati dal processo di pulizia in un file di Excel.  
  
6.  Importare i valori dal progetto di pulizia in domini per ampliare le informazioni della Knowledge base con nuove regole, valori, correzioni e così via.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 1: Creazione di un progetto Data Quality](../../2014/tutorials/task-1-creating-a-data-quality-project.md)  
  
  
