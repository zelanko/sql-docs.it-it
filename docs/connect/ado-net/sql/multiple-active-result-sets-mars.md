---
title: MARS (Multiple Active Result Sets)
description: Viene descritto come avere più di un oggetto SqlDataReader aperto su una connessione quando ogni istanza di SqlDataReader viene avviata da un comando separato.
ms.date: 08/15/2019
ms.assetid: c90ef863-bac7-44cf-adc1-f05c36fcf57d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 4475e4b8a71b4abcf4e1c2324a49e03a8bb64fbb
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896676"
---
# <a name="multiple-active-result-sets-mars"></a>MARS (Multiple Active Result Sets)

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

MARS (Multiple Active Result Set) è una funzionalità che consente l'esecuzione di più batch in un'unica connessione. Nelle versioni precedenti era possibile eseguire un solo batch alla volta su una singola connessione. L'esecuzione di più batch con MARS non implica l'esecuzione simultanea di operazioni.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
[Abilitazione di MARS (Multiple Active Result Set)](enable-multiple-active-result-sets.md)  
Viene descritto come usare MARS con SQL Server.  
  
[Manipolazione dei dati](manipulate-data.md)  
Fornisce esempi di codifica di applicazioni MARS.  
  
## <a name="related-sections"></a>Sezioni correlate  
[Operazioni asincrone](asynchronous-operations.md)  
Fornisce informazioni dettagliate sull'uso delle nuove funzionalità asincrone in .NET.  
  
## <a name="next-steps"></a>Passaggi successivi
- [SQL Server e ADO.NET](index.md)
