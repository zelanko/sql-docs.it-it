---
title: Proprietà di campo estese per un database di Analysis Services (SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 1d7d87e2-bf0d-4ebb-a287-80b5a967a3f2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d315aa1c5037e27d5c48e1ee03addef35cbc22df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65573314"
---
# <a name="extended-field-properties-for-an-analysis-services-database-ssrs"></a>Proprietà di campo estese per un database di Analysis Services (SSRS)
  L'estensione per l'elaborazione dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta proprietà di campo estese. Le proprietà di campo estese sono proprietà aggiuntive rispetto alle proprietà di campo **Value** e **IsMissing** , disponibili nell'origine dati e supportate dall'estensione per l'elaborazione dati. Le proprietà estese non vengono visualizzate nel riquadro Dati report all'interno della raccolta di campi per un set di dati del report. È possibile includere valori di proprietà di campo estese in un report scrivendo espressioni mediante la raccolta predefinita **Campi** nelle quali i valori sono specificati per nome.  
  
 Le proprietà estese includono proprietà predefinite e proprietà personalizzate. Le proprietà predefinite sono comuni a più origini dati, per le quali viene eseguito il mapping a nomi di proprietà di campo specifiche e risultano accessibili per nome tramite la raccolta predefinita **Campi** . Le proprietà personalizzate sono specifiche per ogni provider di dati ed è possibile accedervi mediante la raccolta predefinita **Campi** solo tramite la sintassi che usa il nome della proprietà estesa come stringa.  
  
 Quando si usa la finestra Progettazione query MDX con interfaccia grafica di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per definire la query, a quest'ultima viene automaticamente aggiunto un set predefinito di proprietà delle celle e delle dimensioni. Nel report è possibile utilizzare solo le proprietà estese specificatamente elencate nella query MDX. A seconda del report, potrebbe essere opportuno modificare il testo del comando MDX in modo che includa altre proprietà personalizzate o delle dimensioni definite nel cubo. Per altre informazioni sui campi estesi disponibili nelle origini dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Creazione e uso di valori di proprietà &#40;MDX&#41;](https://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2).  
  
## <a name="working-with-field-properties-in-a-report"></a>Utilizzo delle proprietà di campo in un report  
 Le proprietà di campo estese includono proprietà predefinite e proprietà specifiche del provider di dati. Le proprietà di campo non vengono visualizzate con l'elenco dei campi nel riquadro **Dati report** , sebbene siano incluse nella query compilata per un set di dati. Non è possibile pertanto trascinarle nell'area di progettazione del report. È invece necessario trascinare il campo nel report e quindi modificare la proprietà **Value** del campo impostando la proprietà che si vuole usare. Se, ad esempio, i dati delle celle di un cubo sono già stati formattati, è possibile usare la proprietà di campo FormattedValue usando l'espressione seguente: `=Fields!FieldName.FormattedValue`.  
  
 Per fare riferimento a una proprietà estesa non predefinita, utilizzare la sintassi seguente in un'espressione:  
  
-   *Fields!FieldName("PropertyName")*  
  
## <a name="predefined-field-properties"></a>Proprietà di campo predefinite  
 Nella maggior parte dei casi, le proprietà di campo predefinite si applicano a misure, livelli o dimensioni. Una proprietà di campo predefinita deve avere un valore corrispondente archiviato nell'origine dati di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se non esiste un valore o se si specifica una proprietà dei campi solo di misura, ad esempio per un livello, la proprietà restituisce un valore Null.  
  
 Per fare riferimento a una proprietà predefinita da un'espressione, utilizzare uno dei due tipi di sintassi seguenti:  
  
-   *Fields!FieldName.PropertyName*  
  
-   *Fields!FieldName("PropertyName")*  
  
 Nella tabella seguente viene illustrato un elenco di proprietà di campo predefinite che è possibile utilizzare.  
  
|**Proprietà**|**Tipo**|**Descrizione o valore previsto**|  
|------------------|--------------|---------------------------------------|  
|**Value**|**Oggetto**|Specifica il valore dei dati del campo.|  
|**IsMissing**|**Boolean**|Indica se il campo è stato trovato nel set di dati risultante.|  
|**UniqueName**|**String**|Restituisce il nome completo di un livello. Ad esempio, il valore **UniqueName** per un dipendente può essere *[Dipendente].[Reparto dipendente].[Reparto].&[Vendite].&[Responsabile vendite Nord America].&[272]* .|  
|**BackgroundColor**|**String**|Restituisce il colore di sfondo definito nel database per il campo.|  
|**Colore**|**String**|Restituisce il colore di primo piano definito nel database per l'elemento.|  
|**FontFamily**|**String**|Restituisce il nome del tipo di carattere definito nel database per l'elemento.|  
|**FontSize**|**String**|Restituisce le dimensioni in punti del tipo di carattere definito nel database per l'elemento.|  
|**SpessoreCarattere**|**String**|Restituisce lo spessore del carattere definito nel database per l'elemento.|  
|**FontStyle**|**String**|Restituisce lo stile del tipo di carattere definito nel database per l'elemento.|  
|**TextDecoration**|**String**|Restituisce la formattazione di testo speciale definita nel database per l'elemento.|  
|**FormattedValue**|**String**|Restituisce un valore formattato per una misura o una cifra chiave. La proprietà **FormattedValue** di **Quote vendite** restituisce, ad esempio, un formato valuta come $ 1.124.400,00.|  
|**Key**|**Oggetto**|Restituisce la chiave per un livello.|  
|**LevelNumber**|**Integer**|Per gerarchie padre-figlio, questa proprietà restituisce il numero del livello o della dimensione.|  
|**ParentUniqueName**|**String**|Per gerarchie padre-figlio, restituisce un nome completo del livello padre.|  
  
> [!NOTE]  
>  I valori per queste proprietà di campo estese sono disponibili solo se vengono forniti dall'origine dati, ad esempio il cubo di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , quando il report viene eseguito e vengono recuperati i dati per i relativi set di dati. È quindi possibile fare riferimento a tali valori delle proprietà di campo in qualsiasi espressione utilizzando la sintassi descritta nella sezione seguente. Poiché, tuttavia, questi campi sono specifici del provider di dati in uso, eventuali modifiche apportate a tali valori non vengono salvate con la definizione del report.  
  
### <a name="example-extended-properties"></a>Proprietà estese di esempio  
 Per illustrare le proprietà estese, la query MDX seguente e il relativo set di risultati includono diverse proprietà del membro disponibili da un attributo delle dimensioni definito per un cubo. Le proprietà del membro incluse sono MEMBER_CAPTION, UNIQUENAME, Properties("Day Name"), MEMBER_VALUE, PARENT_UNIQUE_NAME e MEMBER_KEY.  
  
 La query MDX viene eseguita sul cubo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] nel database [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] DW incluso nei database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
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
  
 Quando si esegue la query in un riquadro di query MDX, si ottiene un set di risultati costituito da 1158 righe. Le prime quattro righe sono illustrate nella tabella seguente.  
  
