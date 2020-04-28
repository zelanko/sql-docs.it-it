---
title: Istruzione CREATE SESSION CUBE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ac95afcebcf07a5d691db5f2599b3290b9587d44
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68038366"
---
# <a name="mdx-data-definition---create-session-cube"></a>Definizione dei dati MDX - CREATE SESSION CUBE


  Crea e popola un cubo di sessione da un cubo esistente presente sul server. Il cubo di sessione è visibile solo all'interno della sessione corrente. Non può essere visualizzato, né possono essere eseguite query su di esso da altre sessioni. Viene eliminato in modo implicito alla chiusura della sessione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CREATE SESSION CUBE session_cube_name FROM <cube list> (<param list>)  
  
<cube list>::= source_cube_name [,<cube list>]  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= <reg dim from clause>   
  
<dim reg from clause>::= dimension_name  
  
<dim content def>::= ( <level list> [,<grouping list>] [,<member slice list>] [,<default member>] )  
  
<level list>::= <level def> [, <level list>]  
  
<level def>::= LEVEL level_name [<level type> ] [AS level_name] [<level content def>]  
  
<level content def>::= ( <property list> ) | NO_PROPERTIES  
  
<level type>::= GROUPING  
  
<property list>::= <property def> [, <property list>]  
  
<property def>::= PROPERTY property_name   
  
<grouping list>::= <grouping entity> [,<grouping list>]  
  
<grouping entity>::= GROUP group_level_name.group_name (<mixed list>)  
  
<grp mixed list>::= <grp mixed element> [,<grp mixed list>]  
  
<grp mixed element>::= <grouping entity> | <member def>  
  
<member slice list>::= <member list>  
  
<member list>::= <member def> [, <member list>]  
  
<member def>::= MEMBER member_name  
  
<default member>::= DEFAULT_MEMBER AS MDX_expression  
  
<visibility qualifier>::= HIDDEN  
  
