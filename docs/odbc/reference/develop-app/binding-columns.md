---
title: Colonne di associazione . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fca4cfb1455c91ca57f7b1769266e2040d6a3511
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301822"
---
# <a name="binding-columns"></a>Associazione di colonne
I dati recuperati dall'origine dati vengono restituiti all'applicazione nelle variabili allocate dall'applicazione a questo scopo. Prima di eseguire questa operazione, l'applicazione deve associare, o *associare*, queste variabili alle colonne del set di risultati; concettualmente, questo processo equivale all'associazione di variabili di applicazione ai parametri dell'istruzione. Quando l'applicazione associa una variabile a una colonna del set di risultati, descrive tale variabile - indirizzo, tipo di dati e così via - al driver. Il driver archivia queste informazioni nella struttura che gestisce per tale istruzione e utilizza le informazioni per restituire il valore dalla colonna quando viene recuperata la riga.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di colonne di set di risultati](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Uso di SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
