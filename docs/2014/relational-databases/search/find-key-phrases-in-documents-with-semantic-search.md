---
title: Trovare frasi chiave nei documenti tramite la ricerca semantica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- semantic search [SQL Server], key phrase queries
ms.assetid: 6ee3676e-ed5d-43ec-aeca-1eed78967111
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7ead6e45099ef16f8ee7d4935c5f02b528bd5750
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52406998"
---
# <a name="find-key-phrases-in-documents-with-semantic-search"></a>Trovare frasi chiave nei documenti mediante ricerca semantica
  Viene descritto come individuare le frasi chiave nei documenti o nelle colonne di testo configurati per l'indicizzazione semantica statistica.  
  
##  <a name="BasicsQueryKey"></a> Ricerca di frasi chiave nei documenti  
  
###  <a name="howtofind"></a> Come si fa: Individuare le frasi chiave nei documenti con SEMANTICKEYPHRASETABLE  
 Per identificare le frasi chiave in documenti specifici o identificare documenti che contengono frasi chiave specifiche, eseguire una query sulla funzione [semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql).  
  
 SEMANTICKEYPHRASETABLE restituisce una tabella con zero, una o più righe per le frasi chiave associate alle colonne nella tabella specificata. A questa funzione per i set di righe è possibile fare riferimento nella clausola FROM di un'istruzione SELECT come se fosse un normale nome di tabella.  
  
> [!NOTE]  
>  In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]solo singole parole vengono indicizzate per la ricerca semantica; le frasi composte da più parole (ngrams) non vengono indicizzate. Inoltre, varie forme della stessa parola vengono indicizzate separatamente; ad esempio "calcolo" e "calcoli" vengono indicizzati separatamente.  
  
 Per informazioni dettagliate sui parametri necessari per la funzione SEMANTICKEYPHRASETABLE e sulla tabella dei risultati restituita, vedere [semantickeyphrasetable &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/semantickeyphrasetable-transact-sql).  
  
> [!IMPORTANT]  
>  Per le colonne di destinazione deve essere abilitata l'indicizzazione full-text e semantica.  
  
###  <a name="HowToTopPhrases"></a> Esempio 1: Trovare le principali frasi chiave in un documento specifico  
 L'esempio seguente recupera le prime 10 frasi chiave dal documento specificato tramite la variabile @DocumentId nella colonna Document della tabella Production.Document del database di esempio AdventureWorks. La variabile @DocumentId rappresenta un valore della colonna chiave dell'indice full-text.  
  
```tsql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
GO  
```  
  
 La funzione **SEMANTICKEYPHRASETABLE** recupera in modo efficiente questi risultati tramite una ricerca nell'indice anziché un'analisi della tabella.  
  
###  <a name="HowToTopDocuments"></a> Esempio 2: Trovare i documenti principali che contengono una frase chiave specifica  
 Nell'esempio seguente vengono recuperati i primi 25 documenti che contengono la frase chiave "Bracket" dalla colonna Documento della tabella Production.Document del database di esempio AdventureWorks.  
  
```tsql  
SELECT TOP (25) DOC_TBL.DocumentID, DOC_TBL.DocumentSummary  
FROM Production.Document AS DOC_TBL  
    INNER JOIN SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document  
    ) AS KEYP_TBL  
ON DOC_TBL.DocumentID = KEYP_TBL.document_key  
WHERE KEYP_TBL.keyphrase = 'Bracket'  
ORDER BY KEYP_TBL.Score DESC;  
GO  
```  
  
  
