---
title: MSSQLSERVER_33128 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 33128 (Database Engine error)
ms.assetid: 12c1096f-d120-439b-85f3-f794859503c9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 493513f21fbf61dd516160e61a7afb9e71e477fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908431"
---
# <a name="mssqlserver33128"></a>MSSQLSERVER_33128
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|33128|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|SEC_DEPRECATED_ALGO|  
|Testo del messaggio|Crittografia non riuscita. La chiave utilizza l'algoritmo deprecato '%.*ls' che non è più supportato.|  
  
## <a name="explanation"></a>Spiegazione  
Questo messaggio viene visualizzato quando si fa riferimento all'algoritmo di crittografia RC4 (o RC4_128). RC4 e RC4_128 sono algoritmi vulnerabili e deprecati. Utilizzare un algoritmo più avanzato, ad esempio uno degli algoritmi AES.  
  
Quando il livello di compatibilità del database è 90 o 100, l'operazione riesce, viene generato l'evento Deprecation e il messaggio viene visualizzato solo nel buffer circolare.  
  
Quando il livello di compatibilità del database è 110 o superiore, le operazioni di decrittografia riescono, viene generato l'evento Deprecation e il messaggio viene visualizzato solo nel buffer circolare. Le operazioni di crittografia non riusciranno, l'evento Deprecation viene generato e il messaggio viene visualizzato per l'utente e visualizzato nel buffer circolare.  
  
> [!NOTE]  
> Il buffer circolare è un componente interno non documentato pienamente e che non deve essere utilizzato dai clienti. I messaggi dal buffer circolare sono utili quando si contatta il Servizio Supporto Tecnico Clienti [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Per visualizzare il buffer circolare, eseguire una query sulla DMV sys.dm_os_ring_buffers.  
  
|State|Descrizione|  
|---------|---------------|  
|1|Una chiave RC4 viene utilizzata nella funzione encryptbykey() predefinita. La funzione predefinita restituisce NULL. Questo messaggio viene visualizzato solo nel buffer circolare.|  
|2|Una chiave RC4 viene utilizzata nella funzione decryptbykey() predefinita. Questo messaggio viene visualizzato solo nel buffer circolare.|  
|3|Una chiave RC4 deprecata viene crittografata da una chiave simmetrica. Visualizzato dagli utenti e nel buffer circolare. Impossibile modificare chiavi simmetriche RC4 deprecate a livello di compatibilità 110. Provare a utilizzare chiavi non-RC4 adatta per le operazioni di crittografia. Se necessario, impostare il livello di compatibilità con versioni precedenti su 90 o 100.|  
|4|Una chiave non RC4 deprecata viene crittografata da una chiave simmetrica RC4 deprecata. Visualizzato dagli utenti e nel buffer circolare. Modificare l'applicazione per utilizzare chiavi simmetriche non RC4 o impostare la compatibilità con versioni precedenti su 90 o 100.|  
|5|Una chiave RC4 deprecata viene decrittografata da una chiave simmetrica. Questo messaggio viene visualizzato solo nel buffer circolare.|  
|6|Una chiave non RC4 viene decrittografata da una chiave RC4 simmetrica. Questo messaggio viene visualizzato solo nel buffer circolare.|  
|7|Una chiave RC4 simmetrica viene crittografata dal certificato. Visualizzato dagli utenti e nel buffer circolare.|  
|8|Una chiave RC4 simmetrica viene decrittografata dal certificato. Questo messaggio viene visualizzato solo nel buffer circolare.|  
|9|Una chiave RC4 simmetrica viene crittografata da una chiave EKM.|  
|10|Una chiave RC4 simmetrica viene decrittografata da una chiave EKM. Questo messaggio viene visualizzato solo nel buffer circolare.|  
  
## <a name="user-action"></a>Azione dell'utente  
Utilizzare un algoritmo più avanzato, ad esempio uno degli algoritmi AES. (Consigliato)  
  
Utilizzare ALTER DATABASE SET COMPATIBILITY_LEVEL per impostare il database sul livello di compatibilità 100 (Non consigliato.)  
  
