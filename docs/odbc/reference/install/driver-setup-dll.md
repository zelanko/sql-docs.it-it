---
title: DLL di installazione del driver Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0a2878591c92fe0b2070a295d9dc622c245c17e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306422"
---
# <a name="driver-setup-dll"></a>DLL di installazione driver
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. È consigliabile installare ODBC in modo esplicito solo nelle versioni precedenti di Windows.  
  
 La DLL di installazione del driver contiene le funzioni **ConfigDriver** e **ConfigDSN.** **ConfigDriver** esegue attività di installazione specifiche del driver, ad esempio l'immissione di informazioni specifiche del driver nel Registro di sistema. **ConfigDSN** gestisce informazioni specifiche del driver sulle origini dati nel Registro di sistema. Per una descrizione completa di queste funzioni, vedere Guida di [riferimento all'API DELLA DLL](../../../odbc/reference/syntax/setup-dll-api-reference.md)di installazione .  
  
 **ConfigDSN** chiama le seguenti funzioni nella DLL del programma di installazione per mantenere le informazioni sull'origine dati nel Registro di sistema:  
  
-   **SQLWriteDSNToIni**. Aggiungere un'origine dati.  
  
-   **SQLRemoveDSNFromIni**. Eliminare un'origine dati.  
  
-   **SQLWritePrivateProfileString**. Scrivere un valore specifico del driver in una sottochiave di specifica dell'origine dati.  
  
-   **SQLGetPrivateProfileString**. Leggere un valore specifico del driver da una sottochiave di specifica dell'origine dati.  
  
-   **SQLGetTranslator**. Richiedere all'utente un nome e un'opzione del traduttore. Questa funzione chiama **ConfigTranslator** nella DLL di installazione del convertitore.  
  
 La DLL di installazione del driver viene scritta dallo sviluppatore del driver. Può essere parte della DLL del driver o di una DLL separata.
