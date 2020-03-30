---
title: Uso della risoluzione dell'IP di rete trasparente | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d255208f-d486-4ad3-8080-61c6e0261825
author: MightyPen
ms.author: genemi
ms.openlocfilehash: df5b0233168c52b4f79cdc6d2d03cd7b72e16046
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "68008481"
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

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recovery"></a>Per altre informazioni su MultiSubnetFailover, vedere [Driver ODBC in Linux e macOS - Disponibilità elevata e ripristino di emergenza](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).
--------------------------------------------------
## <a name="see-also"></a>Vedere anche  
* [Microsoft ODBC Driver for SQL Server in Windows](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [Clustering su più subnet di SQL Server (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
