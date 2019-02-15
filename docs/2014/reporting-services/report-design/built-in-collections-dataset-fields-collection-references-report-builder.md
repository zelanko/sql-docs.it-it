---
title: Riferimenti alla raccolta di campi del set di dati (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 006c6bd3-d776-4c20-9092-32e40688ac49
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d4717b1f8a905576d2f59657fd8ae8ad00396e3b
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56297429"
---
# <a name="dataset-fields-collection-references-report-builder-and-ssrs"></a>Riferimenti alla raccolta di campi del set di dati (Generatore report e SSRS)
  In ogni set di dati di un report è contenuta una raccolta Campi. La raccolta Campi rappresenta il set di campi specificati dalla query del set di dati, più qualsiasi campo calcolato aggiuntivo creato dall'utente. Dopo la creazione di un set di dati, la raccolta di campi viene visualizzata nel riquadro **Dati report** .  
  
 In un'espressione un riferimento di campo semplice viene visualizzato nell'area di progettazione come un'espressione semplice. Quando ad esempio si trascina il campo `Sales` dal riquadro dei dati del report in una cella della tabella nell'area di progettazione, viene visualizzato `[Sales]` . Questo parametro rappresenta l'espressione `=Fields!Sales.Value` sottostante impostata nella proprietà Value della casella di testo. Durante l'esecuzione del report, questa espressione viene valutata in Elaborazione report e i dati effettivi vengono visualizzati dall'origine dati nella casella di testo nella cella della tabella. Per altre informazioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md) e [Riferimenti alla raccolta di campi del set di dati &#40;Generatore report e SSRS&#41;](../report-data/dataset-fields-collection-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="displaying-the-field-collection-for-a-dataset"></a>Visualizzazione della raccolta di campi per un set di dati  
 Per visualizzare i singoli valori per una raccolta di campi, trascinare ogni campo in una riga di dettaglio della tabella ed eseguire il report. I riferimenti dalla riga di dettaglio di un'area dati tabella o elenco consentono di visualizzare un valore per ogni riga del set di dati.  
  
 Per visualizzare i valori di riepilogo per un campo, trascinare ogni campo numerico nell'area dati di una matrice. La funzione di aggregazione predefinita per la riga del totale è Sum, ad esempio `=Sum(Fields!Sales.Value)`. È possibile modificare la funzione predefinita per calcolare totali diversi. Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
 Per visualizzare valori di riepilogo per una raccolta di campi in una casella di testo direttamente nell'area di progettazione (non appartenente a un'area dati), è necessario specificare il nome del set di dati come ambito per la funzione di aggregazione. Per un set di dati denominato `SalesData`, ad esempio, l'espressione seguente specifica il totale di tutti i valori per il campo `Sales`: `=Sum(Fields!Sales,"SalesData")`.  
  
 Quando si usa la finestra di dialogo **Espressione** per definire un riferimento di campo semplice, è possibile selezionare la raccolta Campi nel riquadro Categoria e visualizzare l'elenco dei campi disponibili nel riquadro **Campo** . A ogni campo sono associate diverse proprietà, ad esempio Value e IsMissing. Le proprietà rimanenti sono proprietà di campo estese predefinite che possono essere disponibili per il set di dati in base al tipo dell'origine dati.  
  
### <a name="detecting-nulls-for-a-dataset-field"></a>Rilevamento di valori Null per un campo del set di dati  
 Per rilevare un valore Null in un campo (`Nothing` in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), è possibile utilizzare la funzione `IsNothing`. Quando è posizionata in una casella di testo in una riga dei dettagli della tabella, l'espressione seguente esegue il test del campo `MiddleName` . Se il valore è Null, viene sostituito il testo "No Middle Name". In caso contrario, viene sostituito il valore del campo stesso:  
  
 `=IIF(IsNothing(Fields!MiddleName.Value),"No Middle Name",Fields!MiddleName.Value)`  
  
### <a name="detecting-missing-fields-for-dynamic-queries-at-run-time"></a>Rilevamento di campi mancanti per query dinamiche in fase di esecuzione  
 Per impostazione predefinita, gli elementi nella raccolta di campi hanno due proprietà: Value e IsMissing. La proprietà IsMissing indica se un campo definito per un set di dati in fase di progettazione è incluso nei campi recuperati in fase di runtime. La query può ad esempio chiamare una stored procedure in cui il set di risultati varia in base a un parametro di input oppure la query può essere `SELECT * FROM` *\<table>*, in cui la definizione della tabella è stata modificata.  
  
