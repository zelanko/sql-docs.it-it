---
title: Utilizzi dei dati del catalogo | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306812"
---
# <a name="uses-of-catalog-data"></a>Utilizzi dei dati del catalogo
Le applicazioni utilizzano i dati del catalogo in diversi modi. Di seguito sono riportati alcuni usi comuni:  
  
-   **Creazione di istruzioni SQL in fase di esecuzione.** Le applicazioni verticali, ad esempio un'applicazione Order entry, contengono istruzioni SQL hardcoded. Le tabelle e le colonne utilizzate dall'applicazione sono fisse in anticipo, così come le istruzioni che accedono a queste tabelle. Un'applicazione Order entry, ad esempio, contiene in genere un'unica istruzione **Insert** con parametri per l'aggiunta di nuovi ordini al sistema.  
  
     Le applicazioni generiche, ad esempio un programma di foglio di calcolo che usa ODBC per recuperare i dati, spesso costruiscono istruzioni SQL in fase di esecuzione in base all'input dell'utente. Tale applicazione potrebbe richiedere all'utente di digitare i nomi delle tabelle e delle colonne da utilizzare. Tuttavia, sarà più semplice per l'utente se l'applicazione Visualizza gli elenchi di tabelle e colonne da cui l'utente può effettuare le selezioni. Per compilare questi elenchi, l'applicazione chiama le funzioni del catalogo **SQLTables** e **SQLColumns** .  
  
-   **Creazione di istruzioni SQL durante lo sviluppo.** Gli ambienti di sviluppo di applicazioni consentono in genere al programmatore di creare query di database durante lo sviluppo di un programma. Le query vengono quindi hardcoded nell'applicazione in fase di compilazione.  
  
     Tali ambienti possono inoltre utilizzare **SQLTables** e **SQLColumns** per creare elenchi da cui il programmatore può effettuare selezioni. Questi ambienti possono inoltre utilizzare **SQLPrimaryKeys** e **SQLForeignKeys** per determinare e visualizzare automaticamente le relazioni tra le tabelle selezionate e utilizzare **SQLStatistics** per determinare ed evidenziare i campi indicizzati in modo che il programmatore possa creare query efficienti.  
  
-   **Creazione di cursori.** Un'applicazione, un driver o un middleware che fornisce un motore di cursore scorrevole può utilizzare **SQLSpecialColumns** per determinare la colonna o le colonne che identificano in modo univoco una riga. Il programma può compilare un *Keyset* contenente i valori di queste colonne per ogni riga recuperata. Quando l'applicazione esegue lo scorrimento alla riga, utilizzerà questi valori per recuperare i dati più recenti per la riga. Per ulteriori informazioni sui cursori scorrevoli e sui set di tasti, vedere [cursori scorrevoli](../../../odbc/reference/develop-app/scrollable-cursors.md).
