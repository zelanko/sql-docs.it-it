---
title: Estendi da esempio (strumenti di analisi tabelle per Excel) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: d1e09e439469f23412c84ea7bab65c0aa748f286
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081323"
---
# <a name="fill-from-example-table-analysis-tools-for-excel"></a>Estendi da esempio (Strumenti di analisi tabelle per Excel)
  ![Pulsante Estendi da esempio in strumenti di analisi tabelle](media/tat-fillex.gif "pulsante Estendi da esempio in strumenti di analisi tabelle")  
  
 Il **Estendi da esempio** lo strumento consente di compilare nuove colonne di dati in base ai valori esistenti.  
  
 Ad esempio, si supponga che i dati contengono un **importo di acquisto** colonna, un **quantità ordini** colonna e un **clienti Premier** colonna che si basa su alcune formule utilizzando la altre colonne. Se il **clienti Premier** colonna contiene molte righe vuote, è possibile usare i **importo di acquisto** e **quantità ordini** colonne come input per dedurre i valori mancanti. Lo strumento analizza modelli esistenti nei dati insieme agli esempi immessi e stima la categoria da assegnare a ogni cliente.  
  
 Se i risultati non sono soddisfacenti, è possibile migliorarli immettendo ulteriori esempi.  
  
## <a name="using-the-fill-from-example-tool"></a>Utilizzo dello strumento Estendi da esempio  
  
1.  Nel **Analyze** sulla barra multifunzione, fare clic su **Estendi da esempio**.  
  
2.  Tramite lo strumento viene automaticamente selezionata la colonna da compilare in base all'analisi dei dati ed è possibile accettare o ignorare il suggerimento.  
  
3.  Creare una colonna per i nuovi dati e digitare esempi dei valori che si desidera stimare. Verificare che sia presente almeno un esempio per ogni valore da stimare. Se si immettono i dati in una colonna esistente, selezionare la colonna con valori mancanti.  
  
4.  Facoltativamente, fare clic su **scegliere le colonne da utilizzare nell'analisi**. Nel **selezione colonne avanzata** finestra di dialogo, specificare le colonne più probabilmente utili durante la compilazione dei dati mancanti.  
  
     Se, per esperienza, si sa che esiste un rapporto di causa-effetto tra una colonna e la colonna con valori mancanti, è possibile deselezionare le altre colonne per ottenere risultati migliori.  
  
     Fare clic su **OK**.  
  
5.  Fare clic su **Esegui**.  
  
     Quando l'analisi è stata completata, lo strumento crea un nuovo **modelli** foglio di lavoro contenente i risultati dell'analisi. Nel report vengono elencate le regole, o fattori di influenza chiave, trovati e viene visualizzata la probabilità per ogni regola.  
  
     Nella tabella dati originale viene aggiunta automaticamente una colonna contenente i nuovi valori. È possibile esaminare tali valori e confrontarli con l'originale.  
  
### <a name="requirements"></a>Requisiti  
 È possibile utilizzare lo strumento solo sui dati disponibili in colonne. Se la serie che si desidera completare è archiviata in una riga, è possibile utilizzare la funzionalità Incolla, Trasponi in Excel per convertire i dati nel formato a colonne.  
  
## <a name="understanding-the-pattern-report"></a>Informazioni sul report dei modelli  
 Quando si esegue la **Estendi da esempio** strumento, viene creato un report che fornisce ulteriori informazioni sui modelli che sono stati rilevati. Questi modelli vengono utilizzati per estrapolare i nuovi valori dei dati.  
  
 Nel report dei modelli sono indicati i fattori di influenza chiave per ogni valore stimato. Ogni fattore di influenza o regola viene descritto come combinazione di colonna, valore della colonna e impatto relativo della regola sulla stima.  
  
 Ad esempio, se è necessario completare un foglio di lavoro che indica la distanza di spedizione per gli ordini, è prevedibile da un punto di vista logico che la destinazione abbia un impatto significativo sul valore della distanza di spedizione. In questo caso, il report potrebbe contenere la riga seguente:  
  
|colonna|Value|Predilige|Impatto relativo|  
|------------|-----------|------------|---------------------|  
|StateProvinceCode|AB|> gt;500 chilometri|80%|  
  
 Ciò significa che il valore AB nella **StateProvinceCode** colonna fortemente consente di stimare una distanza di spedizione di > gt;500 chilometri.  
  
 Le stime sono in genere basate su modelli molto più complessi rispetto a questo esempio e il report potrebbe includere numerose righe di regole per ogni stima. Per derivare il valore stimato vengono combinati gli effetti di tutte le regole.  
  
> [!NOTE]  
>  **Impatto relativo** viene visualizzato come una barra ombreggiata. Più lunga è la barra, maggiore è la probabilità che la regola sia predittiva per il valore inserito.  
  
 Lo strumento aggiunge inoltre una nuova colonna alla tabella dati originale, denominata \<nome colonna > estesa.  
  
 Se la colonna dei dati originale contiene un valore, tale valore viene copiato nella nuova colonna. Se la colonna originale contiene una cella vuota, invece, la nuova colonna conterrà il valore stimato dalla procedura guidata.  
  
## <a name="related-tools-and-information"></a>Strumenti e informazioni correlati  
 È anche possibile usare la [Esplora dati](explore-data-sql-server-data-mining-add-ins.md) procedura guidata, disponibile nel Client di Data Mining per Excel, per esaminare la distribuzione dei valori in una colonna di Excel. Per altre informazioni, vedere [esplorazione e pulizia dei dati](exploring-and-cleaning-data.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)  
  
  
