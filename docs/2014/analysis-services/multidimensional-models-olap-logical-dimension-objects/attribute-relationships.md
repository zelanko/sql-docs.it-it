---
title: Relazioni tra attributi | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- member properties [Analysis Services], attribute relationships
- security [Analysis Services], properties
- PROPERTIES keyword
- storage [Analysis Services], attribute relationships
- natural hierarchies [Analysis Services]
- dimensions [Analysis Services], member properties
- queries [MDX], attribute relationships
- user-defined hierarchies [Analysis Services]
- attributes [Analysis Services], relationships
- member properties [Analysis Services]
- members [Analysis Services], attribute relationships
- storing data [Analysis Services], attribute relationships
- relationships [Analysis Services], attributes
ms.assetid: 2491422a-4cf5-4b23-b6ab-289222b22ce8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4401eea7e5c5b42c1706095e4c14aee348298bc5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52512777"
---
# <a name="attribute-relationships"></a>Relazioni tra attributi
  Nelle [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], gli attributi all'interno di una dimensione sono sempre correlati direttamente o indirettamente all'attributo chiave. Quando si definisce una dimensione in base a uno schema star, in cui tutti gli attributi della dimensione sono derivati dalla stessa tabella relazionale, viene automaticamente definita una relazione tra l'attributo chiave e ogni attributo non chiave della dimensione. Quando si definisce una dimensione in base a uno schema snowflake, in cui gli attributi della dimensione sono derivati da più tabelle correlate, viene automaticamente definita una relazione tra attributi come indicato di seguito:  
  
-   Tra l'attributo chiave e ogni attributo non chiave associato alle colonne della tabella principale della dimensione.  
  
-   Tra l'attributo chiave e l'attributo associato alla chiave esterna della tabella secondaria che collega le tabelle delle dimensioni sottostanti.  
  
-   Tra l'attributo associato alla chiave esterna della tabella secondaria e ogni attributo non chiave associato alle colonne della tabella secondaria.  
  
 Vi sono, tuttavia, molti motivi per cui potrebbe essere necessario modificare queste relazioni tra attributi predefinite. Potrebbe, ad esempio, essere necessario definire una gerarchia naturale, un ordinamento personalizzato o una granularità della dimensione basata su un attributo non chiave. Per altre informazioni, vedere [Dimension Attribute Properties Reference](../multidimensional-models/dimension-attribute-properties-reference.md).  
  
> [!NOTE]  
>  Le relazioni tra attributi sono note nelle espressioni MDX (Multidimensional Expression) come proprietà del membro.  
  
## <a name="natural-hierarchy-relationships"></a>Relazioni di gerarchia naturale  
 Una gerarchia è naturale quando ogni attributo incluso nella gerarchia definita dall'utente ha una relazione uno-a-molti con l'attributo immediatamente sottostante. Considerare, ad esempio, una dimensione Customer basata su una tabella di origine relazionale con otto colonne:  
  
-   CustomerKey  
  
-   CustomerName  
  
-   Age  
  
-   Gender  
  
-   Email  
  
-   Città  
  
-   Country  
  
-   Region  
  
 La dimensione di Analysis Services corrispondente ha sette attributi:  
  
-   Customer (basato su CustomerKey, con CustomerName che definisce i nomi dei membri)  
  
-   Age, Gender, Email, City, Region, Country  
  
 Le relazioni che rappresentano gerarchie naturali vengono applicate creando una relazione fra l'attributo per un livello e l'attributo per il livello sottostante. Per [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] questa operazione specifica una relazione naturale e un'aggregazione potenziale. Nella dimensione Customer è presente una gerarchia naturale per gli attributi Country, Region, City e Customer. La gerarchia naturale per `{Country, Region, City, Customer}` viene descritta aggiungendo le relazioni tra attributi seguenti:  
  
-   Attributo Country come relazione tra attributi dell'attributo Region.  
  
-   Attributo Region come relazione tra attributi dell'attributo City.  
  
-   Attributo City come relazione tra attributi dell'attributo Customer.  
  
 Per l'esplorazione dei dati nel cubo, è anche possibile creare una gerarchia definita dall'utente che non rappresenta una gerarchia naturale nei dati (che viene chiamato un *ad hoc* oppure *reporting* gerarchia). È ad esempio possibile creare una gerarchia basata su `{Age, Gender}`. Gli utenti non viene visualizzata alcuna differenza nel comportano dei due gerarchie, anche se la gerarchia naturale tragga vantaggio dall'aggregazione e indicizzazione di strutture, nascoste all'utente - dall'account per le relazioni naturali nei dati di origine.  
  
 La proprietà `SourceAttribute` di un livello determina l'attributo utilizzato per descrivere il livello. La proprietà `KeyColumns` dell'attributo specifica la colonna della vista origine dati che definisce i membri. La proprietà `NameColumn` dell'attributo può specificare una colonna dei nomi differente per i membri.  
  
 Per definire un livello in una gerarchia definita dall'utente tramite [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], il **progettazione dimensioni** consente di selezionare un attributo della dimensione, una colonna nella tabella della dimensione o una colonna di una tabella correlata inclusa nella vista origine dati per il cubo. Per altre informazioni sulla creazione di gerarchie definite dall'utente, vedere [gerarchie definite dall'utente](../multidimensional-models/user-defined-hierarchies-create.md).  
  
 Relativamente al contenuto dei membri, in Analysis Services ci si basa in genere sul presupposto che i membri foglia non abbiano discendenti e contengano dati derivati dalle origini dei dati sottostanti, mentre i membri non foglia abbiano discendenti e contengano dati derivati dalle aggregazioni eseguite sui membri figlio. Nei livelli aggregati i membri sono basati sulle aggregazioni di livelli subordinati. Quando, perciò, la proprietà `IsAggregatable` viene impostata su `False` in un attributo di origine per un livello, non devono essere aggiunti attributi che possono essere aggregati come livelli al di sopra di esso.  
  
## <a name="defining-an-attribute-relationship"></a>Definizione di una relazione tra attributi  
 Il vincolo principale quando si crea una relazione tra attributi consiste nel verificare che l'attributo a cui la relazione fa riferimento non abbia più di un valore per ogni membro nell'attributo a cui appartiene la relazione tra attributi. Se, ad esempio, si definisce una relazione tra un attributo City e un attributo State, ogni città può essere in relazione solo con un unico stato.  
  
## <a name="attribute-relationship-queries"></a>Query sulla relazione tra attributi  
 È possibile utilizzare query MDX per recuperare dati dalle relazioni tra attributi in forma di proprietà del membro, tramite la parola chiave `PROPERTIES` dell'istruzione `SELECT` MDX. Per altre informazioni su come usare MDX per recuperare le proprietà dei membri, vedere [usando le proprietà del membro &#40;MDX&#41;](../multidimensional-models/mdx/mdx-member-properties.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi e gerarchie di attributi](attributes-and-attribute-hierarchies.md)   
 [Riferimento alle proprietà degli attributo delle dimensioni](../multidimensional-models/dimension-attribute-properties-reference.md)   
 [Gerarchie definite dall'utente](user-hierarchies.md)   
 [Proprietà delle gerarchie definite dall'utente](user-hierarchies-properties.md)  
  
  
