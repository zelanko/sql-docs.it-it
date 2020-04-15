---
title: Usi dei dati del catalogo Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 429d42d4a82d0f9f34e33eb4f5f3293100505da9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306812"
---
# <a name="uses-of-catalog-data"></a>Utilizzi dei dati del catalogo
Le applicazioni utilizzano i dati del catalogo in diversi modi. Ecco alcuni usi comuni:  
  
-   **Costruzione di istruzioni SQL in fase di esecuzione.** Le applicazioni verticali, ad esempio un'applicazione per la voce degli ordini, contengono istruzioni SQL hardcoded. Le tabelle e le colonne utilizzate dall'applicazione vengono fissate in anticipo, così come le istruzioni che accedono a queste tabelle. Ad esempio, un'applicazione di immissione ordini contiene in genere una singola istruzione **INSERT** con parametri per l'aggiunta di nuovi ordini al sistema.  
  
     Le applicazioni generiche, ad esempio un programma per fogli di calcolo che utilizza ODBC per recuperare i dati, spesso costruiscono istruzioni SQL in fase di esecuzione in base all'input dell'utente. Un'applicazione di questo tipo potrebbe richiedere all'utente di digitare i nomi delle tabelle e delle colonne da utilizzare. Tuttavia, sarebbe più facile per l'utente se l'applicazione visualizzato elenchi di tabelle e colonne da cui l'utente potrebbe effettuare selezioni. Per compilare questi elenchi, l'applicazione chiamerebbe le funzioni di catalogo **SQLTables** e **SQLColumns.**  
  
-   **Creazione di istruzioni SQL durante lo sviluppo.** Gli ambienti di sviluppo delle applicazioni consentono in genere al programmatore di creare query di database durante lo sviluppo di un programma. Le query vengono quindi hardcoded nell'applicazione in fase di compilazione.  
  
     Tali ambienti potrebbero anche utilizzare **SQLTables** e **SQLColumns** per creare elenchi da cui il programmatore potrebbe effettuare selezioni. Questi ambienti possono anche utilizzare **SQLPrimaryKeys** e **SQLForeignKeys** per determinare e mostrare automaticamente le relazioni tra le tabelle selezionate e utilizzare **SQLStatistics** per determinare ed evidenziare i campi indicizzati in modo che il programmatore possa creare query efficienti.  
  
-   **Costruzione di cursori.** Un'applicazione, un driver o un middleware che fornisce un motore di cursore scorrevole potrebbe utilizzare **SQLSpecialColumns** per determinare quale colonna o colonne identifica noviziamente una riga. Il programma potrebbe compilare un *keyset* contenente i valori di queste colonne per ogni riga che è stata recuperata. Quando l'applicazione scorre indietro fino alla riga, quindi utilizzerà questi valori per recuperare i dati più recenti per la riga. Per ulteriori informazioni sui cursori e i keyset scorrevoli, consultate [Cursori scorrevoli.](../../../odbc/reference/develop-app/scrollable-cursors.md)
