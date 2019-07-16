---
title: Connessione diretta ai driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44b9de304069849e965fc335e130ae57d9ec8bad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083158"
---
# <a name="connecting-directly-to-drivers"></a>Connessione diretta ai driver
Come illustrato [scelta di un'origine dati o Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md), più indietro in questa sezione, alcune applicazioni non si desidera utilizzare un'origine dati affatto. Si vuole invece di connettersi direttamente a un driver. **SQLDriverConnect** fornisce un modo per l'applicazione per connettersi direttamente a un driver senza specificare un'origine dati. Concettualmente, viene creata un'origine dei dati temporanei in fase di esecuzione.  
  
 Per connettersi direttamente a un driver, l'applicazione specifica la **DRIVER** parola chiave nella stringa di connessione anziché la **DSN** (parola chiave). Il valore della **DRIVER** parola chiave che rappresenta la descrizione del driver restituito da **SQLDrivers**. Si supponga, ad esempio, un driver con la descrizione del Driver Paradox e richiede il nome di una directory contenente i file di dati. Per connettersi a questo driver, l'applicazione potrebbe usare una delle stringhe di connessione seguenti:  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 Con la prima stringa, il driver non necessario eventuali informazioni aggiuntive. Con la seconda stringa, il driver necessario per la richiesta per il nome della directory contenente i file di dati.
