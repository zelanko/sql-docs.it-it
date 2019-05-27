---
title: Formati di dati numerici | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- integer data types [Integration Services]
- numeric data formats for fast parse
- locale-sensitive parsing [Integration Services]
- fast parse [Integration Services]
ms.assetid: fa3975ce-9d21-408a-857d-f85e30af27b0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d0f48c3a6cebe079d93601f53698afafb350587e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66057392"
---
# <a name="numeric-data-formats"></a>Formati di dati numerici
  L'analisi veloce offre un set di routine semplici e veloci per l'analisi dei dati, indipendenti dalle impostazioni locali. Supporta solo un limitato set di formati per i tipi di dati integer.  
  
## <a name="integer-data-types"></a>Tipi di dati integer  
 In [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sono disponibili i tipi di dati integer DT_I1, DT_UI1, DT_I2, DT_UI2, DT_I4, DT_UI4, DT_I8 e DT_UI8. Per altre informazioni, vedere [Tipi di dati di Integration Services](data-flow/integration-services-data-types.md).  
  
 L'analisi veloce supporta i formati seguenti per i tipi di dati integer:  
  
-   Zero o più spazi o tabulazioni iniziali e finali o arresti di tabulazioni. Ad esempio, il valore "  123  " è valido. Un valore costituito da soli spazi viene considerato equivalente a zero.  
  
-   Un segno più (+), un segno meno (-) o nessun segno iniziale. Ad esempio, i valori +123, -123 e 123 sono validi.  
  
-   Una o più cifre arabe (0-9). Ad esempio, il valore 345 è valido. Gli altri tipi di cifre non sono supportati.  
  
 Di seguito sono elencati alcuni formati di dati non supportati:  
  
-   Caratteri speciali. Il carattere di valuta $, ad esempio, non è supportato e il valore $20 non può essere analizzato.  
  
-   Caratteri spazio quali i caratteri di avanzamento riga, ritorno a capo e spazio unificatore. Il valore " 123", ad esempio, non può essere analizzato.  
  
-   Rappresentazioni esadecimali di valori interi. Il valore 2EE, ad esempio, non può essere analizzato.  
  
-   Valori interi in notazione scientifica. Il valore 1E+10, ad esempio, non può essere analizzato.  
  
 Di seguito sono elencati alcuni formati di output per i dati integer:  
  
-   Un segno meno (-) per i numeri negativi e nessun segno per i numeri positivi.  
  
-   Nessun carattere spazio.  
  
-   Una o più cifre arabe (0-9).  
  
  
