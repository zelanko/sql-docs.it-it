---
title: 'Attività 2: Test e pubblicazione dei criteri di corrispondenza | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 21f0cf5a4d096bfa0f4b673fdd716e2e48ee1396
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63250288"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>Attività 2: Test e pubblicazione dei criteri di corrispondenza
  In questa attività viene testato e pubblicato le **Rimuovi fornitori duplicati** criteri di corrispondenza.  
  
1.  Nel **risultati corrispondenza** pagina, fare clic su **avviare** per testare tutti i criteri. Nel caso in questione, si dispone di una sola regola nei criteri, pertanto i risultati del test della regola e dei criteri devono essere uguali.  
  
2.  Controllare tutti i record corrispondenti e il punteggio di corrispondenza nella casella di riepilogo. Un record con un **verde** icona associato è un duplicato del record pivot che la precede. Di seguito sono riportati un paio di esempi:  
  
    1.  Il record con **ID Record: 1000005** è una corrispondenza del record con **Id Record: 1000004** con **punteggio: 100%** perché entrambi i record hanno gli stessi valori per **SupplierID (prerequisito)**, **Supplier Name**, e **ContactEmailAddress columns**. In DQS la selezione di un record come record pivot per un cluster viene eseguita in modo casuale.  
  
    2.  Il record **1000023** è una corrispondenza del record **1000022** con il punteggio di corrispondenza: 93% perché i due record hanno gli stessi valori per **SupplierID (prerequisito)** e **Supplier Name** colonne, ma valori diversi per il **ContactEmailAddress** colonna.  
  
    3.  Scorrere fino alla fine dell'elenco per visualizzare i due record con ID: **1000051** e **1000052**. Record **1000052** viene considerata una corrispondenza con punteggio di corrispondenza **91%** perché i due record hanno gli stessi valori per il **SupplierID** e  **ContactEmailAddress** colonne, ma valori diversi per il **Supplier Name** colonna.  
  
     ![Definizione di criteri - risultati dei criteri](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "definizione di criteri - risultati dei criteri")  
  
3.  Fare doppio clic su qualsiasi record corrispondente (con l'icona verde) e fare clic su **visualizzare i dettagli** per visualizzare altri dettagli sulla corrispondenza, ad esempio contributo di ogni campo di valutazione al punteggio di corrispondenza complessivo.  
  
     ![Punteggio di corrispondenza dei dettagli nella finestra di dialogo](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "punteggio di corrispondenza dei dettagli nella finestra di dialogo")  
  
4.  Fare clic su **chiudere** per chiudere la **Dettagli punteggio corrispondente** nella finestra di dialogo.  
  
5.  Fare clic su **risultati corrispondenza** scheda nella parte inferiore della pagina. In questa scheda vengono visualizzati dettagli quali il numero di record corrispondenti, il numero di record non corrispondenti, il numero di cluster con record corrispondenti e le dimensioni medie, minime e massime del cluster. Visualizzare [creare criteri di corrispondenza](https://msdn.microsoft.com/library/hh270290.aspx) per altri dettagli. Non è possibile esportare i risultati di questa attività. Si sta definendo solo un criterio di corrispondenza utilizzando i dati di esempio per testare le regole e i criteri nei dati di esempio.  
  
     ![Scheda risultati corrispondenza](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "scheda dei risultati di corrispondenza")  
  
6.  Fare clic su **fine** per completare la creazione dei criteri di corrispondenza.  
  
    > [!NOTE]  
    >  Sono stati definiti i criteri di corrispondenza, pertanto non è possibile esportare i risultati in un file di output. Fondamentalmente, è stato utilizzato un file di input di esempio, sono state create regole e sono stati testati criteri e regole nei dati di esempio con l'obiettivo di definire i criteri.  
  
7.  Nella finestra di dialogo di SQL Server Data Quality Services, fare clic su **Publish** e fare clic su **OK** nella finestra di messaggio. A questo punto, i criteri di corrispondenza definiti vengono pubblicati nella **Suppliers** Knowledge Base. È possibile utilizzare la Knowledge Base per eseguire il processo di corrispondenza in un file di input per identificare e rimuovere duplicati.  
  
## <a name="next-step"></a>Passaggio successivo  
 [Attività 3: Creazione ed esecuzione di un progetto Data Quality per la corrispondenza](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  
