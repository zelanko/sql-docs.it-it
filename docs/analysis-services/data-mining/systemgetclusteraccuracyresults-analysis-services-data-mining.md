---
title: SystemGetClusterAccuracyResults (Analysis Services - Data Mining) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b9521cfd6e2b9ec0d08f290c60167c682c98e46f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209659"
---
# <a name="systemgetclusteraccuracyresults-analysis-services---data-mining"></a>SystemGetClusterAccuracyResults (Analysis Services - Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Restituisce la metrica di accuratezza per la convalida incrociata di una struttura di data mining e dei modelli di clustering correlati.  
  
 Questa stored procedure restituisce la metrica per l'intero set di dati come un'unica partizione. Per partizionare il set di dati in sezioni trasversali e restituire la metrica per ogni partizione, usare [SystemGetClusterCrossValidationResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Questa stored procedure può essere utilizzata solo per modelli di clustering. Per i modelli non di clustering, usare [SystemGetAccuracyResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SystemGetClusterAccuracyResults(  
<mining structure>   
[,<mining model list>]  
,<data set>  
,<test list>])  
```  
  
## <a name="arguments"></a>Argomenti  
 *struttura di data mining*  
 Nome di una struttura di data mining nel database corrente.  
  
 (Obbligatorio)  
  
 *elenco di modelli data mining*  
 Elenco delimitato da virgole dei modelli da convalidare.  
  
 L'impostazione predefinita è **null**e indica che vengono usati tutti i modelli applicabili. Se si utilizza l'impostazione predefinita, i modelli non di clustering vengono esclusi automaticamente dall'elenco di candidati per l'elaborazione.  
  
 (Facoltativo)  
  
 *set di dati*  
 Valore integer che indica quale partizione nella struttura di data mining deve essere utilizzata per il test. Il valore è derivato da una maschera di bit che rappresenta la somma dei valori seguenti, dove qualsiasi singolo valore è facoltativo:  
  
|||  
|-|-|  
|Case di training|0x0001|  
|Test case|0x0002|  
|Filtro modello|0x0004|  
  
 Per un elenco completo dei valori possibili, vedere la sezione Osservazioni di questo argomento.  
  
 (Obbligatorio)  
  
 *elenco di test*  
 Stringa che specifica le opzioni di testing. Questo parametro è riservato per usi futuri.  
  
 (facoltativo).  
  
## <a name="return-type"></a>Tipo restituito  
 Tabella che contiene i punteggi per ogni singola partizione e le aggregazioni per tutti i modelli.  
  
 Nella tabella seguente vengono elencate le colonne restituite da **SystemGetClusterAccuracyResults**. Per altre informazioni sull'interpretazione delle informazioni restituite dalla stored procedure, vedere [Misure nel report di convalida incrociata](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|ModelName|Nome del modello sottoposto a test. **All** indica che il risultato è un'aggregazione per tutti i modelli.|  
|AttributeName|Non applicabile a modelli di clustering.|  
|AttributeState|Non applicabile a modelli di clustering.|  
|PartitionIndex|Numero che indica la partizione.<br /><br /> Per questa stored procedure, il numero è sempre 0.|  
|PartitionCases|Valore integer che indica il numero di case sottoposti a test.|  
|Test|Tipo di test eseguito.|  
|Misura|Nome della misura restituita dal test. Le misure per ogni modello dipendono dal tipo di modello e dal tipo del valore stimabile.<br /><br /> Per un elenco delle misure restituite per ogni tipo stimabile, vedere [Misure nel report di convalida incrociata](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).<br /><br /> Per la definizione delle diverse misure, vedere [Convalida incrociata &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).|  
|Value|Punteggio di probabilità che indica la probabilità del case di cluster.|  
  
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
 In questo esempio vengono restituite le misure di accuratezza per due modelli di clustering, denominati `Cluster 1` e `Cluster 2`, associati alla struttura di data mining vTargetMail. Il codice nella quarta riga indica che i risultati devono essere basati solo sui test case, senza l'utilizzo di eventuali filtri associati a ogni modello.  
  
```  
CALL SystemGetClusterAccuracyResults (  
[vTargetMail],  
[Cluster 1], [Cluster 2],  
2  
)  
```  
  
 Risultati dell'esempio:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Test|Misura|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Cluster 1|||0|5545|Clustering|Probabilità del case|0.796514342249313|  
|Cluster 2|||0|5545|Clustering|Probabilità del case|0.732122471228572|  
  
## <a name="requirements"></a>Requisiti  
 La convalida incrociata è disponibile solo in [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] a partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [SystemGetCrossValidationResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemClusterGetAccuracyResults](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
