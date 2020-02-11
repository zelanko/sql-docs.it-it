---
title: Attributi nelle gerarchie padre-figlio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data members [Analysis Services]
- nonleaf members
- MembersWithDataCaption property
- members [Analysis Services]
- members [Analysis Services], data
- leaf members
- parent-child dimensions [Analysis Services]
- MembersWithData property
ms.assetid: 249971cc-4bcd-44f1-8241-bdacc04d3d38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 35521a8f12d3e5c16e63ba883a2b5d561bde4c96
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073475"
---
# <a name="attributes-in-parent-child-hierarchies"></a>Attributi nelle gerarchie padre-figlio
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]viene in genere fatto un presupposto generale sul contenuto dei membri di una dimensione. I membri foglia contengono dati derivati direttamente da origini dei dati sottostanti, mentre i membri non foglia contengono dati derivati da aggregazioni eseguite su membri figlio.  
  
 In una gerarchia padre-figlio, tuttavia, alcuni membri non foglia potrebbero includere dati derivati da origini dei dati sottostanti oltre ai dati aggregati da membri figlio. Per questi membri non foglia di una gerarchia padre-figlio vengono creati membri figlio speciali generati dal sistema contenenti i dati della tabella dei fatti sottostante. Questi membri, denominati *membri dei dati*, contengono un valore direttamente associato a un membro non foglia indipendente dal valore di riepilogo calcolato dai discendenti del membro non foglia.  
  
 I membri dei dati sono disponibili solo per le dimensioni con gerarchie padre-figlio e sono visibili solo se l'attributo padre lo consente. È possibile utilizzare Progettazione dimensioni per controllare la visibilità dei membri dei dati. Per esporre i membri dei dati, impostare la proprietà `MembersWithData` dell'attributo padre su `NonLeafDataVisible.` Per nascondere i membri dei dati inclusi nell'attributo padre, impostare la proprietà `MembersWithData` dell'attributo padre su `NonLeafDataHidden`.  
  
 Questa impostazione non altera la normale modalità di aggregazione dei membri non foglia in quanto il membro dei dati viene sempre incluso come membro figlio ai fini dell'aggregazione. È tuttavia possibile utilizzare una formula personalizzata di rollup per ignorare la normale modalità di aggregazione. La funzione MDX (Multidimensional Expressions) [DataMember](/sql/mdx/datamember-mdx) consente di accedere al valore del membro dati associato indipendentemente dal valore della `MembersWithData` proprietà.  
  
 La proprietà `MembersWithDataCaption` dell'attributo padre indica a [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] il modello di denominazione da utilizzare per generare i nomi dei membri dei dati.  
  
## <a name="using-data-members"></a>Utilizzo dei membri dei dati  
 I membri dei dati sono utili durante l'aggregazione di misure in base a dimensioni organizzative con gerarchie padre-figlio. Ad esempio, nella figura seguente viene illustrata una dimensione con tre livelli, rappresentante il volume delle vendite lorde dei prodotti. Il primo livello indica il volume delle vendite lorde per tutti i rappresentanti. Il secondo livello include il volume delle vendite lorde per tutto il personale addetto alle vendite raggruppato in base al responsabile delle vendite e il terzo livello include il volume delle vendite lorde per tutto il personale addetto alle vendite raggruppato in base al rappresentante.  
  
 ![Dimensione del volume delle vendite lorde con tre livelli](../media/agdatamember1.gif "Dimensione del volume delle vendite lorde con tre livelli")  
  
 In genere, il valore del membro Sales Manager 1 verrebbe derivato dall'aggregazione dei valori dei membri Salesperson 1 e Salesperson 2. Tuttavia, poiché anche Sales Manager 1 può vendere prodotti, tale membro può inoltre includere dati derivati dalla tabella dei fatti, in quanto a Sales Manager 1 potrebbero essere associate vendite lorde.  
  
 Le commissioni individuali per ogni membro del personale addetto alle vendite, inoltre, possono essere diverse. In questo caso, vengono utilizzate due scale diverse per calcolare le commissioni per le vendite lorde individuali dei responsabili delle vendite rispetto alle vendite lorde totali generate dai rappresentanti. Pertanto, è importante poter accedere ai dati della tabella dei fatti sottostante per i membri non foglia. Per recuperare il volume delle vendite lorde individuali per il membro Sales Manager 1, è possibile utilizzare la funzione MDX `DataMember`, mentre per escludere il membro dei dati dal valore aggregato del membro Sales Manager 1 in modo da ottenere il volume delle vendite lorde per i rappresentanti associati a tale membro, è possibile utilizzare un'espressione di rollup personalizzata.  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento alle proprietà degli attributi delle dimensioni](dimension-attribute-properties-reference.md)   
 [Gerarchia padre-figlio](parent-child-dimension.md)  
  
  
