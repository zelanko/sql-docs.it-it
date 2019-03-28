---
title: Gli argomenti e le proprietà dell'indice spaziale Stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- spatial indexes [SQL Server], stored procedures
ms.assetid: ee26082b-c0ed-40ff-b5ad-f5f6b00f0475
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31afdbb14229fa7c0eaf13f1b3a215e31356945f
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528813"
---
# <a name="spatial-index-stored-procedures---arguments-and-properties"></a>Stored procedure - argomenti e le proprietà di indice spaziale
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  In questo argomento vengono descritti gli argomenti e le proprietà per le stored procedure relative agli indici spaziali.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento")[Convenzioni della sintassi Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
 Per la sintassi di stored procedure relative agli indici spaziali specifiche, vedere gli argomenti seguenti:  
  
-   [sp_help_spatial_geometry_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [sp_help_spatial_geometry_index_xml &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [sp_help_spatial_geography_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [sp_help_spatial_geography_index_xml &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="arguments"></a>Argomenti  
`[ @tabname = ] 'tabname'` È il nome completo o non qualificato della tabella per cui è stato specificato l'indice spaziale.  
  
 Le virgolette sono necessarie solo se viene specificata una tabella qualificata. Nel caso di un nome completo, ovvero contenente un nome di database, il nome del database deve corrispondere a quello del database corrente. *TabName* viene **nvarchar**(776) e non prevede alcun valore predefinito.  
  
`[ @indexname = ] 'indexname'` È il nome dell'indice spaziale specificato. *IndexName* viene **sysname** non prevede alcun valore predefinito.  
  
`[ @verboseoutput = ] 'verboseoutput'` È l'intervallo di nomi di proprietà e valori da restituire.  
  
 0 = proprietà principali  
  
 \>0 = tutte le proprietà  
  
 *verboseoutput* viene **tinyint** non prevede alcun valore predefinito.  
  
`[ @query_sample = ] 'query_sample'` È un esempio rappresentativo di query che può essere usato per verificare l'utilità dell'indice. Tale campione può essere un oggetto rappresentativo o una finestra Query. *query_sample* viene **geometry** non prevede alcun valore predefinito.  
  
`[ @xml_output = ] 'xml_output'` È un parametro di output che restituisce il risultato impostato in un frammento XML. *xml_output* viene **xml** non prevede alcun valore predefinito.  
  
## <a name="properties"></a>Proprietà  
 Impostare **@verboseoutput** = 0 per restituire le proprietà principali come illustrato nella tabella sottostante. **@verboseoutput** > 0 per restituire tutte le proprietà dell'indice spaziale.  
  
 **Base_Table_Rows**  
 Numero di righe nella tabella di base. Valore è **bigint**.  
  
 **Bounding_Box_xmin**  
 Delimitazione proprietà casella di indice spaziale per X-minimo **geometria** tipo. Valore di questa proprietà è NULL per **geografia**tipo. Valore è **float**.  
  
 **Bounding_Box_ymin**  
 Delimitazione proprietà casella di indice spaziale per valore minimo Y **geometria** tipo. Valore di questa proprietà è NULL per **geografia** tipo. Valore è **float**.  
  
 **Bounding_Box_xmax**  
 Delimitazione proprietà casella di indice spaziale per X-massimo **geometria** tipo. Valore di questa proprietà è NULL per **geografia** tipo. Valore è **float**.  
  
 **Bounding_Box_ymax**  
 Valore massimo di Y proprietà casella dell'indice spaziale per la delimitazione **geometria** tipo. Valore di questa proprietà è NULL per **geografia** tipo. Valore è **float**.  
  
 **Grid_Size_Level_1**  
 Densità della griglia di livello 1 dell'indice spaziale:  
  
 16 per LOW  
  
 64 per MEDIUM  
  
 256 per HIGH  
  
 Valore è **int**.  
  
 **Grid_Size_Level_2**  
 Densità della griglia di livello 2 dell'indice spaziale:  
  
 16 per LOW  
  
 64 per MEDIUM  
  
 256 per HIGH  
  
 Valore è **int**.  
  
 **Grid_Size_Level_3**  
 Densità della griglia di livello 3 dell'indice spaziale:  
  
 16 per LOW  
  
 64 per MEDIUM  
  
 256 per HIGH  
  
 Valore è **int**.  
  
 **Grid_Size_Level_4**  
 Densità della griglia di livello 4 dell'indice spaziale:  
  
 16 per LOW  
  
 64 per MEDIUM  
  
 256 per HIGH  
  
 Valore è **int**.  
  
 **Cells_Per_Object**  
 Numero di celle per oggetto (proprietà dell'indice). Valore è **int**.  
  
 **Total_Primary_Index_Rows**  
 Numero di righe nell'indice. Valore è **bigint**.  
  
 **Total_Primary_Index_Pages**  
 Numero di pagine nell'indice. Valore è **bigint**.  
  
 **Average_Number_Of_Index_Rows_Per_Base_Row**  
 Rapporto tra il numero di righe dell'indice e il numero di righe della tabella di base. Valore è **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample**  
 Indica se il campione rappresentativo di query rientra all'esterno del rettangolo di **geometria** indice e nella cella radice (cella di livello 0). Il valore può essere 0 (campione esterno alla cella di livello 0) oppure 1. Se il campione di query è interno alla cella di livello 0, l'indice controllato non è appropriato. Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level0_In_Index**  
 Numero di istanze della cella di oggetti indicizzati suddivisi a mosaico di livello 0 (cella radice, all'esterno della casella per la delimitazione **geometria**). Si tratta di una proprietà principale. Valore è **bigint**.  
  
 Per la **geometria** indici, ciò si verifica se il rettangolo di selezione dell'indice è minore di dominio dei dati. Un numero elevato di oggetti a livello 0 può essere necessario filtri secondari se la finestra di query è parzialmente esterna al riquadro finestra e comporterà una riduzione delle prestazioni dell'indice (ad esempio, **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample** 1). Se la finestra Query è interna al riquadro, un numero elevato di oggetti presenti a livello 0 può migliorare effettivamente le prestazioni dell'indice.  
  
 Le istanze NULL e vuote vengono conteggiate a livello 0, ma non avranno alcun impatto sulle prestazioni. A livello 0 sarà presente un numero di celle pari a quello delle istanze NULL e vuote nella tabella di base. Per la **geografia** gli indici, livello 0 hanno il numero di celle come NULL e le istanze vuote + 1 cella, in quanto l'esempio di query viene conteggiato come 1.  
  
 **Total_Number_Of_ObjectCells_In_Level1_In_Index**  
 Numero di istanze della cella di oggetti indicizzati suddivisi a mosaico con precisione di livello 1. Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level2_In_Index**  
 Numero di istanze della cella di oggetti indicizzati suddivisi a mosaico con precisione di livello 2. Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level3_In_Index**  
 Numero di istanze della cella di oggetti indicizzati suddivisi a mosaico con precisione di livello 3. Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_ObjectCells_In_Level4_In_Index**  
 Numero di istanze della cella di oggetti indicizzati suddivisi a mosaico con precisione di livello 4. Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level1_In_Index**  
 Numero di celle completamente coperte da un oggetto in corrispondenza dello schema a mosaico di livello 1 e pertanto è interna all'oggetto. (Cell_attributevalue è 2). Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level2_In_Index**  
 Numero di celle completamente coperte da un oggetto in corrispondenza dello schema a mosaico di livello 2 e pertanto è interna all'oggetto. (Il valore di Cell_attribute è 2). Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level3_In_Index**  
 Numero di celle completamente coperte da un oggetto in corrispondenza dello schema a mosaico di livello 3 e pertanto è interna all'oggetto. (Il valore di Cell_attribute è 2). Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_interior_ObjectCells_In_Level4_In_Index**  
 Numero di celle completamente coperte da un oggetto a livello 4 del mosaico e di conseguenza interne all'oggetto. (Il valore di Cell_attribute è 2). Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level1_In_Index**  
 Numero di celle intersecate da un oggetto a livello di schema a mosaico 1. (Il valore di Cell_attribute è 1). Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level2_In_Index**  
 Numero di celle intersecate da un oggetto dello schema a mosaico livello 2. (Il valore di Cell_attribute è 1). Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level3_In_Index**  
 Numero di celle intersecate da un oggetto a livello di schema a mosaico 3. (Il valore di Cell_attribute è 1). Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level4_In_Index**  
 Numero di celle intersecate da un oggetto a livello 4 del mosaico. (Il valore di Cell_attribute è 1). Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_For_QuerySample**  
 Indica se il campione di query si trova nella cella radice 0 esterna al riquadro, ma contigua a esso. Si tratta di una proprietà principale. Valore è **bigint**.  
  
> [!NOTE]  
>  Questa informazione è utile solo per determinare se vi sono oggetti eventualmente mancanti nel riquadro.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_In_Index**  
 Numero di oggetti a livello 0 contigui al riquadro. Il valore di Cell_attribute è 0.  Valore è **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level1_In_Index**  
 Numero di celle dell'oggetto che incontrano un limite di celle della griglia a livello di schema a mosaico 1. Il valore di Cell_attribute è 0. Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level2_In_Index**  
 Numero di celle dell'oggetto che incontrano un limite di celle della griglia a livello di schema a mosaico 2. Il valore di Cell_attribute è 0. Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level3_In_Index**  
 Numero di celle dell'oggetto che incontrano un limite di celle della griglia a livello di schema a mosaico 3. Il valore di Cell_attribute è 0. Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Total_Number_Of_Border_ObjectCells_In_Level4_In_Index**  
 Numero di celle dell'oggetto contigue a un limite della cella della griglia a livello 4 del mosaico. Il valore di Cell_attribute è 0. Si tratta di una proprietà principale. Valore è **bigint**.  
  
 **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 Percentuale dell'area totale (celle foglia totali) della griglia in cui sono contenute celle foglia coperte da un oggetto.  
  
 Si supponga che un oggetto sia suddiviso a mosaico in 10 celle a 4 livelli della griglia diversi coprendo un'area equivalente a 100 celle foglia totali e che siano presenti 3 celle interne completamente coperte dall'oggetto. L'area coperta dalle 3 celle interne è equivalente a 42 celle foglia. Di conseguenza, la percentuale di area coperta è 42%. Tale valore rappresenta una misura efficace del livello di suddivisione degli oggetti nell'indice.  
  
 Valore è **float**.  
  
 **Intersecting_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 Uguale allo **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**, ad eccezione del fatto che queste sono le celle parzialmente coperte. Valore è **float**.  
  
 **Border_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 Uguale allo **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage** ad eccezione del fatto che queste sono le celle sul bordo. Valore è **float**.  
  
 **Average_Cells_Per_Object_Normalized_To_Leaf_Grid**  
 Numero medio di celle per oggetto normalizzato rispetto alla griglia foglia. Indica le dimensioni spaziali dell'oggetto o le dimensioni degli oggetti. Valore è **float**.  
  
 **Average_Objects_PerLeaf_GridCell**  
 Livello di distribuzione dell'indice. Numero medio di oggetti per cella foglia. Valore è **float**.  
  
 **Number_Of_SRIDs_Found**  
 Numero di identificatori SRID univoci presenti nell'indice e nella colonna. Valore è **int**.  
  
 Poiché una colonna può contenere più di un identificatore SRID e gli oggetti con identificatori SRID diversi non si intersecano mai, il numero di identificatori SRID indica la selettività dell'indice.  
  
 **Width_Of_Cell_In_Level1**  
 Proprietà relativa alla larghezza della cella nella griglia di indicizzazione. L'unità di misura viene specificata dall'indice e dipende dall'identificatore SRID dei dati indicizzati. Valore è **float**.  
  
 **Width_Of_Cell_In_Level2**  
 Proprietà relativa alla larghezza della cella nella griglia di indicizzazione. L'unità di misura viene specificata dall'indice e dipende dall'identificatore SRID dei dati indicizzati. Valore è **float**.  
  
 **Width_Of_Cell_In_Level3**  
 Proprietà relativa alla larghezza della cella nella griglia di indicizzazione. L'unità di misura viene specificata dall'indice e dipende dall'identificatore SRID dei dati indicizzati. Valore è **float**.  
  
 **Width_Of_Cell_In_Level4**  
 Proprietà relativa alla larghezza della cella nella griglia di indicizzazione. L'unità di misura viene specificata dall'indice e dipende dall'identificatore SRID dei dati indicizzati. Valore è **float**.  
  
 **Height_Of_Cell_In_Level1**  
 Proprietà relativa all'altezza della cella nella griglia di indicizzazione. L'unità di misura viene specificata dall'indice e dipende dall'identificatore SRID dei dati indicizzati. Valore è **float**.  
  
 **Height_Of_Cell_In_Level2**  
 Proprietà relativa all'altezza della cella nella griglia di indicizzazione. L'unità di misura viene specificata dall'indice e dipende dall'identificatore SRID dei dati indicizzati. Valore è **float**.  
  
 **Height_Of_Cell_In_Level3**  
 Proprietà relativa all'altezza della cella nella griglia di indicizzazione. L'unità di misura viene specificata dall'indice e dipende dall'identificatore SRID dei dati indicizzati. Valore è **float**.  
  
 **Height_Of_Cell_In_Level4**  
 Proprietà relativa all'altezza della cella nella griglia di indicizzazione. L'unità di misura viene specificata dall'indice e dipende dall'identificatore SRID dei dati indicizzati. Valore è **float**.  
  
 **Area_Of_Cell_In_Level1**  
 Proprietà relativa all'area della cella nella griglia di indicizzazione. L'unità di misura viene specificata dall'indice e dipende dall'identificatore SRID dei dati indicizzati. Valore è **float**.  
  
 **Area_Of_Cell_In_Level2**  
 Proprietà relativa all'area della cella nella griglia di indicizzazione. L'unità di misura viene specificata dall'indice e dipende dall'identificatore SRID dei dati indicizzati. Valore è **float**.  
  
 **Area_Of_Cell_In_Level3**  
 Proprietà relativa all'area della cella nella griglia di indicizzazione. L'unità di misura viene specificata dall'indice e dipende dall'identificatore SRID dei dati indicizzati. Valore è **float**.  
  
 **Area_Of_Cell_In_Level4**  
 Proprietà relativa all'area della cella nella griglia di indicizzazione. L'unità di misura viene specificata dall'indice e dipende dall'identificatore SRID dei dati indicizzati. Valore è **float**.  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level1**  
 La percentuale di copertura del rettangolo di selezione da una cella di livello 1. Valore è **float**.  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level2**  
 La percentuale di copertura del rettangolo di selezione da una cella di livello 2. Valore è **float**.  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level3**  
 La percentuale di copertura del rettangolo di selezione da una cella di livello 3. Valore è **float**.  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level4**  
 Percentuale di copertura del riquadro da una cella di livello 4. Valore è **float**.  
  
 **Number_Of_Rows_Selected_By_Primary_Filter**  
 Numero di righe selezionate dal filtro primario. Si tratta di una proprietà principale. Valore è **bigint.**  
  
 **Number_Of_Rows_Selected_By_Internal_Filter**  
 Numero di righe selezionate dal filtro interno. Per queste righe il filtro secondario non viene utilizzato. Si tratta di una proprietà principale. Valore è **bigint.**  
  
 Il numero restituito è applicabile solo per **STintersects**.  
  
 **Number_Of_Times_Secondary_Filter_Is_Called**  
 Numero di volte in cui viene utilizzato il filtro secondario. Si tratta di una proprietà principale. Valore è **bigint.**  
  
 **Percentage_Of_Rows_NotSelected_By_Primary_Filter**  
 Se nella tabella di base sono presenti N righe e se P è il numero di righe selezionate dal filtro primario, questa proprietà restituisce il valore (N-P)/N come percentuale. Si tratta di una proprietà principale. Valore è **float.**  
  
 **Percentage_Of_Primary_Filter_Rows_Selected_By_internal_Filter**  
 Se P è il numero di righe selezionate dal filtro primario, mentre S è quello delle righe selezionate dal filtro interno, questa proprietà restituisce il valore S/P come percentuale. Maggiore è la percentuale, migliore è il livello di efficacia dell'indice nell'evitare il filtro secondario più costoso in termini di prestazioni. Si tratta di una proprietà principale. Valore è **float.**  
  
 **Number_Of_Rows_Output**  
 Numero di righe di output dalla query. Si tratta di una proprietà principale. Valore è **bigint.**  
  
 **Internal_Filter_Efficiency**  
 Se O è il numero di righe di output, questa proprietà restituisce il valore S/O come percentuale. Si tratta di una proprietà principale. Valore è **float.**  
  
 **Primary_Filter_Efficiency**  
 Se P righe selezionate dal filtro primario e O è il numero di righe di output, questo returnsO/P come percentuale. Maggiore è l'efficienza dell'indice principale, minore è il numero di falsi positivi che il filtro secondario deve elaborare. Si tratta di una proprietà principale. Valore è **float.**  
  
## <a name="permissions"></a>Permissions  
 Utente deve essere un membro del **pubblica** ruolo. È necessario disporre dell'autorizzazione READ ACCESS per il server e l'oggetto. Queste condizioni si applicano a tutte le stored procedure relative agli indici spaziali.  
  
## <a name="remarks"></a>Note  
 Le proprietà che contengono valori NULL non sono incluse nel set restituito.  
  
## <a name="examples"></a>Esempi  
 Per gli esempi, vedere gli argomenti seguenti:  
  
-   [sp_help_spatial_geometry_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [sp_help_spatial_geometry_index_xml &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [sp_help_spatial_geography_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [sp_help_spatial_geography_index_xml &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="requirements"></a>Requisiti  
  
## <a name="see-also"></a>Vedere anche  
 [Indice spaziale Stored procedure &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [Panoramica degli indici spaziali](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [XQuery Basics](../../xquery/xquery-basics.md)   
 [Riferimento al linguaggio XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
