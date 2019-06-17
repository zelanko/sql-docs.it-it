---
title: Requisiti hardware e Software (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- hardware requirements [ODBC], desktop database drivers
- software requirements [ODBC], desktop database drivers
- system requirements [ODBC], desktop database drivers
- requirements [ODBC], desktop database drivers
ms.assetid: 6df2e9cd-de10-4629-97bd-32f2782616c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b3f40621645aad2d1e52cb0a89baa8ff29b01446
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62471322"
---
# <a name="hardware-and-software-requirements-odbc"></a>Requisiti hardware e software (ODBC)
Questo argomento elenca i requisiti per l'utilizzo di driver di Database Desktop ODBC.  
  
## <a name="hardware-requirements"></a>Requisiti hardware  
 Per usare i driver di Database Desktop ODBC, è necessario disporre di:  
  
-   Un computer di personal compatibili con IBM.  
  
-   Un disco rigido con 6 MB di spazio libero su disco.  
  
-   Almeno 16 MB di memoria (RAM).  
  
## <a name="software-requirements"></a>Requisiti software  
 Per accedere ai dati con un driver ODBC, è necessario disporre di:  
  
-   Il driver ODBC.  
  
-   32 bit gestione Driver ODBC, versione 3.51 o versioni successive (Odbc32.dll).  
  
-   Microsoft Windows 95 o versione successiva, o Windows NT 4.0 o Windows 2000.  
  
-   Una dimensione dello stack di almeno 20 KB per un'applicazione tramite un driver ODBC di Microsoft.  
  
 Quando si utilizza Microsoft Windows NT 4.0 o Windows 2000, il driver a 32 bit è thread-safe, ma solo tramite l'uso di un semaforo globale che controlla l'accesso al driver. Usare contemporaneamente il driver è molto limitata in Windows NT. Tutti gli accessi al livello Jet ISAM sarà a thread singolo per tutte le applicazioni che usano la gestione di Microsoft Jet.  
  
 Quando si esegue più applicazioni a 16 bit Windows on Windows (WOW) su Microsoft Windows NT 4.0, è necessario eseguire le applicazioni in spazi di memoria separati. (Lo stesso spazio di memoria non può essere utilizzato poiché ODBC non supporta più ambienti nello stesso processo.) Per eseguire un'applicazione in uno spazio di memoria separate, selezionare l'icona dell'applicazione in Program Manager, aprire il **File** dal menu **proprietà**e quindi fare clic su **eseguiti In memoria separata Spazio**.  
  
 Non è supportato l'uso di questi driver per applicazioni a 16 bit in Windows 95.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>Requisiti specifici del driver Hardware e Software  
  
-   Il MicrosoftAccess e dBASEdrivers potrebbero richiedere modifiche nei file Autoexec.
