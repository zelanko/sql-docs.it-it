---
title: Utilizzo dell'istruzione DRILLTHROUGH per recuperare i dati di origine (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 81c873d0ea6e5c21d97fc719ce1c72a773df43e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62802836"
---
# <a name="mdx-data-manipulation---retrieve-source-data-using-drillthrough"></a>Manipolazione dei dati MDX - Recuperare i dati di origine con DRILLTHROUGH
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Nel linguaggio MDX (Multidimensional Expressions) è disponibile l'istruzione [DRILLTHROUGH](../../../mdx/mdx-data-manipulation-drillthrough.md), che consente di recuperare un set di righe dai dati di origine per una cella di un cubo.  
  
 Per eseguire un'istruzione **DRILLTHROUGH** su un cubo, è necessario definire un'azione drill-through per tale cubo. Per definire un'azione drill-through, in Progettazione cubi di [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]nel riquadro **Azioni** fare clic sul pulsante **Nuova azione drill-through**della barra degli strumenti. Nella nuova azione drill-through specificare il nome, la destinazione e la condizione dell'azione, nonché le colonne restituite dall'istruzione **DRILLTHROUGH** .  
  
## <a name="drillthrough-statement-syntax"></a>Sintassi dell'istruzione DRILLTHROUGH  
 La sintassi dell'istruzione **DRILLTHROUGH** è la seguente:  
  
```  
<drillthrough> ::= DRILLTHROUGH [<Max_Rows>] [<First_Rowset>] <MDX select> [<Return_Columns>]  
   < Max_Rows> ::= MAXROWS <positive number>  
   <First_Rowset> ::= FIRSTROWSET <positive number>  
   <Return_Columns> ::= RETURN <member or attribute> [, <member or attribute>]  
```  
  
 La clausola **SELECT** identifica la cella del cubo che contiene i dati di origine da recuperare. Questa clausola **SELECT** è identica a una normale istruzione **SELECT** MDX, con la differenza che in questo caso nella clausola **SELECT** è possibile specificare solo un membro per ogni asse. Se su un asse sono specificati più membri, verrà generato un errore.  
  
 La sintassi `<Max_Rows>` specifica il numero massimo di righe in ogni set di righe restituito. Se il provider OLE DB uso per connettersi all'origine dati non supporta **DBPROP_MAXROWS**, l'impostazione `<Max_Rows>` verrà ignorata.  
  
 La sintassi `<First_Rowset>` identifica la partizione il cui set di righe viene restituito per primo.  
  
 La sintassi `<Return_Columns>` identifica le colonne del database sottostante da restituire.  
  
## <a name="drillthrough-statement-example"></a>Esempio di istruzione DRILLTHROUGH  
 Nell'esempio seguente viene illustrato l'uso dell'istruzione **DRILLTHROUGH** . In questo esempio l'istruzione DRILLTHROUGH esegue una query sugli elementi foglia delle dimensioni Store, Product e Time, lungo la dimensione Stores (l'asse di sezionamento), e quindi restituisce il gruppo di misure del reparto, l'ID del reparto e il nome del dipendente.  
  
```  
DRILLTHROUGH  
Select {Leaves(Store), Leaves(Product), Leaves(Time),*} on 0  
From Stores  
RETURN [Department MeasureGroup].[Department Id], [Employee].[First Name]  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Manipolazione dei dati &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
