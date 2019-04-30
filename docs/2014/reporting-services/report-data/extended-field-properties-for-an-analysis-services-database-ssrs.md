---
title: Proprietà di campo estese per un'analisi dei servizi di Database (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1d7d87e2-bf0d-4ebb-a287-80b5a967a3f2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eec122493d7af91bc5aa5483fbdb1de842705c90
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62695805"
---
# <a name="extended-field-properties-for-an-analysis-services-database-ssrs"></a>Proprietà di campo estese per un Database di Analysis Services (SSRS)
  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] estensione per l'elaborazione dati supporta la proprietà di campo estese. Proprietà di campo estese sono proprietà oltre alle proprietà di campo `Value` e `IsMissing` che sono disponibili nell'origine dati e supportate dall'estensione per l'elaborazione dati. Le proprietà estese non vengono visualizzati nel riquadro dei dati del Report come parte della raccolta di campi per un set di dati di report. È possibile includere valori di proprietà di campo estese nel report scrivendo espressioni che essi sono specificati per nome usando l'elemento predefinito `Fields` raccolta.  
  
 Le proprietà estese includono proprietà predefinite e proprietà personalizzate. Le proprietà predefinite sono comuni a più origini dati che vengono mappate ai nomi delle proprietà di campo specifico e sono accessibili tramite l'elemento predefinito `Fields` raccolta in base al nome. Proprietà personalizzate sono specifiche per ogni provider di dati e sono accessibili tramite l'elemento predefinito `Fields` raccolta solo tramite la sintassi con il nome della proprietà estesa come stringa.  
  
 Quando si usa il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Progettazione query MDX in modalità grafica per definire la query, un set predefinito di proprietà delle celle e proprietà dimensione vengono aggiunti automaticamente alla query MDX. È possibile utilizzare solo le proprietà estese specificatamente elencate nella query MDX nel report. A seconda del report, è possibile modificare il testo del comando MDX predefinita in modo da includere altre proprietà personalizzate definite nel cubo o dimensione. Per altre informazioni sui campi estesi disponibili nelle [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] origini dati, vedere [creazione e utilizzo dei valori di proprietà &#40;MDX&#41;](../../analysis-services/creating-and-using-property-values-mdx.md).  
  
## <a name="working-with-field-properties-in-a-report"></a>Uso delle proprietà di campo in un Report  
 Proprietà di campo estese includono proprietà predefinite e proprietà specifiche del provider di dati. Le proprietà di campo non vengono visualizzati con l'elenco dei campi nel **i dati del Report** riquadro, sebbene siano incluse nella query compilata per un set di dati; pertanto, non è possibile trascinare le proprietà di campo nell'area di progettazione del report. In alternativa, è necessario trascinare il campo nel report e quindi modificare il `Value` proprietà del campo impostando la proprietà che si desidera utilizzare. Ad esempio, se i dati delle celle da un cubo sono già stati formattati, è possibile usare la proprietà di campo FormattedValue usando l'espressione seguente: `=Fields!FieldName.FormattedValue`.  
  
 Per fare riferimento a una proprietà estesa non predefinita, usare la sintassi seguente in un'espressione:  
  
-   *Fields!FieldName("PropertyName")*  
  
## <a name="predefined-field-properties"></a>Proprietà di campo predefinite  
 Nella maggior parte dei casi, le proprietà di campo predefinite si applicano a misure, livelli o dimensioni. Una proprietà di campo predefinite deve avere un valore corrispondente archiviato nel [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] zdroj dat. Se un valore non esiste o se si specifica una proprietà di campo solo di misura su un livello (ad esempio), la proprietà restituisce un valore null.  
  
 Per fare riferimento a una proprietà predefinita da un'espressione, è possibile usare una delle sintassi seguenti:  
  
-   *Fields!FieldName.PropertyName*  
  
-   *Fields!FieldName("PropertyName")*  
  
 Nella tabella seguente fornisce un elenco delle proprietà di campo predefinite che è possibile usare.  
  
|**Property**|**Type**|**Descrizione o valore previsto**|  
|------------------|--------------|---------------------------------------|  
|`Value`|`Object`|Specifica il valore di dati del campo.|  
|`IsMissing`|`Boolean`|Indica se il campo è stato trovato nel set di dati risultante.|  
|`UniqueName`|`String`|Restituisce il nome completo di un livello. Ad esempio, il `UniqueName` valore per un dipendente potrebbe essere *[Employee]. [ Reparto dipendente]. [Reparto]. & [vendite]. & [responsabile vendite Nord America]. America.&[272]*.|  
|`BackgroundColor`|`String`|Restituisce il colore di sfondo definito nel database per il campo.|  
|`Color`|`String`|Restituisce il colore di primo piano definito nel database per l'elemento.|  
|`FontFamily`|`String`|Restituisce il nome del tipo di carattere definito nel database per l'elemento.|  
|`FontSize`|`String`|Restituisce la dimensione del carattere definito nel database per l'elemento.|  
|`FontWeight`|`String`|Restituisce lo spessore del carattere definito nel database per l'elemento.|  
|`FontStyle`|`String`|Restituisce lo stile del carattere definito nel database per l'elemento.|  
|`TextDecoration`|`String`|Restituisce formattazione di testo speciale definita nel database per l'elemento.|  
|`FormattedValue`|`String`|Restituisce un valore formattato per una misura o una cifra chiave. Ad esempio, il `FormattedValue` proprietà per **Sales Amount Quota** restituisce un formato valuta come $1,124,400.00.|  
|`Key`|`Object`|Restituisce la chiave per un livello.|  
|`LevelNumber`|`Integer`|Per le gerarchie padre-figlio, restituisce il numero di livello o alla dimensione.|  
|`ParentUniqueName`|`String`|Per le gerarchie padre-figlio, restituisce un nome completo del livello padre.|  
  
> [!NOTE]  
>  Esistenza di valori per queste proprietà di campo estese solo se l'origine dati (ad esempio, il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cubo) fornisce tali valori quando il report viene eseguita e recupera i dati per il set di dati. È quindi possibile fare riferimento a questi valori di proprietà di campo da qualsiasi espressione utilizzando la sintassi descritta nella sezione seguente. Tuttavia, poiché questi campi sono specifici per questo provider di dati, le modifiche apportate a tali valori non vengono salvate con la definizione del report.  
  
### <a name="example-extended-properties"></a>Esempio di proprietà estese  
 Per illustrare le proprietà estese, la seguente query MDX e risultato set includono diverse proprietà del membro disponibili da un attributo della dimensione definito per un cubo. La proprietà del membro incluse sono MEMBER_CAPTION, UNIQUENAME, proprietà ("Day Name"), MEMBER_VALUE, PARENT_UNIQUE_NAME e MEMBER_KEY.  
  
 Questa query MDX viene eseguita sul [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] cubo la [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] database del data Warehouse, inclusi con il [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] database di esempio.  
  
```  
WITH MEMBER [Measures].[DateCaption]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_CAPTION'   
   MEMBER [Measures].[DateUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.UNIQUENAME'   
   MEMBER [Measures].[DateDayName]   
      AS '[Date].[Date].Properties("Day Name")'   
   MEMBER [Measures].[DateValueinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_VALUE'   
   MEMBER [Measures].[DateParentUniqueName]   
      AS '[Date].[Date].CURRENTMEMBER.PARENT_UNIQUE_NAME'   
   MEMBER [Measures].[DateMemberKeyinOriginalDatatype]   
      AS '[Date].[Date].CURRENTMEMBER.MEMBER_KEY'   
SELECT {  
   [Measures].[DateCaption],   
   [Measures].[DateUniqueName],   
   [Measures].[DateDayName],   
   [Measures].[DateValueinOriginalDatatype],  
   [Measures].[DateParentUniqueName],  
   [Measures].[DateMemberKeyinOriginalDatatype]  
   } ON COLUMNS , [Date].[Date].ALLMEMBERS ON ROWS   
FROM [Adventure Works]  
  
```  
  
 Quando si esegue questa query nel riquadro di una query MDX, si ottiene un set costituito da 1158 righe di risultati. Nella tabella seguente vengono visualizzate le prime quattro righe.  
  
|DateCaption|DateUniqueName|DateDayName|DateValueinOriginalDatatype|DateParentUniqueName|DateMemberKeyinOriginalDatatype|  
|-----------------|--------------------|-----------------|---------------------------------|--------------------------|-------------------------------------|  
|Tutti i periodi|[Date]. [Date]. [Tutti i periodi]|(null)|(null)|(null)|0|  
|1-luglio-01|[Date]. [Date]. & [1]|Domenica|7/1/2001|[Date]. [Date]. [Tutti i periodi]|1|  
|2-luglio-01|[Date]. [Date]. & [2]|Lunedì|7/2/2001|[Date]. [Date]. [Tutti i periodi]|2|  
|3-luglio-01|[Date]. [Date]. & [3]|Martedì|7/3/2001|[Date]. [Date]. [Tutti i periodi]|3|  
  
 Le query MDX predefinite compilate usando la finestra Progettazione Query MDX con interfaccia grafica solo in modalità includono MEMBER_CAPTION e UNIQUENAME per le proprietà di dimensione. Per impostazione predefinita, questi valori sono sempre di tipo `String`.  
  
 Se occorre una proprietà del membro nel tipo di dati originale, è possibile includere un'ulteriore proprietà MEMBER_VALUE modificando l'istruzione MDX predefinita in Progettazione query basata su testo. Nell'istruzione MDX semplice seguente, MEMBER_VALUE è stata aggiunta all'elenco di proprietà delle dimensioni da recuperare.  
  
```  
SELECT NON EMPTY {[Measures].[Order Count]} ON COLUMNS,   
NON EMPTY { ([Date].[Month of Year].[Month of Year] ) }   
DIMENSION PROPERTIES   
   MEMBER_CAPTION, MEMBER_UNIQUE_NAME, MEMBER_VALUE ON ROWS   
FROM [Adventure Works]  
CELL PROPERTIES   
   VALUE, BACK_COLOR, FORE_COLOR,   
   FORMATTED_VALUE, FORMAT_STRING,   
   FONT_NAME, FONT_SIZE, FONT_FLAGS  
```  
  
 Le prime quattro righe del risultato nel riquadro risultati MDX vengono visualizzati nella tabella seguente.  
  
|Mese dell'anno|Numero di ordini|  
|-------------------|-----------------|  
|Gennaio|2,481|  
|Febbraio|2,684|  
|Marzo|2,749|  
|Aprile|2,739|  
  
 Anche se le proprietà sono parte dell'istruzione MDX select, non sono visualizzate nelle colonne del set di risultati. Tuttavia, i dati sono disponibili per un report usando la funzionalità di proprietà estese. In un riquadro risultati delle query MDX [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], è possibile fare doppio clic sulla cella e visualizzare i valori di proprietà di cella se impostati nel cubo. Se si fa doppio clic sulla prima cella Order Count contenente 1,379, verrà visualizzato una finestra popup con le proprietà di cella seguenti:  
  
|Proprietà|Value|  
|--------------|-----------|  
|CellOrdinal|0|  
|VALUE|2481|  
|BACK_COLOR|(null)|  
|FORE_COLOR|(null)|  
|FORMATTED_VALUE|2,481|  
|FORMAT_STRING|#,#|  
|FONT_NAME|(null)|  
|FONT_SIZE|(null)|  
|FONT_FLAGS|(null)|  
  
 Se si crea un set di dati con questa query e associare il set di dati a una tabella, è possibile vedere la proprietà valore predefinito per un campo, ad esempio, `=Fields!Month_of_Year!Value`. Se si imposta questa espressione come espressione di ordinamento per la tabella, i risultati saranno nella tabella viene ordinata alfabeticamente in base al mese perché Usa il campo del valore un `String` tipo di dati. Per ordinare la tabella in modo che i mesi si trovino nell'ordine in cui vengono generati nell'anno con gennaio primo e dicembre ultimo, utilizzare l'espressione seguente:  
  
```  
=Fields!Month_of_Year("MEMBER_VALUE")  
```  
  
 In questo modo il valore del campo nel tipo di dati interi originale dell'origine dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Le espressioni &#40;Report e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)   
 [Raccolte predefinite nelle espressioni &#40;Report e SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md)   
 [Raccolta di campi del set di dati &#40;Report e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
