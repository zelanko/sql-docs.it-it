---
description: Regole di gestione di diagnostica
title: Regole di gestione diagnostica | Microsoft Docs
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
ms.openlocfilehash: 3112f6db31a4369ec880e31a7bb8be6e15071bed
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424663"
---
# <a name="diagnostic-handling-rules"></a>Regole di gestione di diagnostica
Le regole seguenti regolano la gestione della diagnostica in **SQLGetDiagRec** e **SQLGetDiagField**.  
  
 Per tutti i componenti ODBC:  
  
-   Non devono sostituire, modificare o mascherare gli errori o gli avvisi ricevuti da un altro componente ODBC.  
  
-   Potrebbe aggiungere un record di stato aggiuntivo quando ricevono un messaggio di diagnostica da un altro componente ODBC. Il record aggiunto deve aggiungere un valore di informazioni reali al messaggio originale.  
  
 Per il componente ODBC che interfaccia direttamente un'origine dati:  
  
-   Deve precedere l'identificatore del fornitore, l'identificatore del componente e l'identificatore dell'origine dati al messaggio di diagnostica ricevuto dall'origine dati.  
  
-   Deve mantenere il codice di errore nativo dell'origine dati.  
  
-   Deve conservare il messaggio di diagnostica dell'origine dati.  
  
 Per qualsiasi componente ODBC che genera un errore o un avviso indipendente dall'origine dati:  
  
-   Per l'errore o l'avviso è necessario specificare il SQLSTATE corretto.  
  
-   Deve generare il testo del messaggio di diagnostica.  
  
-   È necessario anteporre al messaggio di diagnostica l'identificatore del fornitore e l'identificatore del componente.  
  
-   Deve restituire un codice di errore nativo, se disponibile e significativo.  
  
 Per il componente ODBC che si interfaccia con Gestione driver:  
  
-   Deve inizializzare gli argomenti di output di **SQLGetDiagRec** e **SQLGetDiagField**.  
  
-   Deve formattare e restituire le informazioni di diagnostica come argomenti di output di **SQLGetDiagRec** e **SQLGetDiagField** quando viene chiamata la funzione.  
  
 Per un componente ODBC diverso da Gestione driver:  
  
-   È necessario impostare il SQLSTATE in base all'errore nativo. Per i driver basati su file e i driver basati su DBMS che non utilizzano un gateway, è necessario che il driver imposti il valore SQLSTATE. Per i driver basati su DBMS che usano un gateway, il driver o un gateway che supporta ODBC può impostare il valore SQLSTATE.
