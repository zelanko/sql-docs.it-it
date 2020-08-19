---
description: Associazione di colonne
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
ms.openlocfilehash: 8f3f02ec6487b34a6ca2c973c3115c3940ca8fa9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429433"
---
# <a name="binding-columns"></a>Associazione di colonne
I dati recuperati dall'origine dati vengono restituiti all'applicazione in variabili che l'applicazione ha allocato a questo scopo. Prima di eseguire questa operazione, l'applicazione deve associare o *associare*tali variabili alle colonne del set di risultati. concettualmente, questo processo equivale a associare le variabili dell'applicazione ai parametri dell'istruzione. Quando l'applicazione associa una variabile a una colonna del set di risultati, descrive l'indirizzo variabile, il tipo di dati e così via al driver. Il driver archivia queste informazioni nella struttura che gestisce per tale istruzione e utilizza le informazioni per restituire il valore dalla colonna quando viene recuperata la riga.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione di colonne di set di risultati](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [Uso di SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
