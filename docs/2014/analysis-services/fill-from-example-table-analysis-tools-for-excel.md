---
title: Compilare da esempio (strumenti di analisi tabelle per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- fill from example
ms.assetid: dac57d8f-1c65-4878-8ea0-9c680df5e4fb
author: minewiskan
ms.author: owend
ms.openlocfilehash: f3894f8ea42c0c5c91c3b6a5c5e7a6677b763b02
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528347"
---
# <a name="fill-from-example-table-analysis-tools-for-excel"></a>Estendi da esempio (Strumenti di analisi tabelle per Excel)
  ![Pulsante Estendi da esempio in Strumenti di analisi tabelle](media/tat-fillex.gif "Pulsante Estendi da esempio in Strumenti di analisi tabelle")  
  
 Lo strumento **Compila da esempio** consente di compilare nuove colonne di dati in base ai valori esistenti.  
  
 Si supponga, ad esempio, che i dati contengano una colonna **importo acquisti** , una colonna **Orders Quantity** e una colonna **Customer Premier** basata su una formula che utilizza le altre colonne. Se nella colonna **Customer Premier** sono contenute molte righe vuote, è possibile utilizzare le colonne **purchase amount** e **Orders Quantity** come input per dedurre i valori mancanti. Lo strumento analizza modelli esistenti nei dati insieme agli esempi immessi e stima la categoria da assegnare a ogni cliente.  
  
 Se i risultati non sono soddisfacenti, è possibile migliorarli immettendo ulteriori esempi.  
  
## <a name="using-the-fill-from-example-tool"></a>Utilizzo dello strumento Estendi da esempio  
  
1.  Nella barra multifunzione **analizza** fare clic su **Compila da esempio**.  
  
2.  Tramite lo strumento viene automaticamente selezionata la colonna da compilare in base all'analisi dei dati ed è possibile accettare o ignorare il suggerimento.  
  
3.  Creare una colonna per i nuovi dati e digitare esempi dei valori che si desidera stimare. Verificare che sia presente almeno un esempio per ogni valore da stimare. Se si immettono i dati in una colonna esistente, selezionare la colonna con valori mancanti.  
  
4.  Facoltativamente, fare clic su **Scegli colonne da utilizzare nell'analisi**. Nella finestra di dialogo **Selezione colonne avanzate** specificare le colonne che più probabilmente saranno utili quando si compilano i dati mancanti.  
  
     Se, per esperienza, si sa che esiste un rapporto di causa-effetto tra una colonna e la colonna con valori mancanti, è possibile deselezionare le altre colonne per ottenere risultati migliori.  
  
     Fare clic su **OK**.  
  
5.  Fare clic su **Esegui**.  
  
     Al termine dell'analisi, lo strumento crea un nuovo foglio di **disegno** che contiene i risultati dell'analisi. Nel report vengono elencate le regole, o fattori di influenza chiave, trovati e viene visualizzata la probabilità per ogni regola.  
  
     Nella tabella dati originale viene aggiunta automaticamente una colonna contenente i nuovi valori. È possibile esaminare tali valori e confrontarli con l'originale.  
  
### <a name="requirements"></a>Requisiti  
 È possibile utilizzare lo strumento solo sui dati disponibili in colonne. Se la serie che si desidera completare è archiviata in una riga, è possibile utilizzare la funzionalità Incolla, Trasponi in Excel per convertire i dati nel formato a colonne.  
  
## <a name="understanding-the-pattern-report"></a>Informazioni sul report dei modelli  
 Quando si esegue lo strumento **Compila da esempio** , viene creato un report che fornisce ulteriori informazioni sui modelli rilevati. Questi modelli vengono utilizzati per estrapolare i nuovi valori dei dati.  
  
 Nel report dei modelli sono indicati i fattori di influenza chiave per ogni valore stimato. Ogni fattore di influenza o regola viene descritto come combinazione di colonna, valore della colonna e impatto relativo della regola sulla stima.  
  
 Ad esempio, se è necessario completare un foglio di lavoro che indica la distanza di spedizione per gli ordini, è prevedibile da un punto di vista logico che la destinazione abbia un impatto significativo sul valore della distanza di spedizione. In questo caso, il report potrebbe contenere la riga seguente:  
  
|Colonna|Valore|Predilige|Impatto relativo|  
|------------|-----------|------------|---------------------|  
|StateProvinceCode|AB|>500 chilometri|80%|  
  
 Questo significa che il valore AB nella colonna **StateProvinceCode** stima fortemente una distanza di spedizione di >500 chilometri.  
  
 Le stime sono in genere basate su modelli molto più complessi rispetto a questo esempio e il report potrebbe includere numerose righe di regole per ogni stima. Per derivare il valore stimato vengono combinati gli effetti di tutte le regole.  
  
> [!NOTE]  
>  L' **effetto relativo** viene visualizzato come una barra ombreggiata. Più lunga è la barra, maggiore è la probabilità che la regola sia predittiva per il valore inserito.  
  
 Lo strumento aggiunge anche una nuova colonna alla tabella dati originale, denominata \<column name> Extended.  
  
 Se la colonna dei dati originale contiene un valore, tale valore viene copiato nella nuova colonna. Se la colonna originale contiene una cella vuota, invece, la nuova colonna conterrà il valore stimato dalla procedura guidata.  
  
## <a name="related-tools-and-information"></a>Strumenti e informazioni correlati  
 È inoltre possibile utilizzare la procedura guidata [esplorazione dati](explore-data-sql-server-data-mining-add-ins.md) , disponibile nel client di data mining per Excel, per esaminare la distribuzione dei valori in una colonna di Excel. Per ulteriori informazioni, vedere [esplorazione e pulizia dei dati](exploring-and-cleaning-data.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)  
  
  
