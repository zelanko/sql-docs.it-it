---
title: Associazione di colonne | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 88e3593276851b6ab38fde0472a70be31b7cbf34
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199459"
---
# <a name="binding-columns"></a>Associazione di colonne
Dati recuperati dall'origine dati viene restituiti all'applicazione in variabili che l'applicazione è allocato a questo scopo. Prima di questa operazione può essere eseguita, è necessario associare l'applicazione, oppure *associare*, impostare queste variabili per le colonne del risultato; concettualmente, questo processo è lo stesso come variabili di applicazione di associazione di parametri dell'istruzione. Quando l'applicazione associa una variabile a una colonna del set di risultati, descrive la variabile indirizzo, tipo di dati e così via - il driver. Il driver di queste informazioni vengono memorizzate nella struttura mantenuta per l'istruzione e utilizza le informazioni per restituire il valore della colonna quando viene recuperata la riga.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di colonne di set di risultati](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Utilizzo di SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
