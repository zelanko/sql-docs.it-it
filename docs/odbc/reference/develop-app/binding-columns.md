---
title: Binding di colonne | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301822"
---
# <a name="binding-columns"></a>Associazione di colonne
I dati recuperati dall'origine dati vengono restituiti all'applicazione in variabili che l'applicazione ha allocato a questo scopo. Prima di eseguire questa operazione, l'applicazione deve associare o *associare*tali variabili alle colonne del set di risultati. concettualmente, questo processo equivale a associare le variabili dell'applicazione ai parametri dell'istruzione. Quando l'applicazione associa una variabile a una colonna del set di risultati, descrive l'indirizzo variabile, il tipo di dati e così via al driver. Il driver archivia queste informazioni nella struttura che gestisce per tale istruzione e utilizza le informazioni per restituire il valore dalla colonna quando viene recuperata la riga.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di colonne di set di risultati](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Uso di SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