|DateCaption|DateUniqueName|DateDayName|DateValueinOriginalDatatype|DateParentUniqueName|DateMemberKeyinOriginalDatatype|  
|-----------------|--------------------|-----------------|---------------------------------|--------------------------|-------------------------------------|  
|All Periods|[Date].[Date].[All Periods]|(null)|(null)|(null)|0|  
|1-Jul-01|[Date].[Date].&[1]|Domenica|7/1/2001|[Date].[Date].[All Periods]|1|  
|2-Jul-01|[Date].[Date].&[2]|Lunedì|7/2/2001|[Date].[Date].[All Periods]|2|  
|3-Jul-01|[Date].[Date].&[3]|Martedì|7/3/2001|[Date].[Date].[All Periods]|3|  
  
 Le query MDX predefinite compilate mediante Progettazione query MDX in modalità grafica includono solo MEMBER_CAPTION e UNIQUENAME per le proprietà delle dimensioni. Per impostazione predefinita, tali valori sono sempre di tipo **String**.  
  
 Se è necessaria una proprietà del membro nel tipo di dati originale, è possibile includere un'ulteriore proprietà MEMBER_VALUE modificando l'istruzione MDX predefinita in Progettazione query basata su testo. Nella semplice istruzione MDX seguente, MEMBER_VALUE è stata aggiunta all'elenco delle proprietà delle dimensioni da recuperare.  
  
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
  
 Le prime quattro righe visualizzate nel riquadro risultati MDX sono illustrate nella tabella seguente.  
  
|Month of Year|Order Count|  
|-------------------|-----------------|  
|Gennaio|2,481|  
|Febbraio|2,684|  
|Marzo|2,749|  
|April|2,739|  
  
 Sebbene le proprietà facciano parte dell'istruzione MDX SELECT, non sono incluse nelle colonne del set di risultati. I dati sono tuttavia disponibili per un report mediante la caratteristica delle proprietà estese. Nel riquadro risultati di una query MDX di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]fare doppio clic sulla cella per visualizzare i relativi valori delle proprietà, se impostati nel cubo. Se si fa doppio clic sulla prima cella Order Count contenente 1,379, verrà visualizzata una finestra popup con le proprietà della cella seguenti:  
  
|Proprietà|valore|  
|--------------|-----------|  
|CellOrdinal|0|  
|Value|2481|  
|BACK_COLOR|(null)|  
|FORE_COLOR|(null)|  
|FORMATTED_VALUE|2,481|  
|FORMAT_STRING|#,#|  
|FONT_NAME|(null)|  
|FONT_SIZE|(null)|  
|FONT_FLAGS|(null)|  
  
 Se si crea un set di dati del report con questa query e lo si associa a una tabella, sarà possibile visualizzare la proprietà VALUE predefinita per un campo, ad esempio `=Fields!Month_of_Year!Value`. Se si imposta questa espressione come espressione di ordinamento per la tabella, la tabella verrà ordinata alfabeticamente in base al mese poiché il tipo di dati del campo Value è **String** . Per ordinare la tabella in modo che i mesi si trovino nell'ordine di successione nell'anno, con gennaio primo e dicembre ultimo, utilizzare l'espressione seguente:  
  
```  
=Fields!Month_of_Year("MEMBER_VALUE")  
```  
  
 In questo modo i valori del campo verranno ordinati in base al tipo di dati interi originale dell'origine dei dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Raccolte predefinite nelle espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
