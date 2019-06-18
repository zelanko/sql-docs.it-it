---
title: Proprietà intrinseche dei membri (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e54aa6bb53e6ce9f34e6647927f29b7aadb97180
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740251"
---
# <a name="mdx-member-properties---intrinsic-member-properties"></a>Proprietà dei membri MDX - proprietà intrinseche dei membri
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] espone proprietà intrinseche sui membri della dimensione che è possibile includere in una query per restituire dati o metadati aggiuntivi da usare in un'applicazione personalizzata o per supportare la costruzione o l'analisi dei modelli. Se si utilizzano gli strumenti client di SQL Server, è possibile visualizzare le proprietà intrinseche in SQL Server Management Studio (SSMS).  
  
 Le proprietà intrinseche includono **ID**, **KEY**, **KEYx**e **NAME**, che sono proprietà esposte da ogni membro a qualsiasi livello. È anche possibile restituire informazioni sulla posizione, ad esempio **LEVEL_NUMBER** o **PARENT_UNIQUE_NAME**.  
  
 In base al modo in cui si costruisce la query e all'applicazione client che si utilizza per eseguire le query, le proprietà dei membri possono essere visibili o meno nel set dei risultati. Se si utilizza SQL Server Management Studio per eseguire i test o le query, è possibile fare doppio clic su un membro nel set di risultati per aprire la finestra di dialogo Proprietà membro, nella quale sono indicati i valori di ciascuna proprietà del membro intrinseca.  
  
 Per un'introduzione all'uso e alla visualizzazione delle proprietà del membro di dimensione, vedere [Viewing SSAS Member Properties within an MDX Query Window in SSMS (Visualizzazione delle proprietà del membro SSAS in una finestra di query MDX in SSMS)](http://go.microsoft.com/fwlink/?LinkId=317362).  
  
> [!NOTE]
>  Essendo un provider conforme alla sezione OLAP della specifica OLE DB del mese di marzo 1999 (2.6), [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] supporta le proprietà intrinseche dei membri elencate in questo argomento.  
> 
>  I provider diversi da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] possono supportare altre proprietà intrinseche dei membri. Per ulteriori informazioni sulle proprietà intrinseche dei membri supportate da altri provider, consultare la documentazione fornita con tali provider.  
  
## <a name="types-of-member-properties"></a>Tipi di proprietà dei membri  
 Le proprietà intrinseche dei membri supportate da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] sono di due tipi:  
  
 Proprietà dei membri sensibili al contesto  
 Queste proprietà del membro devono essere utilizzate nel contesto di una gerarchia o di un livello specifico e definiscono valori per ogni membro della dimensione o del livello specificato.  
  
 Notare come nell'esempio seguente è incluso il percorso per la proprietà **KEY** : `MEMBER [Measures].[Parent Member Key] AS [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("KEY")`.  
  
 Proprietà dei membri non sensibili al contesto  
 Queste proprietà del membro non possono essere utilizzate nel contesto di una dimensione o di un livello specifico e restituiscono i valori di tutti i membri su un asse.  
  
 Le proprietà non sensibili al contesto sono autonome e non includono informazioni sul percorso. Notare che nel seguente esempio per **PARENT_UNIQUE_NAME** non è specificato alcun livello né alcuna dimensione: `DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS`  
  
 Indipendentemente dal fatto che una proprietà intrinseca di un membro sia sensibile o meno al contesto, valgono le regole di utilizzo seguenti:  
  
-   È possibile specificare solo le proprietà intrinseche dei membri correlate ai membri delle dimensioni proiettati sull'asse.  
  
-   In una stessa query è possibile includere sia richieste per proprietà dei membri sensibili al contesto che per proprietà intrinseche dei membri non sensibili al contesto.  
  
-   Nelle query relative alle proprietà è necessario usare la parola chiave **PROPERTIES** .  
  
 Le sezioni seguenti descrivono sia le proprietà intrinseche dei membri sensibili al contesto, sia quelle non sensibili al contesto disponibili in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Viene inoltre indicata la modalità di utilizzo della parola chiave **PROPERTIES** con ogni tipo di proprietà.  
  
## <a name="context-sensitive-member-properties"></a>Proprietà dei membri sensibili al contesto  
 Tutti i membri delle dimensioni e dei livelli supportano un elenco di proprietà intrinseche sensibili al contesto. Nella tabella seguente sono elencate tali proprietà sensibili al contesto.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**ID**|ID gestito internamente per il membro.|  
