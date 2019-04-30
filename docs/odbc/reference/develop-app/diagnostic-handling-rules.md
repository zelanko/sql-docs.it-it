---
title: Diagnostica di gestione delle regole | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f59953dee77453bb8b453a40a36d17e865a1fe5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63034928"
---
# <a name="diagnostic-handling-rules"></a>Regole di gestione di diagnostica
Le regole seguenti determinano nella gestione di diagnostica **SQLGetDiagRec** e **SQLGetDiagField**.  
  
 Per tutti i componenti ODBC:  
  
-   È necessario non sostituire, modificare o mascherare gli errori o avvisi ricevuti da un altro componente ODBC.  
  
-   Può aggiungere un record di stato aggiuntivi quando ricevono un messaggio di diagnostica da un altro componente ODBC. Il record aggiunto deve aggiungere valore informazione reale al messaggio originale.  
  
 Per ODBC componente interfacce che direttamente un'origine dati:  
  
-   Necessario anteporre il relativo identificatore fornitore e il relativo identificatore componente identificatore dell'origine dati per il messaggio ricevuto dall'origine dati di diagnostica.  
  
-   È necessario mantenere il codice di errore nativo dell'origine dati.  
  
-   È necessario mantenere messaggio di diagnostica dell'origine dati.  
  
 Per qualsiasi componente ODBC che genera un errore o avviso indipendente dell'origine dati:  
  
-   Specificare il valore SQLSTATE corretto per l'errore o avviso.  
  
-   È necessario generare il testo del messaggio di diagnostica.  
  
-   È necessario anteporre il relativo identificatore fornitore e il relativo identificatore componente per il messaggio di diagnostica.  
  
-   Deve restituire un codice di errore nativo, se uno è disponibile e significativo.  
  
 Per il componente ODBC che si interfaccia con gestione Driver:  
  
-   Argomenti di output deve essere inizializzato **SQLGetDiagRec** e **SQLGetDiagField**.  
  
-   È necessario formattare e restituire le informazioni di diagnostica come argomenti di output **SQLGetDiagRec** e **SQLGetDiagField** quando viene chiamata tale funzione.  
  
 Per un componente ODBC diverso da Gestione Driver:  
  
-   È necessario impostare il valore SQLSTATE errori nativi in base. Per i driver basati su file e i driver basati su DBMS che non usano un gateway, il driver deve impostare il valore SQLSTATE. Per i driver basati su DBMS che usano un gateway, il driver o un gateway che supporti ODBC possa impostare il valore SQLSTATE.
