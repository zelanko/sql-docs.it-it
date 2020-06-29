---
title: Analisi veloce | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- fast parse [Integration Services]
ms.assetid: 6688707d-3c5b-404e-aa2f-e13092ac8d95
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 343b8b8b74338512dbf29b3d2efd436df1ffa8ae
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425698"
---
# <a name="fast-parse"></a>Analisi veloce
  L'analisi veloce offre un set di routine semplici e veloci per l'analisi dei dati. Tali routine sono indipendenti dalle impostazioni locali e supportano solo un subset dei formati di data, ora e integer.  
  
## <a name="requirements-and-limitations"></a>Requisiti e limitazioni  
 I pacchetti che implementano l'analisi veloce hanno una capacità limitata di interpretare le informazioni di data, ora e numeriche nei formati che dipendono dalle impostazioni locali e nei formati ISO 8601 di base ed estesi maggiormente utilizzati, ma offrono prestazioni superiori. L'analisi veloce supporta ad esempio solo le rappresentazioni dei formati di data utilizzate più di frequente, quali AAAAMMGG e AAAA-MM-GG, non esegue analisi specifiche delle impostazioni locali, non riconosce i caratteri speciali nei dati di valuta e non è in grado di convertire la rappresentazione esadecimale o scientifica dei valori interi.  
  
 L'analisi veloce è disponibile solo quando si utilizza l'origine file flat o la trasformazione Conversione dati. Poiché l'aumento di prestazioni può essere significativo, se possibile in tali componenti del flusso di dati è consigliabile utilizzare l'analisi veloce.  
  
 Se il flusso di dati nel pacchetto richiede analisi che dipendono dalle impostazioni locali, è consigliabile utilizzare l'analisi standard anziché l'analisi veloce. L'analisi veloce non riconosce ad esempio dati dipendenti dalle impostazioni locali che includono simboli quali il separatore decimale, formati di data diversi dai formati anno-mese-giorno e simboli di valuta.  
  
 Le rappresentazioni troncate che includono in modo implicito una o più parti della data, ad esempio il secolo, l'anno o il mese, non vengono riconosciute dall'analisi veloce. L'analisi veloce non riconosce né il formato "**-AAMM**", che specifica l'anno e il mese in un secolo implicito, né il formato "**--MM**", che specifica un mese in un anno implicito. Vengono tuttavia riconosciute alcune rappresentazioni con precisione ridotta, ad esempio il formato "hhmm;" che indica solo le ore e i minuti, e il formato "**AAAA**", che indica solo l'anno.  
  
 L'analisi veloce è specificata a livello di colonna. Nell'origine file flat e nella trasformazione Conversione dati è possibile specificare l'analisi veloce nelle colonne di output. Input e output possono includere sia colonne dipendenti dalle impostazioni locali che colonne indipendenti dalle impostazioni locali.  
  
 Per ulteriori informazioni sui formati di data supportati dall'analisi veloce, vedere [Numeric Data Formats](../../2014/integration-services/numeric-data-formats.md) e [Date and Time Formats](../../2014/integration-services/date-and-time-formats.md).  
  
## <a name="related-tasks"></a>Attività correlate  
 [Impostazione dell'analisi veloce](../../2014/integration-services/set-fast-parse.md)  
  
  
