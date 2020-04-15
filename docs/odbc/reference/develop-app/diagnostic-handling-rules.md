---
title: Regole di gestione diagnostica - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], diagnostic handling rules
- SQLGetDiagRec function [ODBC], diagnostic handling rules
- diagnostic information [ODBC], SqlGetDiagRec
ms.assetid: 74387c3a-d6b3-4c35-b209-b9612602b20a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9f7f9d19a5a369e9da0efbc0d62f8e556b0597c1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305842"
---
# <a name="diagnostic-handling-rules"></a>Regole di gestione di diagnostica
Le regole seguenti regolano la gestione diagnostica in **SQLGetDiagRec** e **SQLGetDiagField**.  
  
 Per tutti i componenti ODBC:  
  
-   Non devono sostituire, modificare o mascherare errori o avvisi ricevuti da un altro componente ODBC.  
  
-   Può aggiungere un record di stato aggiuntivo quando ricevono un messaggio di diagnostica da un altro componente ODBC. Il record aggiunto deve aggiungere informazioni reali al messaggio originale.  
  
 Per il componente ODBC che interfaccia direttamente un'origine dati:  
  
-   Deve anteporre l'identificatore del fornitore, l'identificatore del componente e l'identificatore dell'origine dati al messaggio di diagnostica ricevuto dall'origine dati.  
  
-   È necessario mantenere il codice di errore nativo dell'origine dati.  
  
-   È necessario mantenere il messaggio di diagnostica dell'origine dati.  
  
 Per qualsiasi componente ODBC che genera un errore o un avviso indipendentemente dall'origine dati:  
  
-   Deve fornire il valore SQLSTATE corretto per l'errore o l'avviso.  
  
-   Deve generare il testo del messaggio di diagnostica.  
  
-   Deve anteporre l'identificatore del fornitore e l'identificatore del componente al messaggio di diagnostica.  
  
-   Deve restituire un codice di errore nativo, se disponibile e significativo.  
  
 Per il componente ODBC che si interfaccia con Gestione Driver:  
  
-   È necessario inizializzare gli argomenti di output di **SQLGetDiagRec** e **SQLGetDiagField**.  
  
-   È necessario formattare e restituire le informazioni di diagnostica come argomenti di output di **SQLGetDiagRec** e **SQLGetDiagField** quando viene chiamata tale funzione.  
  
 Per un componente ODBC diverso da Gestione Driver:  
  
-   È necessario impostare SQLSTATE in base all'errore nativo. Per i driver basati su file e i driver basati su DBMS che non utilizzano un gateway, il driver deve impostare SQLSTATE. Per i driver basati su DBMS che utilizzano un gateway, il driver o un gateway che supporta ODBC può impostare SQLSTATE.
