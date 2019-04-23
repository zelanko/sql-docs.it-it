---
title: rsProcessingError - Errore di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsProcessingError
ms.assetid: 414ee58a-8251-4367-9a8e-10c068d17280
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3f9826e22c617bbcae2630121ce1be23b2511a35
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59932687"
---
# <a name="rsprocessingerror---reporting-services-error"></a>rsProcessingError - Errore di Reporting Services
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID evento|rsProcessingError|  
|Origine evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings.resources|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Testo del messaggio|Errori durante l'elaborazione del report.|  
  
## <a name="explanation"></a>Spiegazione  
 Sono stati rilevati uno o più errori durante la pubblicazione, l'elaborazione, la visualizzazione in anteprima locale, la visualizzazione dal server di report o la creazione di una sottoscrizione per un report. Il messaggio di errore indica che è stato rilevato almeno un errore.  
  
### <a name="possible-causes"></a>Possibili cause  
 Le cause possibili includono:  
  
-   Si è verificato un errore di elaborazione nel server di report.  
  
-   Si è verificato un errore di elaborazione durante l'elaborazione del report locale quando è stata visualizzata l'anteprima di un report.  
  
-   Un'espressione di raggruppamento ha restituito un tipo di dati non corretto.  
  
-   Una definizione del filtro ha specificato due espressioni che hanno restituito tipi di dati che non è stato possibile confrontare.  
  
-   Un'espressione ha fatto riferimento a un campo non esistente dell'insieme Fields.  
  
-   Un'espressione ha incluso una chiamata di funzione di aggregazione con un ambito non valido o in conflitto.  
  
-   Un'espressione ha fatto riferimento a un parametro non esistente nella raccolta dei parametri del report.  
  
-   Un assembly personalizzato o un assembly di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] distribuito in modo non corretto non è stato caricato.  
  
-   Un parametro con le proprietà che ammette valori null è impostata su `False` ha rilevato un valore null nel parametro.  
  
-   Un'espressione per la proprietà Hidden di un'area dati contiene un errore: Riferimento oggetto non impostato su un'istanza di un oggetto.  
  
-   Un'espressione ha incluso una chiamata di funzione non valida oppure un errore di sintassi.  
  
## <a name="user-action"></a>Azione dell'utente  
  
### <a name="finding-more-information"></a>Per ulteriori informazioni  
 Eseguire una o più delle operazioni seguenti:  
  
-   Se si visualizza il report dal server di report o come sottoscrizione, esaminare il testo completo del messaggio di errore per ottenere ulteriori informazioni.  
  
-   Se il report viene creato in Progettazione report e questo errore viene visualizzato durante l'anteprima o la pubblicazione del report, ulteriori informazioni saranno disponibili nella finestra Elenco errori.  
  
-   Se il report viene creato in Anteprima di Progettazione report, esaminare il testo completo del messaggio di errore per ottenere ulteriori informazioni.  
  
-   Se si visualizza un report nel server di report e si esegue il servizio come amministratore locale nel server di report, è possibile visualizzare lo stack di chiamate facendo clic con il pulsante destro del mouse sulla pagina e scegliendo **Visualizza origine**. Nello stack di chiamate verranno fornite ulteriori informazioni.  
  
-   Se l'accesso al server di report è stato eseguito come amministratore locale, ricercare `ReportProcessingException`nel file di log. Le voci del log contengono ulteriori informazioni. Il file di log del server di report si trova in genere nel percorso \<*unità*>:\Programmi\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles\ReportServerService__*datetimestamp*.log. Per altre informazioni, vedere [File di log e origini di Reporting Services](../report-server/reporting-services-log-files-and-sources.md).  
  
### <a name="failed-to-load-expression-host-assembly"></a>Impossibile caricare l'assembly delle espressioni  
 Gli assembly personalizzati devono essere firmati con nome sicuro. È inoltre necessario che il relativo attributo AllowPartiallyTrustedCallers sia impostato. Per altre informazioni, vedere [Utilizzo di assembly personalizzati con i report](../custom-assemblies/using-custom-assemblies-with-reports.md) e [Informazioni sui criteri di sicurezza](../extensions/secure-development/understanding-security-policies.md).  
  
### <a name="a-built-in-global-name-does-not-exist"></a>Impossibile trovare un nome globale predefinito  
 Controllare l'ortografia nelle espressioni. I nomi predefiniti globali, dei parametri e dei campi rispettano la distinzione tra maiuscole e minuscole. Nell'espressione che provoca l'errore controllare che il nome esista effettivamente nel report e che sia stato digitato correttamente. Per altre informazioni, vedere [Raccolte predefinite nelle espressioni &#40;Generatore report e SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
