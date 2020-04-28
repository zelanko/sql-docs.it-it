---
title: Cronologia dei driver del database desktop | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89434b397c07fdee751ca4272b65ac2eada94cf3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304982"
---
# <a name="history-of-the-desktop-database-drivers"></a>Cronologia dei driver di database desktop
La tabella seguente illustra la cronologia delle versioni dei driver di database desktop.  
  
|Versione|Data di rilascio|Descrizione|  
|-------------|------------------|-----------------|  
|1.0|1993 agosto|Utilizzato il processore di query SIMBA prodotto da PageAhead Software. SIMBA ha ricevuto chiamate ODBC e istruzioni SQL, le ha elaborate in chiamate ISAM installabili da Microsoft Jet e quindi ha chiamato il livello di invio ISAM di Microsoft Jet per caricare e chiamare il driver ISAM installabile appropriato.|  
|2.0|1994 dicembre|Utilizzato con ODBC 2,0, che ha espanso significativamente la funzionalità ODBC. Il cambiamento principale della versione 2,0 è che il motore di database di Microsoft Jet ha sostituito SIMBA query processor. Con il motore di database di Microsoft Jet, i driver di database desktop si integrano molto più strettamente con i driver ISAM installabili di Microsoft Jet e la tecnologia Microsoft Access. Sono stati apportati miglioramenti significativi:<br /><br /> -Supporto nativo per i cursori scorrevoli.<br />-Supporto nativo per outer join, join aggiornabili ed eterogenei e transazioni.<br />-versioni a 32 bit dei driver per Microsoft Windows NT.|  
|3.0|1995 ottobre|Fornito supporto per la workstation Windows 95 e Windows NT o NT Server 3,51. In questa versione sono stati inclusi solo driver a 32 bit. i driver a 16 bit per Windows versione 3,1 sono stati rimossi.|  
|3,5|1996 ottobre|Questi driver erano abilitati per il set di caratteri DBCS (Double-byte character set), erano più adatti per l'uso con applicazioni Internet rispetto alle versioni precedenti e contenevano l'uso di DSN (Data Source Name). Il driver Microsoft Access è stato rilasciato in una versione RISC per l'uso su piattaforme Alpha per Windows 95/98 e Windows NT 3,51 e sistemi operativi successivi.|  
|4.0|Tardi 1998|Fornisce supporto per il formato Unicode del motore Jet Microsoft insieme alla compatibilità per il formato ANSI delle versioni precedenti.|  
  
> [!NOTE]  
>  I driver della versione 3.5 sono stati progettati per funzionare con ODBC2. *x*. Sebbene funzionino anche con ODBC 3,0, non supportano tutte le funzionalità ODBC 3,0. Per ulteriori informazioni sul funzionamento di questi driver con ODBC 3,0, vedere [compatibilità con le versioni precedenti e conformità agli standard](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).
