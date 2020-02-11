---
title: 'Attività 2: test e pubblicazione dei criteri di corrispondenza | Microsoft Docs'
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: e1ffb6d7-fbc5-4695-b538-cc2302d1a17d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: a9957625e09bde8bb733eca6e564dfdcfbb0bd98
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484733"
---
# <a name="task-2-testing-and-publishing-the-matching-policy"></a>Attività 2: Test e pubblicazione dei criteri di corrispondenza
  In questa attività viene testato e pubblicato il criterio di corrispondenza **Rimuovi fornitori duplicati** .  
  
1.  Nella pagina **Risultati corrispondenza** fare clic su **Avvia** per testare l'intero criterio. Nel caso in questione, si dispone di una sola regola nei criteri, pertanto i risultati del test della regola e dei criteri devono essere uguali.  
  
2.  Controllare tutti i record corrispondenti e il punteggio di corrispondenza nella casella di riepilogo. Un record a cui è associata un'icona **verde** è un duplicato del record pivot che lo precede. Di seguito sono riportati un paio di esempi:  
  
    1.  Il record con **ID record: 1000005** è una corrispondenza del record con **id record: 1000004** con **Punteggio: 100%** perché entrambi i record hanno gli stessi valori per le colonne **SupplierID (prerequisite)**, **Supplier Name**e **ContactEmailAddress**. In DQS la selezione di un record come record pivot per un cluster viene eseguita in modo casuale.  
  
    2.  Il record **1000023** è una corrispondenza del record **1000022** con il punteggio corrispondente: 93% perché i due record hanno gli stessi valori per le colonne **SupplierID (prerequisite)** e **Supplier Name** , ma valori diversi per la colonna **ContactEmailAddress** .  
  
    3.  Scorrere fino alla fine dell'elenco per visualizzare due record con ID record: **1000051** e **1000052**. Il **Record 1000052** è considerato una corrispondenza con punteggio **corrispondente 91%** perché i due record hanno gli stessi valori per le colonne **SupplierID** e **ContactEmailAddress** , ma valori diversi per la colonna **Supplier Name** .  
  
     ![Definizione dei criteri- Risultati dei criteri](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-01.jpg "Definizione dei criteri- Risultati dei criteri")  
  
3.  Fare clic con il pulsante destro del mouse su qualsiasi record corrispondente (con icona verde) e fare clic su **Visualizza dettagli** per visualizzare altri dettagli sulla corrispondenza, ad esempio il contributo di ciascun punteggio del campo al Punteggio di corrispondenza complessivo.  
  
     ![Finestra di dialogo Dettagli punteggio corrispondente](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-02.jpg "Finestra di dialogo Dettagli punteggio corrispondente")  
  
4.  Fare clic su **Chiudi** per chiudere la finestra di dialogo **Dettagli punteggio corrispondente** .  
  
5.  Fare clic sulla scheda **Risultati corrispondenza** nella parte inferiore della pagina. In questa scheda vengono visualizzati dettagli quali il numero di record corrispondenti, il numero di record non corrispondenti, il numero di cluster con record corrispondenti e le dimensioni medie, minime e massime del cluster. Per altri dettagli, vedere [creare criteri di corrispondenza](https://msdn.microsoft.com/library/hh270290.aspx) . Non è possibile esportare i risultati di questa attività. Si sta definendo solo un criterio di corrispondenza utilizzando i dati di esempio per testare le regole e i criteri nei dati di esempio.  
  
     ![Scheda Risultati corrispondenza](../../2014/tutorials/media/et-testingandpublishingthematchingpolicy-03.jpg "Scheda Risultati corrispondenza")  
  
6.  Fare clic su **fine** per completare la creazione dei criteri di corrispondenza.  
  
    > [!NOTE]  
    >  Sono stati definiti i criteri di corrispondenza, pertanto non è possibile esportare i risultati in un file di output. Fondamentalmente, è stato utilizzato un file di input di esempio, sono state create regole e sono stati testati criteri e regole nei dati di esempio con l'obiettivo di definire i criteri.  
  
7.  Nella finestra di dialogo SQL Server Data Quality Services fare clic su **pubblica** e quindi su **OK** nella finestra di messaggio. A questo punto, i criteri di corrispondenza definiti verranno pubblicati nella Knowledge base **Suppliers** . È possibile utilizzare la Knowledge Base per eseguire il processo di corrispondenza in un file di input per identificare e rimuovere duplicati.  
  
## <a name="next-step"></a>passaggio successivo  
 [Attività 3: Creazione ed esecuzione di un progetto Data Quality per la corrispondenza](../../2014/tutorials/task-3-creating-and-running-a-data-quality-project-for-matching.md)  
  
  
