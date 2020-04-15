---
title: Proprietà Descriptors . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca8299daae744fb9398ed6ffc99c838ce8edff48
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305902"
---
# <a name="descriptors"></a>Descrittori
Un handle descrittore fa riferimento a una struttura di dati che contiene informazioni su colonne o parametri dinamici.  
  
 Le funzioni ODBC che operano sui dati di colonna e parametri impostano e recuperano in modo implicito i campi descrittore. Ad esempio, quando **SQLBindCol** viene chiamato per associare i dati della colonna, imposta i campi descrittore che descrivono completamente l'associazione. Quando **SQLColAttribute** viene chiamato per descrivere i dati della colonna, restituisce i dati archiviati nei campi del descrittore.  
  
 Un'applicazione che chiama le funzioni ODBC non deve preoccuparsi di descrittori. Nessuna operazione di database richiede che l'applicazione ottenga l'accesso diretto ai descrittori. Tuttavia, per alcune applicazioni, ottenere l'accesso diretto ai descrittori semplifica molte operazioni. Ad esempio, l'accesso diretto ai descrittori fornisce un modo per riassociare i dati delle colonne, che può essere più efficiente rispetto alla chiamata **di SQLBindCol** nuovamente.  
  
> [!NOTE]  
>  La rappresentazione fisica del descrittore non è definita. Le applicazioni ottengono l'accesso diretto a un descrittore solo modificandone i campi chiamando le funzioni ODBC con l'handle del descrittore.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di descrittori](../../../odbc/reference/develop-app/types-of-descriptors.md)  
  
-   [Campi del descrittore](../../../odbc/reference/develop-app/descriptor-fields.md)  
  
-   [Allocazione e rilascio di descrittori](../../../odbc/reference/develop-app/allocating-and-freeing-descriptors.md)  
  
-   [Recupero e configurazione dei campi del descrittore](../../../odbc/reference/develop-app/getting-and-setting-descriptor-fields.md)
