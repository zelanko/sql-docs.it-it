---
title: Impostare la proprietà Slice delle partizioni (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 08/05/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- partitions [Analysis Services], data slices
- data slices [Analysis Services]
ms.assetid: 507b91e5-7f85-4c22-be97-4d7a676e6667
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d9d7b41de3505c3b6e3ccf3886254958ee71e456
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66072934"
---
# <a name="set-the-partition-slice-property-analysis-services"></a>Impostare la proprietà Slice delle partizioni (Analysis Services)
  Una sezione di dati è una funzionalità di ottimizzazione importante che semplifica l'indirizzamento delle query sui dati delle partizioni appropriate. Impostare in modo esplicito la proprietà Slice può migliorare le prestazioni delle query tramite l'override delle sezioni predefinite generate per le partizioni MOLAP e HOLAP. Inoltre, la proprietà Slice offre un ulteriore controllo di convalida durante l'elaborazione della partizione.  
  
 È possibile specificare una sezione di dati dopo avere creato una partizione, ma prima di elaborarla, utilizzando la proprietà Slice. Nella scheda Partizioni espandere un gruppo di misure, fare clic con il pulsante destro del mouse su una partizione e selezionare **Proprietà**.  
  
## <a name="defining-a-slice"></a>Definizione di una proprietà Slice  
 I valori validi per una proprietà Slice sono un membro, un set o una tupla MDX. Negli esempi seguenti viene illustrata la sintassi valida per la proprietà Slice:  
  
|Sezione|Membro, set o tupla|  
|-----------|--------------------------|  
|[Date].[Calendar].[Calendar Year].&[2010]|Specificare questa sezione in una partizione contenente i fatti dall'anno 2010 (supponendo che il modello includa una dimensione Date con la gerarchia Calendar Year, dove 2010 è un membro). Sebbene la clausola WHERE o la tabella di origine della partizione possa già prevedere il filtraggio in base all'anno 2010, la specificazione della proprietà Slice fornisce un ulteriore controllo durante l'elaborazione, nonché analisi maggiormente mirate durante l'esecuzione della query.|  
|{ [Sales Territory].[Sales Territory Country].&[Australia], [Sales Territory].[Sales Territory Country].&[Canada] }|Specificare questa sezione in una partizione contenente i fatti che includono informazioni sui territori di vendita. Una sezione può essere un set MDX costituito da due o più membri.|  
|[Measures].[Sales Amount Quota] > '5000'|Per questa sezione viene utilizzata un'espressione MDX.|  
  
 Una sezione di dati di una partizione deve riflettere quanto più accuratamente possibile i dati della partizione. Se ad esempio una partizione contiene solo i dati relativi al 2012, la sezione di dati corrispondente deve specificare il membro 2012 della dimensione temporale. Non è tuttavia possibile specificare sempre una sezione di dati che rifletta il contenuto esatto di una partizione. Se ad esempio una partizione contiene solo i dati relativi ai mesi di gennaio e febbraio ma i livelli della dimensione temporale sono Anno, Trimestre e Mese, nella Creazione guidata partizione non è possibile selezionare entrambi i membri Gennaio e Febbraio. In tali casi, selezionare il padre dei membri che riflettono il contenuto della partizione, che in questo esempio è Trimestre 1.  
  
 Per una illustrazione dei vantaggi delle sezioni di dati, vedere l'articolo relativo all' [impostazione di una sezione nella partizione del cubo SSAS](https://go.microsoft.com/fwlink/?LinkId=317783).  
  
> [!NOTE]  
>  Si noti che le funzioni MDX dinamiche, ad esempio [Generate &#40;MDX&#41;](/sql/mdx/generate-mdx) o [Except &#40;MDX&#41;](/sql/mdx/except-mdx-function) non sono supportate nella proprietà Slice per le partizioni. È necessario definire la sezione usando tuple esplicite o riferimenti ai membri.  
>   
>  Ad esempio, invece di usare la [: &#40;intervallo&#41; &#40;MDX&#41; ](/sql/mdx/range-mdx) function per definire un intervallo, è necessario enumerare ogni membro in base agli anni specifici.  
>   
>  Se occorre definire una sezione complessa, è consigliabile definire le tuple nella sezione mediante uno script XMLA Alter. È quindi possibile usare lo strumento da riga di comando ascmd o l'attività [Analysis Services Execute DDL Task](../../integration-services/control-flow/analysis-services-execute-ddl-task.md) di SSIS per eseguire lo script e creare il set di membri specificato immediatamente prima dell'elaborazione della partizione.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare e gestire una partizione locale &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)  
  
  
