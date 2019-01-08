---
title: Regole per l'aggiornamento dei risultati (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- updating query results
- Query Designer [SQL Server], Results pane
- Results pane
ms.assetid: de131ef0-ccbd-446f-9400-b93c7b8fa537
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8f1814c96a5f58052be6271d2a35c1bbf78f87b1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52792424"
---
# <a name="rules-for-updating-results-visual-database-tools"></a>Regole per l'aggiornamento dei risultati (Visual Database Tools)
  Normalmente è possibile aggiornare il set di risultati visualizzato nel [riquadro Risultati](visual-database-tools.md). Talvolta non è tuttavia possibile.  
  
 Normalmente, per aggiornare i risultati, è necessario che in [Progettazione query e Progettazione viste](query-and-view-designer-tools-visual-database-tools.md) siano disponibili informazioni sufficienti per identificare in modo univoco la riga specifica all'interno della tabella. Questo è ad esempio possibile quando la query include una chiave primaria nell'elenco di output. Occorre inoltre disporre delle autorizzazioni necessarie per l'aggiornamento del database.  
  
 Se la query si basa su una vista, dovrebbe essere possibile aggiornarla. Restano valide le stesse indicazioni, con l'eccezione che si applicano non solo alla vista in sé, ma anche alle tabelle sottostanti.  
  
> [!NOTE]  
>  Progettazione query e Progettazione viste non è in grado di determinare in anticipo se sia possibile aggiornare un set di risultati sulla base di una vista. Vengono pertanto visualizzate tutte le viste, anche se alcune potrebbero non essere aggiornabili.  
  
 La tabella che segue contiene un riepilogo di istanze specifiche in cui è o non è possibile aggiornare i risultati delle query nel riquadro Risultati. In numerosi casi la possibilità di aggiornare o meno i risultati delle query dipende dal database utilizzato.  
  
|Query|Possibilità di aggiornare i risultati|  
|-----------|-----------------------------|  
|Query basata su una tabella con chiave primaria nell'elenco di output|Sì, ad eccezione di quanto elencato di seguito.|  
|Query basata su una tabella senza indice univoco e senza chiave primaria|Dipende dalla query e dal database. Alcuni database consentono l'aggiornamento se sono disponibili informazioni sufficienti per l'identificazione univoca dei record.|  
|Query basata su più tabelle non unite|No.|  
|Query basata su dati contrassegnati in sola lettura nel database|No.|  
|Query basata su una vista relativa a una tabella senza vincoli|Sì, ad eccezione di quanto elencato di seguito.|  
|Query basata su tabelle unite da una relazione uno-a-uno|Sì, ad eccezione di quanto elencato di seguito.|  
|Query basata su tabelle unite da una relazione uno-a-molti|In genere sì.|  
|Query basata su tre o più tabelle unite da una relazione molti-a-molti|No.|  
|Query basata su una tabella per la quale non è stata concessa l'autorizzazione di aggiornamento|Possibile l'eliminazione ma non l'aggiornamento.|  
|Query basata su una tabella per la quale non è stata concessa l'autorizzazione di eliminazione|Possibile l'aggiornamento ma non l'eliminazione.|  
|Query di aggregazione|No.|  
|Query basata su una sottoquery contenente totali o funzioni di aggregazione|No.|  
|Query che include la parola chiave DISTINCT per l'esclusione di righe duplicate|No.|  
|Query la cui clausola FROM include una funzione definita dall'utente che contiene più istruzioni Select e che restituisce una tabella|No.|  
|Query la cui clausola FROM include una funzione inline definita dall'utente|Sì.|  
  
 Può inoltre non essere possibile aggiornare colonne specifiche dei risultati delle query. L'elenco che segue contiene un riepilogo delle colonne che non è possibile aggiornare nel riquadro Risultati.  
  
-   Colonne basate su espressioni  
  
-   Colonne basate su funzioni scalari definite dall'utente  
  
-   Righe o colonne eliminate da un altro utente  
  
-   Righe o colonne bloccate da un altro utente. Le righe bloccate possono in genere essere aggiornate appena vengono sbloccate.  
  
-   Colonne timestamp o BLOB  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
  
