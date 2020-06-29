---
title: Editor trasformazione aggregazione (scheda aggregazioni) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.aggregationtransformation.aggregations.f1
helpviewer_keywords:
- Aggregate Transformation Editor
ms.assetid: a01cb124-ec79-4673-b1a1-bf4d60ee1b45
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 59bf17aa0c13fcc771a75253d5ac9f46a160c57c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439508"
---
# <a name="aggregate-transformation-editor-aggregations-tab"></a>Editor trasformazione Aggregazione (scheda Aggregazioni)
  Usare la scheda **Aggregazioni** della finestra di dialogo **Editor trasformazione Aggregazione** per specificare le colonne per l'aggregazione e le proprietà di aggregazione. È possibile applicare più aggregazioni. Questa trasformazione non genera output degli errori.  
  
> [!NOTE]  
>  Le opzioni per il conteggio delle chiavi, la scala delle chiavi, il conteggio delle chiavi distinct e la scala delle chiavi distinct vengono applicate a livello di componente quando vengono specificate nella scheda **Avanzate** , a livello di output quando vengono specificate nella sezione delle opzioni avanzate della scheda **Aggregazioni** e a livello di colonna quando vengono specificate nell'elenco delle colonne nella parte inferiore della scheda **Aggregazioni** .  
>   
>  Nella trasformazione Aggregazione **Chiavi** e **Scala chiavi** fanno riferimento al numero di gruppi che dovrebbero risultare da un'operazione **Group by** . **Chiavi conteggio valori distinct** e **Scala conteggio valori distinct** fanno riferimento al numero di valori distinct che dovrebbero risultare da un'operazione **Distinct count** .  
  
 Per altre informazioni sulla trasformazione Aggregazione, vedere [Trasformazione Aggregazione](data-flow/transformations/aggregate-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Avanzate/Standard**  
 Consente di visualizzare o nascondere le opzioni per la configurazione di più aggregazioni per più output. Le opzioni avanzate sono nascoste per impostazione predefinita.  
  
 **Nome aggregazione**  
 Consente di digitare un nome descrittivo per l'aggregazione nella sezione delle opzioni avanzate.  
  
 **Colonne GROUP BY**  
 Nella sezione delle opzioni avanzate, selezionare le colonne da raggruppare usando l'elenco **Colonne di input disponibili** come descritto di seguito.  
  
 **Scala chiavi**  
 Nella sezione delle opzioni avanzate è inoltre possibile specificare il numero approssimativo di chiavi che possono essere scritte dall'aggregazione. Per impostazione predefinita, il valore di questa opzione è **Non specificata**. Se le proprietà **Scala chiavi** e **Chiavi** sono entrambe impostate, il valore della proprietà **Chiavi** ha la precedenza.  
  
|valore|Description|  
|-----------|-----------------|  
|Non specificata|La proprietà Scala chiavi non viene utilizzata.|  
|Basso|L'aggregazione può scrivere circa 500.000 chiavi.|  
|Media|L'aggregazione può scrivere circa 5.000.000 di chiavi.|  
|Alto|L'aggregazione può scrivere oltre 25.000.000 di chiavi.|  
  
 **Chiavi**  
 Nella sezione delle opzioni avanzate è inoltre possibile specificare il numero esatto di chiavi che possono essere scritte dall'aggregazione. Se le proprietà **Scala chiavi** e **Chiavi** sono entrambe specificate, la proprietà **Chiavi** ha la precedenza.  
  
 **Colonne di input disponibili**  
 Consente di selezionare le colonne di input nell'elenco delle colonne di input disponibili utilizzando le caselle controllo presenti nella tabella.  
  
 **Colonna di input**  
 Consente di selezionare una colonna di input nell'elenco delle colonne di input disponibili.  
  
 **Alias di output**  
 Consente di digitare un alias per ogni colonna. Per impostazione predefinita viene suggerito il nome della colonna di input. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
 **Operazione**  
 Selezionare un'operazione nell'elenco delle operazioni disponibili utilizzando la tabella seguente come guida.  
  
|Operazione|Descrizione|  
|---------------|-----------------|  
|**GroupBy**|Consente di dividere i set di dati in gruppi. Per il raggruppamento è possibile utilizzare colonne con qualsiasi tipo di dati. Per ulteriori informazioni, vedere GROUP BY.|  
|**Somma**|Consente di sommare i valori di una colonna. È possibile sommare solo le colonne con tipi di dati numerici. Per ulteriori informazioni, vedere SUM.|  
|**Media**|Consente di restituire la media dei valori di una colonna. È possibile calcolare la media soltanto delle colonne con tipi di dati numerici. Per ulteriori informazioni, vedere AVG.|  
|**Numero**|Consente di restituire il numero di elementi di un gruppo. Per ulteriori informazioni, vedere COUNT.|  
|**CountDistinct**|Consente di restituire il numero di valori non Null univoci di un gruppo. Per ulteriori informazioni, vedere COUNT e Distinct.|  
|**Minimo**|Restituisce il valore minimo in un gruppo. Limitata soltanto ai tipi di dati numerici.|  
|**Massimo**|Restituisce il valore massimo in un gruppo. Limitata soltanto ai tipi di dati numerici.|  
  
 **Flag di confronto**  
 Se si scegliere **Group By**, usare le caselle di controllo per controllare la modalità con cui la trasformazione esegue il confronto. Per altre informazioni sulle opzioni per il confronto di stringhe, vedere [Confronto di dati stringa](data-flow/comparing-string-data.md).  
  
 **Scala conteggio valori distinct**  
 È possibile specificare il numero approssimativo di valori distinct che l'aggregazione può scrivere. Per impostazione predefinita, il valore di questa opzione è **Non specificata**. Se `CountDistinctScale` vengono specificati sia che **CountDistinctKeys** , **CountDistinctKeys** avrà la precedenza.  
  
|valore|Description|  
|-----------|-----------------|  
|Non specificata|La proprietà `CountDistinctScale` non viene utilizzata.|  
|Basso|L'aggregazione può scrivere circa 500.000 valori distinct.|  
|Media|L'aggregazione può scrivere circa 5.000.000 di valori distinct.|  
|Alto|L'aggregazione può scrivere oltre 25.000.000 di valori distinct.|  
  
 **Chiavi conteggio valori distinct**  
 È possibile specificare il numero esatto di valori distinct che l'aggregazione può scrivere. Se `CountDistinctScale` vengono specificati sia che **CountDistinctKeys** , **CountDistinctKeys** avrà la precedenza.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor trasformazione aggregazione &#40;scheda Avanzate&#41;](../../2014/integration-services/aggregate-transformation-editor-advanced-tab.md)   
 [Aggregazione di valori in un set di dati utilizzando la trasformazione Aggregazione](data-flow/transformations/aggregate-values-in-a-dataset-by-using-the-aggregate-transformation.md)  
  
  
