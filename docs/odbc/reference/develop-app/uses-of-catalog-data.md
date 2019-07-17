---
title: Utilizzi del catalogo dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dc8999c0a7189772145f553646b45eb1f1fbd695
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091608"
---
# <a name="uses-of-catalog-data"></a>Utilizzi dei dati del catalogo
Le applicazioni utilizzano i dati del catalogo in diversi modi. Ecco alcuni usi comuni:  
  
-   **Costruzione di istruzioni SQL in fase di esecuzione.** Applicazioni verticali, ad esempio un'applicazione di immissione dell'ordine, contengono le istruzioni SQL hard-coded. Le tabelle e colonne utilizzate dall'applicazione sono fisse anticipatamente, perché sono istruzioni che accedono a tali tabelle. Ad esempio, un'applicazione di immissione dell'ordine contiene in genere un singolo, con parametri **Inserisci** istruzione per l'aggiunta di nuovi ordini nel sistema.  
  
     Applicazioni generiche, ad esempio un foglio di calcolo che usa ODBC per recuperare i dati, spesso costruire istruzioni SQL in fase di esecuzione in base all'input dell'utente. Tale applicazione potrebbe richiedere all'utente di digitare i nomi delle tabelle e colonne da utilizzare. Tuttavia, sarebbe più semplice per l'utente se l'applicazione visualizzata gli elenchi di tabelle e colonne da cui l'utente è stato possibile effettuare le selezioni. Per compilare questi elenchi, l'applicazione chiama il **SQLTables** e **SQLColumns** funzioni di catalogo.  
  
-   **Costruzione di istruzioni SQL durante lo sviluppo.** Gli ambienti di sviluppo di applicazioni in genere consentono al programmatore di creare query sul database durante lo sviluppo di un programma. Le query vengono quindi impostate come hardcoded nell'applicazione in fase di compilazione.  
  
     Inoltre è possibile utilizzare tali ambienti **SQLTables** e **SQLColumns** per creare elenchi da cui il programmatore è stato possibile effettuare selezioni. Questi ambienti possono essere utilizzate anche **SQLPrimaryKeys** e **SQLForeignKeys** per determinare automaticamente e mostrare le relazioni tra le tabelle selezionate e usare **SQLStatistics** per determinare ed evidenziare i campi indicizzati per consentire al programmatore di creare query efficienti.  
  
-   **Costruzione di cursori.** Impossibile utilizzare un'applicazione, driver o middleware che offre un motore con cursori scorrevoli **SQLSpecialColumns** per determinare quale colonna o colonne di identificano in modo univoco una riga. Il programma è stato possibile creare un *keyset* contenente i valori di queste colonne per ogni riga che è stata recuperata. Quando si scorre verso l'applicazione torna alla riga, utilizzerebbe quindi questi valori per recuperare i dati più recenti per la riga. Per altre informazioni sui cursori scorrevoli e keyset, vedere [cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md).
