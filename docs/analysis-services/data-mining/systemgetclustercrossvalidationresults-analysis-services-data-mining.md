---
title: SystemGetClusterCrossValidationResults (Analysis Services - Data Mining) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ce11f7cb54d40336633d09a5d6601f0366c6bf55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209623"
---
# <a name="systemgetclustercrossvalidationresults-analysis-services---data-mining"></a>SystemGetClusterCrossValidationResults (Analysis Services - Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Partiziona la struttura di data mining nel numero specificato di sezioni incrociate, esegue il training di un modello per ogni partizione, quindi restituisce la metrica di accuratezza per ogni partizione.  
  
 **Nota** Questa stored procedure può essere usata solo con una struttura di data mining contenente almeno un modello di clustering. Per eseguire la convalida incrociata di modelli non di clustering, è necessario usare [SystemGetCrossValidationResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SystemGetClusterCrossValidationResults(  
<structure name>,   
[,<mining model list>]  
,<fold count>}  
,<max cases>  
<test list>])  
```  
  
## <a name="arguments"></a>Argomenti  
 *struttura di data mining*  
 Nome di una struttura di data mining nel database corrente.  
  
 (obbligatorio)  
  
 *mining model list*  
 Elenco delimitato da virgole dei modelli di data mining da convalidare.  
  
 Se non si specifica un elenco di modelli di data mining, la convalida incrociata viene eseguita su tutti i modelli di clustering associati alla struttura specificata.  
  
> [!NOTE]  
>  Per eseguire la convalida incrociata di modelli non di clustering, è necessario usare una stored procedure specifica, ovvero [SystemGetCrossValidationResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md).  
  
 (facoltativo).  
  
 *conteggio di riduzione*  
 Valore integer che specifica il numero di partizioni in cui separare il set di dati. Il valore minimo è 2. Il numero massimo di riduzioni è il **numero intero massimo** o il numero di case, a seconda di quale valore è inferiore.  
  
 Ogni partizione conterrà all'incirca questo numero di case: *numero massimo di case*/*conteggio di riduzione*.  
  
 Nessun valore predefinito.  
  
> [!NOTE]  
>  Il numero di riduzioni influisce in modo significativo sul tempo richiesto per l'esecuzione della convalida incrociata. Se si seleziona un numero troppo elevato, l'esecuzione della query potrebbe richiedere molto tempo e in alcuni casi potrebbe verificarsi il blocco o il timeout del server.  
  
 (obbligatorio)  
  
 *max cases*  
 Valore integer che specifica il numero massimo di case che è possibile sottoporre a test.  
  
 Il valore 0 indica che verranno utilizzati tutti i case nell'origine dati.  
  
 Se si specifica un numero maggiore del numero effettivo di case presenti nel set di dati, verranno utilizzati tutti i case nell'origine dati.  
  
 (obbligatorio)  
  
 *test list*  
 Stringa che specifica le opzioni di testing.  
  
 **Nota** Questo parametro è riservato per usi futuri.  
  
 (facoltativo).  
  
## <a name="return-type"></a>Tipo restituito  
 La tabella dei tipi restituiti contiene i punteggi per ogni singola partizione e le aggregazioni per tutti i modelli.  
  
 Nella tabella seguente vengono descritte le colonne restituite.  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|ModelName|Nome del modello sottoposto a test.|  
|AttributeName|Nome della colonna stimabile. Per i modelli del cluster, è sempre **null**.|  
|AttributeState|Valore di destinazione specificato nella colonna stimabile. Per i modelli del cluster, è sempre **null.**|  
|PartitionIndex|Indice in base 1 che identifica la partizione a cui si applicano i risultati.|  
|PartitionSize|Valore integer che indica il numero di case inclusi in ogni partizione.|  
|Test|Tipo di test eseguito.|  
|Misura|Nome della misura restituita dal test. Le misure per ogni modello dipendono dal tipo del valore stimabile. Per la definizione delle diverse misure, vedere [Convalida incrociata &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).<br /><br /> Per un elenco delle misure restituite per ogni tipo stimabile, vedere [Misure nel report di convalida incrociata](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).|  
|Value|Valore della misura di test specificata.|  
  
## <a name="remarks"></a>Note  
 Per restituire la metrica di accuratezza per l'intero set di dati, usare [SystemGetClusterAccuracyResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md).  
  
 Se il modello di data mining è già stato partizionato in riduzioni, è inoltre possibile ignorare l'elaborazione e restituire solo i risultati di convalida incrociata usando [SystemGetClusterAccuracyResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato come partizionare una struttura di data mining per la convalida incrociata in tre riduzioni, quindi come sottoporre a test due modelli di clustering associati alla struttura di data mining.  
  
 Nella terza riga del codice sono specificati i modelli di data mining che si desidera sottoporre a test. Se non si specifica l'elenco, vengono utilizzati tutti i modelli di clustering associati alla struttura.  
  
 Nella quarta riga del codice è specificato il numero di riduzioni, mentre nella quinta riga è specificato il numero massimo di case da utilizzare.  
  
 Poiché si tratta di modelli di clustering, non è necessario specificare un attributo o un valore stimabile.  
  
```  
CALL SystemGetClusterCrossValidationResults(  
[v Target Mail],  
[Cluster 1], [Cluster 2],  
3,  
10000  
)  
```  
  
 Risultati dell'esempio:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Test|Misura|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Cluster 1|||1|3025|Clustering|Probabilità del case|0.930524511864121|  
|Cluster 1|||2|3025|Clustering|Probabilità del case|0.919184178430778|  
|Cluster 1|||3|3024|Clustering|Probabilità del case|0.929651120490248|  
|Cluster 2|||1|1289|Clustering|Probabilità del case|0.922789726933607|  
|Cluster 2|||2|1288|Clustering|Probabilità del case|0.934865535691068|  
|Cluster 2|||3|1288|Clustering|Probabilità del case|0.924724595688798|  
  
## <a name="requirements"></a>Requisiti  
 La convalida incrociata è disponibile solo in [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] a partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [SystemGetCrossValidationResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
