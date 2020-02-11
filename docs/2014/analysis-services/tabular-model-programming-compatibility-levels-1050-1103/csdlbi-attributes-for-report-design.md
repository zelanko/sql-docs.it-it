---
title: Attributi CSDLBI per la progettazione di report | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 61ba3a27-790e-43bc-b421-e01bf2fdbda6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b7d2a9f075879ce1bfa0c0e7257ea8a2495562c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62757933"
---
# <a name="csdlbi-attributes-for-report-design"></a>Attributi CSDLBI per la progettazione di report
  In questa sezione vengono descritti gli attributi nelle estensioni a CSDL per la modellazione tabulare che influiscono sulla progettazione delle query di [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)].  
  
## <a name="model-attributes"></a>Attributi di modellazione  
 Questi attributi sono definiti su un sottoelemento di un elemento [ENTITYCONTAINER](https://msdn.microsoft.com/library/bb399169.aspx) CSDL.  
  
|Nome attributo|Tipo di dati|Descrizione|  
|--------------------|---------------|-----------------|  
|Impostazioni cultura|Text|Indica le impostazioni cultura utilizzate per i formati della valuta. Se omesso, viene utilizzato EN-US.|  
|IsRightToLeft|Boolean|Indica se i valori dei campi di testo devono essere letti da destra a sinistra per impostazione predefinita|  
  
## <a name="entity-attributes"></a>Attributi di entità  
 Questi attributi sono definiti su un sottoelemento di un elemento EntitySet o EntityType di CSDL.  
  
|Nome attributo|Tipo di dati|Descrizione|  
|--------------------|---------------|-----------------|  
|`ReferenceName`|Text|Identificatore utilizzato per fare riferimento a questa entità in una query DAX. Se omesso, viene utilizzato il nome.|  
|`Caption`|Text|Nome visualizzato per l'entità.|  
|`Documentation`|Text|Testo descrittivo per agevolare la comprensione del significato dei dati in ambito aziendale.|  
|`Hidden`|Boolean|Indica se l'entità deve essere visualizzata. Il valore predefinito è `false`.|  
|`CollectionCaption`|Text|Nome plurale per fare riferimento a un set di istanze dell'entità. Se omesso, viene utilizzato l'attributo Caption.|  
|`DisplayKey`|MemberRef[]|Elenco ordinato di campi utilizzato per identificare un'istanza di entità per gli utenti in ambito aziendale. I riferimenti possono includere proprietà di navigazione e proprietà di istanza. Quando viene fatto riferimento a una proprietà di navigazione, viene visualizzato il valore `DisplayKey` dell'entità di destinazione. Se il valore `DisplayKey` viene omesso, viene utilizzato il campo chiave.|  
|`DefaultImage`|MemberRef|Riferimento al campo contenente un'immagine utilizzata per identificare visivamente un'istanza di entità per gli utenti in ambito aziendale. Se omesso, viene utilizzato il primo campo immagine nell'entità, se presente.|  
|`DefaultDetails`|MemberRef[]|Elenco ordinato di campi che rappresentano il set predefinito di informazioni dettagliate visualizzato agli utenti in ambito aziendale relativamente a una istanza di entità. Se omesso, vengono utilizzati i primi cinque (5) campi dell'entità, escludendo quelli a cui `Key`, `DisplayKey` o `DefaultImage` fanno riferimento.|  
|`SortProperties`|MemberRef[]|Elenco ordinato di campi in base al quale vengono ordinate le istanze di entità. Quando l'ordinamento viene basato su questi campi, viene utilizzato il valore `SortDirection` specificato su ogni campo. Se omesso, vengono utilizzati i campi `DisplayKey`|  
|`DefaultMeasure`|MemberRef|Riferimento a una misura definita nel modello o a un campo numerico con una funzione di aggregazione predefinita per indicare che la misura o il campo deve essere utilizzato come rappresentazione predefinita per più istanze dell'entità. Se omesso, viene utilizzato un conteggio delle istanze di entità.|  
|`DefaultLocation`|MemberRef|Riferimento a un campo il cui valore rappresenta il percorso predefinito associato a un'istanza di entità. Se omesso, viene utilizzato il primo campo percorso nell'entità, se presente.|  
  
## <a name="field-attributes"></a>Attributi di campo  
 Questi attributi sono definiti su un sottoelemento di una proprietà CSDL o di un elemento [NavigationProperty](https://msdn.microsoft.com/library/bb387104.aspx) .  
  
|Nome attributo|Tipo di dati|Descrizione|  
|--------------------|---------------|-----------------|  
|`ReferenceName`|Text|Identificatore utilizzato per fare riferimento a questa entità in una query DAX. Se omesso, viene utilizzato il nome del campo.|  
|`Caption`|Text|Nome visualizzato per l'entità. Se omesso, `ReferenceName` viene utilizzato il campo.|  
|`Documentation`|Text|Testo descrittivo per agevolare la comprensione del significato del campo in ambito aziendale.|  
|`Hidden`|Boolean|Indica se il campo deve essere visualizzato. Il valore predefinito è `false` che indica che il campo verrà visualizzato.|  
|`DisplayFolder`|Text|Nome (percorso completo) della cartella in cui viene visualizzato questo campo. Se omesso, il campo viene visualizzato alla radice del modello.|  
|`ContextualNameRule`|Enum|Valore che indica se e come deve essere modificato il nome della proprietà in base al contesto in cui viene utilizzato. I valori possibili sono i seguenti: `None`, `Role`, `Merge`.|  
|`Alignment`|Enum|Valore che indica come devono essere allineati i valori del campo in una presentazione tabulare. I valori possibili sono i seguenti: `Default`, `Center`, `Left`, `Right`. Se omesso, il valore predefinito determina l'allineamento in base al tipo di dati del campo.|  
|`FormatString`|Text|Stringa di formato .NET che indica il modo in cui il valore del campo deve essere formattato per impostazione predefinita. Se omesso, si presuppone il formato seguente:<br /><br /> -Campi DateTime: data breve regionale o "d"<br />-Campi a virgola mobile e campi integrali con una funzione di aggregazione predefinita: numero regionale o "n"<br />-Integer senza funzione di aggregazione predefinita: numero decimale regionale o "d"<br /><br /> Per tutti gli altri tipi di campi, non è applicabile alcuna stringa di formato.|  
|`Units`|Text|Simbolo applicato ai valori del campo per esprimere unità. Se omesso, si presuppone che le unità non siano note.|  
|`Width`|Integer|Larghezza preferita in caratteri che devono essere riservati per visualizzare i valori del campo in una presentazione tabulare. Se omesso, una larghezza predefinita è basata sul tipo di dati del campo.|  
|`SortDirection`|Enum|Valore che indica la modalità di ordinamento dei valori del campo. I valori possibili sono i seguenti: `Default`, `Ascending`, `Descending`. Se omesso, il valore predefinito assegna una direzione di ordinamento è basato sul tipo di dati del campo.|  
|`IsRightToLeft`|Boolean|Indica se il campo contiene testo che deve essere letto da destra a sinistra. Se omesso, si presuppone l'impostazione del modello.|  
|`OrderBy`|MemberRef|Riferimento a un altro campo all'interno del modello che definisce l'ordinamento per i valori di questo campo. I valori per i due campi devono presentare un mapping 1:1 oppure il comportamento di ordinamento non è definito. Se omesso, il campo viene ordinato in base al proprio valore.|  
|`Contents`|Enum|Enumerazione che descrive il sottotipo o il contenuto del campo. Se omesso, non viene utilizzato alcun sottotipo specifico, a meno che il tipo di dati del campo non sia binario, nel qual caso si presuppone che venga utilizzata l'immagine. Per un elenco completo dei tipi di contenuto supportati, vedere la documentazione AMO.|  
|`DefaultAggregateFunction`|Enum|Valore che indica la funzione predefinita, se presente, generalmente utilizzata per aggregare questo campo. I valori possibili sono i seguenti: `None`, `Sum`, `Average`, `Count`, `Min`, `Max`. Se omesso, si presuppone `Sum` per i campi numerici e `None` per tutti gli altri campi.|  
|`IsSimpleMeasure`|Boolean|Indica se una misura è soltanto una semplice aggregazione di un campo numerico. Tali aggregazioni possono essere facilmente definite nella query in base alle necessità, pertanto è preferibile ometterle dalla definizione del modello per migliorare le prestazioni. Se omesso, si presuppone `false`.|  
|`Kpi`<br /><br /> `KpiGoal`<br /><br /> `KpiStatus`|Sottoelemento|Indica che l'elemento della misura deve essere utilizzato come indicatore KPI. Il sottoelemento KPI utilizza gli elementi KpiGoal e KpiStauts per definire l'immagine di visualizzazione associata e gli intervalli di destinazione.|  
  
  
