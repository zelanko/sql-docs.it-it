---
title: Oggetto member (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member
helpviewer_keywords:
- Member object [ADO MD], members
ms.assetid: 3dedf755-0741-4c3f-8b4e-bff8ff8809c8
author: rothja
ms.author: jroth
ms.openlocfilehash: d4d512d651c8162124c935ffdb260c4abe4ecb14
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82753203"
---
# <a name="member-object-ado-md"></a>Oggetto Member (ADO MD)
Rappresenta un membro di un livello in un cubo, gli elementi figlio di un membro di un livello o un membro di una posizione lungo un asse di un insieme di celle.  
  
## <a name="remarks"></a>Commenti  
 Le proprietà di un **membro** variano a seconda del contesto in cui viene utilizzata. Un **membro** di un [livello](../../../ado/reference/ado-md-api/level-object-ado-md.md) in un [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) ha una proprietà [Children](../../../ado/reference/ado-md-api/children-property-ado-md.md) che restituisce i **membri** al livello inferiore successivo della gerarchia dal **membro**corrente. Per un **membro** di una [posizione](../../../ado/reference/ado-md-api/position-object-ado-md.md), la raccolta **Children** è sempre vuota. Inoltre, la proprietà [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md) si applica solo ai **membri** di un **livello**.  
  
 Un **membro** di **position** dispone di due proprietà che risultano utili quando si visualizzano le [celle](../../../ado/reference/ado-md-api/cellset-object-ado-md.md): [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) e [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md). Si verificherà un errore se si accede a queste proprietà in un **membro** di un **livello**.  
  
 Con le raccolte e le proprietà di un oggetto **membro** di un **livello**, è possibile eseguire le operazioni seguenti:  
  
-   Identificare il **membro** con le proprietà [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Restituisce una stringa da usare quando si Visualizza il **membro** con la proprietà [Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md) .  
  
-   Restituisce una stringa significativa che descrive un **membro** della misura o della formula con la proprietà [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Determinare la natura del **membro** con la proprietà [Type](../../../ado/reference/ado-md-api/type-property-ado-md.md) .  
  
-   Ottenere informazioni sul **livello** del **membro** con le proprietà [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) e [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) .  
  
-   Ottenere **membri** correlati in una [gerarchia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) con le proprietà [Parent](../../../ado/reference/ado-md-api/parent-property-ado-md.md) e [Children](../../../ado/reference/ado-md-api/children-property-ado-md.md) .  
  
-   Contare gli elementi figlio di un **membro** con la proprietà [childCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) .  
  
-   Utilizzare la raccolta delle [Proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) ADO standard per ottenere informazioni aggiuntive sull'oggetto **Level** .  
  
 Con le raccolte e le proprietà di un **membro** di una **posizione** lungo un [asse](../../../ado/reference/ado-md-api/axis-object-ado-md.md), è possibile eseguire le operazioni seguenti:  
  
-   Identificare il **membro** con le proprietà [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) .  
  
-   Restituisce una stringa da usare quando si Visualizza il **membro** con la proprietà [Caption](../../../ado/reference/ado-md-api/caption-property-ado-md.md) .  
  
-   Restituisce una stringa significativa che descrive un **membro** della misura o della formula con la proprietà [Description](../../../ado/reference/ado-md-api/description-property-ado-md.md) .  
  
-   Ottenere informazioni sul **livello** del **membro** con le proprietà [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) e [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) .  
  
-   Contare gli elementi figlio di un **membro** con la proprietà [childCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) .  
  
-   Utilizzare la proprietà [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) per determinare se è presente almeno un elemento figlio sull' **asse** che segue immediatamente il **membro**.  
  
-   Utilizzare la proprietà [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md) per determinare se l'elemento padre di questo **membro** è uguale all'elemento padre del **membro**immediatamente precedente.  
  
-   Utilizzare la raccolta delle [Proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) ADO standard per ottenere informazioni aggiuntive sull'oggetto **Level** .  
  
 La raccolta **Properties** contiene proprietà fornite dal provider. Nella tabella seguente sono elencate le proprietà che potrebbero essere disponibili. L'elenco di proprietà effettivo può variare a seconda dell'implementazione del provider. Per un elenco più completo delle proprietà disponibili, vedere la documentazione relativa al provider.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|CatalogName|Nome del catalogo a cui appartiene il cubo.|  
|ChildrenCardinality|Numero di elementi figlio del membro.|  
|CubeName|Nome del cubo.|  
|Descrizione|Descrizione significativa del membro.|  
|DimensionUniqueName|Nome non ambiguo della [dimensione](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|Nome non ambiguo della gerarchia.|  
|LevelNumber|Distanza tra il livello e la radice della gerarchia.|  
|LevelUniqueName|Nome non ambiguo del livello.|  
|MemberCaption|Etichetta o didascalia associata al membro.|  
|MemberGUID|GUID del membro.|  
|MemberName|Nome del membro.|  
|MemberOrdinal|Numero ordinale del membro.|  
|MemberType|Tipo del membro.|  
|MemberUniqueName|Nome non ambiguo del membro.|  
|ParentCount|Conteggio del numero di elementi padre del membro.|  
|ParentLevel|Numero di livello dell'elemento padre del membro.|  
|ParentUniqueName|Nome non ambiguo dell'elemento padre del membro.|  
|SchemaName|Nome dello schema a cui appartiene il cubo.|  
  
 Questa sezione contiene l'argomento seguente.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di catalogo (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Raccolta Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Raccolta Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
