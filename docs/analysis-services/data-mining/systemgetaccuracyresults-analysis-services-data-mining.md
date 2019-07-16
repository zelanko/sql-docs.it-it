---
title: SystemGetAccuracyResults (Analysis Services - Data Mining) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 54fc91b67a695110383c19422befab0d7b0f7a9d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209668"
---
# <a name="systemgetaccuracyresults-analysis-services---data-mining"></a>SystemGetAccuracyResults (Analysis Services - Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Restituisce la metrica di accuratezza per la convalida incrociata di una struttura di data mining e di tutti i modelli correlati, tranne i modelli di clustering.  
  
 Questa stored procedure restituisce la metrica per l'intero set di dati come un'unica partizione. Per partizionare il set di dati in sezioni trasversali e restituire la metrica per ogni partizione, usare [SystemGetCrossValidationResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Questa stored procedure non è supportata per i modelli compilati mediante l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering. Per i modelli di clustering, inoltre, usare la stored procedure separata [SystemGetClusterAccuracyResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SystemGetAccuracyResults(<mining structure>,   
[,<mining model list>]  
,<data set>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>Argomenti  
 *struttura di data mining*  
 Nome di una struttura di data mining nel database corrente.  
  
 (Obbligatorio)  
  
 *model list*  
 Elenco delimitato da virgole dei modelli da convalidare.  
  
 Il valore predefinito è **null**. In questo modo vengono utilizzati tutti i modelli applicabili. Se si utilizza l'impostazione predefinita, i modelli di clustering vengono esclusi automaticamente dall'elenco di candidati per l'elaborazione.  
  
 (Facoltativo)  
  
 *set di dati*  
 Valore integer che indica quale partizione nella struttura di data mining viene utilizzato per il test. Il valore è derivato da una maschera di bit che rappresenta la somma dei valori seguenti, dove qualsiasi singolo valore è facoltativo:  
  
|||  
|-|-|  
|Case di training|0x0001|  
|Test case|0x0002|  
|Filtro modello|0x0004|  
  
 Per un elenco completo dei valori possibili, vedere la sezione Osservazioni di questo argomento.  
  
 (obbligatorio)  
  
 *target attribute*  
 Stringa che contiene il nome di un oggetto stimabile. Un oggetto stimabile può essere una colonna, una colonna della tabella nidificata o una colonna chiave della tabella nidificata di un modello di data mining.  
  
 (obbligatorio)  
  
 *target state*  
 Stringa che contiene un valore specifico da stimare.  
  
 Se si specifica un valore, viene raccolta la metrica per tale stato specifico.  
  
 Se non si specifica alcun valore oppure si specifica un valore null, viene calcolata la metrica per lo stato più probabile per ogni stima.  
  
 Il valore predefinito è **null**.  
  
 (facoltativo).  
  
 *target threshold*  
 Numero compreso tra 0.0 e 1 che specifica la probabilità minima entro cui il valore della stima viene conteggiato come corretto.  
  
 Il valore predefinito è **null**, ovvero tutte le stime vengono conteggiate come corrette.  
  
 (facoltativo).  
  
 *test list*  
 Stringa che specifica le opzioni di testing. Questo parametro è riservato per usi futuri.  
  
 (facoltativo).  
  
## <a name="return-type"></a>Tipo restituito  
 Il set di righe restituito contiene punteggi per ogni partizione e aggregazioni per tutti i modelli.  
  
 Nella tabella seguente vengono elencate le colonne restituite da **GetValidationResults**.  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|Modello|Nome del modello sottoposto a test. **All** indica che il risultato è un'aggregazione per tutti i modelli.|  
|AttributeName|Nome della colonna stimabile.|  
|AttributeState|Valore di destinazione nella colonna stimabile.<br /><br /> Se questa colonna contiene un valore, la metrica viene raccolta solo per lo stato specifico.<br /><br /> Se questo valore non è specificato oppure è null, viene calcolata la metrica per lo stato più probabile per ogni stima.|  
|PartitionIndex|Indica la partizione a cui si applica il risultato.<br /><br /> Per questa procedura, è sempre 0.|  
|PartitionCases|Un intero che indica il numero di righe nel case set, in base il  *\<set di dati >* parametro.|  
|Test|Tipo di test eseguito.|  
|Misura|Nome della misura restituita dal test. Le misure per ogni modello dipendono dal tipo di modello e dal tipo del valore stimabile.<br /><br /> Per un elenco delle misure restituite per ogni tipo stimabile, vedere [Misure nel report di convalida incrociata](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).<br /><br /> Per la definizione delle diverse misure, vedere [Convalida incrociata &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).|  
|Value|Valore per la misura specificata.|  
  
## <a name="remarks"></a>Note  
 Nella tabella seguente vengono forniti esempi dei valori che è possibile utilizzare per specificare i dati nella struttura di data mining utilizzata per la convalida incrociata. Se si desidera utilizzare test case per la convalida incrociata, è necessario che la struttura di data mining contenga già un set di dati di testing. Per informazioni sulla definizione di un set di dati di testing quando si crea una struttura di data mining, vedere [Set di dati di training e di testing](../../analysis-services/data-mining/training-and-testing-data-sets.md).  
  
|Valore integer|Descrizione|  
|-------------------|-----------------|  
|1|Vengono utilizzati solo i case di training.|  
|2|Vengono utilizzati solo i test case.|  
|3|Vengono utilizzati sia i case di training sia i test case.|  
|4|Combinazione non valida.|  
|5|Vengono utilizzati i case di training e viene applicato il filtro del modello.|  
|6|Vengono utilizzati solo i test case e viene applicato il filtro del modello.|  
|7|Vengono utilizzati sia i case di training sia i test case e viene applicato il filtro del modello.|  
  
 Per altre informazioni sugli scenari in cui è possibile usare la convalida incrociata, vedere [Test e convalida &#40;Data mining&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md).  
  
## <a name="examples"></a>Esempi  
 Questo esempio restituisce le misure di accuratezza per un singolo modello di albero delle decisioni, ovvero `v Target Mail DT`, associato alla struttura di data mining `vTargetMail` . Il codice nella quarta riga indica che i risultati devono essere basati sui test case, filtrati per ogni modello per il filtro specifico di tale modello.  `[Bike Buyer]` specifica che la colonna deve essere stimata e il numero 1 nella riga successiva indica che il modello deve essere valutato solo per il valore 1 specifico, indicando che l'acquisto verrà effettuato.  
  
 L'ultima riga del codice specifica che il valore soglia di stato corrisponde a 0.5. Ciò significa che le stime con una probabilità maggiore del 50 percento devono essere conteggiate come stime affidabili durante il calcolo dell'accuratezza.  
  
```  
CALL SystemGetAccuracyResults (  
[vTargetMail],  
[vTargetMail DT],  
6,  
'Bike Buyer',  
1,  
0.5  
)  
```  
  
 Risultati dell'esempio:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Test|Misura|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|v Target Mail DT|Bike Buyer|1|0|1638|classificazione|Vero positivo|605|  
|v Target Mail DT|Bike Buyer|1|0|1638|classificazione|Falso positivo|177|  
|v Target Mail DT|Bike Buyer|1|0|1638|classificazione|Vero negativo|501|  
|v Target Mail DT|Bike Buyer|1|0|1638|classificazione|Falso negativo|355|  
|v Target Mail DT|Bike Buyer|1|0|1638|Probabilità|Punteggio in forma logaritmica|-0.598454638753028|  
|v Target Mail DT|Bike Buyer|1|0|1638|Probabilità|Accuratezza|0.0936717116894395|  
|v Target Mail DT|Bike Buyer|1|0|1638|Probabilità|Radice errore quadratico medio|0.361630800104946|  
  
## <a name="requirements"></a>Requisiti  
 La convalida incrociata è disponibile solo in [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] a partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [SystemGetCrossValidationResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
