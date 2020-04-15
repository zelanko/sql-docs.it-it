---
title: Requisiti hardware e software (ODBC) Documenti Microsoft
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
ms.openlocfilehash: fe69775e379e9a9d661b4ddf81e577b738fcf34d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81295241"
---
# <a name="hardware-and-software-requirements-odbc"></a>Requisiti hardware e software (ODBC)
In questo argomento vengono elencati i requisiti per l'utilizzo dei driver di database desktop ODBC.  
  
## <a name="hardware-requirements"></a>Requisiti hardware  
 Per utilizzare i driver di database desktop ODBC, è necessario disporre di:  
  
-   Un personal computer compatibile con IBM.  
  
-   Un disco rigido con 6 MB di spazio libero su disco.  
  
-   Almeno 16 MB di memoria ad accesso casuale (RAM).  
  
## <a name="software-requirements"></a>Requisiti software  
 Per accedere ai dati con un driver ODBC, è necessario disporre di:To access data with an ODBC driver, you must have:  
  
-   Driver ODBC.  
  
-   Gestione driver ODBC a 32 bit, versione 3.51 o successiva (Odbc32.dll).  
  
-   Microsoft Windows 95 o versione successiva oppure Windows NT 4.0 o Windows 2000.  
  
-   Dimensioni dello stack di almeno 20 KB per un'applicazione che utilizzano un driver Microsoft ODBC.  
  
 Quando si utilizza Microsoft Windows NT 4.0 o Windows 2000, il driver a 32 bit è thread-safe, ma solo tramite l'utilizzo di un semaforo globale che controlla l'accesso al driver. L'utilizzo simultaneo del driver è molto limitato in Windows NT. Tutti gli accessi al livello Jet ISAM verranno a thread singolo per tutte le applicazioni che utilizzano il motore Microsoft Jet.  
  
 Quando si eseguono più applicazioni a 16 bit in Windows (WOW) in Microsoft Windows NT 4.0, le applicazioni devono essere eseguite in spazi di memoria separati. Lo stesso spazio di memoria non può essere utilizzato perché ODBC non supporta più ambienti nello stesso processo. Per eseguire un'applicazione in uno spazio di memoria separato, selezionare l'icona dell'applicazione in Program Manager, aprire il menu **File** e fare clic su **Proprietà**, quindi fare clic su Esegui in spazio di **memoria separato**.  
  
 L'utilizzo di questi driver da parte di applicazioni a 16 bit in Windows 95 non è supportato.  
  
## <a name="driver-specific-hardware-and-software-requirements"></a>Requisiti hardware e software specifici del driver  
  
-   I driver MicrosoftAccess e dBASE potrebbero richiedere modifiche nei file Autoexec.bat o Config.sys.
