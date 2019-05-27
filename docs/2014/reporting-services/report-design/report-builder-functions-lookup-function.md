---
title: Funzione Lookup (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: e60e5bab-b286-4897-9685-9ff12703517d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 93e53646314d211ced489d3538b40c77195f494b
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66105219"
---
# <a name="lookup-function-report-builder-and-ssrs"></a>Funzione Lookup (Generatore report e SSRS)
  Viene restituito il primo valore corrispondente per il nome specificato da un set di dati contenente coppie nome/valore.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Lookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>Parametri  
 *source_expression*  
 (`Variant`) Espressione valutata nell'ambito corrente che specifica il nome o la chiave da ricercare, Ad esempio `=Fields!ProdID.Value`.  
  
 *destination_expression*  
 (`Variant`) Espressione valutata per ogni riga in un set di dati che specifica il nome o la chiave con cui eseguire la corrispondenza, Ad esempio `=Fields!ProductID.Value`.  
  
 *result_expression*  
 (`Variant`) Espressione valutata per la riga nel set di dati in cui *source_expression* = *destination_expression*, che specifica il valore da recuperare. Ad esempio `=Fields!ProductName.Value`.  
  
 *set di dati*  
 Costante che specifica il nome di un set di dati nel report, ad esempio, "Prodotti".  
  
## <a name="return"></a>Return  
 Restituisce `Variant` o `Nothing` se non viene rilevata alcuna corrispondenza.  
  
## <a name="remarks"></a>Note  
 Utilizzare la funzione `Lookup` per recuperare il valore dal set di dati specificato per una coppia nome/valore in cui esiste una relazione uno-a-uno. Ad esempio per un campo ID in una tabella, è possibile utilizzare `Lookup` per recuperare il campo Nome corrispondente da un set di dati non associato all'area dati.  
  
 Tramite la funzione `Lookup` vengono effettuate le operazioni seguenti:  
  
-   Valuta l'espressione di origine nell'ambito corrente.  
  
-   Valuta l'espressione di destinazione per ogni riga del set di dati specificato dopo che sono stati applicati i filtri, in base alle regole di confronto del set di dati specificato.  
  
-   Nella prima corrispondenza di espressione di origine ed espressione di destinazione, valuta l'espressione di risultato per quella riga nel set di dati.  
  
-   Restituisce il valore dell'espressione di risultato.  
  
 Per recuperare più valori per un solo nome o un campo chiave in cui esiste una relazione uno-a-molti, usare [Funzione LookupSet &#40;Generatore report e SSRS&#41;](report-builder-functions-lookupset-function.md). Per chiamare `Lookup` per un set di valori, usare [funzione Multilookup &#40;Generatore Report e SSRS&#41;](report-builder-functions-lookup-function.md).  
  
 Sono previste le restrizioni seguenti:  
  
-   La funzione `Lookup` viene valutata dopo l'applicazione di tutte le espressioni di filtro.  
  
-   È supportato solo un livello di ricerca. Un'espressione di origine, destinazione o risultato non può includere un riferimento a una funzione di ricerca.  
  
-   Le espressioni di origine e di destinazione devono restituire lo stesso tipo di dati. Il tipo restituito è lo stesso del tipo di dati dell'espressione di risultato valutata.  
  
-   Le espressioni di origine, di destinazione e di risultato non possono includere riferimenti a variabili di report o di gruppo.  
  
-   La funzione `Lookup` non può essere utilizzata come espressione per gli elementi del report seguenti:  
  
    -   Stringhe di connessione dinamiche per un'origine dati.  
  
    -   Campi calcolati in un set di dati.  
  
    -   Parametri di query in un set di dati.  
  
    -   Filtri in un set di dati.  
  
    -   Parametri di report.  
  
    -   Proprietà Report.Language.  
  
 Per altre informazioni, vedere [Riferimento a funzioni di aggregazione &#40;Generatore report e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente, si supponga che una tabella sia associata a un set di dati che include un campo per l'identificatore del prodotto ProductID. Un set di dati separato denominato "Prodotto" contiene l'ID dell'identificatore del prodotto e il Nome del nome del prodotto corrispondenti.  
  
 Nell'espressione seguente, la funzione `Lookup` confronta il valore di ProductID con l'ID in ogni riga del set di dati denominata "Prodotto" e, quando viene rilevata una corrispondenza, restituisce il valore del campo Name per quella riga.  
  
```  
=Lookup(Fields!ProductID.Value, Fields!ID.Value, Fields!Name.Value, "Product")  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo delle espressioni nei report &#40;Generatore report e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipi di dati nelle espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ambito di espressioni per totali, aggregazioni e raccolte predefinite &#40;Generatore report e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
