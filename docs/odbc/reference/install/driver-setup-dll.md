---
title: DLL di installazione driver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df91638f91091940e00e7a6a19d0fd6cb700f85f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094158"
---
# <a name="driver-setup-dll"></a>DLL di installazione driver
> [!NOTE]  
>  A partire da Windows XP e Windows Server 2003, ODBC è incluso nel sistema operativo Windows. Solo nelle versioni precedenti di Windows è necessario installare ODBC in modo esplicito.  
  
 Il programma di installazione di driver DLL contiene il **ConfigDriver** e **ConfigDSN** funzioni. **ConfigDriver** esegue le attività di installazione specifici del driver, quali l'immissione di informazioni specifiche del driver nel Registro di sistema. **ConfigDSN** mantiene le informazioni specifiche del driver sulle origini dati nel Registro di sistema. Per una descrizione completa di queste funzioni, vedere [riferimento API DLL di installazione](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 **ConfigDSN** chiama le funzioni seguenti nel programma di installazione DLL per conservare le informazioni di origine dati nel Registro di sistema:  
  
-   **SQLWriteDSNToIni**. Aggiungere un'origine dati.  
  
-   **SQLRemoveDSNFromIni**. Eliminare un'origine dati.  
  
-   **SQLWritePrivateProfileString**. Scrivere un valore specifico del driver in una sottochiave di specifica origine dati.  
  
-   **SQLGetPrivateProfileString**. Leggere un valore specifico del driver da una sottochiave di specifica origine dati.  
  
-   **SQLGetTranslator**. Richiedere all'utente un nome di funzione di conversione e l'opzione. Questa funzione chiama **ConfigTranslator** nel convertitore DLL di configurazione.  
  
 Il programma di installazione di driver DLL è scritta dallo sviluppatore del driver. Può essere parte del driver della DLL o una DLL separata.
