---
title: Novità dell'integrazione con CLR |&#39;Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
ms.assetid: 871fcccd-b726-4b13-9f95-d02b4b39d8ab
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 45e4f0578d06eeafc545bea2b6374a37b8ef7cbc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874063"
---
# <a name="what39s-new-in-clr-integration"></a>Novità dell'integrazione con CLR&#39;
  Di seguito sono elencate le nuove caratteristiche dell'integrazione con CLR in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]:  
  
-   Nella versione 4 di CLR tramite gli oggetti di database CLR non vengono più rilevate le eccezioni relative allo stato danneggiato. Queste eccezioni vengono ora rilevate nel livello host dell'integrazione con CLR. Queste eccezioni possono comunque essere rilevate dai componenti del database CLR impostando un attributo Code ([\<legacyCorruptedStateExceptionsPolicy> elemento](https://go.microsoft.com/fwlink/?LinkId=204954)). Questa operazione non è tuttavia consigliata, in quanto i risultati non sono affidabili nel caso di un'eccezione relativa allo stato danneggiato.  
  
-   A causa dei rigidi requisiti di sicurezza di [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], nei componenti di database CLR continua a essere utilizzato il modello di sicurezza dall'accesso di codice definito nella versione 2.0 di CLR.  
  
-   Nella versione 4 di CLR un errore di formato in un valore `System.TimeSpan` comporta la generazione di un evento `System.FormatExceptions`. Nelle versioni di CLR precedenti alla 4, un errore di formato in `System.TimeSpan` viene ignorato. Le applicazioni di database basate sul comportamento delle versioni di CLR precedenti alla 4 devono essere eseguite con un livello di compatibilità del database (`ALTER DATABASE Compatibility Level`) minore o uguale a 100. Per ulteriori informazioni, vedere [<TimeSpan_LegacyFormatMode> elemento](https://go.microsoft.com/fwlink/?LinkId=205109).  
  
-   La versione 4 di CLR supporta Unicode 5.1. Le operazioni di ordinamento che includono accenti e simboli verranno migliorate. Possono verificarsi problemi di compatibilità se l'applicazione è basata sul comportamento di ordinamento delle versioni precedenti. Per abilitare l'ordinamento delle versioni precedenti, il livello di compatibilità del database (`ALTER DATABASE Compatibility Level`) deve essere impostato su 100 o su un valore inferiore. Per offrire il supporto necessario, tramite [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] viene installato il file sort00001000.dll nella directory di .NET Framework 4 (C:\Windows\Microsoft.NET\Framework\v4.0.30319). Per ulteriori informazioni, vedere [ \<CompatSortNLSVersion> element](https://go.microsoft.com/fwlink/?LinkId=205110).  
  
-   Le colonne seguenti sono state aggiunte a [sys. dm_clr_appdomains](/sql/relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql): `total_processor_time_ms`, `total_allocated_memory_kb`e `survived_memory_kb`.  
  
  
