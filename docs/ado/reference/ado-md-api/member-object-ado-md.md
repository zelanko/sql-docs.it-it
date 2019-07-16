---
title: Oggetto Member (ADO MD) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44d6b5f06bffb1cea786ba34d3d2aa8a3efb45ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949490"
---
# <a name="member-object-ado-md"></a>Oggetto Member (ADO MD)
Rappresenta un membro di un livello in un cubo, gli elementi figlio di un membro di un livello o un membro di una posizione lungo un asse di un set di celle.  
  
## <a name="remarks"></a>Note  
 Le proprietà di un **membro** differiscono a seconda del contesto in cui viene utilizzata. A **membro** di un [a livello](../../../ado/reference/ado-md-api/level-object-ado-md.md) in un [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) ha un [figli](../../../ado/reference/ado-md-api/children-property-ado-md.md) proprietà che restituisce il **membri** su il livello inferiore successivo della gerarchia dal corrente **membro**. Per un **membro** di un [posizione](../../../ado/reference/ado-md-api/position-object-ado-md.md), il **figli** raccolta è sempre vuota. Inoltre, il [tipo](../../../ado/reference/ado-md-api/type-property-ado-md.md) proprietà si applica solo a **membri** di un **livello**.  
  
 Oggetto **membro** di **posizione** ha due proprietà che sono utili quando si visualizzano i [Cellset](../../../ado/reference/ado-md-api/cellset-object-ado-md.md): [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) e [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md). Si verifica un errore se si accede a queste proprietà su un **membro** di un **livello**.  
  
 Con le raccolte e le proprietà di un **membro** oggetto di un **livello**, è possibile eseguire le operazioni seguenti:  
  
-   Identificare le **membro** con il [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) proprietà.  
  
-   Restituisce una stringa da usare quando si visualizzano le **membro** con il [didascalia](../../../ado/reference/ado-md-api/caption-property-ado-md.md) proprietà.  
  
-   Restituire una stringa significativa che descrive una misura o una formula **membro** con il [descrizione](../../../ado/reference/ado-md-api/description-property-ado-md.md) proprietà.  
  
-   Determinare la natura del **membro** con il [tipo](../../../ado/reference/ado-md-api/type-property-ado-md.md) proprietà.  
  
-   Ottenere informazioni sul **livello** del **membro** con il [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) e [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) proprietà.  
  
-   Ottenere correlati **membri** in un [gerarchia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md) con il [padre](../../../ado/reference/ado-md-api/parent-property-ado-md.md) e [figli](../../../ado/reference/ado-md-api/children-property-ado-md.md) proprietà.  
  
-   Numero di elementi figlio di un **membro** con il [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) proprietà.  
  
-   Utilizzare ADO standard [delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) insieme per ottenere informazioni aggiuntive sul **livello** oggetto.  
  
 Con le raccolte e le proprietà di un **membro** di un **posizione** lungo un [asse](../../../ado/reference/ado-md-api/axis-object-ado-md.md), è possibile eseguire le operazioni seguenti:  
  
-   Identificare le **membro** con il [Name](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) proprietà.  
  
-   Restituisce una stringa da usare quando si visualizzano le **membro** con il [didascalia](../../../ado/reference/ado-md-api/caption-property-ado-md.md) proprietà.  
  
-   Restituire una stringa significativa che descrive una misura o una formula **membro** con il [descrizione](../../../ado/reference/ado-md-api/description-property-ado-md.md) proprietà.  
  
-   Ottenere informazioni sul **livello** del **membro** con il [LevelDepth](../../../ado/reference/ado-md-api/leveldepth-property-ado-md.md) e [LevelName](../../../ado/reference/ado-md-api/levelname-property-ado-md.md) proprietà.  
  
-   Numero di elementi figlio di un **membro** con il [ChildCount](../../../ado/reference/ado-md-api/childcount-property-ado-md.md) proprietà.  
  
-   Usare la [DrilledDown](../../../ado/reference/ado-md-api/drilleddown-property-ado-md.md) proprietà per determinare se è presente almeno un elemento figlio nel **asse** subito dopo questo **membro**.  
  
-   Usare la [ParentSameAsPrev](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md) proprietà per determinare se l'elemento padre di questo **membro** corrisponde al padre di immediatamente precedente **membro**.  
  
-   Utilizzare ADO standard [delle proprietà](../../../ado/reference/ado-api/properties-collection-ado.md) insieme per ottenere informazioni aggiuntive sul **livello** oggetto.  
  
 Il **proprietà** raccolta contiene le proprietà specifiche del provider. La tabella seguente elenca le proprietà che potrebbero essere disponibili. L'elenco di proprietà effettivo può variare in base all'implementazione del provider. Vedere la documentazione per il provider per un elenco completo delle proprietà disponibili.  
  
|Nome|Descrizione|  
|----------|-----------------|  
|CatalogName|Il nome del catalogo a cui appartiene il cubo.|  
|ChildrenCardinality|Numero di elementi figlio del membro.|  
|CubeName|Nome del cubo.|  
|Descrizione|Una descrizione significativa del membro.|  
|DimensionUniqueName|Nome univoco della [dimensione](../../../ado/reference/ado-md-api/dimension-object-ado-md.md).|  
|HierarchyUniqueName|Nome univoco della gerarchia.|  
|LevelNumber|La distanza tra il livello e la radice della gerarchia.|  
|LevelUniqueName|Nome univoco del livello.|  
|MemberCaption|Etichetta o didascalia associata al membro.|  
|MemberGUID|GUID del membro.|  
|MemberName|Nome del membro.|  
|MemberOrdinal|Il numero ordinale del membro.|  
|Tipo di membro|Tipo del membro.|  
|MemberUniqueName|Nome univoco del membro.|  
|ParentCount|Il conteggio del numero di elementi padre con questo membro.|  
|ParentLevel|Il numero del livello dell'elemento padre del membro.|  
|ParentUniqueName|Nome univoco del padre membro.|  
|SchemaName|Il nome dello schema a cui appartiene il cubo.|  
  
 In questa sezione contiene gli argomenti seguenti.  
  
-   [Proprietà, metodi ed eventi](../../../ado/reference/ado-md-api/member-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di Catalog (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Raccolta Members (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)   
 [Raccolta delle proprietà (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
