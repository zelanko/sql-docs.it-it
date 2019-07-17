---
title: Descrittori | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC]
- descriptors [ODBC], about descriptors
- descriptor handles [ODBC]
- handles [ODBC], descriptor
ms.assetid: ef2cbb93-cd00-40f8-b1d2-5f5723a991aa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f2138a5f8417fc9156c916719e96d707b9a29de9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040016"
---
# <a name="descriptors"></a>Descrittori
Handle descrittore fa riferimento a una struttura di dati che contiene informazioni relative a colonne o parametri dinamici.  
  
 Funzioni ODBC che operano sui dati di parametro e colonna in modo implicito impostare e recupero i campi di descrizione. Ad esempio, quando **SQLBindCol** viene chiamato per associare i dati della colonna, imposta i campi di descrizione che descrivono completamente l'associazione. Quando **SQLColAttribute** viene chiamato per descrivere i dati della colonna, vengono restituiti i dati archiviati nei campi del descrittore.  
  
 Un'applicazione che chiama funzioni ODBC necessario non preoccuparsi dei descrittori. Nessuna operazione di database richiede che l'applicazione l'accesso diretto alla descrittori. Tuttavia, per alcune applicazioni, ottenere l'accesso diretto ai descrittori semplifica molte operazioni. Ad esempio, indirizzare l'accesso ai descrittori fornisce un modo per riassociare i dati della colonna, che possono essere più efficienti rispetto alla chiamata **SQLBindCol** nuovamente.  
  
> [!NOTE]  
>  La rappresentazione fisica del descrittore non è definita. Le applicazioni accedono diretto a un descrittore solo modificando i campi chiamando le funzioni ODBC con l'handle descrittore.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di descrittori](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [Campi del descrittore](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [Allocazione e liberazione di descrittori](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [Recupero e configurazione dei campi del descrittore](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
