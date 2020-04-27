---
title: Usare funzioni di aggregazione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- aggregate functions [Analysis Services]
ms.assetid: c42166ef-b75c-45f4-859c-09a3e9617664
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4c8d65325f8008756a65a584a2538b9d56ebd579
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66072721"
---
# <a name="use-aggregate-functions"></a>Utilizzare le funzioni di aggregazione
  Quando una dimensione viene usata per sezionare una misura, la misura viene riepilogata in base alle gerarchie contenute in tale dimensione. Il comportamento della somma dipende dalla funzione di aggregazione specificata per la misura. Per la maggior parte delle misure contenenti dati numerici, la funzione di aggregazione è `Sum`. Il valore della misura sarà la somma di quantità diverse a seconda di quale sarà il livello della gerarchia attivo.  
  
 In Analysis Services, ogni misura creata è supportata da una funzione di aggregazione che determina l'operazione della misura. I tipi di aggregazione `Sum`predefiniti `Min`includono `Max`, `Count`,,, **Distinct Count**e molte altre funzioni più specializzate. In alternativa, se sono necessarie aggregazioni basate su formule complesse o personalizzate, è possibile creare un calcolo MDX anziché una funzione di aggregazione predefinita. Se ad esempio si vuole definire una misura per un valore percentuale, si procede in MDX, usando una misura calcolata. Vedere [Istruzione CREATE MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member).  
  
 Le misure create tramite la Creazione guidata cubo vengono assegnate a un tipo di aggregazione come parte della definizione della misura. Il tipo di aggregazione è sempre `Sum`, supponendo che la colonna di origine contenga dati numerici. `Sum`viene assegnato a prescindere dal tipo di dati della colonna di origine. Se ad esempio si usa la Creazione guidata cubo per creare misure, e si inseriscono tutte le colonne di una tabella dei fatti, si noterà che tutte le misure risultanti presentano un'aggregazione di `Sum`, anche se l'origine è una colonna data e ora. Controllare sempre i metodi di aggregazione pre-assegnati per le misure create tramite la procedura guidata, per assicurarsi che la funzione di aggregazione sia adatta.  
  
 È possibile assegnare o modificare il metodo di aggregazione sia nella definizione del cubo, tramite [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)], sia tramite MDX. Per altre istruzioni, vedere [Creare misure e gruppi di misure nei modelli multidimensionali](create-measures-and-measure-groups-in-multidimensional-models.md) o [Aggregate &#40;MDX&#41;](/sql/mdx/aggregate-mdx).  
  
##  <a name="aggregate-functions"></a><a name="AggFunction"></a>Funzioni di aggregazione  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] fornisce funzioni per aggregare misure insieme alle dimensioni contenute in gruppi di misure. L' *additività* di una funzione di aggregazione determina la modalità di aggregazione della misura in tutte le dimensioni del cubo. Le funzioni di aggregazione presentano tre livelli di additività:  
  
 Additive  
 Una misura additiva, definita anche misura completamente additiva, può essere aggregata in tutte le dimensioni incluse nel gruppo di misure contenente la misura, senza restrizioni.  
  
 Semiadditive  
 Una misura semiadditiva può essere aggregata in alcune ma non in tutte le dimensioni incluse nel gruppo contenente la misura. Una misura che rappresenta ad esempio la quantità disponibile di scorte può essere aggregata in una dimensione di tipo Geografia per produrre una quantità totale disponibile per tutti i magazzini, ma non può essere aggregata in una dimensione temporale perché rappresenta uno snapshot periodico di quantità disponibili. L'aggregazione di tale misura in una dimensione temporale genererebbe risultati non corretti. Per informazioni dettagliate, vedere [Definire una funzione semiadditiva](define-semiadditive-behavior.md) .  
  
 Nonadditive  
 Una misura non additiva non può essere aggregata in alcuna dimensione inclusa nel gruppo contenente la misura. La misura deve essere invece calcolata singolarmente per ogni cella inclusa nel cubo che rappresenta la misura. Una misura calcolata che restituisce una percentuale, quale un margine di profitto, non può ad esempio essere aggregata dai valori della percentuale dei membri figlio in alcuna dimensione.  
  
 Nella tabella seguente vengono elencate le funzioni di aggregazione disponibili in [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]e vengono descritti sia il livello di additività che l'output previsto della funzione.  
  
|Funzione di aggregazione|additività|Valore restituito|  
|--------------------------|----------------|--------------------|  
|`Sum`|Additive|Calcola la somma dei valori per tutti i membri figlio. Si tratta della funzione di aggregazione predefinita.|  
|`Count`|Additive|Recupera il numero di tutti i membri figlio.|  
|`Min`|Semiadditive|Recupera il valore minimo per tutti i membri figlio.|  
|`Max`|Semiadditive|Recupera il valore massimo per tutti i membri figlio.|  
|`DistinctCount`|Nonadditive|Recupera il numero di tutti i membri figlio univoci. Per altri dettagli, vedere [Informazioni sulle misure totale valori distinti](use-aggregate-functions.md#bkmk_distinct) nella sezione successiva.|  
|`None`|Nonadditive|Non viene eseguita alcuna aggregazione e tutti i valori per i membri foglia e non foglia in una dimensione vengono specificati direttamente dalla tabella dei fatti per il gruppo di misure contenente la misura. Se non è possibile leggere alcun valore dalla tabella dei fatti per un membro, il valore per il membro è impostato su Null.|  
|`ByAccount`|Semiadditive|Calcola l'aggregazione in base alla funzione di aggregazione assegnata al tipo di conto per un membro in una dimensione di tipo Conti. Se nel gruppo di misure non è presente alcuna dimensione di tipo Conti, deve essere considerata come la funzione di aggregazione `None`.<br /><br /> Per altre informazioni sulle dimensioni di tipo Conti, vedere [Creare un conto finanziario della dimensione di tipo padre-figlio](database-dimensions-finance-account-of-parent-child-type.md).|  
|`AverageOfChildren`|Semiadditive|Calcola la media dei valori per tutti i membri figlio non vuoti.|  
|`FirstChild`|Semiadditive|Recupera il valore del primo membro figlio.|  
|`LastChild`|Semiadditive|Recupera il valore dell'ultimo membro figlio.|  
|`FirstNonEmpty`|Semiadditive|Recupera il valore del primo membro figlio non vuoto.|  
|`LastNonEmpty`|Semiadditive|Recupera il valore dell'ultimo membro figlio non vuoto.|  
  
##  <a name="about-distinct-count-measures"></a><a name="bkmk_distinct"></a> Informazioni sulle misure totale valori distinti  
 Una misura con il valore della proprietà **Funzione di aggregazione** impostato su **Totale valori distinti** viene denominata misura totale valori distinti. Una misura totale valori distinti può essere usata per conteggiare le occorrenze dei membri di livello più basso di una dimensione nella tabella dei fatti. Poiché si tratta di un conteggio di valori distinti, un membro con più occorrenze viene conteggiato una sola volta. Una misura totale valori distinti viene sempre inserita in un gruppo di misure dedicato. L'inserimento di una misura totale valori distinti nel proprio gruppo di misure è una procedura consigliata che è stata creata nella finestra di progettazione come tecnica di ottimizzazione delle prestazioni.  
  
 Le misure totale valori distinti vengono in genere usate per determinare per ogni membro di una dimensione il numero dei membri distinti di livello più basso di un'altra dimensione che condividono righe nella tabella dei fatti. In un cubo Sales, ad esempio, è possibile determinare il numero di prodotti distinti acquistati per ogni cliente e gruppo di clienti, individuando per ogni membro della dimensione Customers il numero di membri distinti di livello più basso della dimensione Products che condividono righe nella tabella dei fatti. In un cubo Internet Site Visits, invece, è ad esempio possibile determinare il numero di pagine distinte visitate nel sito Internet, individuando per ogni membro della dimensione Site Visitors il numero di membri distinti di livello più basso della dimensione Pages che condividono righe nella tabella dei fatti. In ognuno di questi esempi, i membri di livello più basso della seconda dimensione vengono conteggiati mediante una misura totale valori distinti.  
  
 Questo tipo di analisi non deve necessariamente essere limitata a due dimensioni. Una misura totale valori distinti può infatti essere separata e sezionata con qualsiasi combinazione di dimensioni del cubo, inclusa la dimensione contenente i membri conteggiati.  
  
 Una misura totale valori distinti con conteggio dei membri è basata su una colonna chiave esterna nella tabella dei fatti, identificata dalla proprietà **Colonna di origine** della misura. Questa colonna viene unita in join alla colonna della tabella della dimensione che identifica i membri conteggiati mediante la misura totale valori distinti.  
  
## <a name="see-also"></a>Vedi anche  
 [Misure e gruppi di misure](measures-and-measure-groups.md)   
 [Guida di riferimento alle funzioni MDX &#40;&#41;MDX](/sql/mdx/mdx-function-reference-mdx)   
 [Definire una funzione semiadditiva](define-semiadditive-behavior.md)  
  
  
