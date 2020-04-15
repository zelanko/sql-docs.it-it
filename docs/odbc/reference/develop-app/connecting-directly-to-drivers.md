---
title: Connessione diretta ai driver Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d6aacb5d3df985949e04cdd47a9fe460cddbde6a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299081"
---
# <a name="connecting-directly-to-drivers"></a>Connessione diretta ai driver
Come descritto in [Scelta di un'origine dati o](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)di un driver , più indietro in questa sezione, alcune applicazioni non desiderano utilizzare affatto un'origine dati. Al contrario, si desidera connettersi direttamente a un driver. **SQLDriverConnect** fornisce un modo per l'applicazione di connettersi direttamente a un driver senza specificare un'origine dati. Concettualmente, un'origine dati temporanea viene creata in fase di esecuzione.  
  
 Per connettersi direttamente a un driver, l'applicazione specifica la parola chiave **DRIVER** nella stringa di connessione anziché la parola chiave **DSN.** Il valore della parola chiave **DRIVER** è la descrizione del driver restituita da **SQLDrivers**. Si supponga, ad esempio, che un driver abbia la descrizione Paradox Driver e richieda il nome di una directory contenente i file di dati. Per connettersi a questo driver, l'applicazione potrebbe utilizzare una delle seguenti stringhe di connessione:  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 Con la prima stringa, il driver non avrebbe bisogno di informazioni aggiuntive. Con la seconda stringa, il driver dovrebbe richiedere il nome della directory contenente i file di dati.
