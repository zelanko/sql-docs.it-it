---
title: Configurare le proprietà delle misure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- additivity [Analysis Services]
- ID property
- ErrorConfiguration property
- AggregateFunction property
- DisplayFolder property
- IgnoreUnrelatedDimensions property
- FormatString property
- Description property
- semiadditive
- properties [Analysis Services], measure groups
- aggregate functions [Analysis Services]
- DataType property
- ProcessingMode property
- MeasureExpression property
- AggregationPrefix property
- Visible property
- properties [Analysis Services], measures
- StorageLocation property
- StorageMode property
- formats [Analysis Services], measures
- Source property
- aggregations [Analysis Services], measures
- measures [Analysis Services], properties
- nonadditive [Analysis Services]
- Name property
- measures [Analysis Services], display formats
- ProcessingPriority property
- measure groups [Analysis Services], properties
- Type property
- ProactiveCaching property
ms.assetid: e9031078-c4f5-4986-b0c9-4d064b622ab7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7b1acd9e33865f1f60c1d1134e3173af4e4a562b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66076610"
---
# <a name="configure-measure-properties"></a>Configurare le proprietà delle misure
  Le proprietà delle misure consentono di definirne il funzionamento e di controllare il modo in cui vengono visualizzate agli utenti.  
  
 È possibile impostare proprietà in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante la creazione o la modifica di un cubo o una misura. Queste proprietà possono essere impostate anche a livello di programmazione mediante MDX o AMO. Per informazioni dettagliate, vedere [Creare misure e gruppi di misure nei modelli multidimensionali](create-measures-and-measure-groups-in-multidimensional-models.md) o [Istruzione CREATE MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member) o [Programmazione di oggetti di base OLAP in AMO](https://docs.microsoft.com/bi-reference/amo/programming-amo-olap-basic-objects).  
  
## <a name="measure-properties"></a>Proprietà delle misure  
 Le misure ereditano alcune proprietà dal gruppo di misure di cui sono membri, a meno che tali proprietà non vengano sostituite a livello di misura. Le proprietà delle misure ne determinano la modalità di aggregazione, il tipo di dati, il nome visualizzato dall'utente, la cartella di visualizzazione in cui appariranno, la stringa di formato, l'espressione, la colonna di origine sottostante e la visibilità da parte degli utenti.  
  
|Proprietà|Definizione|  
|--------------|----------------|  
|`AggregateFunction`|Obbligatorio. Determina la modalità di aggregazione delle misure. `Sum`è l'aggregazione predefinita. Per altre informazioni, vedere [Utilizzare le funzioni di aggregazione](use-aggregate-functions.md) per una descrizione di ogni funzione.|  
|`DataType`|Obbligatorio. Specifica il tipo di dati della colonna della tabella dei fatti sottostante a cui è associata la misura. Per impostazione predefinita, questo valore viene ereditato dalla colonna di origine.|  
|`Description`|Fornisce una descrizione della misura, che può essere esposta in applicazioni client.|  
|`DisplayFolder`|Specifica la cartella in cui verrà visualizzata la misura quando gli utenti si connettono al cubo. Quando in un cubo sono presenti numerose misure, è possibile usare le cartelle di visualizzazione per categorizzare le misure e migliorare l'esplorazione dell'utente.|  
|`FormatString`|È possibile selezionare il formato in cui gli utenti visualizzeranno i valori della misura utilizzando la proprietà `FormatString` della misura.<br /><br /> Anche se in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]è disponibile un elenco di formati di visualizzazione, è possibile specificare formati aggiuntivi non inclusi nell'elenco. È possibile specificare qualsiasi formato denominato o definito dall'utente che risulti valido in Microsoft Visual Basic.|  
|`ID`|Obbligatorio. Visualizza l'identificatore univoco (ID) della misura. Questa proprietà è di sola lettura.|  
|`MeasureExpression`|Specifica un'espressione MDX vincolata che definisce il valore della misura. L'espressione viene valutata a livello foglia prima dell'aggregazione e consente la ponderazione di un valore, ad esempio in una conversione valuta in cui un importo di vendita viene ponderato in base al tasso di cambio.|  
|`Name`|Obbligatorio. Specifica il nome della misura.|  
|`Source`|Obbligatorio. Specifica la colonna nella vista origine dati a cui è associata la misura. Vedere [Origini dati e associazioni &#40;SSAS - multidimensionale&#41;](data-sources-and-bindings-ssas-multidimensional.md).|  
|`Visible`|Determina la visibilità della misura nelle applicazioni client.|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le proprietà dei gruppi di misure](configure-measure-group-properties.md)   
 [Modifica delle misure](../lesson-3-1-modifying-measures.md)  
  
  
