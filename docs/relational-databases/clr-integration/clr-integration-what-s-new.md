---
title: Novità dell'integrazione con CLR |&#39;Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: clr
ms.topic: conceptual
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
ms.openlocfilehash: 8d37d476808f80cf132037542d17cb3de61eeccc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68134867"
---
# <a name="clr-integration---what39s-new"></a>Integrazione con CLR-novità di&#39;
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Di seguito sono elencate le nuove caratteristiche dell'integrazione con CLR in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]:  
  
-   Nella versione 4 di CLR tramite gli oggetti di database CLR non vengono più rilevate le eccezioni relative allo stato danneggiato. Queste eccezioni vengono ora rilevate nel livello host dell'integrazione con CLR. Queste eccezioni possono comunque essere rilevate dai componenti del database CLR impostando un attributo Code ([\<legacyCorruptedStateExceptionsPolicy> elemento](https://go.microsoft.com/fwlink/?LinkId=204954)). Questa operazione non è tuttavia consigliata, in quanto i risultati non sono affidabili nel caso di un'eccezione relativa allo stato danneggiato.  
  
-   A causa dei rigidi requisiti di sicurezza di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], nei componenti di database CLR continua a essere utilizzato il modello di sicurezza dall'accesso di codice definito nella versione 2.0 di CLR.  
  
-   In CLR versione 4, un errore di formato in un valore **System. TimeSpan** genererà un oggetto **System. le eccezioni FormatException**. Prima della versione 4 di CLR, un errore di formato in un valore **System. TimeSpan** è stato ignorato. Le applicazioni di database basate sul comportamento precedente alla versione 4 di CLR devono essere eseguite con un livello di compatibilità del database (**livello di compatibilità ALTER database**) di 100 o inferiore. Per ulteriori informazioni, vedere [<TimeSpan_LegacyFormatMode> elemento](https://go.microsoft.com/fwlink/?LinkId=205109).  
  
-   La versione 4 di CLR supporta Unicode 5.1. Le operazioni di ordinamento che includono accenti e simboli verranno migliorate. Possono verificarsi problemi di compatibilità se l'applicazione è basata sul comportamento di ordinamento delle versioni precedenti. Per abilitare l'ordinamento legacy, il livello di compatibilità del database (**livello di compatibilità ALTER database**) deve essere impostato su 100 o su un valore inferiore. Per offrire il supporto necessario, tramite [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] viene installato il file sort00001000.dll nella directory di .NET Framework 4 (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Per ulteriori informazioni, vedere [ \<CompatSortNLSVersion> element](https://go.microsoft.com/fwlink/?LinkId=205110).  
  
-   Le colonne seguenti sono state aggiunte a [sys. dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md): **total_processor_time_ms**, **total_allocated_memory_kb**e **survived_memory_kb**.  
  
  
