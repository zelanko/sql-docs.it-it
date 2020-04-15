---
title: Cronologia dei driver di database del desktop Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304982"
---
# <a name="history-of-the-desktop-database-drivers"></a>Cronologia dei driver di database desktop
Nella tabella seguente viene illustrata la cronologia delle versioni dei driver di Database desktop.  
  
|Versione|Data di rilascio|Descrizione|  
|-------------|------------------|-----------------|  
|1.0|Agosto 1993|Utilizzato l'elaboratore di query SIMBA prodotto da PageAhead Software. SIMBA ha ricevuto chiamate ODBC e istruzioni SQL, le ha elaborate in chiamate ISAM installabili di Microsoft Jet e quindi ha chiamato il livello di invio ISAM di Microsoft Jet per caricare e chiamare il driver ISAM installabile appropriato.|  
|2.0|Dicembre 1994|Utilizzato con ODBC 2.0, che ha ampliato in modo significativo la funzionalità ODBC. La modifica principale nella versione 2.0 è stata che il modulo di gestione di database Microsoft Jet ha sostituito il processore di query SIMBA. Con il modulo di gestione di database Microsoft Jet, i driver di database desktop si sono integrati molto più strettamente con i driver ISAM installabili di Microsoft Jet e la tecnologia Microsoft Access. Miglioramenti significativi sono stati:<br /><br /> - Supporto nativo per cursori scorrevoli.- Native support for scrollable cursors.<br />- Supporto nativo per outer join, join aggiornabili ed eterogenei e transazioni.- Native support for outer joins, updatable and eterogeneous joins, and transactions.<br />- versioni a 32 bit dei driver per Microsoft Windows NT.|  
|3.0|Ottobre 1995|Fornito il supporto per Windows 95 e Windows NT Workstation o NT Server 3.51. Solo i driver a 32 bit sono stati inclusi in questa versione; i driver a 16 bit per Windows versione 3.1 sono stati rimossi.|  
|3,5|Ottobre 1996|Questi driver erano abilitati per DBCS (Double-Byte Character Set), erano più adatti per l'uso con le applicazioni Internet rispetto alle versioni precedenti e supportavano l'uso dei nomi delle origini dati file (DSN). Il driver Microsoft Access è stato rilasciato in una versione RISC per l'utilizzo su piattaforme Alpha per sistemi operativi Windows 95/98 e Windows NT 3.51 e versioni successive.|  
|4.0|Fine 1998|Fornisce supporto per il formato Unicode di Microsoft Jet Engine insieme alla compatibilità con il formato ANSI delle versioni precedenti.|  
  
> [!NOTE]  
>  I driver della versione 3.5 sono stati progettati per funzionare con ODBC2. *x*. Sebbene funzionino anche con ODBC 3.0, non supportano tutte le funzionalità di ODBC 3.0. Per ulteriori informazioni sul funzionamento di questi driver con ODBC 3.0, vedere [Compatibilità con](../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)le versioni precedenti e conformità agli standard .
