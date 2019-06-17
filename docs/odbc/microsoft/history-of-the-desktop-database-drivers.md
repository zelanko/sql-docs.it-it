---
title: Cronologia dei driver di Database Desktop | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], history
- ODBC desktop database drivers [ODBC], history
- desktop database drivers [ODBC], history
ms.assetid: b4a2aff8-bde7-4bd5-8580-bc50f27311c8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a77aeafff6b27b2de0b947700cef1c7251cd7548
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127261"
---
# <a name="history-of-the-desktop-database-drivers"></a>Cronologia dei driver di database desktop
Nella tabella seguente mostra la cronologia delle versioni di driver di Database Desktop.  
  
|Version|Data di rilascio|Descrizione|  
|-------------|------------------|-----------------|  
|1,0|1993 agosto|Hanno usato il processore di query SIMBA prodotto da PageAhead Software. Amministratore o SIMBA ricevuto chiamate ODBC e istruzioni SQL, li elaborati in chiamate ISAM installabile Microsoft Jet e quindi chiamata il livello di invio Microsoft Jet ISAM per caricare e chiamare il driver ISAM installabile appropriato.|  
|2.0|1994 dicembre|Usata con ODBC 2.0, che esteso in modo significativo la funzionalità ODBC. La modifica principale nella versione 2.0 è che il motore di database Microsoft Jet sostituiti in query processor SIMBA. Con il motore di database Microsoft Jet, i driver di Database Desktop molto più strettamente integrato con la tecnologia di Microsoft Access e i driver ISAM installabili Microsoft Jet. Miglioramenti significativi sono stati:<br /><br /> -Supporto nativo per i cursori scorrevoli.<br />-Supporto nativo per gli outer join, join aggiornabile ed eterogenei e transazioni.<br />-le versioni a 32 bit dei driver per Microsoft Windows NT.|  
|3.0|Ottobre 1995|Fornisce supporto per Windows 95 e Windows NT Workstation o Server nt3.51. Solo driver a 32 bit sono stati inclusi in questa versione. il driver a 16 bit per Windows versione 3.1 sono state rimosse.|  
|3.5|Ottobre 1996|Questi driver sono stati double byte character set (DBCS)-abilitata, sono stati più adatti per l'uso con applicazioni Internet rispetto alle versioni precedenti e inserire l'uso di nomi delle origini dati di File (DSN). Il driver Microsoft Access è stato rilasciato in una versione RISC per l'utilizzo in piattaforme alfa per Windows 95 o 98 e Windows NT 3.51 e sistemi operativi successivi.|  
|4.0|Ritardo 1998|Fornisce il supporto per il formato Unicode motore Jet di Microsoft e compatibilità per le versioni precedenti il formato ANSI.|  
  
> [!NOTE]  
>  I driver version3.5 sono stati progettati per funzionare con ODBC2. *x*. Anche se funzionano anche con ODBC 3.0, non supportano tutte le funzionalità di ODBC 3.0. Per altre informazioni sul funzionano di questi driver con ODBC 3.0, vedere [garantire la compatibilità e conformità agli standard](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).