```  
  
## <a name="syntax-elements"></a>Elementi della sintassi  
 session_cube_name  
 Nome del cubo di sessione.  
  
 source_cube_name  
 Nome del cubo su cui è basato il cubo di sessione.  
  
 source_cube_name.measure_name  
 Nome completo della misura di origine inclusa nel cubo di sessione. I membri calcolati della dimensione Measures non sono consentiti.  
  
 measure_name  
 Nome della misura nel cubo di sessione.  
  
 source_cube_name.dimension_name  
 Nome completo della dimensione di origine inclusa nel cubo di sessione.  
  
 dimension_name  
 Nome della dimensione nel cubo di sessione.  
  
 DALLA \<clausola dim from>  
 Specifica valida solo per la definizione di una dimensione derivata.  
  
 NOT_RELATED_TO_FACTS  
 Specifica valida solo per la definizione di una dimensione derivata.  
  
 \<tipo di livello>  
 Specifica valida solo per la definizione di una dimensione derivata.  
  
## <a name="remarks"></a>Osservazioni  
 A differenza dei cubi locali e presenti sul server, un cubo di sessione non viene mantenuto oltre la sessione che l'ha creato. Viene definito in termini di misure e definizioni che lo definiscono. Sono presenti due tipi di dimensioni:  
  
-   Dimensioni di origine: si tratta delle dimensioni che fanno parti di uno o più cubi di origine.  
  
-   Dimensioni derivate: si tratta di dimensioni che garantiscono nuove possibilità di analisi. Una dimensione derivata può essere una dimensione regolare definita in base a una dimensione di origine con sezionamento verticale o orizzontale o che contiene un raggruppamento personalizzato di membri della dimensione. Una dimensione derivata può inoltre essere rappresentata da una dimensione di data mining basata su un modello di data mining.  
  
> [!NOTE]  
>  La parola chiave Dimension può fare riferimento a dimensioni o gerarchie.  
  
 I cubi di sessione vengono utilizzati soprattutto per il raggruppamento dinamico dei membri degli attributi in gruppi di membri personalizzati da parte di applicazioni client, ad esempio Microsoft Excel. In un cubo di sessione è possibile eseguire le attività seguenti:  
  
-   Eliminazione delle dimensioni presenti nel cubo di origine.  
  
-   Aggiunta o eliminazione di gerarchie da una dimensione.  
  
-   Eliminazione di gruppi di misure o misure specifiche.  
  
-   Aggiunta di un nuovo attributo in base all'associazione di attributi allo scopo di creare gruppi rispetto a un attributo esistente.  
  
> [!IMPORTANT]  
>  La sicurezza degli oggetti cubo di sessione viene ereditata dagli oggetti di origine sottostanti. Anche altri oggetti, ad esempio azioni e script di calcolo, vengono ereditati dal cubo di sessione.  
  
 Per l'istruzione CREATE SESSION CUBE sono valide le regole seguenti:  
  
-   Non è possibile eseguire il raggruppamento su gerarchie padre-figlio.  
  
-   Non è possibile eseguire il raggruppamento su dimensioni ROLAP.  
  
-   Non è possibile eseguire il raggruppamento su dimensioni collegate.  
  
-   Non è possibile eseguire il raggruppamento su livelli con rollup personalizzati.  
  
-   Non è possibile eseguire il raggruppamento su gerarchie di attributi discretizzate.  
  
-   Non è possibile eseguire il raggruppamento su gerarchie non naturali, ovvero gerarchie con relazioni molti-a-molti tra livelli (ad esempio età e sesso).  
  
-   I riferimenti espliciti a un nome di cubo nello script MDX non funzionano in quanto il cubo di sessione ha un nome diverso. Utilizzare la parola chiave CURRENTCUBE.  
  
-   Non è possibile eseguire il raggruppamento su dimensioni con membri predefiniti espliciti.  
  
-   Quando si esegue il raggruppamento, i membri calcolati con ambito sessione sul cubo originale presente sul server vengono rimossi.  
  
-   Quando si esegue il raggruppamento su una dimensione di un cubo presente sul server, tale raggruppamento riguarderà tutte le dimensioni del cubo basate sulla stessa dimensione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrata la creazione di una versione con ambito sessione del cubo Adventure Works, che contiene la misura Reseller Sales Amount, la dimensione Rivenditore, la dimensione Prodotto, la dimensione Geografia e la dimensione Data. All'interno di questo cubo di sessione, vengono creati due gruppi: un gruppo contiene paesi Europai e un gruppo contiene paesi dell'America del nord. Questo esempio è una versione semplificata dell'istruzione CREATE SESSION CUBE eseguita da Microsoft Excel quando un utente crea un raggruppamento personalizzato di membri.  
  
```  
CREATE SESSION CUBE [Adventure Works_XL_GROUPING1]   
   FROM [Adventure Works]   
   ( MEASURE [Adventure Works].[Internet Sales Amount]  
   ,MEASURE [Adventure Works].[Reseller Sales Amount]  
   ,DIMENSION [Adventure Works].[Date].[Calendar]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Year]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Semester]  
   ,DIMENSION [Adventure Works].[Date].[Calendar Quarter]  
   ,DIMENSION [Adventure Works].[Date].[Month Name]  
   ,DIMENSION [Adventure Works].[Date].[Date]  
   ,DIMENSION [Adventure Works].[Geography].[Country]   
      HIDDEN AS _XL_GROUPING81  
   ,DIMENSION [Adventure Works].[Geography].[State-Province]  
   ,DIMENSION [Adventure Works].[Geography].[City]  
   ,DIMENSION [Adventure Works].[Geography].[Postal Code]  
   ,DIMENSION [Adventure Works].[Geography].[Geography]  
   ,DIMENSION [Adventure Works].[Product].[Product Categories]  
   ,DIMENSION [Adventure Works].[Product].[Category]  
   ,DIMENSION [Adventure Works].[Product].[Subcategory]  
   ,DIMENSION [Adventure Works].[Product].[Product]  
   ,DIMENSION [Adventure Works].[Product].[Product Key]  
   ,DIMENSION [Adventure Works].[Reseller].[Reseller]  
   ,DIMENSION [Adventure Works].[Reseller].[Geography Key]  
   ,DIMENSION [Geography].[Country]   
      NOT_RELATED_TO_FACTS FROM _XL_GROUPING81   
          ( LEVEL [(All)]  
         ,LEVEL [Country1] GROUPING  
         ,LEVEL [Country]  
            ,GROUP [Country1].[CountryXl_Grp_1]   
                ( MEMBER [Geography].[Country].&[Canada]  
                  ,MEMBER [Geography].[Country].&[United States] )  
            ,GROUP [Country1].[CountryXl_Grp_2]   
                ( MEMBER [Geography].[Country].&[France]  
                  ,MEMBER [Geography].[Country].&[Germany]  
                  ,MEMBER [Geography].[Country].&[United Kingdom] )   
            )   
   )  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni MDX per la definizione dei dati &#40;&#41;MDX](../mdx/mdx-data-definition-statements-mdx.md)   
 [Istruzione CREATE GLOBAL CUBE &#40;&#41;MDX](../mdx/mdx-data-definition-create-global-cube.md)  
  
  
