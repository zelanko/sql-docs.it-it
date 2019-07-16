---
title: Attributi CSDLBI per la progettazione di Report | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c7f4b1ef3b46e4564ffc4622b39e8326adf443a6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68163458"
---
# <a name="csdlbi-attributes-for-report-design"></a>Attributi CSDLBI per la progettazione di report
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In questa sezione vengono descritti gli attributi nelle estensioni a CSDL per la modellazione tabulare che influiscono sulla progettazione delle query di [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
## <a name="model-attributes"></a>Attributi di modellazione  
 Questi attributi sono definiti su un sottoelemento dell'elemento di un CSDL [EntityContainer](http://msdn.microsoft.com/library/bb399169.aspx) elemento.  
  
|Nome dell'attributo|Tipo di dati|Descrizione|  
|--------------------|---------------|-----------------|  
|Impostazioni cultura|Testo|Indica le impostazioni cultura utilizzate per i formati della valuta. Se omesso, viene utilizzato EN-US.|  
|IsRightToLeft|Boolean|Indica se i valori dei campi di testo devono essere letti da destra a sinistra per impostazione predefinita|  
  
## <a name="entity-attributes"></a>Attributi di entità  
 Questi attributi sono definiti su un sottoelemento di un elemento EntitySet o EntityType di CSDL.  
  
|Nome dell'attributo|Tipo di dati|Descrizione|  
|--------------------|---------------|-----------------|  
|**ReferenceName**|Testo|Identificatore utilizzato per fare riferimento a questa entità in una query DAX. Se omesso, viene utilizzato il nome.|  
|**Caption**|Testo|Nome visualizzato per l'entità.|  
|**Documentazione**|Testo|Testo descrittivo per agevolare la comprensione del significato dei dati in ambito aziendale.|  
|**Hidden**|Boolean|Indica se l'entità deve essere visualizzata. Il valore predefinito è **false**.|  
|**CollectionCaption**|Testo|Nome plurale per fare riferimento a un set di istanze dell'entità. Se omesso, viene utilizzato l'attributo Caption.|  
|**DisplayKey**|MemberRef[]|Elenco ordinato di campi utilizzato per identificare un'istanza di entità per gli utenti in ambito aziendale. I riferimenti possono includere proprietà di navigazione e proprietà di istanza. Quando viene fatto riferimento a una proprietà di navigazione, la **DisplayKey** della destinazione di entità viene visualizzata. Se il **DisplayKey** valore viene omesso, viene usato il campo di chiave.|  
|**DefaultImage**|MemberRef|Riferimento al campo contenente un'immagine utilizzata per identificare visivamente un'istanza di entità per gli utenti in ambito aziendale. Se omesso, viene utilizzato il primo campo immagine nell'entità, se presente.|  
|**DefaultDetails**|MemberRef[]|Un elenco ordinato di campi che rappresentano il valore predefinito di set di informazioni dettagliate visualizzato agli utenti in ambito aziendale su un'istanza di entità. Se omesso, vengono utilizzati i primi cinque (5) campi nell'entità, escludendo quelli già fa **Key**, **DisplayKey**, o **DefaultImage**.|  
|**SortProperties**|MemberRef[]|Elenco ordinato di campi in base al quale vengono ordinate le istanze di entità. L'ordinamento su questi campi, il **SortDirection** specificato su ogni campo viene usato. Se omesso, il **DisplayKey** vengono usati i campi|  
|**DefaultMeasure**|MemberRef|Riferimento a una misura definita nel modello o a un campo numerico con una funzione di aggregazione predefinita per indicare che la misura o il campo deve essere utilizzato come rappresentazione predefinita per più istanze dell'entità. Se omesso, viene utilizzato un conteggio delle istanze di entità.|  
|**DefaultLocation**|MemberRef|Riferimento a un campo il cui valore rappresenta il percorso predefinito associato a un'istanza di entità. Se omesso, viene utilizzato il primo campo percorso nell'entità, se presente.|  
  
## <a name="field-attributes"></a>Attributi di campo  
 Questi attributi sono definiti su un sottoelemento di una proprietà CSDL o [NavigationProperty](http://msdn.microsoft.com/library/bb387104.aspx) elemento.  
  
|Nome dell'attributo|Tipo di dati|Descrizione|  
|--------------------|---------------|-----------------|  
|**ReferenceName**|Testo|Identificatore utilizzato per fare riferimento a questa entità in una query DAX. Se omesso, viene utilizzato il nome del campo.|  
|**Caption**|Testo|Nome visualizzato per l'entità. Se omesso, il campo **ReferenceName** viene usato.|  
|**Documentazione**|Testo|Testo descrittivo per agevolare la comprensione del significato del campo in ambito aziendale.|  
|**Hidden**|Boolean|Indica se il campo deve essere visualizzato. Il valore predefinito è **false**, vale a dire il campo viene visualizzato.|  
|**DisplayFolder**|Testo|Nome (percorso completo) della cartella in cui viene visualizzato questo campo. Se omesso, il campo viene visualizzato alla radice del modello.|  
|**ContextualNameRule**|Enum|Valore che indica se e come deve essere modificato il nome della proprietà in base al contesto in cui viene utilizzato. I valori possibili sono:  **None**, **ruolo**, **Merge**.|  
|**Allineamento**|Enum|Valore che indica come devono essere allineati i valori del campo in una presentazione tabulare. I valori possibili sono **predefinite**, **Center**, **sinistra**, **destra**. Se omesso, il valore predefinito determina l'allineamento basato sul tipo di dati del campo.|  
|**FormatString**|Testo|Una stringa di formato .NET che indica come deve essere formattato il valore del campo per impostazione predefinita. Se omesso, si presuppone il formato seguente:<br /><br /> Campi Datetime:: data breve regionale o "d"<br /><br /> -Funzione di aggregazione di campi a virgola mobile e integrali con un valore predefinito: numero regionale o "n"<br /><br /> -Funzione di aggregazione numeri interi non prevede alcun valore predefinito: numero decimale regionale o "d"<br /><br /> Per tutti gli altri tipi di campi, non è applicabile alcuna stringa di formato.|  
|**Unità**|Testo|Simbolo applicato ai valori del campo per esprimere unità. Se omesso, si presuppone che le unità non siano note.|  
|**Width**|Integer|Larghezza preferita espressa in caratteri che deve essere riservata per visualizzare i valori del campo in una presentazione tabulare. Se omesso, una larghezza predefinita si basa sul tipo di dati del campo.|  
|**SortDirection**|Enum|Valore che indica la modalità di ordinamento dei valori del campo. I valori possibili sono **predefinite**, **crescente**, **Descending**. Se omesso, digitare il valore predefinito assegna che una direzione di ordinamento è basata sui dati del campo.|  
|**IsRightToLeft**|Boolean|Indica se il campo contiene testo che deve essere letto da destra a sinistra. Se omesso, si presuppone l'impostazione del modello.|  
|**OrderBy**|MemberRef|Un riferimento a un altro campo all'interno del modello che definisce l'ordinamento per i valori del campo. I valori per i due campi devono presentare un mapping 1:1 oppure il comportamento di ordinamento non è definito. Se omesso, il campo viene ordinato in base al proprio valore.|  
|**Sommario**|Enum|Enumerazione che descrive il sottotipo o il contenuto del campo. Se omesso, non specifico il sottotipo si presuppone che, a meno che il tipo del campo dati è Binary, nel qual caso si presuppone Image. Per un elenco completo dei tipi di contenuto supportati, vedere la documentazione AMO.|  
|**DefaultAggregateFunction**|Enum|Valore che indica la funzione predefinita, se presente, generalmente utilizzata per aggregare questo campo. I valori possibili sono **None**, **somma**, **medio**, **conteggio**, **Min**, **Max**. Se omesso, **somma** si presuppone che per i campi numerici **None** per tutti gli altri campi.|  
|**IsSimpleMeasure**|Boolean|Indica se una misura è soltanto una semplice aggregazione di un campo numerico. Tali aggregazioni possono essere facilmente definite nella query in base alle necessità, pertanto è preferibile ometterle dalla definizione del modello per migliorare le prestazioni. Se omesso, **false** presuppone.|  
|**Indicatore KPI**<br /><br /> **KpiGoal**<br /><br /> **KpiStatus**|Sottoelemento|Indica che l'elemento della misura deve essere utilizzato come indicatore KPI. Il sottoelemento KPI utilizza gli elementi KpiGoal e KpiStauts per definire l'immagine di visualizzazione associata e gli intervalli di destinazione.|  
  
  
