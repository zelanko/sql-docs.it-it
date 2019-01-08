---
title: Usando le proprietà delle celle (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- intrinsic cell properties [MDX]
- cells [MDX]
- cell properties [MDX]
- CELL PROPERTIES keyword
ms.assetid: a593c74d-8c5e-485e-bd92-08f9d22451d4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a8b302391eb4e7384a54181b102f4ae8f3de522
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52417752"
---
# <a name="using-cell-properties-mdx"></a>Utilizzo delle proprietà delle celle (MDX)
  Nel linguaggio MDX (Multidimensional Expressions) le proprietà delle celle includono informazioni sul contenuto e il formato delle celle di un'origine dei dati multidimensionale, ad esempio un cubo.  
  
 MDX supporta l'utilizzo della parola chiave CELL PROPERTIES in un'istruzione MDX SELECT per il recupero delle proprietà intrinseche delle celle. Le proprietà intrinseche delle celle vengono in genere utilizzate per la presentazione visiva dei dati delle celle.  
  
## <a name="cell-properties-keyword-syntax"></a>Sintassi della parola chiave CELL PROPERTIES  
 La sintassi della parola chiave `CELL PROPERTIES` dell'istruzione MDX `SELECT` è la seguente:  
  
```  
SELECT [<axis_specification>  
       [, <axis_specification>...]]  
  FROM [<cube_specification>]  
[WHERE [<slicer_specification>]]  
[<cell_props>]  
```  
  
 Nella sintassi seguente è illustrato il formato del valore `<cell_props>` e come tale valore utilizza la parola chiave `CELL PROPERTIES` insieme a una o più proprietà intrinseche delle celle:  
  
```  
<cell_props> ::= CELL PROPERTIES <property> [, <property>...]  
```  
  
## <a name="supported-intrinsic-cell-properties"></a>Proprietà intrinseche delle celle supportate  
 Nella tabella seguente sono elencate le proprietà intrinseche delle celle supportate che vengono utilizzate nel valore `<property>` .  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|`ACTION_TYPE`|Maschera di bit che indica i tipi di azioni esistenti sulla cella. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **MDACTION_TYPE_URL**<br /><br /> **MDACTION_TYPE_HTML**<br /><br /> **MDACTION_TYPE_STATEMENT**<br /><br /> **MDACTION_TYPE_DATASET**<br /><br /> **MDACTION_TYPE_ROWSET**<br /><br /> **MDACTION_TYPE_COMMANDLINE**<br /><br /> **MDACTION_TYPE_PROPRIETARY**<br /><br /> **MDACTION_TYPE_REPORT**<br /><br /> **MDACTION_TYPE_DRILLTHROUGH**<br /><br /> <br /><br /> Nota: Le operazioni di drill-through non sono incluse per le query che contengono un set nella clausola WHERE.|  
|**BACK_COLOR**|Colore di sfondo per la visualizzazione della proprietà `VALUE` o `FORMATTED_VALUE`. Per altre informazioni, vedere [Contenuto di FORE_COLOR e BACK_COLOR &#40;MDX&#41;](mdx-cell-properties-fore-color-and-back-color-contents.md).|  
|`CELL_ORDINAL`|Numero ordinale della cella nel set di dati.|  
|**FONT_FLAGS**|Maschera di bit che indica in dettaglio gli effetti sul carattere. Il valore 5 rappresenta ad esempio l'applicazione combinata degli effetti grassetto (`MDFF_BOLD`) e sottolineato (`MDFF_UNDERLINE`) al carattere. Il valore è il risultato di un'operazione con OR bit per bit su una o più delle costanti seguenti:<br /><br /> `MDFF_BOLD` = 1<br /><br /> `MDFF_ITALIC` = 2<br /><br /> `MDFF_UNDERLINE` = 4<br /><br /> `MDFF_STRIKEOUT` = 8|  
|**FONT_NAME**|Tipo di carattere da utilizzare per la visualizzazione della proprietà `VALUE` o `FORMATTED_VALUE`.|  
|**FONT_SIZE**|Dimensioni del carattere da utilizzare per la visualizzazione della proprietà `VALUE` o `FORMATTED_VALUE`.|  
|**FORE_COLOR**|Colore di primo piano per la visualizzazione della proprietà `VALUE` o `FORMATTED_VALUE`. Per altre informazioni, vedere [Contenuto di FORE_COLOR e BACK_COLOR &#40;MDX&#41;](mdx-cell-properties-fore-color-and-back-color-contents.md).|  
|`FORMAT`|Come per `FORMAT_STRING`.|  
|`FORMAT_STRING`|Stringa di formato utilizzata per creare il valore della proprietà `FORMATTED_VALUE`. Per altre informazioni, vedere [Contenuto di FORMAT_STRING &#40;MDX&#41;](mdx-cell-properties-format-string-contents.md).|  
|`FORMATTED_VALUE`|Stringa di caratteri che rappresenta una visualizzazione formattata della proprietà `VALUE`.|  
|`LANGUAGE`|Le impostazioni locali dove verrà applicato `FORMAT_STRING`. `LANGUAGE` è utilizzato generalmente per la conversione della valuta.|  
|`UPDATEABLE`|Valore che indica se la cella può essere aggiornata. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> `MD_MASK_ENABLED` (0x00000000) la cella può essere aggiornata.<br /><br /> `MD_MASK_NOT_ENABLED` (0x10000000) la cella non può essere aggiornata.<br /><br /> `CELL_UPDATE_ENABLED` (0x00000001) la cella può essere aggiornata nel set di celle.<br /><br /> `CELL_UPDATE_ENABLED_WITH_UPDATE` (0x00000002) la cella può essere aggiornata con un'istruzione update. Se si aggiorna una cella foglia non abilitata per la scrittura, l'aggiornamento potrebbe non riuscire.<br /><br /> `CELL_UPDATE_NOT_ENABLED_FORMULA` (0x10000001) la cella non può essere aggiornata perché la cella contiene un membro calcolato le sue coordinate; la cella è stata recuperata con un set in where clausola. È possibile aggiornare una cella anche se il suo valore è influenzato da una formula o da una cella calcolata, ovvero si trova in un punto qualsiasi del percorso di aggregazione. In questo scenario, il valore finale della cella potrebbe non essere il valore aggiornato, perché il risultato è influenzato dal calcolo.<br /><br /> `CELL_UPDATE_NOT_ENABLED_NONSUM_MEASURE` (0x10000002) la cella non può essere aggiornata perché non è possibile aggiornare misure non sum (count, min, max, distinct count, semiadditive e).<br /><br /> `CELL_UPDATE_NOT_ENABLED_NACELL_VIRTUALCUBE` (0x10000003) la cella non può essere aggiornata perché non esiste, poiché si trova in corrispondenza dell'intersezione di una misura e un membro della dimensione non correlato al gruppo di misure della misura.<br /><br /> `CELL_UPDATE_NOT_ENABLED_SECURE` (0x10000005) la cella non può essere aggiornata perché è protetta.<br /><br /> `CELL_UPDATE_NOT_ENABLED_CALCLEVEL` (0x10000006) riservato per utilizzi futuri.<br /><br /> `CELL_UPDATE_NOT_ENABLED_CANNOTUPDATE` (0x10000007) la cella non può essere aggiornata per motivi interni.<br /><br /> `CELL_UPDATE_NOT_ENABLED_INVALIDDIMENSIONTYPE` (0x10000009) la cella non può essere aggiornata perché l'aggiornamento non è supportato in modelli di data mining, indirette o di dimensioni di data mining.|  
|`VALUE`|Valore non formattato della cella.|  
  
 Sono obbligatorie solo le proprietà `CELL_ORDINAL`, `FORMATTED_VALUE` e `VALUE`. Tutte le proprietà delle celle, intrinseche o specifiche del provider, sono definite nel set di righe dello schema `PROPERTIES`, inclusi i tipi di dati e il supporto del provider. Per altre informazioni sul `PROPERTIES` set di righe dello schema, vedere [set di righe MDSCHEMA_PROPERTIES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-properties-rowset).  
  
 Per impostazione predefinita, se non viene utilizzata la parola chiave `CELL PROPERTIES` verranno restituite, nell'ordine, le proprietà delle celle `VALUE`, `FORMATTED_VALUE` e `CELL_ORDINAL`. Se è specificata la parola chiave `CELL PROPERTIES`, verranno restituite solo le proprietà delle celle indicate in modo esplicito con la parola chiave.  
  
 Nell'esempio seguente viene illustrato l'utilizzo della parola chiave `CELL PROPERTIES` in una query MDX:  
  
```  
SELECT  
   {[Measures].[Reseller Gross Profit]} ON COLUMNS,  
   {[Reseller].[Reseller Type].[Reseller Name].Members} ON ROWS  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORMAT_STRING, FORE_COLOR, BACK_COLOR  
```  
  
 Le proprietà delle celle non vengono restituite per le query MDX che restituiscono set di righe bidimensionali. In questo caso, ogni cella viene rappresentata come se fosse restituita solo la proprietà `FORMATTED_VALUE` della cella.  
  
## <a name="setting-cell-properties"></a>Impostazione delle proprietà delle celle  
 In [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] è possibile impostare le proprietà di cella in diverse posizioni. È possibile, ad esempio, impostare la proprietà Stringa di formato per misure regolari nella scheda Struttura cubo dell'Editor di cubi in [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]. La stessa proprietà può essere impostata per misure calcolate definite nel cubo nella scheda Calcoli dell'Editor di cubi. La stringa di formato delle misure calcolate definite nella clausola WITH di una query è anch'essa definita in questa clausola. La query seguente illustra come è possibile impostare le proprietà di cella in una misura calcolata:  
  
```  
WITH MEMBER MEASURES.CELLPROPERTYDEMO AS [Measures].[Internet Sales Amount]  
, FORE_COLOR=RGB(0,0,255)  
, BACK_COLOR=IIF([Measures].[Internet Sales Amount]>7000000, RGB(255,0,0), RGB(0,255,0))  
, FONT_SIZE=10  
, FORMAT_STRING='#,#.000'  
SELECT MEASURES.CELLPROPERTYDEMO ON 0,  
[Date].[Calendar Year].[Calendar Year].MEMBERS ON 1  
FROM [Adventure Works]  
CELL PROPERTIES VALUE, FORMATTED_VALUE, FORE_COLOR, BACK_COLOR, FONT_SIZE  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
