---
title: Selezionare DISTINCT FROM &lt;Model &gt; (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 67ed5236aad0549fa6850114280ee15d8cebcaeb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892537"
---
# <a name="select-distinct-from-ltmodel-gt-dmx"></a>Selezionare DISTINCT FROM &lt;Model &gt; (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Restituisce tutti gli stati possibili della colonna selezionata nel modello. I valori restituiti variano a seconda che la colonna specificata contenga valori discreti, valori numerici discretizzati o valori numerici continui.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SELECT [FLATTENED] DISTINCT [TOP <n>] <expression list> FROM <model>   
[WHERE <condition list>][ORDER BY <expression>]  
```  
  
## <a name="arguments"></a>Argomenti  
 *n*  
 Facoltativa. Valore intero che specifica il numero di righe da restituire.  
  
 *elenco di espressioni*  
 Elenco delimitato da virgole contenente espressioni o identificatori di colonne correlate (derivati dal modello).  
  
 *model*  
 Identificatore del modello.  
  
 *Elenco condizioni*  
 Condizione per limitare i valori restituiti dall'elenco di colonne.  
  
 *espressione*  
 Facoltativa. Espressione che restituisce un valore scalare.  
  
## <a name="remarks"></a>Osservazioni  
 L'istruzione **SELECT DISTINCT from** funziona solo con una singola colonna o con un set di colonne correlate. Non è possibile utilizzare questa clausola con un set di colonne non correlate.  
  
 L'istruzione **SELECT DISTINCT from** consente di fare riferimento direttamente a una colonna all'interno di una tabella nidificata. Ad esempio:  
  
```  
<model>.<table column reference>.<column reference>  
```  
  
 I risultati dell'istruzione **SELECT DISTINCT FROM \<Model>** variano a seconda del tipo di colonna. Nella tabella seguente sono descritti i tipi di colonna supportati e l'output dell'istruzione.  
  
|Tipo di colonna|Output|  
|-----------------|------------|  
|Discrete|Valori univoci nella colonna.|  
|Discretizzato|Punto medio di ogni bucket discretizzato nella colonna.|  
|Continuo|Punto medio dei valori nella colonna.|  
  
## <a name="discrete-column-example"></a>Esempio con una colonna discreta  
 L'esempio di codice seguente si basa sul `[TM Decision Tree]` modello creato nell' [esercitazione di base sul data mining](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). La query restituisce i valori univoci presenti nella colonna discreta `Gender`.  
  
```  
SELECT DISTINCT [Gender]  
FROM [TM Decision Tree]  
```  
  
 Risultati dell'esempio:  
  
|Sesso|  
|------------|  
||  
|F|  
|M|  
  
 Per le colonne che contengono valori discreti, i risultati includono sempre lo stato Missing, mostrato come valore null.  
  
## <a name="continuous-column-example"></a>Esempio con una colonna continua  
 L'esempio di codice seguente restituisce il punto medio e l'età massima e minima per tutti i valori nella colonna.  
  
```  
SELECT DISTINCT [Age] AS [Midpoint Age],   
    RangeMin([Age]) AS [Minimum Age],   
    RangeMax([Age]) AS [Maximum Age]  
FROM [TM Decision Tree]  
```  
  
 Risultati dell'esempio:  
  
|Midpoint Age|Minimum Age|Maximum Age|  
|------------------|-----------------|-----------------|  
||||  
|62|26|97|  
  
 La query restituisce inoltre una singola riga di valori null per rappresentare valori mancanti.  
  
## <a name="discretized-column-example"></a>Esempio con una colonna discretizzata  
 L'esempio di codice seguente restituisce i valori medio, massimo e minimo per ogni bucket creato dall'algoritmo per la colonna [`Yearly Income]`. Per riprodurre i risultati per questo esempio è necessario creare una nuova struttura di data mining che corrisponde a `[Targeted Mailing]`. Nella procedura guidata, modificare il tipo di contenuto della `Yearly Income` colonna da **continuo** a **discretizzazione**.  
  
> [!NOTE]  
>  È inoltre possibile modificare anche il modello di data mining creato nell'esercitazione di base sul data mining per discretizzare la colonna della struttura di data mining [`Yearly Income]`. Per informazioni su come eseguire questa operazione, vedere [modificare la discretizzazione di una colonna in un modello di data mining](https://docs.microsoft.com/analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model). Tuttavia, quando si modifica la discretizzazione della colonna, viene forzata la rielaborazione della struttura di data mining modificando i risultati degli altri modelli compilati utilizzando tale struttura.  
  
```  
SELECT DISTINCT [Yearly Income] AS [Bucket Average],   
    RangeMin([Yearly Income]) AS [Bucket Minimum],   
    RangeMax([Yearly Income]) AS [Bucket Maximum]  
FROM [TM Decision Tree]  
```  
  
 Risultati dell'esempio:  
  
|Bucket Average|Bucket Minimum|Bucket Maximum|  
|--------------------|--------------------|--------------------|  
||||  
|24610,7|10000|39221,41|  
|55115,73|39221,41|71010,05|  
|84821,54|71010,05|98633,04|  
|111633,9|98633,04|124634,7|  
|147317,4|124634,7|170000|  
  
 È possibile notare che i valori della colonna [Yearly Income] sono stati discretizzati in cinque bucket, più una riga aggiuntiva di valori null per rappresentare i valori mancanti.  
  
 Il numero di posizioni decimali nei risultati dipende dal client utilizzato per l'esecuzione delle query. Nell'esempio i risultati sono stati arrotondati a due posizioni decimali, sia per semplicità che per riflettere i valori visualizzati in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Ad esempio, se si esplora il modello mediante il visualizzatore Microsoft Decision Trees e si seleziona un nodo contenente i clienti raggruppati in base al reddito, nella descrizione comandi vengono visualizzate le seguenti proprietà del nodo:  
  
 Age >= 69 e Annual Income < 39221,41  
  
> [!NOTE]  
>  Il valore minimo del bucket minimo e il valore massimo del bucket massimo rappresentano i valori minimo e massimo osservati. Tutti i valori che non rientrano in questo intervallo osservato vengono considerati appartenenti ai bucket minimo e massimo.  
  
## <a name="see-also"></a>Vedere anche  
 [SELEZIONARE &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Le estensioni di data mining &#40;DMX&#41; le istruzioni di manipolazione dei dati](../dmx/dmx-statements-data-manipulation.md)   
 [Guida di riferimento alle istruzioni DMX&#41; &#40;di Data Mining Extensions](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
