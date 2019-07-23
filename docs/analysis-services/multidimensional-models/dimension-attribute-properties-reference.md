---
title: Dimension Attribute Properties Reference | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 26975562f3617742cbcc3bfb3a47e41af09ba8b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208919"
---
# <a name="dimension-attribute-properties-reference"></a>Riferimento alle proprietà degli attributo delle dimensioni
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]esistono molte proprietà che determinano le modalità di funzionamento delle dimensioni e degli attributi delle dimensioni. Nella tabella seguente vengono elencate e descritte queste proprietà degli attributi.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**AttributeHierarchyDisplayFolder**|Identifica la cartella in cui viene visualizzata all'utente la gerarchia dell'attributo associata.|  
|**AttributeHierarchyEnabled**|Determina se tramite [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene generata una gerarchia per l'attributo. Se la gerarchia dell'attributo non è attivata, l'attributo non può essere utilizzato in una gerarchia definita dall'utente e non è possibile fare riferimento alla gerarchia in istruzioni MDX (Multidimensional Expressions).|  
|**AttributeHierarchyOptimizedState**|Determina il livello di ottimizzazione applicato alla gerarchia dell'attributo. Per impostazione predefinita, una gerarchia dell'attributo è **FullyOptimized**, pertanto in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono compilati indici per la gerarchia dell’attributo al fine di migliorare le prestazioni di esecuzione delle query. L'altra opzione, **NotOptimized**, indica che non vengono compilati indici per la gerarchia dell'attributo. **NotOptimized** è utile se la gerarchia dell'attributo è usata per attività diverse dall'esecuzione di una query, poiché non viene compilato alcun indice aggiuntivo per l'attributo. La gerarchia dell'attributo può anche essere utilizzata per consentire di ordinare un altro attributo.|  
|**AttributeHierarchyOrdered**|Determina se la gerarchia dell'attributo associata viene ordinata. Il valore predefinito è **True**. Tuttavia, se una gerarchia dell'attributo non viene usata per l'esecuzione di query, è possibile risparmiare tempo di elaborazione impostando il valore di questa proprietà su **False**.|  
|**AttributeHierarchyVisible**|Determina se la gerarchia dell'attributo è visibile alle applicazioni client. Il valore predefinito è **True**. Tuttavia, se una gerarchia dell'attributo non viene usata per l'esecuzione di query, è possibile risparmiare tempo di elaborazione impostando il valore di questa proprietà su **False**.|  
|**CustomRollupColumn**|Specifica la colonna che definisce una formula personalizzata di rollup.|  
|**CustomRollupPropertiesColumn**|Specifica la colonna che contiene le proprietà di una formula personalizzata di rollup.|  
|**DefaultMember**|Specifica un'espressione MDX (Multidimensional Expressions) che definisce la misura predefinita per l'attributo.|  
|**Descrizione**|Contiene la descrizione dell'attributo.|  
|**DiscretizationBucketCount**|Contiene il numero di bucket per la discretizzazione.|  
|**DiscretizationMethod**|Definisce il metodo da utilizzare per la discretizzazione.|  
|**EstimatedCount**|Specifica il numero stimato di membri nell'attributo. Il valore predefinito è zero fino all'esecuzione di Progettazione guidata aggregazioni. È possibile contare il numero di record attraverso la procedura guidata oppure immettere un valore stimato. Immettere un valore manualmente se si conosce il numero di membri e si desidera risparmiare il tempo necessario per eseguire la query sul database per recuperare il conteggio. Se si sta utilizzando un subset di test dei dati di produzione, è possibile utilizzare i conteggi relativi ai dati di produzione affinché la progettazione delle aggregazioni venga ottimizzata per i dati di produzione piuttosto che per i dati di test.|  
|**GroupingBehavior**|Valore definito dall'utente che fornisce un hint alle applicazioni client su come raggruppare gli attributi.|  
|**ID**|Contiene l'identificatore univoco (ID) della dimensione.|  
|**InstanceSelection**|Fornisce un hint alle applicazioni client sul modo in cui deve venire visualizzato un elenco di elementi, in base al numero previsto di elementi presenti nell'elenco. Sono disponibili le seguenti opzioni:<br /><br /> **None** Nessun hint viene fornito all'applicazione client. Rappresenta il valore predefinito.<br /><br /> **DropDown** Il numero di elementi è sufficientemente ridotto per la visualizzazione in un elenco a discesa.<br /><br /> **List** Il numero di elementi è troppo grande per la visualizzazione in un **elenco**a discesa, ma non richiede l'applicazione di filtri.<br /><br /> **FilteredList** Il numero di elementi è grande a sufficienza per richiedere l'utilizzo di filtri per la visualizzazione.<br /><br /> **MandatoryFilter** Il numero di elementi è talmente grande che per la visualizzazione è sempre necessario l'utilizzo di filtri.|  
|**IsAggregatable**|Specifica se i valori dei membri dell'attributo possono essere aggregati. Il valore predefinito è **True**, che indica che la gerarchia dell'attributo contiene un livello (Totale). Se il valore di questa proprietà è **False**, la gerarchia dell'attributo non contiene un livello (Totale).|  
|**KeyColumns**|Contiene la colonna o le colonne che rappresentano la chiave per un attributo, ovvero la colonna della tabella relazionale sottostante nella vista origine dati a cui è associato l'attributo. All’utente viene visualizzato il valore di questa colonna per ogni membro a meno che non sia specificato un valore per la proprietà **NameColumn** .|  
|**MemberNamesUnique**|Determina se i nomi dei membri nella gerarchia dell'attributo devono essere univoci.|  
|**MembersWithData**|Utilizzata dagli attributi padre per determinare se visualizzare i membri dei dati per i membri non foglia nell'attributo padre. Il valore di questa proprietà viene usato solo quando il valore di **Usage** è impostato su Parent. Ciò significa che è stata definita una gerarchia padre-figlio. Sono disponibili le seguenti opzioni:<br /><br /> **NonLeafDataHidden** I dati non foglia sono nascosti.<br /><br /> **NonLeafDataVisible** I dati non foglia sono visibili.|  
|**MembersWithDataCaption**|Fornisce una stringa modello utilizzata dagli attributi padre per la creazione di didascalie per i membri dei dati generati dal sistema nell'attributo padre. Il valore di questa proprietà viene usato solo quando il valore di **Usage** è impostato su Parent. Ciò significa che è stata definita una gerarchia padre-figlio.|  
|**Name**|Contiene il nome descrittivo dell'attributo.|  
|**NameColumn**|Identifica la colonna che specifica il nome dell'attributo visualizzato agli utenti al posto del valore della colonna chiave per l'attributo. Questa colonna viene utilizzata quando il valore della colonna chiave per un membro dell'attributo è di difficile comprensione o non utile per l'utente oppure quando la colonna chiave è basata su una chiave composta. La proprietà **NameColumn** non viene usata nelle gerarchie padre-figlio, ma viene usata  per i membri figlio come nome dei membri in una gerarchia padre-figlio.|  
|**NamingTemplate**|Definisce in che modo vengono denominati i livelli in una gerarchia padre-figlio creata dall'attributo padre. Il valore di questa proprietà viene usato solo quando il valore di **Usage** è impostato su Parent. Ciò significa che è stata definita una gerarchia padre-figlio.|  
|**OrderBy**|Descrive in che modo ordinare i membri contenuti nella gerarchia dell'attributo. Il valore predefinito è Name, che specifica che l'ordine dei membri dell'attributo si basa sul valore della proprietà **NameColumn** , se disponibile. In caso contrario, i membri vengono ordinati in base al valore della colonna chiave. Sono disponibili le seguenti opzioni:<br /><br /> **NameColumn** L’ordine viene definito in base al valore della proprietà **NameColumn** .<br /><br /> **Key** L'ordinamento avviene in base al valore della colonna chiave del membro dell'attributo.<br /><br /> **AttributeKey** L'ordinamento avviene in base al valore della chiave del membro di un attributo specificato, che deve presentare una relazione tra attributi con l'attributo.<br /><br /> **AttributeName** L'ordinamento avviene in base al valore del nome del membro di un attributo specificato, che deve presentare una relazione tra attributi con l'attributo.|  
|**OrderByAttribute**|Identifica l'attributo in base al quale vengono ordinati i membri della gerarchia dell'attributo.|  
|**RootMemberIf**|Determina il modo in cui vengono identificati i membri di livello radice o più alto di una gerarchia padre-figlio. Il valore di questa proprietà viene usato solo quando il valore di **Usage** è impostato su Parent. Ciò significa che è stata definita una gerarchia padre-figlio. Il valore predefinito è **ParentIsBlankSelfOrMissing**, che indica che solo i membri che soddisfano una o più delle condizioni descritte per **ParentIsBlank**, **ParentIsSelf**o **ParentIsMissing** vengono trattati come membri radice. Sono inoltre disponibili i valori seguenti.<br /><br /> **ParentIsBlank** Solo i membri con una stringa Null, pari a zero o vuota nella colonna o nelle colonne chiave vengono trattati come membri radice.<br /><br /> **ParentIsSelf** Solo i membri che hanno se stessi come padre vengono trattati come membri radice.<br /><br /> **ParentIsMissing** Solo i membri per i quali non è possibile trovare l'elemento padre vengono trattati come membri radice.|  
|**Tipo**|Contiene il tipo dell'attributo. Per altre informazioni, vedere [Configurare tipi di attributi](../../analysis-services/multidimensional-models/attribute-properties-configure-attribute-types.md).|  
|**UnaryOperatorColumn**|Specifica la colonna che indica gli operatori unari. È un'associazione di tipo DataItem che definisce i dettagli di una colonna che fornisce un operatore unario.|  
|**Usage**|Descrive la modalità di utilizzo di un attributo.<br /><br /> Sono disponibili le seguenti opzioni:<br /><br /> **Regular** L’attributo è un attributo regolare. Rappresenta il valore predefinito.<br /><br /> **Key** L'attributo è un attributo chiave.<br /><br /> **Parent** L'attributo è un attributo padre.|  
|**ValueColumn**|Identifica la colonna che indica il valore dell'attributo. Se l'elemento **NameColumn** dell'attributo è specificato, come valori predefiniti dell'elemento **DataItem** vengono usati gli stessi valori di **ValueColumn** . Se l'elemento **NameColumn** dell’attributo non è specificato e la raccolta **KeyColumns** dell'attributo contiene un unico elemento **KeyColumn** che rappresenta una colonna chiave con dati di tipo stringa, come valori predefiniti dell'elemento **ValueColumn** vengono usati gli stessi valori di **DataItem** .|  
  
> [!NOTE]  
>  Per altre informazioni sull'impostazione dei valori per la proprietà **KeyColumn** in presenza di valori Null e di altri problemi di integrità dei dati, vedere l’articolo relativo alla [gestione dei problemi di integrità dei dati in Analysis Services 2005](http://go.microsoft.com/fwlink/?LinkId=81891).  
  
> [!NOTE]  
>  Il membro predefinito di un attributo viene utilizzato per valutare le espressioni quando un membro della gerarchia non viene esplicitamente incluso in una query. Il membro predefinito per un attributo viene specificato tramite la proprietà **DefaultMember** nell'attributo. Se in una query è inclusa una gerarchia di una dimensione, verranno ignorati tutti i membri predefiniti degli attributi corrispondenti ai livelli della gerarchia. Se in una query non viene inclusa alcuna gerarchia di una dimensione, i membri predefiniti vengono utilizzati per tutti gli attributi della dimensione. Per altre informazioni sui membri predefiniti, vedere [Definire un membro predefinito](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi e gerarchie di attributi](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)  
  
  