|**Key**|Valore della chiave del membro nel tipo di dati originale. MEMBER_KEY è disponibile per compatibilità con le versioni precedenti.  MEMBER_KEY ha lo stesso valore di KEY0 per le chiavi non composte e la proprietà MEMBER_KEY è Null per le chiavi composte.|  
|**KEYx**|Chiave del membro, in cui x è il numero ordinale in base zero della chiave. KEY0 è disponibile per le chiavi composte e non composte, ma è utilizzato principalmente per le chiavi composte.<br /><br /> Le chiavi KEY0, KEY1, KEY2 e via di seguito formano collettivamente una chiave composta. È possibile utilizzare ciascuna chiave in modo indipendente in una query per restituire la parte corrispondente della chiave composta. Se ad esempio si specifica KEY0, viene restituita la prima parte della chiave composta, se si specifica KEY1 viene restituita la parte successiva e così via.<br /><br /> Se la chiave non è composta, KEY0 equivale a **Key**.<br /><br /> Notare che **KEYx** può essere usata sia in contesto che fuori contesto. Per questo motivo appare in entrambi gli elenchi.<br /><br /> Per un esempio di come usare la proprietà dei membri, vedere [Tidbit MDX semplice: Key0, Key1, Key2](http://go.microsoft.com/fwlink/?LinkId=317364).|  
|**Name**|Nome del membro.|  
  
### <a name="properties-syntax-for-context-sensitive-properties"></a>Sintassi della parola chiave PROPERTIES per le proprietà sensibili al contesto  
 Queste proprietà dei membri possono essere utilizzate nel contesto di una dimensione o di un livello specifico e definiscono valori per ogni membro della dimensione o del livello specificato.  
  
 Nel caso delle proprietà dei membri di una dimensione, è necessario anteporre al nome della proprietà quello della dimensione a cui si riferisce la proprietà. La sintassi appropriata è illustrata nell'esempio seguente:  
  
 `DIMENSION PROPERTIES Dimension.Property_name`  
  
 Nel caso delle proprietà dei membri di un livello, è possibile anteporre al nome della proprietà solo il nome del livello oppure, per maggiore precisione, sia il nome della dimensione che quello del livello. La sintassi appropriata è illustrata nell'esempio seguente:  
  
 `DIMENSION PROPERTIES [Dimension.]Level.Property_name`  
  
 Si supponga ad esempio di voler restituire i nomi di tutti i membri a cui viene fatto riferimento nella dimensione `[Sales]` . Per restituire tali nomi, è necessario utilizzare l'istruzione seguente in una query MDX (Multidimensional Expressions):  
  
 `DIMENSION PROPERTIES [Sales].Name`  
  
## <a name="non-context-sensitive-member-properties"></a>Proprietà dei membri non sensibili al contesto  
 Tutti i membri supportano un elenco di proprietà intrinseche dei membri che rimangono invariate indipendentemente dal contesto. Tali proprietà forniscono ulteriori informazioni che possono essere utilizzate dalle applicazioni per migliorare l'interazione con l'utente.  
  
 Nella tabella seguente sono elencate le proprietà intrinseche non sensibili al contesto supportate da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
> [!NOTE]  
>  Le colonne nel set di righe dello schema MEMBERS supportano le proprietà intrinseche dei membri elencate nella tabella seguente. Per altre informazioni sul set di righe dello schema **MEMBERS** , vedere [Set di righe MDSCHEMA_MEMBERS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-members-rowset).  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|**CATALOG_NAME**|Nome del cubo a cui appartiene il membro.|  
|**CHILDREN_CARDINALITY**|Numero di elementi figlio del membro. Poiché può trattarsi di una stima, il conteggio potrebbe non essere esatto. I provider restituiscono la migliore stima possibile.|  
|**CUSTOM_ROLLUP**|Espressione di membro personalizzata.|  
|**CUSTOM_ROLLUP_PROPERTIES**|Proprietà personalizzate del membro.|  
|**DESCRIPTION**|Descrizione discorsiva del membro.|  
|**DIMENSION_UNIQUE_NAME**|Nome univoco della dimensione a cui appartiene il membro. Per i provider che generano nomi univoci tramite qualificazione, i singoli componenti di tale nome sono delimitati.|  
|**HIERARCHY_UNIQUE_NAME**|Nome univoco della gerarchia. Se il membro appartiene a più di una gerarchia, sarà presente una riga per ogni gerarchia a cui appartiene il membro. Per i provider che generano nomi univoci tramite qualificazione, i singoli componenti di tale nome sono delimitati.|  
|**IS_DATAMEMBER**|Valore booleano che indica se il membro è un membro dati.|  
|**IS_PLACEHOLDERMEMBER**|Valore booleano che indica se il membro è un segnaposto.|  
|**KEYx**|Chiave del membro, in cui x è il numero ordinale in base zero della chiave. KEY0 è disponibile per le chiavi composte e non composte.<br /><br /> Se la chiave non è composta, KEY0 equivale a **Key**.<br /><br /> Le chiavi KEY0, KEY1, KEY2 e via di seguito formano collettivamente una chiave composta. È possibile fare riferimento a ciascuna chiave in modo indipendente in una query per restituire la parte corrispondente della chiave composta. Se ad esempio si specifica KEY0, viene restituita la prima parte della chiave composta, se si specifica KEY1 viene restituita la parte successiva e così via.<br /><br /> Notare che **KEYx** può essere usata sia in contesto che fuori contesto. Per questo motivo appare in entrambi gli elenchi.<br /><br /> Per un esempio di come usare la proprietà dei membri, vedere [Tidbit MDX semplice: Key0, Key1, Key2](http://go.microsoft.com/fwlink/?LinkId=317364).|  
|**LCID** *x*|Conversione della didascalia del membro del valore esadecimale dell'ID impostazioni locali, dove *x* è il valore decimale dell'ID impostazioni locali, ad esempio LCID1009 per Inglese-Canada. È disponibile solo se nella conversione la colonna della didascalia è associata all'origine dei dati.|  
|**LEVEL_NUMBER**|Distanza del membro dalla radice della gerarchia. Per il livello radice è zero.|  
|**LEVEL_UNIQUE_NAME**|Nome univoco del livello a cui appartiene il membro. Per i provider che generano nomi univoci tramite qualificazione, i singoli componenti di tale nome sono delimitati.|  
|**MEMBER_CAPTION**|Etichetta o didascalia associata al membro. La didascalia viene utilizzata soprattutto a scopo di visualizzazione. Se non esiste una didascalia, la query restituirà **MEMBER_NAME**.|  
|**MEMBER_KEY**|Valore della chiave del membro nel tipo di dati originale. MEMBER_KEY è disponibile per compatibilità con le versioni precedenti.  MEMBER_KEY ha lo stesso valore di KEY0 per le chiavi non composte e la proprietà MEMBER_KEY è Null per le chiavi composte.|  
|**MEMBER_NAME**|Nome del membro.|  
|**MEMBER_TYPE**|Tipo del membro. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **MDMEMBER_TYPE_REGULAR**<br /><br /> **MDMEMBER_TYPE_ALL**<br /><br /> **MDMEMBER_TYPE_FORMULA**<br /><br /> **MDMEMBER_TYPE_MEASURE**<br /><br /> **MDMEMBER_TYPE_UNKNOWN**<br /><br /> <br /><br /> Nota: MDMEMBER_TYPE_FORMULA ha la precedenza rispetto a MDMEMBER_TYPE_MEASURE. Di conseguenza, se nella dimensione Measures esiste un membro di tipo formula (calcolato), la proprietà **MEMBER_TYPE** del membro calcolato sarà MDMEMBER_TYPE_FORMULA.|  
|**MEMBER_UNIQUE_NAME**|Nome univoco del membro. Per i provider che generano nomi univoci tramite qualificazione, i singoli componenti di tale nome sono delimitati.|  
|**MEMBER_VALUE**|Valore del membro nel tipo originale.|  
|**PARENT_COUNT**|Numero di elementi padre del membro.|  
|**PARENT_LEVEL**|Distanza dell'elemento padre del membro dal livello radice della gerarchia. Per il livello radice è zero.|  
|**PARENT_UNIQUE_NAME**|Nome univoco del nodo padre del membro. Viene restituito**NULL** per tutti i membri al livello di radice. Per i provider che generano nomi univoci tramite qualificazione, i singoli componenti di tale nome sono delimitati.|  
|**SKIPPED_LEVELS**|Il numero di livelli ignorati per il membro.|  
|**UNARY_OPERATOR**|Operatore unario per il membro.|  
|**UNIQUE_NAME**|Nome completo del membro nel formato: [dimension].[level].[key6].|  
  
### <a name="properties-syntax-for-non-context-sensitive-properties"></a>Sintassi della parola chiave PROPERTIES per le proprietà non sensibili al contesto  
 Usare la sintassi seguente per specificare una proprietà intrinseca di un membro non sensibile al contesto, tramite la parola chiave **PROPERTIES** :  
  
 `DIMENSION PROPERTIES Property`  
  
 Si noti che questa sintassi non consente di qualificare la proprietà con una dimensione o un livello. La proprietà non può essere qualificata perché le proprietà intrinseche dei membri che non sono sensibili al contesto vengono applicate a tutti i membri di un asse.  
  
 Ad esempio, la sintassi dell'istruzione MDX che specifica la proprietà intrinseca dei membri **DESCRIPTION** è la seguente:  
  
 `DIMENSION PROPERTIES DESCRIPTION`  
  
 Questa istruzione restituisce la descrizione di ogni membro nella dimensione dell'asse. Se si tenta di qualificare la proprietà con una dimensione o un livello, ad esempio *Dimension*`.DESCRIPTION` o *Level*`.DESCRIPTION`, l'istruzione non verrà convalidata.  
  
### <a name="example"></a>Esempio  
 Negli esempi seguenti vengono illustrate query MDX che restituiscono proprietà intrinseche.  
  
 **Esempio 1: Utilizzare proprietà intrinseche sensibili al contesto di query**  
  
 Nell'esempio seguente vengono restituiti l'ID padre, la chiave e il nome per ciascuna categoria di prodotti. Notare il modo in cui le proprietà sono esposte come misure. Ciò consente di visualizzare le proprietà in un set di celle quando si esegue la query, anziché nella finestra di dialogo Proprietà membro in SSMS. Questo tipo di query può essere eseguito per recuperare i metadati dei membri da un cubo già distribuito.  
  
```  
WITH  
MEMBER [Measures].[Parent Member ID] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("ID")  
MEMBER [Measures].[Parent Member Key] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("KEY")  
MEMBER [Measures].[Parent Member Name] AS  
 [Product].[Product Categories].CurrentMember.Parent.PROPERTIES("Name")  
SELECT  
 {[Measures].[Parent Member ID], [Measures].[Parent Member Key], [Measures].[Parent Member Name] } on COLUMNS,   
 [Product].[Product Categories].AllMembers on ROWS  
FROM [Adventure Works]  
```  
  
 **Esempio 2: Proprietà intrinseche non sensibili al contesto**  
  
 Nell'esempio seguente è riportato l'elenco completo delle proprietà intrinseche non sensibili al contesto. Dopo aver eseguito la query in SSMS, fare clic sui singoli membri per visualizzare le proprietà nella finestra di dialogo Proprietà membro.  
  
```  
SELECT [Measures].[Sales Amount Quota] on COLUMNS,  
[Employee].[Employees].members  
DIMENSION PROPERTIES  
 CATALOG_NAME ,   
 CHILDREN_CARDINALITY ,  
 CUSTOM_ROLLUP ,   
 CUSTOM_ROLLUP_PROPERTIES ,   
 DESCRIPTION ,   
 DIMENSION_UNIQUE_NAME ,   
 HIERARCHY_UNIQUE_NAME ,  
 IS_DATAMEMBER ,   
 IS_PLACEHOLDERMEMBER ,   
 KEY0 ,  
 LCID ,  
 LEVEL_NUMBER ,  
 LEVEL_UNIQUE_NAME ,  
 MEMBER_CAPTION ,   
 MEMBER_KEY ,   
 MEMBER_NAME ,   
 MEMBER_TYPE ,  
 MEMBER_UNIQUE_NAME ,   
 MEMBER_VALUE ,   
 PARENT_COUNT ,   
 PARENT_LEVEL ,   
 PARENT_UNIQUE_NAME ,  
 SKIPPED_LEVELS ,   
 UNARY_OPERATOR ,   
 UNIQUE_NAME    
 ON ROWS  
FROM [Adventure Works]  
WHERE [Employee].[Employee Department].[Department].&[Sales]  
```  
  
 **Esempio 3: Restituisce le proprietà dei membri come dati in un set di risultati**  
  
 Nell'esempio seguente viene restituita la didascalia tradotta del membro della categoria di prodotto della dimensione Prodotto nel cubo Adventure Works per impostazioni locali specifiche.  
  
```  
WITH   
MEMBER Measures.CategoryCaption AS Product.Category.CurrentMember.MEMBER_CAPTION  
MEMBER Measures.SpanishCategoryCaption AS Product.Category.CurrentMember.Properties("LCID3082")  
MEMBER Measures.FrenchCategoryCaption AS Product.Category.CurrentMember.Properties("LCID1036")  
SELECT   
{ Measures.CategoryCaption, Measures.SpanishCategoryCaption, Measures.FrenchCategoryCaption } ON 0  
,[Product].[Category].MEMBERS ON 1  
FROM [Adventure Works]  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [PeriodsToDate &#40;MDX&#41;](../../../mdx/periodstodate-mdx.md)   
 [Children &#40;MDX&#41;](../../../mdx/children-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../../../mdx/hierarchize-mdx.md)   
 [Count &#40;Set&#41; &#40;MDX&#41;](../../../mdx/count-set-mdx.md)   
 [Filter &#40;MDX&#41;](../../../mdx/filter-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../../../mdx/drilldownlevel-mdx.md)   
 [Properties &#40;MDX&#41;](../../../mdx/properties-mdx.md)   
 [PrevMember &#40;MDX&#41;](../../../mdx/prevmember-mdx.md)   
 [Utilizzo delle proprietà dei membri &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-member-properties.md)   
 [Guida di riferimento alle funzioni MDX &#40;MDX&#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