> [!NOTE]  
>  IsMissing consente di rilevare le modifiche nello schema del set di dati tra la fase di progettazione e quella di runtime per qualsiasi tipo di origine dati. IsMissing non può essere usata per rilevare membri vuoti in un cubo multidimensionale e non è correlata ai concetti di linguaggio di query MDX di `EMPTY` e `NON EMPTY`.  
  
 È possibile eseguire il test della proprietà IsMissing con un codice personalizzato per determinare se un campo è presente nel set di risultati. Non è possibile eseguire il test relativo a tale presenza utilizzando un'espressione con una chiamata a una funzione [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], ad esempio `IIF` o `SWITCH`, poiché in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] vengono valutati tutti i parametri presenti nella chiamata alla funzione e viene restituito un errore quando viene valutato il riferimento al parametro mancante.  
  
#### <a name="example-for-controlling-the-visibility-of-a-dynamic-column-for-a-missing-field"></a>Esempio per il controllo della visibilità di una colonna dinamica per un campo mancante  
 Per impostare un'espressione che controlla la visibilità di una colonna in cui viene visualizzato un campo in un set di dati, è necessario innanzitutto definire una funzione di codice personalizzata che restituisca un valore booleano in base alla presenza o all'assenza del campo. La funzione di codice personalizzata seguente, ad esempio, restituisce true se il campo non è presente. In caso contrario, restituisce false.  
  
```  
Public Function IsFieldMissing(field as Field) as Boolean  
 If (field.IsMissing) Then  
 Return True  
  Else   
  Return False  
 End If  
End Function  
```  
  
 Per usare questa funzione al fine di controllare la visibilità di una colonna, impostare la proprietà Nascosto della colonna sull'espressione seguente:  
  
 `=Code.IsFieldMissing(Fields!FieldName)`  
  
 Quando il campo non esiste, la colonna è nascosta.  
  
#### <a name="example-for-controlling-the-text-box-value-for-a-missing-field"></a>Esempio per il controllo del valore della casella di testo per un campo mancante  
 Per sostituire il testo da scrivere al posto del valore di un campo mancante, è necessario scrivere codice personalizzato che restituisca il testo da utilizzare in sostituzione di un valore di campo quando quest'ultimo non è presente. La funzione di codice personalizzata seguente restituisce ad esempio il valore del campo se il campo esiste e il messaggio specificato dall'utente come secondo parametro se il campo non esiste:  
  
```  
Public Function IsFieldMissingThenString(field as Field, strMessage as String) as String  
 If (field.IsMissing) Then  
  Return strMessage  
 Else   
  Return field.Value  
  End If  
End Function  
```  
  
 Per usare questa funzione in una casella di testo, aggiungere l'espressione seguente alla proprietà Value:  
  
 `=Code.IsFieldMissingThenString(Fields!FieldName,"Missing")`  
  
 Nella casella di testo viene visualizzato il valore del campo o il testo specificato dall'utente.  
  
### <a name="using-extended-field-properties"></a>Utilizzo delle proprietà di campo estese  
 Le proprietà di campo estese sono proprietà aggiuntive definite in un campo dall'estensione per l'elaborazione dati determinata dal tipo di origine dati per il set di dati. Tali proprietà sono predefinite o specifiche per un tipo di origine dati. Per altre informazioni, vedere [Proprietà di campo estese per un database di Analysis Services &#40;SSRS&#41;](../report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
 Se si specifica una proprietà non supportata per un campo specifico, tale espressione restituirà `null` (`Nothing` in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]). Se un provider di dati non supporta le proprietà di campo estese o se il campo non viene trovato durante l'esecuzione della query, il valore della proprietà è `null` (`Nothing` in [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) per le proprietà di tipo `String` e `Object` e zero (0) per le proprietà di tipo `Integer`. Un'estensione per l'elaborazione dati può sfruttare le proprietà predefinite ottimizzando le query che includono tale sintassi.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Aggiungere dati a un Report &#40;Report e SSRS&#41;](../report-data/report-datasets-ssrs.md)  
  
  
