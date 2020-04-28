---
title: Novità dell'integrazione con CLR | Microsoft Docs
description: Microsoft SQL Server host CLR è denominato integrazione con CLR. Questo articolo descrive le nuove funzionalità dell'integrazione con CLR in SQL Server 2012.
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: clr
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
ms.openlocfilehash: d27bf0d925d3a98dda488fb85aff7446434cc8ad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488090"
---
# <a name="clr-integration---what39s-new"></a>Integrazione con CLR-novità di&#39;
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Di seguito sono elencate le nuove caratteristiche dell'integrazione con CLR in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]:  
  
-   Nella versione 4 di CLR tramite gli oggetti di database CLR non vengono più rilevate le eccezioni relative allo stato danneggiato. Queste eccezioni vengono ora rilevate nel livello host dell'integrazione con CLR. Queste eccezioni possono comunque essere rilevate dai componenti del database CLR impostando un attributo Code ([\<legacyCorruptedStateExceptionsPolicy> elemento](https://go.microsoft.com/fwlink/?LinkId=204954)). Questa operazione non è tuttavia consigliata, in quanto i risultati non sono affidabili nel caso di un'eccezione relativa allo stato danneggiato.  
  
-   A causa dei rigidi requisiti di sicurezza di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], nei componenti di database CLR continua a essere utilizzato il modello di sicurezza dall'accesso di codice definito nella versione 2.0 di CLR.  
  
-   In CLR versione 4, un errore di formato in un valore **System. TimeSpan** genererà un oggetto **System. le eccezioni FormatException**. Prima della versione 4 di CLR, un errore di formato in un valore **System. TimeSpan** è stato ignorato. Le applicazioni di database basate sul comportamento precedente alla versione 4 di CLR devono essere eseguite con un livello di compatibilità del database (**livello di compatibilità ALTER database**) di 100 o inferiore. Per ulteriori informazioni, vedere [<TimeSpan_LegacyFormatMode> elemento](https://go.microsoft.com/fwlink/?LinkId=205109).  
  
-   La versione 4 di CLR supporta Unicode 5.1. Le operazioni di ordinamento che includono accenti e simboli verranno migliorate. Possono verificarsi problemi di compatibilità se l'applicazione è basata sul comportamento di ordinamento delle versioni precedenti. Per abilitare l'ordinamento legacy, il livello di compatibilità del database (**livello di compatibilità ALTER database**) deve essere impostato su 100 o su un valore inferiore. Per offrire il supporto necessario, tramite [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] viene installato il file sort00001000.dll nella directory di .NET Framework 4 (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Per ulteriori informazioni, vedere [ \<CompatSortNLSVersion> element](https://go.microsoft.com/fwlink/?LinkId=205110).  
  
-   Le colonne seguenti sono state aggiunte a [sys. dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **total_processor_time_ms**, **total_allocated_memory_kb**e **survived_memory_kb**.  
  
  
