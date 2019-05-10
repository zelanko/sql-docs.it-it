---
title: Configurare le proprietà delle misure | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e93b254e42b117f97ea6bc2d71afe5487f6a5197
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2019
ms.locfileid: "65357407"
---
# <a name="configure-measure-properties"></a>Configurare le proprietà delle misure
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Le proprietà delle misure consentono di definirne il funzionamento e di controllare il modo in cui vengono visualizzate agli utenti.  
  
 È possibile impostare proprietà in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante la creazione o la modifica di un cubo o una misura. Queste proprietà possono essere impostate anche a livello di programmazione mediante MDX o AMO. Per informazioni dettagliate, vedere [Creare misure e gruppi di misure nei modelli multidimensionali](../../analysis-services/multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md) o [Istruzione CREATE MEMBER &#40;MDX&#41;](../../mdx/mdx-data-definition-create-member.md) o [Programmazione di oggetti di base OLAP in AMO](https://docs.microsoft.com/bi-reference/amo/programming-amo-olap-basic-objects).  
  
## <a name="measure-properties"></a>Proprietà delle misure  
 Le misure ereditano alcune proprietà dal gruppo di misure di cui sono membri, a meno che tali proprietà non vengano sostituite a livello di misura. Le proprietà delle misure ne determinano la modalità di aggregazione, il tipo di dati, il nome visualizzato dall'utente, la cartella di visualizzazione in cui appariranno, la stringa di formato, l'espressione, la colonna di origine sottostante e la visibilità da parte degli utenti.  
  
|Proprietà|Definizione|  
|--------------|----------------|  
|**AggregateFunction**|Obbligatorio. Determina la modalità di aggregazione delle misure. **Sum** è l'aggregazione predefinita. Per altre informazioni, vedere [Utilizzare le funzioni di aggregazione](../../analysis-services/multidimensional-models/use-aggregate-functions.md) per una descrizione di ogni funzione.|  
|**DataType**|Obbligatorio. Specifica il tipo di dati della colonna della tabella dei fatti sottostante a cui è associata la misura. Per impostazione predefinita, questo valore viene ereditato dalla colonna di origine.|  
|**Descrizione**|Fornisce una descrizione della misura, che può essere esposta in applicazioni client.|  
|**DisplayFolder**|Specifica la cartella in cui verrà visualizzata la misura quando gli utenti si connettono al cubo. Quando in un cubo sono presenti numerose misure, è possibile usare le cartelle di visualizzazione per categorizzare le misure e migliorare l'esplorazione dell'utente.|  
|**FormatString**|È possibile selezionare il formato in cui gli utenti visualizzeranno i valori della misura usando la proprietà **FormatString** della misura.<br /><br /> Anche se in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]è disponibile un elenco di formati di visualizzazione, è possibile specificare formati aggiuntivi non inclusi nell'elenco. È possibile specificare qualsiasi formato denominato o definito dall'utente che risulti valido in Microsoft Visual Basic.|  
|**ID**|Obbligatorio. Visualizza l'identificatore univoco (ID) della misura. Questa proprietà è di sola lettura.|  
|**MeasureExpression**|Specifica un'espressione MDX vincolata che definisce il valore della misura. L'espressione viene valutata a livello foglia prima dell'aggregazione e consente la ponderazione di un valore, ad esempio in una conversione valuta in cui un importo di vendita viene ponderato in base al tasso di cambio.|  
|**Name**|Obbligatorio. Specifica il nome della misura.|  
|**Origine**|Obbligatorio. Specifica la colonna nella vista origine dati a cui è associata la misura. Vedere [Origini dati e associazioni &#40;SSAS - multidimensionale&#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).|  
|**Visible**|Determina la visibilità della misura nelle applicazioni client.|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare le proprietà dei gruppi di misure](../../analysis-services/multidimensional-models/configure-measure-group-properties.md)   
 [Modifica delle misure](../multidimensional-tutorial/lesson-3-1-modifying-measures.md)  
  
  
