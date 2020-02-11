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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083158"
---
# <a name="connecting-directly-to-drivers"></a>Connessione diretta ai driver
Come è stato illustrato nella [scelta di un'origine dati o di un driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md), più indietro in questa sezione alcune applicazioni non desiderano utilizzare un'origine dati. Ma vogliono connettersi direttamente a un driver. **SQLDriverConnect** consente all'applicazione di connettersi direttamente a un driver senza specificare un'origine dati. Concettualmente, un'origine dati temporanea viene creata in fase di esecuzione.  
  
 Per connettersi direttamente a un driver, l'applicazione specifica la parola chiave **driver** nella stringa di connessione invece della parola chiave **DSN** . Il valore della parola chiave **driver** è la descrizione del driver restituita da **SQLDrivers.** Si supponga, ad esempio, che un driver disponga della descrizione del driver Paradox e che richieda il nome di una directory contenente i file di dati. Per connettersi a questo driver, l'applicazione può usare una delle seguenti stringhe di connessione:  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 Con la prima stringa, il driver non necessita di informazioni aggiuntive. Con la seconda stringa, il driver deve richiedere il nome della directory contenente i file di dati.