### <a name="parameter-properties-and-null"></a>Proprietà dei parametri e valori Null  
 Il valore di un parametro multivalore non può essere Null. Per ulteriori informazioni, vedere la pagina relativa al [Parametri report &#40;Generatore report e Progettazione report&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
### <a name="main-report-with-subreport-could-not-be-processed"></a>Impossibile elaborare un report principale con sottoreport  
 È necessario che un report con sottoreport venga elaborato dalla stessa versione di Elaborazione report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Durante l'aggiornamento di report alla versione corrente dello schema di definizione del report, è possibile che il report principale e i sottoreport non vengano aggiornati contemporaneamente. Se la versione non è compatibile tra report e il sottoreport, viene visualizzato il messaggio seguente: "Impossibile elaborare un sottoreport."  
  
 È necessario modificare il report principale o i sottoreport in modo che tutti i report possano essere elaborati dalla stessa versione di Elaborazione report. Per informazioni sui motivi relativi all'impossibilità di aggiornare un report, vedere [Aggiornare i report](../install-windows/upgrade-reports.md).  
  
### <a name="verify-function-calls-are-visual-basic-and-not-sql"></a>Chiamate di funzione di Visual Basic e non SQL  
 È possibile usare le funzioni SQL nel testo della query in un database relazionale. Nel testo della query non è possibile usare funzioni [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .  
  
 In espressioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]è possibile usare funzioni [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] , funzioni System.Math o System.String, funzioni [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] complete o funzioni personalizzate incluse in codice o in un assembly personalizzato. Non è possibile usare funzioni SQL in un'espressione.  
  
 Verificare che le chiamate di funzione eseguite nella query e nelle espressioni siano valide.  
  
### <a name="cannot-compare-data-types-for-a-filter"></a>Impossibile confrontare tipi di dati per un filtro  
 In un'equazione di filtro è necessario che il tipo di dati dell'espressione che definisce gli elementi da filtrare e quello del valore del filtro sia lo stesso, in modo che sia possibile eseguirne il confronto. Se viene visualizzato uno degli errori seguenti, modificare l'espressione del campo o il valore del filtro in modo che i tipi di dati corrispondano:  
  
-   Impossibile eseguire l'elaborazione di *\<tipo di elemento del report>* per l'oggetto *\<nome dell'elemento del report>*. Non è possibile confrontare dati di tipo *\<tipo>* e *\<tipo>*. Verificare il tipo di dati restituito da *\<nome dell'elemento del report>*.  
  
-   Impossibile valutare *\<nome proprietà>*.  
  
-   Impossibile valutare *\<nome proprietà>*. Fa riferimento a un campo del set di dati che contiene un errore: *\<stringa di errore>*.  
  
 Per altre informazioni, vedere [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
### <a name="invalid-or-conflicting-scope-specification-in-an-aggregate-function-call"></a>Specifica di un ambito non valido o in conflitto in una chiamata di funzione di aggregazione  
 Quando si includono chiamate di funzioni di aggregazione in un'espressione di una cella Tablix, in Elaborazione report l'espressione viene valutata nell'ambito dei gruppi più interni cui la cella appartiene.  
  
 È anche possibile passare il nome di un ambito specifico a una funzione di aggregazione. L'ambito può fare riferimento al nome di un set di dati o di un'area dati oppure al nome di un ambito a livello più elevato nella gerarchia dei dati. Questa condizione è valida per i seguenti messaggi:  
  
-   *\<tipo di elemento del report>* '*\<nome dell'elemento del report>*' con ambito non valido "*\<nome ambito>*". L'ambito deve essere l'ambito corrente oppure deve essere contenuto nell'ambito corrente.  
  
-   L'espressione per *\<nome proprietà>* per l'oggetto '*\<nome dell'elemento del report>*' di tipo *\<tipo dell'elemento del report>* ha un parametro di ambito non valido per una funzione di aggregazione. Il parametro di ambito deve essere impostato su una costante stringa uguale al nome di un gruppo contenitore, al nome di un'area dati contenitore oppure al nome di un set di dati.  
  
 Per le funzioni di aggregazione che calcolano i totali parziali (`Previous`, `RunningValue` o `RowNumber`, è possibile specificare come parametro di ambito un nome di un gruppo di righe oppure un nome di un gruppo di colonne, ma non entrambi. Questa condizione è valida per il seguente messaggio di errore:  
  
-   `Previous`, `RunningValue` o `RowNumber` utilizzate nelle celle di dati di funzioni di aggregazione il  *\<tipo dell'elemento del report >* '*\<nome elemento report >*' fanno riferimento ad ambiti di raggruppamento in entrambe le colonne e righe del  *\<tipo di elemento del report >*. I parametri degli ambiti di tutte le `Previous`, `RunningValue` e `RowNumber` funzioni di aggregazione una  *\<tipo di elemento del report >* possono fare riferimento a raggruppamenti di righe o raggruppamenti di colonne di dati, ma non entrambi.  
  
 Per altre informazioni, vedere [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](../report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md) e [Raccolte predefinite nelle espressioni &#40;Generatore report e SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
### <a name="default-dataset-scope-for-a-top-level-text-box"></a>Ambito predefinito del set di dati per una casella di testo di livello principale  
 Non usare un ambito predefinito per una casella di testo aggiunta all'area di progettazione del report quando nel report è contenuto più di un set di dati. Usare invece un'espressione che includa il nome del set di dati come ambito e una funzione di aggregazione, Ad esempio, `=First(Fields!FieldName.Value, "DataSet2")`.  
  
## <a name="see-also"></a>Vedere anche  
 [Espressioni &#40;Generatore report e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)   
 [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](../report-design/report-builder-functions-aggregate-functions-reference.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../report-design/expression-examples-report-builder-and-ssrs.md)   
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](../report-data/report-datasets-ssrs.md)   
 [Filtri di uso comune &#40;Generatore report e SSRS&#41;](../report-design/commonly-used-filters-report-builder-and-ssrs.md)   
 [Raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](../report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [Riferimenti a codice personalizzato e ad assembly in espressioni in Progettazione report &#40;SSRS&#41;](../report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [Riferimenti alla raccolta dei parametri &#40;Generatore report e SSRS&#41;](../report-design/built-in-collections-parameters-collection-references-report-builder.md)  
  
  
