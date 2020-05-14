---
title: Uso della risoluzione dell'IP di rete trasparente
description: Informazioni sulla risoluzione dell'IP di rete trasparente nel driver ODBC per SQL Server e sul modo in cui influisce sulla funzionalità MultiSubnetFailover.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1a003b4817868516c6acfac10df80cafdf044c01
ms.sourcegitcommit: 37a3e2c022c578fc3a54ebee66d9957ff7476922
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922289"
---
# <a name="using-transparent-network-ip-resolution"></a>Uso della risoluzione dell'IP di rete trasparente
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

TransparentNetworkIPResolution è una revisione della funzionalità MultiSubnetFailover esistente, disponibile in Microsoft ODBC Driver 13.1 per SQL Server, che interessa la sequenza di connessione del driver nel caso in cui il primo indirizzo IP risolto del nome host non risponda e siano presenti più indirizzi IP associati al nome host. Interagisce con MultiSubnetFailover per rendere disponibili le tre sequenze di connessione seguenti:

* 0: Viene eseguito un tentativo con un indirizzo IP, seguito da tutti gli indirizzi IP in parallelo
* 1: Viene eseguito un tentativo con tutti gli indirizzi IP in parallelo
* 2: Viene eseguito un tentativo con tutti gli indirizzi IP uno dopo l'altro

|TransparentNetworkIPResolution|MultiSubnetFailover|Comportamento|
|:-:|:-:|:-:|
|(predefinito)|(predefinito)|0|
|(predefinito)|Attivato|1|
|(predefinito)|Disabled|0|
|Attivato|(predefinito)|0|
|Attivato|Attivato|1|
|Attivato|Disabled|0|
|Disabled|(predefinito)|2|
|Disabled|Attivato|1|
|Disabled|Disabled|2|

La stringa di connessione `TransparentNetworkIPResolution` e la parola chiave DSN controllano questa impostazione a livello di stringa di connessione. Il valore predefinito è Attivato.

Parola chiave|Valori|Predefinito
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

L'attributo pre-connessione `SQL_COPT_SS_TNIR` consente a un'applicazione di controllare questa impostazione a livello di codice:

Attributo di connessione|   Dimensioni/Tipo|  Predefinito| valore| Descrizione
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` o `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|Abilita o disabilita TNIR.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recovery"></a>Per altre informazioni su MultiSubnetFailover, vedere [Driver ODBC in Linux e macOS - Disponibilità elevata e ripristino di emergenza](linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).
--------------------------------------------------
## <a name="see-also"></a>Vedere anche  
* [Microsoft ODBC Driver for SQL Server in Windows](windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [Clustering su più subnet di SQL Server (SQL Server)](../../sql-server/failover-clusters/windows/sql-server-multi-subnet-clustering-sql-server.md)
