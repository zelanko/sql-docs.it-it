---
description: Sintassi (SSIS)
title: Sintassi (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- expressions [Integration Services], syntax
- syntax [Integration Services]
ms.assetid: 61c053c5-1182-4ad0-b804-51cbd19aa0ba
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3262135632cc10036bf03c93edd448de16fbbc79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484397"
---
# <a name="syntax-ssis"></a>Sintassi (SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  La sintassi delle espressioni di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è simile a quella utilizzata nei linguaggi C e C#. Le espressioni includono elementi quali identificatori (colonne e variabili), valori letterali, operatori e funzioni. In questo argomento vengono riepilogati i requisiti specifici della sintassi dell'analizzatore di espressioni, in relazione ai diversi elementi delle espressioni.  
  
> [!NOTE]  
>  Nella versioni precedenti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]era presente un limite di 4000 caratteri sul risultato della valutazione di un'espressione quando il tipo di dati [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] del risultato era DT_WSTR o DT_STR. Questo limite è stato eliminato.  
  
 Per esempi di espressioni che usano operatori e funzioni specifiche, vedere l'argomento relativo a ogni operatore e funzione negli argomenti: [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md) e [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md).  
  
 Per esempi di espressioni che usano più operatori e funzioni, nonché identificatori e valori letterali, vedere [Esempi di espressioni avanzate di Integration Services](../../integration-services/expressions/examples-of-advanced-integration-services-expressions.md).  
  
 Per espressioni di esempio da usare nelle espressioni di proprietà, vedere [Usare le espressioni di proprietà nei pacchetti](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
## <a name="identifiers"></a>Identificatori  
 Le espressioni possono includere identificatori di colonna e di variabile. È possibile utilizzare colonne esistenti nell'origine dei dati oppure colonne create da trasformazioni nel flusso di dati. Nelle espressioni è possibile utilizzare identificatori di derivazione per fare riferimento alle colonne. Gli identificatori di derivazione sono numeri che identificano in modo univoco gli elementi di un pacchetto. Per fare riferimento a un identificatore di derivazione nell'ambito di un'espressione, è necessario anteporvi un simbolo di cancelletto (#). Per fare riferimento all'identificatore di derivazione 138, ad esempio, è necessario specificare #138.  
  
 Le espressioni possono includere variabili personalizzate e le variabili di sistema disponibili in [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Quando in un'espressione viene fatto riferimento a una variabile, è necessario anteporre il prefisso \@ al nome della variabile. Per fare riferimento alla variabile `Counter`, ad esempio, è necessario specificare \@Counter. Il carattere \@ non fa parte del nome della variabile, ma consente all'analizzatore di espressioni di identificarla come tale. Per altre informazioni, vedere [Identificatori &#40;SSIS&#41;](../../integration-services/expressions/identifiers-ssis.md).  
  
## <a name="literals"></a>Valori letterali  
 Le espressioni possono includere valori letterali numerici, stringa e booleani. I valori letterali stringa utilizzati nelle espressioni devono essere racchiusi tra virgolette. Le virgolette non devono essere invece utilizzate per i valori letterali numerici e booleani. Il linguaggio delle espressioni include sequenze di escape per i caratteri di escape più comuni. Per altre informazioni, vedere [Valori letterali &#40;SSIS&#41;](../../integration-services/expressions/numeric-string-and-boolean-literals.md).  
  
## <a name="operators"></a>Operatori  
 L'analizzatore di espressioni fornisce un set di operatori con funzionalità analoghe a quelle offerte dai set di operatori di linguaggi quali Transact-SQL, C++ e C#. Oltre a questi, il linguaggio delle espressioni include anche operatori aggiuntivi e utilizza simboli diversi da quelli abitualmente utilizzati in altri linguaggi. Per altre informazioni, vedere [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md).  
  
### <a name="namespace-resolution-operator"></a>Operatore per la risoluzione degli spazi dei nomi  
 Nelle espressioni è possibile utilizzare l'operatore per la risoluzione degli spazi dei nomi (::) per eliminare le ambiguità dovute alla presenza di variabili con lo stesso nome. L'operatore per la risoluzione degli spazi dei nomi consente di qualificare ogni variabile con il relativo spazio dei nomi, permettendo così di utilizzare più variabili con lo stesso nome nell'ambito di un pacchetto.  
  
#### <a name="cast-operator"></a>Operatore cast  
 L'operatore cast consente di convertire da un tipo di dati all'altro i risultati delle espressioni, i valori delle colonne, i valori delle variabili e le costanti. L'operatore cast del linguaggio delle espressioni è simile a quello disponibile nei linguaggi C e C#. In Transact-SQL questa funzionalità è offerta dalle funzioni CAST e CONVERT. La sintassi dell'operatore cast presenta tuttavia le seguenti differenze rispetto a quella delle funzioni CAST e CONVERT:  
  
-   È possibile utilizzare un'espressione come argomento.  
  
-   La sintassi non include la parola chiave CAST.  
  
-   La sintassi non include la parola chiave AS.  
  
##### <a name="conditional-operator"></a>Operatore condizionale  
 L'operatore condizionale restituisce una delle due espressioni specificate, in base al valore restituito da un'espressione booleana. L'operatore condizionale del linguaggio delle espressioni è simile a quello disponibile nei linguaggi C e C#. Nelle espressioni MDX questo tipo di funzionalità è offerto dalla funzione IIF.  
  
###### <a name="logical-operators"></a>Operatori logici  
 Il linguaggio delle espressioni supporta il carattere ! per l'operatore NOT logico. In Transact-SQL l'operatore ! è incorporato nel set degli operatori relazionali. Transact-SQL offre ad esempio gli operatori > e !>. Il linguaggio delle espressioni di [!INCLUDE[ssIS](../../includes/ssis-md.md)] non supporta l'uso dell'operatore ! in combinazione con altri operatori. Non è ad esempio possibile combinare ! e > per ottenere !>. Il linguaggio delle espressioni supporta tuttavia la combinazione predefinita di caratteri !=, che rappresenta l'operatore "diverso da".  
  
###### <a name="equality-operators"></a>Operatori di uguaglianza  
 La grammatica dell'analizzatore di espressioni prevede l'operatore di uguaglianza ==, che equivale all'operatore = di Transact-SQL e all'operatore == di C#.  
  
## <a name="functions"></a>Funzioni  
 Il linguaggio delle espressioni include funzioni di data e ora e funzioni per i valori stringa simili alle funzioni di Transact-SQL e ai metodi di C#.  
  
 Anche se in alcuni casi i nomi delle funzioni dell'analizzatore sono uguali a quelli delle analoghe funzioni di Transact-SQL, esistono tuttavia alcune differenze funzionali.  
  
-   In Transact-SQL la funzione ISNULL sostituisce i valori Null con un valore specificato, mentre la funzione ISNULL dell'analizzatore di espressioni restituisce un valore booleano che indica se l'espressione restituisce Null o meno.  
  
-   In Transact-SQL la funzione ROUND include un'opzione che consente di troncare il set di risultati, ma per la funzione ROUND dell'analizzatore di espressioni tale opzione non è disponibile.  
  
 Per altre informazioni, vedere [Funzioni &#40;espressione SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 [Usare un'espressione in un componente flusso di dati](https://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Articolo tecnico relativo al [foglio d'aiuto per le espressioni SSIS](https://go.microsoft.com/fwlink/?LinkId=746575)sul sito Web pragmaticworks.com  
  
-   Articolo tecnico relativo agli [esempi di espressioni SSIS](https://go.microsoft.com/fwlink/?LinkId=220761)nel sito Web social.technet.microsoft.com  
  
  
