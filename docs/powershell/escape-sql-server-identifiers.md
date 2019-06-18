---
title: Identificatori di escape di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 40897ed67ca661a763a2c654dc2c5fb223956264
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62672588"
---
# <a name="escape-sql-server-identifiers"></a>Identificatori di escape di SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

È possibile usare spesso l'apice inverso (`) come carattere di escape consentito negli identificatori delimitati di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Non è tuttavia possibile usare questo carattere per i nomi dei percorsi di PowerShell. Tuttavia, alcuni caratteri non supportano l'utilizzo dei caratteri di escape. Ad esempio, non è possibile utilizzare i caratteri di escape per i due punti (:) in Windows PowerShell. Gli identificatori che contengono tale carattere devono essere codificati. La codifica è più affidabile dell'utilizzo dei caratteri di escape in quanto è supportata da tutti i caratteri.  

> [!NOTE]
> Esistono due moduli SQL Server PowerShell: **SqlServer** e **SQLPS**. Il modulo **SQLPS** è incluso nell'installazione di SQL Server (per la compatibilità con le versioni precedenti), ma non viene più aggiornato. Il modulo PowerShell più aggiornato è il modulo **SqlServer**. Il modulo **SqlServer** contiene versioni aggiornate dei cmdlet di **SQLPS** e include anche nuovi cmdlet per il supporto delle funzionalità SQL più recenti.
> Le versioni precedenti del modulo **SqlServer** *erano* incluse con SQL Server Management Studio (SSMS), ma solo con le versioni 16.x di SQL Server Management Studio. Per usare PowerShell con SSMS 17.0 e versioni successive, è necessario installare il modulo **SqlServer** da PowerShell Gallery.
> Per installare il modulo **SqlServer**, vedere [Installare il modulo PowerShell SqlServer](download-sql-server-ps-module.md).

L'apice inverso (`) è posto generalmente sul tasto superiore sinistro della tastiera, sotto il tasto ESC.  
  
## <a name="examples"></a>Esempi  
 Di seguito è riportato un esempio di utilizzo dei caratteri di escape in un carattere #:  
  
```  
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```  
  
 Di seguito viene riportato un esempio dell'utilizzo di caratteri di escape parentesi in caso di specifica (impostazioni locali) come nome del computer:  
  
```  
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Identificatori di SQL Server in PowerShell](sql-server-identifiers-in-powershell.md)   
 [Provider PowerShell per SQL Server](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
