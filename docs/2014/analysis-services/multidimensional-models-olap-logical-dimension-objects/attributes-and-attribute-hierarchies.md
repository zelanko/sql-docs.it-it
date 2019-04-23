---
title: Gli attributi e gerarchie di attributi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- regular attributes [Analysis Services]
- parent attributes [Analysis Services]
- hierarchies [Analysis Services], attribute
- attributes [Analysis Services], about attributes
- account attributes [Analysis Services]
- dimensions [Analysis Services], attributes
- key attributes [Analysis Services]
- OLAP objects [Analysis Services], attributes
- attributes [Analysis Services], relationships
- attributes [Analysis Services]
- relationships [Analysis Services], attributes
ms.assetid: 59de1ea2-e7a9-4a53-9ee0-14be52e95643
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c1f1c6644e14beaee7bdcab9e3f50129f73b7bc
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60157267"
---
# <a name="attributes-and-attribute-hierarchies"></a>Attributi e gerarchie di attributi
  Le dimensioni sono raccolte di attributi, associate a una o più colonne in una tabella o una vista della vista origine dati.  
  
## <a name="key-attribute"></a>Attributo chiave  
 Ogni dimensione contiene un attributo chiave. Ogni attributo è associato a una o più colonne di una tabella della dimensione. L'attributo chiave è l'attributo di una dimensione che identifica le colonne della tabella principale della dimensione utilizzate nelle relazioni di chiave esterna con la tabella dei fatti. In genere, l'attributo chiave rappresenta la colonna o le colonne chiave primaria nella tabella della dimensione. È possibile definire una chiave primaria logica in una tabella di una vista origine dati che non disponga di una chiave primaria fisica nell'origine dei dati sottostante. **Per altre informazioni**, vedere [definire chiavi primarie logiche in una vista origine dati &#40;Analysis Services&#41;](../multidimensional-models/define-logical-primary-keys-in-a-data-source-view-analysis-services.md). Quando si definiscono gli attributi chiave, tramite la Creazione guidata cubo e la Creazione guidata dimensione viene eseguito un tentativo di utilizzo delle colonne chiave primaria della tabella della dimensione nella vista origine dati. Se nella tabella della dimensione non è definita una chiave primaria logica o una chiave primaria fisica, tramite le procedure guidate potrebbe non essere possibile definire correttamente gli attributi chiave per la dimensione.  
  
## <a name="binding-an-attribute-to-columns-in-data-source-view-tables-or-views"></a>Associazione di un attributo a colonne di tabelle o viste della vista origine dati  
 Un attributo è associato a colonne di una o più tabelle o viste della vista origine dati. Un attributo è sempre associato a una o più colonne chiave, che determinano i membri inclusi nell'attributo. Per impostazione predefinita, la colonna chiave è l'unica colonna a cui un attributo è associato. Un attributo può inoltre essere associato a una o più colonne aggiuntive per scopi specifici. La proprietà `NameColumn` di un attributo determina, ad esempio, il nome visualizzato all'utente per ogni membro dell'attributo e può essere associata a una colonna della dimensione specifica attraverso una vista origine dati o a una colonna calcolata nella vista origine dati. Per altre informazioni, vedere [Dimension Attribute Properties Reference](../multidimensional-models/dimension-attribute-properties-reference.md).  
  
## <a name="attribute-hierarchies"></a>Gerarchie di attributi  
 Per impostazione predefinita, i membri degli attributi sono organizzati in gerarchie a due livelli, costituite da un livello foglia e da un livello Totale. Il livello Totale contiene il valore aggregato dei membri dell'attributo nelle misure di ogni gruppo di misure di cui la dimensione a cui è correlato l'attributo è membro. Se, tuttavia, la proprietà `IsAggregatable` viene impostata su False, il livello Totale non viene creato. Per altre informazioni, vedere [Dimension Attribute Properties Reference](../multidimensional-models/dimension-attribute-properties-reference.md).  
  
 Gli attributi vengono in genere organizzati in gerarchie definite dall'utente che indicano i percorsi drill-down che è possibile utilizzare per esplorare i dati nei gruppi di misure a cui un attributo è correlato. Nelle applicazioni client gli attributi possono essere utilizzati per ottenere informazioni sui raggruppamenti e sui vincoli. Quando gli attributi sono organizzati in gerarchie definite dall'utente, si definiscono le relazioni tra i livelli della gerarchia quando i livelli sono correlati in un molti-a-uno o una relazione uno a uno (denominata un' *naturale* relazione). In una gerarchia Calendar Time, ad esempio, un livello Day dovrà essere correlato al livello Month, il livello Month al livello Quarter e così via. Grazie alla definizione delle relazioni tra i livelli in una gerarchia definita dall'utente, Analysis Services consente di definire aggregazioni più utili al fine di migliorare le prestazioni di esecuzione delle query e l'utilizzo della memoria da parte dei processi di elaborazione, ottimizzando l'utilizzo di cubi complessi o di grandi dimensioni. Per altre informazioni, vedere [gerarchie definite dall'utente](user-hierarchies.md), [gerarchie definite dall'utente](../multidimensional-models/user-defined-hierarchies-create.md), e [definire relazioni tra attributi](../multidimensional-models/attribute-relationships-define.md).  
  
## <a name="attribute-relationships-star-schemas-and-snowflake-schemas"></a>Relazioni tra attributi, schemi star e schemi snowflake  
 Per impostazione predefinita, in uno schema star tutti gli attributi sono direttamente correlati all'attributo chiave, che consente agli utenti di esplorare i fatti nel cubo in base a qualsiasi gerarchia di attributo nella dimensione. In uno schema snowflake, un attributo è direttamente collegato all'attributo chiave se la relativa tabella sottostante è direttamente collegata alla tabella dei fatti oppure è indirettamente collegato tramite l'attributo associato alla chiave nella tabella sottostante che collega la tabella con schema snowflake alla tabella collegata direttamente.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare gerarchie definite dall'utente](../multidimensional-models/user-defined-hierarchies-create.md)   
 [Definire relazioni tra attributi](../multidimensional-models/attribute-relationships-define.md)   
 [Riferimento alle proprietà degli attributi delle dimensioni](../multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
