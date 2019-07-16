---
title: SystemGetCrossValidationResults (Analysis Services - Data Mining) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2febed19e2bd481a8e442f115f9691e5abb6be4b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209779"
---
# <a name="systemgetcrossvalidationresults-analysis-services---data-mining"></a>SystemGetCrossValidationResults (Analysis Services - Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Partiziona la struttura di data mining nel numero specificato di sezioni incrociate, esegue il training di un modello per ogni partizione, quindi restituisce la metrica di accuratezza per ogni partizione.  
  
> [!NOTE]  
>  Non è possibile usare questa stored procedure per la convalida incrociata di modelli di clustering o di modelli compilati mediante l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series o l'algoritmo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Sequence Clustering. Per eseguire la convalida incrociata di modelli di clustering, usare una stored procedure specifica, ovvero [SystemGetClusterCrossValidationResults &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SystemGetCrossValidationResults(  
<mining structure>  
[, <mining model list>]  
,<fold count>  
,<max cases>  
,<target attribute>  
[,<target state>]  
[,<target threshold>]  
[,<test list>])  
```  
  
## <a name="arguments"></a>Argomenti  
 *struttura di data mining*  
 Nome di una struttura di data mining nel database corrente.  
  
 (obbligatorio)  
  
 *mining model list*  
 Elenco delimitato da virgole dei modelli di data mining da convalidare.  
  
 Se un nome di modello contiene eventuali caratteri non validi nel nome di un identificatore, è necessario racchiudere il nome tra parentesi.  
  
 Se non si specifica un elenco di modelli di data mining, la convalida incrociata viene eseguita su tutti i modelli associati alla struttura specificata e che contengono un attributo stimabile.  
  
> [!NOTE]  
>  Per eseguire la convalida incrociata di modelli di clustering, è necessario usare una stored procedure diversa, ovvero [SystemGetClusterCrossValidationResults &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md).  
  
 (facoltativo).  
  
 *conteggio di riduzione*  
 Valore integer che specifica il numero di partizioni in cui separare il set di dati. Il valore minimo è 2. Il numero massimo di riduzioni è il **numero intero massimo** o il numero di case, a seconda di quale valore è inferiore.  
  
 Ogni partizione conterrà all'incirca questo numero di case: *numero massimo di case*/*conteggio di riduzione*.  
  
 Nessun valore predefinito.  
  
> [!NOTE]  
>  Il numero di riduzioni influisce in modo significativo sul tempo richiesto per l'esecuzione della convalida incrociata. Se si seleziona un numero troppo elevato, l'esecuzione della query potrebbe richiedere molto tempo e in alcuni casi potrebbe verificarsi il blocco o il timeout del server.  
  
 (obbligatorio)  
  
 *numero massimo di case*  
 Valore integer che specifica il numero massimo di case che è possibile sottoporre a test in tutte le riduzioni.  
  
 Il valore 0 indica che verranno utilizzati tutti i case nell'origine dati.  
  
 Se si specifica un valore maggiore del numero effettivo di case nel set di dati, verranno utilizzati tutti i case nell'origine dati.  
  
 Nessun valore predefinito.  
  
 (obbligatorio)  
  
 *target attribute*  
 Stringa che contiene il nome dell'attributo stimabile. Un attributo stimabile può essere una colonna, una colonna della tabella nidificata o una colonna chiave della tabella nidificata di un modello di data mining.  
  
> [!NOTE]  
>  L'esistenza dell'attributo di destinazione viene convalidata solo in fase di esecuzione.  
  
 (obbligatorio)  
  
 *target state*  
 Formula che specifica il valore da stimare. Se si specifica un valore di destinazione, viene raccolta la metrica solo per il valore specificato.  
  
 Se questo valore non è specificato oppure è **Null**, viene calcolata la metrica per lo stato più probabile per ogni stima.  
  
 Il valore predefinito è **Null**.  
  
 Durante la convalida viene generato un errore se il valore specificato non è valido per l'attributo specificato oppure se la formula non è del tipo corretto per l'attributo specificato.  
  
 (facoltativo).  
  
 *target*  *threshold*  
 **Double** è maggiore di 0 e minore di 1. Indica il punteggio di probabilità minimo che deve essere ottenuto per la stima dello stato di destinazione specificato affinché venga conteggiata come corretta.  
  
 Una stima con una probabilità minore o uguale a questo valore viene considerata non corretta.  
  
 Se non si specifica alcun valore oppure il valore è **Null**, viene usato lo stato più probabile, indipendentemente dal punteggio di probabilità corrispondente.  
  
 Il valore predefinito è **null**.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non genererà un errore se si imposta la *state threshold* su 0.0, sebbene non sia mai consigliabile usare questo valore. Con una soglia di 0.0, le stime con una probabilità dello 0 percento vengono di fatto conteggiate come corrette.  
  
 (facoltativo).  
  
 *test list*  
 Stringa che specifica le opzioni di testing.  
  
 **Nota** Questo parametro è riservato per usi futuri.  
  
 (facoltativo).  
  
## <a name="return-type"></a>Tipo restituito  
 Il set di righe restituito contiene punteggi per ogni partizione in ogni modello.  
  
 Nella tabella seguente vengono descritte le colonne nel set di righe.  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|ModelName|Nome del modello sottoposto a test.|  
|AttributeName|Nome della colonna stimabile.|  
|AttributeState|Valore di destinazione specificato nella colonna stimabile. Un valore **Null**indica che è stata usata la stima più probabile.<br /><br /> Se questa colonna contiene un valore, l'accuratezza del modello viene valutata solo rispetto a questo valore.|  
|PartitionIndex|Indice in base 1 che identifica la partizione a cui si applicano i risultati.|  
|PartitionSize|Valore integer che indica il numero di case inclusi in ogni partizione.|  
|Test|Categoria del test eseguito. Per una descrizione delle categorie e dei test inclusi in ogni categoria, vedere [Misure nel report di convalida incrociata](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).|  
|Misura|Nome della misura restituita dal test. Le misure per ogni modello dipendono dal tipo del valore stimabile. Per la definizione delle diverse misure, vedere [Convalida incrociata &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).<br /><br /> Per un elenco delle misure restituite per ogni tipo stimabile, vedere [Misure nel report di convalida incrociata](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).|  
|Value|Valore della misura di test specificata.|  
  
## <a name="remarks"></a>Note  
 Per restituire la metrica di accuratezza per l'intero set di dati, usare [SystemGetAccuracyResults &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md).  
  
 Se il modello di data mining è già stato partizionato in riduzioni, è possibile ignorare l'elaborazione e restituire solo i risultati della convalida incrociata usando [SystemGetAccuracyResults &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md).  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrato come partizionare una struttura di data mining per la convalida incrociata in due riduzioni, quindi come sottoporre a test i due modelli di data mining associati alla struttura di data mining, ovvero `[v Target Mail]`.  
  
 Nella terza riga del codice sono elencati i modelli di data mining che si desidera sottoporre a test. Se non si specifica l'elenco, vengono utilizzati tutti i modelli non di clustering associati alla struttura. La quarta riga del codice specifica il numero di partizioni. Poiché non è stato specificato alcun valore per *numero massimo di case*, tutti i case nella struttura di data mining vengono usati e distribuiti in modo uniforme nelle partizioni.  
  
 La quinta riga del codice specifica l'attributo stimabile, ovvero Bike Buyer, mentre la sesta riga specifica il valore da stimare, ovvero 1, indicando che l'acquisto verrà effettuato.  
  
 Il valore NULL nella settima riga indica che non è presente alcuna barra di probabilità minima da soddisfare. Nella valutazione dell'accuratezza verrà pertanto utilizzata la prima stima che dispone di una probabilità diversa da zero.  
  
```  
CALL SystemGetCrossValidationResults(  
[v Target Mail],  
[Target Mail DT], [Target Mail NB],  
2,  
'Bike Buyer',  
1,  
NULL  
)  
```  
  
 Risultati dell'esempio:  
  
|ModelName|AttributeName|AttributeState|PartitionIndex|PartitionSize|Test|Misura|Value|  
|---------------|-------------------|--------------------|--------------------|-------------------|----------|-------------|-----------|  
|Target Mail DT|Bike Buyer|1|1|500|classificazione|Vero positivo|144|  
|Target Mail DT|Bike Buyer|1|1|500|classificazione|Falso positivo|105|  
|Target Mail DT|Bike Buyer|1|1|500|classificazione|Vero negativo|186|  
|Target Mail DT|Bike Buyer|1|1|500|classificazione|Falso negativo|65|  
|Target Mail DT|Bike Buyer|1|1|500|Probabilità|Punteggio in forma logaritmica|-0.619042807138345|  
|Target Mail DT|Bike Buyer|1|1|500|Probabilità|Accuratezza|0.0740963734002671|  
|Target Mail DT|Bike Buyer|1|1|500|Probabilità|Radice errore quadratico medio|0.346946279977653|  
|Target Mail DT|Bike Buyer|1|2|500|classificazione|Vero positivo|162|  
|Target Mail DT|Bike Buyer|1|2|500|classificazione|Falso positivo|86|  
|Target Mail DT|Bike Buyer|1|2|500|classificazione|Vero negativo|165|  
|Target Mail DT|Bike Buyer|1|2|500|classificazione|Falso negativo|87|  
|Target Mail DT|Bike Buyer|1|2|500|Probabilità|Punteggio in forma logaritmica|-0.654117781086519|  
|Target Mail DT|Bike Buyer|1|2|500|Probabilità|Accuratezza|0.038997399132084|  
|Target Mail DT|Bike Buyer|1|2|500|Probabilità|Radice errore quadratico medio|0.342721344892651|  
  
## <a name="requirements"></a>Requisiti  
 La convalida incrociata è disponibile solo in [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)] a partire da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [SystemGetCrossValidationResults](../../analysis-services/data-mining/systemgetcrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetAccuracyResults &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/systemgetaccuracyresults-analysis-services-data-mining.md)   
 [SystemGetClusterCrossValidationResults &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/systemgetclustercrossvalidationresults-analysis-services-data-mining.md)   
 [SystemGetClusterAccuracyResults &#40;Analysis Services - Data Mining&#41;](../../analysis-services/data-mining/systemgetclusteraccuracyresults-analysis-services-data-mining.md)  
  
  
