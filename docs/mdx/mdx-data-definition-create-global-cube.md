---
description: Definizione dei dati MDX - CREATE GLOBAL CUBE
title: Istruzione CREATE GLOBAL CUBE (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 1bc5a787f6bc1b214aa60ef54b5b8172f07c11a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494864"
---
# <a name="mdx-data-definition---create-global-cube"></a>Definizione dei dati MDX - CREATE GLOBAL CUBE


  Crea e popola un cubo persistente in locale in base a un sottocubo da un cubo nel server. Non è necessaria una connessione al server per connettersi al cubo locale persistente. Per ulteriori informazioni sui cubi locali, vedere la pagina relativa ai [cubi locali &#40;Analysis Services-&#41;di dati multidimensionali ](https://docs.microsoft.com/analysis-services/multidimensional-models/olap-physical/local-cubes-analysis-services-multidimensional-data).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
CREATE GLOBAL CUBE local_cube_name STORAGE 'Cube_Location'   
FROM source_cube_name (<param list>)  
  
<param list>::= <param> ,<param list> | <param>  
  
<param>::= <dims list> | <measures list>  
  
<measures list>::= <measure>[, <measures list>]   
  
<dims list>::= <dim def> [, <dims list>]  
  
<measure>::= MEASURE source_cube_name.measure_name [<visibility qualifier>] [AS measure_name]   
  
<dim def>::= <source dim def> | <derived dim def>  
  
<source dim def>::= DIMENSION source_cube_name.dimension_name [<dim flags>] [<visibility qualifier>] [AS dimension_name>] [FROM <dim from clause> ] [<dim content def>]  
  
<dim flags>::= NOT_RELATED_TO_FACTS   
  
<dim from clause>::= < dim DM from clause> | <reg dim from clause>   
  
<dim DM from clause>::= dm_model_name> COLUMN column_name   
  
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
 local_cube_name  
 Nome del cubo locale.  
  
 'Cube_Location'  
 Nome e percorso del cubo locale persistente.  
  
 source_cube_name  
 Nome del cubo su cui è basato il cubo locale.  
  
 source_cube_name.measure_name  
 Nome completo della misura di origine inclusa nel cubo locale. I membri calcolati della dimensione Measures non sono consentiti.  
  
 measure_name  
 Nome della misura nel cubo locale.  
  
 source_cube_name.dimension_name  
 Nome completo della dimensione di origine inclusa nel cubo locale.  
  
 dimension_name  
 Nome della dimensione nel cubo locale.  
  
 FROM \<dim from clause>  
 Specifica valida solo per la definizione di una dimensione derivata.  
  
 NOT_RELATED_TO_FACTS  
 Specifica valida solo per la definizione di una dimensione derivata.  
  
 \<level type>  
 Specifica valida solo per la definizione di una dimensione derivata.  
  
## <a name="remarks"></a>Osservazioni  
 Un cubo locale è definito in termini di misure e definizioni che lo definiscono. Sono presenti due tipi di dimensioni:  
  
-   Dimensioni di origine: si tratta delle dimensioni che fanno parti di uno o più cubi di origine.  
  
-   Dimensioni derivate: si tratta di dimensioni che garantiscono nuove possibilità di analisi. Una dimensione derivata può essere una dimensione regolare definita in base a una dimensione di origine con sezionamento verticale o orizzontale o che contiene un raggruppamento personalizzato di membri della dimensione. Una dimensione derivata può inoltre essere rappresentata da una dimensione di data mining basata su un modello di data mining.  
  
> [!NOTE]  
>  La parola chiave Dimension può fare riferimento a dimensioni o gerarchie.  
  
 In un cubo locale è possibile eseguire le attività seguenti:  
  
-   Eliminazione delle dimensioni presenti nel cubo di origine.  
  
-   Aggiunta o eliminazione di gerarchie da una dimensione.  
  
-   Eliminazione di gruppi di misure o misure specifiche.  
  
 Per l'istruzione CREATE GLOBAL CUBE sono valide le regole seguenti:  
  
-   L'istruzione CREATE GLOBAL CUBE copia automaticamente tutti i comandi, ad esempio misure calcolate o azioni, nel cubo locale. Se un comando contiene un'espressione MDX che fa riferimento in modo esplicito al cubo padre, tale comando non potrà essere eseguito dal cubo locale. Per evitare questo problema, utilizzare la parola chiave **CURRENTCUBE** durante la definizione di espressioni MDX per i comandi. La parola chiave **CURRENTCUBE** utilizza il contesto del cubo corrente quando fa riferimento a un cubo in un'espressione MDX.  
  
-   Un cubo globale creato da un cubo globale esistente in un file di cubo locale non può essere salvato nello stesso file di cubo locale. A titolo di esempio, si supponga di creare un cubo globale denominato SalesLocal1 e di salvare tale cubo nel file C:\SalesLocal.cub. Si supponga poi di connettersi al file C:\SalesLocal.cub file e di creare un secondo cubo globale denominato SalesLocal2. Se a questo punto si tenta di salvare il cubo globale SalesLocal2 nel file C:\SalesLocal.cub, verrà generato un errore. È invece possibile salvare il cubo globale SalesLocal2 in un diverso file di cubo locale.  
  
-   I cubi globali non supportano misure totale valori distinti. Poiché i cubi che includono misure totale valori distinti non sono additivi, l'istruzione CREATE GLOBAL CUBE non supporta la creazione o l'utilizzo di misure totale valori distinti.  
  
-   Quando si aggiunge una misura a un cubo locale, è necessario includere almeno una dimensione relativa alla misura aggiunta.  
  
-   Quando si aggiunge una gerarchia padre-figlio a un cubo locale, i livelli e i filtri presenti vengono ignorati e viene inclusa tutta la gerarchia padre-figlio.  
  
-   Le proprietà dei membri non sono supportate nei cubi locali.  
  
-   Non è possibile creare un cubo locale da una prospettiva.  
  
-   Se si include una misura semiadditiva a un cubo locale, è necessario rispettare le regole seguenti:  
  
    -   È necessario includere la dimensione Account se la proprietà AggregateFunction della misura aggiunta è ByAccount.  
  
    -   È necessario includere tutta la dimensione Time se la proprietà AggregateFunction della misura aggiunta è FirstChild, LastChild, FirstNonEmpty, LastNonEmpty o AverageOfChildren.  
  
-   Le dimensioni di data mining non possono essere aggiunte a un cubo locale.  
  
-   Le dimensioni di riferimento vengono materializzate e aggiunte come dimensioni regolari.  
  
-   Se si include una dimensione molti-a-molti, è necessario rispettare le regole seguenti:  
  
    -   È necessario aggiungere tutta la dimensione molti-a-molti.  
  
    -   È necessario aggiungere il gruppo di misure intermedio.  
  
    -   È necessario aggiungere in modo completo tutte le dimensioni comuni ai due gruppi di misure inseriti nella relazione molti-a-molti.  
  
 Nell'esempio seguente viene illustrata la creazione di una versione locale persistente del cubo Adventure Works, che contiene solo la misura Reseller Sales Amount, la dimensione Reseller e la dimensione Date.  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller1.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
   )  
```  
  
 Nell'esempio seguente viene illustrata l'operazione di sezionamento durante la creazione di un cubo locale. Il cubo globale creato è basato sul cubo Adventure Works con sezionamento verticale in base al membro 2005 del livello Fiscal Year e con sezionamento orizzontale in base ai livelli Fiscal Year e Month.  
  
```  
CREATE GLOBAL CUBE [LocalReseller]  
   Storage 'C:\LocalAWReseller2.cub'  
   FROM [Adventure Works]  
   (  
      MEASURE  [Adventure Works].[Reseller Sales Amount],  
      DIMENSION [Adventure Works].[Reseller],  
      DIMENSION [Adventure Works].[Date]  
      (  
LEVEL [Fiscal Year],  
LEVEL [Month],  
MEMBER [Date].[Fiscal].[Fiscal Year].&[2005]  
      )  
   )  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzioni MDX per la definizione dei dati &#40;&#41;MDX ](../mdx/mdx-data-definition-statements-mdx.md)   
 [Istruzione CREATE SESSION CUBE &#40;MDX&#41;](../mdx/mdx-data-definition-create-session-cube.md)  
  
  
