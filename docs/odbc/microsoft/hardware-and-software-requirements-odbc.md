---
description: Requisiti hardware e software (ODBC)
title: Requisiti hardware e software (ODBC) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0f88c8877161122c11fb65bcdb62fd4e7b684c3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412487"
---
# <a name="hardware-and-software-requirements-odbc"></a>Requisiti hardware e software (ODBC)
In questo argomento vengono elencati i requisiti per l'utilizzo dei driver di database desktop ODBC.  
  
## <a name="hardware-requirements"></a>Requisiti hardware  
 Per utilizzare i driver di database desktop ODBC, è necessario disporre di:  
  
-   Personal computer compatibile con IBM.  
  
-   Disco rigido con 6 MB di spazio libero su disco.  
  
-   Almeno 16 MB di memoria ad accesso casuale (RAM).  
  
## <a name="software-requirements"></a>Requisiti software  
 Per accedere ai dati con un driver ODBC, è necessario disporre di:  
  
-   Driver ODBC.  
  
-   Gestione driver ODBC a 32 bit, versione 3,51 o successiva (Odbc32.dll).  
  
-   Microsoft Windows 95 o versioni successive o Windows NT 4,0 o Windows 2000.  
  
-   Dimensioni dello stack di almeno 20 KB per un'applicazione che utilizza un driver ODBC Microsoft.  
  
 Quando si usa Microsoft Windows NT 4,0 o Windows 2000, il driver a 32 bit è thread-safe, ma solo tramite l'uso di un semaforo globale che controlla l'accesso al driver. L'utilizzo simultaneo del driver è molto limitato in Windows NT. Tutti gli accessi al livello ISAM Jet saranno a thread singolo per tutte le applicazioni che usano il motore Microsoft Jet.  
  
 Quando si eseguono più applicazioni a 16 bit in Windows in Windows (WOW) in Microsoft Windows NT 4,0, le applicazioni devono essere eseguite in spazi di memoria separati. (Lo stesso spazio di memoria non può essere utilizzato perché ODBC non supporta più ambienti nello stesso processo). Per eseguire un'applicazione in uno spazio di memoria separato, selezionare l'icona dell'applicazione in Program Manager, aprire il menu **file** e fare clic su **Proprietà**e quindi fare clic su **Esegui in spazio di memoria separato**.  
  
 L'uso di questi driver da parte di applicazioni a 16 bit in Windows 95 non è supportato.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>Requisiti hardware e software specifici del driver  
  
-   MicrosoftAccess e dBASEdrivers possono richiedere modifiche nei file Autoexec.bat o Config.sys.
