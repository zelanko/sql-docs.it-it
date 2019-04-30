---
title: Query con parametri (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- parameter queries [SQL Server]
ms.assetid: 4897c41a-324a-47b8-a30b-cbc9e9e19a8b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5a3ea199f6e2e86f5dc2e51199386f31b93e9377
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63194991"
---
# <a name="parameter-queries-visual-database-tools"></a>Query con parametri (Visual Database Tools)
  In alcuni casi potrebbe essere necessario creare una query da utilizzare più volte, specificando però ogni volta un valore diverso. Se, ad esempio, si eseguono di frequente delle query per individuare tutti i `title_ids` di un determinato autore, è possibile utilizzare la stessa query per tutte le richieste specificando però ogni volta un ID o un nome di autore diverso.  
  
 Per creare una query che può accettare valori diversi in momenti diversi, è necessario utilizzare i parametri. Un parametro è un segnaposto per un valore che verrà fornito durante l'esecuzione della query. Un'istruzione SQL con un parametro potrebbe essere simile alla seguente, dove "?" rappresenta il parametro relativo all'ID dell'autore:  
  
```  
SELECT title_id  
FROM titleauthor  
WHERE (au_id = ?)  
```  
  
## <a name="where-you-can-use-parameters"></a>Possibili utilizzi dei parametri  
 È possibile usare i parametri come segnaposto per valori letterali (per valori di testo o numerici). Nella maggior parte dei casi i parametri vengono utilizzati come segnaposto all'interno di condizioni di ricerca per singole righe o per gruppi, ovvero nelle clausole WHERE o HAVING di un'istruzione SQL.  
  
 I parametri possono essere utilizzati nelle espressioni come segnaposto. Si supponga ad esempio di voler calcolare prezzi scontati specificando un valore di sconto diverso a ogni esecuzione della query. A tale scopo, è possibile utilizzare la seguente espressione:  
  
```  
(price * ?)  
```  
  
## <a name="specifying-unnamed-and-named-parameters"></a>Specifica di parametri denominati e non denominati  
 È possibile specificare due tipi di parametri: denominati e non denominati. Un parametro non denominato è un punto di domanda (?) che è possibile inserire in una posizione qualsiasi della query per richiedere o per sostituire un valore letterale. Se, ad esempio, si usa un parametro non denominato per cercare l'ID di un autore nella tabella `titleauthor` , l'istruzione risultante nel [riquadro SQL](visual-database-tools.md) potrebbe essere simile alla seguente:  
  
```  
SELECT title_id  
FROM titleauthor  
WHERE (au_id = ?)  
```  
  
 Al momento dell'esecuzione della query in [Progettazione query e Progettazione viste](query-and-view-designer-tools-visual-database-tools.md), nella [finestra di dialogo Parametri query](query-parameters-dialog-box-visual-database-tools.md) viene visualizzato un punto interrogativo ("?") come nome del parametro.  
  
 In alternativa, è possibile assegnare un nome a un parametro. I parametri denominati risultano particolarmente utili quando in una query sono presenti più parametri. Se, ad esempio, si utilizzano parametri denominati per cercare il nome e il cognome di un autore in una tabella `authors` , l'istruzione risultante nel riquadro SQL potrebbe essere simile alla seguente:  
  
```  
SELECT au_id  
FROM authors  
WHERE au_fname = %first name% AND  
      au_lname = %last name%  
```  
  
> [!TIP]  
>  Prima di creare una query con parametri denominati, è necessario definire i caratteri del prefisso e del suffisso.  
  
 Al momento dell'esecuzione della query in Progettazione query e Progettazione viste, nella [finestra di dialogo Parametri query](query-parameters-dialog-box-visual-database-tools.md) viene visualizzato un elenco di parametri denominati.  
  
## <a name="see-also"></a>Vedere anche  
 [Query con parametri &#40;Visual Database Tools&#41;](query-with-parameters-visual-database-tools.md)   
 [Tipi di Query supportati &#40;Visual Database Tools&#41;](supported-query-types-visual-database-tools.md)   
 [Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
