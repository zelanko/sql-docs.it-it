---
title: Creare una tabella calcolata nei modelli tabulari di Analysis Services | Microsoft Docs
ms.date: 12/19/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 199096efcdf9212e19e1055f1276079eddfb1a75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62469372"
---
# <a name="create-a-calculated-table"></a>Creare una tabella calcolata 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Una *tabella calcolata* è un oggetto calcolato, basato su una query o un'espressione DAX, derivato per intero o in parte da altre tabelle nello stesso modello.  
  
 Un problema di progettazione comune che possono risolvere le tabelle calcolate è esporre una dimensione con ruoli multipli in un contesto specifico in modo che sia possibile esporla come struttura di query nelle applicazioni client.  Si ricorderà che una dimensione con ruoli multipli è semplicemente una tabella esposta in più contesti. Un esempio classico è la tabella Data, esposta come DataOrdine, DataSpedizione o DataScadenza, in base alla relazione di chiave esterna. Creando una tabella calcolata per DataSpedizione in modo esplicito, è possibile ottenere una tabella autonoma disponibile per le query, utilizzabile in modo completo come qualsiasi altra tabella. Un altro uso include la configurazione di un set filtrato di righe, un subset o superset di colonne da altre tabelle esistenti. Questo consente di mantenere la tabella originale intatta e di creare allo stesso tempo varianti della tabella per supportare scenari specifici.  
  
 Per un uso ottimale delle tabelle calcolate è necessario conoscere i principi di base delle espressioni DAX. Quando si lavora con le espressioni per la tabella, può essere utile sapere che una tabella calcolata contiene una singola partizione con un'origine DAXSource, in cui l'espressione è un'espressione DAX.  
Esiste una sola CalculatedTableColumn per ogni colonna restituita dall'espressione, dove SourceColumn è il nome della colonna restituita (in modo analogo a DataColumn nelle tabelle non calcolate). 

Almeno una tabella deve già esistere prima di poter creare una tabella calcolata. Se si sta creando una tabella calcolata come oggetto autonomo nella tabella calcolata, è possibile creare prima di tutto una tabella eseguendo un'importazione da un'origine dati di file (csv, xls, xml). Il file importato da può avere una singola colonna e un singolo valore. È quindi possibile nascondere tale tabella. 
  
## <a name="how-to-create-a-calculated-table"></a>Come creare una tabella calcolata  
  
1.  In primo luogo, verificare che il modello tabulare abbia un livello di compatibilità di 1200 o superiore. È possibile controllare la proprietà **Livello di compatibilità** nel modello in SSDT.  
  
2.  Passare alla vista dati. Non è possibile creare una tabella calcolata nelle vista diagramma.  
  
3.  Selezionare **Tabella** > **Nuova tabella calcolata**.  
  
4.  Digitare o incollare un'espressione DAX (vedere di seguito per alcune idee).  
  
5.  Assegnare un nome alla tabella.  
  
6.  Creare relazioni con altre tabelle nel modello. Visualizzare [creare una relazione tra due tabelle](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md) se occorre assistenza per questo passaggio.  
  
7.  Fare riferimento alla tabella nei calcoli o nelle espressioni nel modello o usare la funzionalità **Analizza in Excel** per l'esplorazione dei dati ad hoc.  
  
### <a name="replicate-a-role-playing-dimension"></a>Replicare una dimensione con ruoli multipli  
 Nella barra della formula immettere una formula DAX che recupera una copia di un'altra tabella. Dopo il popolamento della tabella calcolata, assegnarle un nome descrittivo e quindi impostare una relazione che usa la chiave esterna specifica per il ruolo. Nel database Adventure Works, ad esempio, si potrebbe creare una tabella calcolata per Due Date e usare DueDateKey come base per una relazione con la tabella dei fatti.  
  
```  
=DimDate  
```  
  
### <a name="summarized-or-filtered-dataset"></a>Set di dati riepilogato o filtrato  
 Nella barra della formula immettere un'espressione DAX che consente di filtrare, riepilogare e modificare in altri modi un set di dati in modo che contenga le righe desiderate. Questo esempio raggruppa le vendite per colore e valuta.  
  
```  
=SUMMARIZECOLUMNS(DimProduct[Color]  
, DimCurrency[CurrencyName]   
, "Sales" , SUM(FactInternetSales[SalesAmount])  
)  
```  
  
### <a name="superset-using-columns-from-multiple-tables"></a>Superset che usa le colonne da più tabelle  
 Nella barra della formula immettere un'espressione DAX che combina le colonne da più tabelle. In questo caso, l'output della query elenca la categoria di prodotto per ogni valuta.  
  
```  
=CROSSJOIN(DimProductCategory, DimCurrency)  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Livello di compatibilità](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Data Analysis Expressions &#40;DAX&#41; in Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5)   
 [La comprensione di DAX nei modelli tabulari](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)  
  
  
