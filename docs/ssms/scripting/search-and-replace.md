---
title: Ricerca e sostituzione
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- match case [SQL Server]
- undo operations
- searches [SQL Server Management Studio]
- replacing text
- quick search and replaces [SQL Server Management Studio]
- Query Editor [SQL Server Management Studio], undo
- Query Editor [SQL Server Management Studio], searching
- regular expressions [SQL Server Management Studio]
- finding text [SQL Server Management Studio]
- text [SQL Server], search and replace operations
- finding [SQL Server Management Studio]
- locating text
- Query Editor [SQL Server Management Studio], replacing text
- Find and Replace dialog box
- wildcard options [SQL Server Management Studio]
- match whole word [SQL Server]
- searches [SQL Server Management Studio], replacing
ms.assetid: 3641c7b3-3e3e-4ddd-af82-c15b50004f94
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7fc7b5c7cb0fbd560dc2826af24029d2c7961d95
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75253688"
---
# <a name="search-and-replace"></a>Ricerca e sostituzione
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  È possibile eseguire ricerche e sostituzioni di testo in diversi modi. L'opzione **Trova e sostituisci** del menu **Modifica** offre quattro scelte: **Ricerca veloce**, **Sostituzione veloce**, **Cerca nei file**e **Sostituisci nei file**. L'aspetto della finestra di dialogo **Trova e sostituisci** cambia in base all'opzione selezionata. È inoltre possibile eseguire ricerche senza una finestra di dialogo, utilizzando i tasti di scelta rapida per la ricerca incrementale. Queste tecniche consentono di controllare l'ambito di ricerca e sostituzione e di scegliere il metodo di analisi dei risultati.  
  
 Al momento della ricerca e sostituzione di un testo, è consigliabile tenere presente quanto segue:  
  
-   Le opzioni impostate nella finestra di dialogo **Trova e sostituisci** influenzano tutte le ricerche. Le opzioni disponibili sono **Maiuscole/minuscole**, **Parola intera**, **Cerca in alto**, **Cerca nel testo nascosto**, **Caratteri jolly**, **Espressioni regolari**, **Tutti i documenti aperti**e **Progetto corrente**. Le opzioni effettivamente disponibili dipendono dalla versione usata della finestra di dialogo **Trova e sostituisci** .  
  
-   L'opzione**Annulla** è disponibile solo per i documenti lasciati aperti dopo un'operazione di sostituzione.  
  
-   L'opzione**Annulla** per un'operazione **Sostituisci tutto** eseguita su più di un file è considerata un'unica azione bulk su tutti i file interessati. Non è quindi possibile annullare la modifica in alcuni file e mantenerla in altri.  
  
 Non è in genere possibile eseguire ricerche in elementi grafici.  
  
## <a name="see-also"></a>Vedere anche  
 [Ricerca incrementale in un documento attivo](../../relational-databases/scripting/search-an-active-document-incrementally.md)   
 [Ricerca interattiva all'interno di documenti](../../relational-databases/scripting/search-documents-interactively.md)   
 [Ricerca nei documenti utilizzando gli elenchi dei risultati](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [Testo di ricerca con caratteri jolly](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [Eseguire ricerche di testo con espressioni regolari](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
