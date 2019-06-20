---
title: Istruzione ALTER CUBE Statement (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f9a15108875c7e519948f0e73e0a87d08b70c975
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63315290"
---
# <a name="mdx-data-definition---alter-cube"></a>Definizione dei dati MDX - ALTER CUBE


  Modifica la struttura di un cubo specificato, utilizzato in genere per supportare il writeback della dimensione. Per altre informazioni sull'utilizzo del writeback in un'applicazione, vedere questo blog post: [Creazione di un'applicazione di Writeback con Analysis Services (blog)](https://go.microsoft.com/fwlink/?LinkId=394977)  
  
 Si tenga presente che i writeback delle dimensioni concorrenti possono provocare un deadlock, dove il primo writeback viene bloccato da un commit a causa del blocco condiviso tenuto dal secondo writeback. In tale situazione non viene generato alcun errore ma non potrà essere eseguita alcuna operazione. Infine, viene eseguito il rollback sia del timeout che delle modifiche.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
ALTER CUBE  
      Cube_Name | CURRENTCUBE  
      <alter clause>   
            [ < alter clause> ...n]  
  
< alter clause> ::=   
   <create dimension member clause>   
  | <remove dimension member clause>  
  | <move dimension member clause>   
    | <update clause>   
    | <create cell calculation clause>  
  
<create dimension member clause> ::=  
CREATE DIMENSION MEMBER [ParentName.]MemberName  
    , [[KEY = Key_Value]   
    | [Property_Name = Property_Value[, ...n]]  
  
<dropping clause>::=  
DROP   
      DIMENSION MEMBER Member_Name   
            Member_Name ...n ]   
      [WITH DESCENDANTS]  
      | [ SESSION ] [ CALCULATED ] MEMBER Member_Name   
                  [ ,Member_Name,...n ]   
    | SET Set_Name  
                  [ ,Set_Name,...n ]   
    | [ SESSION ] CELL CALCULATION CellCalc_Name  
                  [ ,CellCalc_Name,...n ]   
    | ACTION Action_Name  
  
<move dimension member clause> ::=  
MOVE DIMENSION MEMBER MemberName  
        [, SKIPPED_LEVELS = Unsigned_Integer]   
      [WITH DESCENDANTS]  
    UNDER ParentName      
  
<update clause> ::=  
UPDATE   
    CUSTOM ROLLUP FOR MEMBER MemberName  
      [,MemberName, ...n] AS MDX_Expression  
   | DIMENSION Dimension_Name | Hierarchy_Name  
      , DEFAULT_MEMBER = MDX_Expression  
   | DIMENSION MEMBER MemberName AS  
   [MDX_Expression]  
   [Property_Name = Property_Value[, ...n]]  
  
<create cell calculation clause>::=  
CELL CALCULATION Calculation_Name   
   FOR Set_Expression AS MDX_Expression   
            [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="creating-a-dimension-member"></a>Creazione di un membro in una dimensione  
 Viene aggiunta una riga alla tabella della dimensione sottostante.  
  
### <a name="arguments"></a>Argomenti  
 *ParentName*  
 Espressione stringa valida che specifica il nome del padre del nuovo membro della dimensione, a meno che questo non venga creato nella radice.  
  
 *MemberName*  
 Espressione stringa valida che specifica il nome di un membro.  
  
 *Key_Value*  
 Espressione scalare valida che definisce il valore chiave del nuovo membro della dimensione.  
  
 *Property_Name*  
 Identificatore MDX (Multidimensional Expression) valido che rappresenta la proprietà di un membro.  
  
 *Property_Value*  
 Espressione scalare MDX (Multidimensional Expression) valida che definisce il valore della proprietà di un membro calcolato.  
  
## <a name="dropping-a-dimension-member"></a>Eliminazione di un membro in una dimensione  
 La rimozione di un membro da una dimensione abilitata per la scrittura consente di eliminare il membro e la riga corrispondente dalla tabella della dimensione sottostante.  
  
### <a name="arguments"></a>Argomenti  
 *Cube_Name*  
 Espressione stringa valida che specifica il nome di un cubo.  
  
 *Member_Name*  
 Espressione stringa valida che specifica il nome o la chiave di un membro.  
  
### <a name="remarks"></a>Note  
 Se non si utilizza la clausola WITH DESCENDANTS, i figli del membro eliminato diventano figli del padre di tale membro. Se si utilizza la clausola WITH DESCENDANTS, vengono inoltre eliminati tutti i discendenti e le relative righe nella tabella della dimensione.  
  
> [!NOTE]  
>  Per informazioni sull'eliminazione di membri calcolati, set denominati, azioni e calcoli di celle, vedere [DROP MEMBER-istruzione &#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md), [DROP impostare l'istruzione &#40;MDX&#41;](../mdx/mdx-data-definition-drop-set.md), [DROP ACTION-istruzione &#40;MDX&#41;](../mdx/mdx-data-definition-drop-action.md), e [DROP cella CALCULATION-istruzione &#40;MDX&#41;](../mdx/mdx-data-definition-drop-cell-calculation.md).  
  
## <a name="updating-the-default-dimension-member"></a>Aggiornamento del membro predefinito in una dimensione  
 Questa clausola consente di aggiornare il membro predefinito di un cubo e viene utilizzata nello script di calcolo MDX per definire un membro predefinito. È possibile specificare il membro predefinito per la dimensione del database, la dimensione di un cubo o l'account di accesso di un utente. È inoltre possibile cambiare il membro predefinito durante una sessione.  
  
### <a name="arguments"></a>Argomenti  
 *Dimension_Name*  
 Stringa valida che specifica il nome di una dimensione.  
  
 *MDX_Expression*  
 Espressione MDX valida che restituisce un unico membro.  
  
### <a name="remarks"></a>Note  
 L'espressione MDX specificata può essere statica o dinamica.  
  
## <a name="moving-a-dimension-member"></a>Spostamento di un membro in una dimensione  
 Nella tabella delle dimensioni sottostante viene modificata una riga.  
  
### <a name="arguments"></a>Argomenti  
 *ParentName*  
 Espressione stringa valida che specifica il nome del nuovo padre per il membro della dimensione da spostare.  
  
 *MemberName*  
 Espressione stringa valida che specifica il nome di un membro.  
  
 Unsigned_*Integer*  
 Numero valido che specifica il numero di livelli da ignorare.  
  
 Se si specifica la clausola WITH DESCENDANTS, viene spostata l'intero albero. Se non si specifica la clausola WITH DESCENDANTS, i figli del membro spostato diventano figli del padre di tale membro. L'effetto dello spostamento è semplicemente l'aggiornamento dei valori della colonna chiave padre nella tabella della dimensione sottostante.  
  
## <a name="updating-a-dimension-member"></a>Aggiornamento di un membro in una dimensione  
 La clausola UPDATE DIMENSION MEMBER consente di modificare le proprietà di un membro oltre alla formula personalizzata membro associata a un membro.  
  
### <a name="arguments"></a>Argomenti  
 *MemberName*  
 Espressione stringa valida che specifica il nome di un membro.  
  
 *MDX_Expression*  
 Espressione MDX valida che restituisce un unico membro.  
  
 *Property_Value*  
 Espressione scalare MDX valida che definisce il valore della proprietà di un membro calcolato.  
  
## <a name="creating-a-cell-calculation"></a>Creazione di una formula per il calcolo di celle  
 Per altre informazioni sulla creazione di un calcolo di celle tramite l'istruzione ALTER CUBE, vedere [DROP cella CALCULATION-istruzione &#40;MDX&#41;](../mdx/mdx-data-definition-drop-cell-calculation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni di definizione dei dati MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
