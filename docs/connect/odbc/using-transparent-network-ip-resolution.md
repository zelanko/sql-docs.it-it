---
title: Uso della risoluzione IP di rete trasparente | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68008481"
---
# <a name="using-transparent-network-ip-resolution"></a>Uso della risoluzione dell'IP di rete trasparente
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

Transparentnetworkipresolution (è una revisione della funzionalità MultiSubnetFailover esistente, disponibile in Microsoft ODBC driver 13,1 for SQL Server, che influiscono sulla sequenza di connessione del driver nel caso in cui il primo IP risolto del nome host non rispondere e sono presenti più indirizzi IP associati al nome host. Interagisce con MultiSubnetFailover per fornire le tre sequenze di connessione seguenti:

* 0: viene eseguito un tentativo IP, seguito da tutti gli indirizzi IP in parallelo
* 1: tutti gli indirizzi IP vengono tentati in parallelo
* 2: tutti gli indirizzi IP vengono tentati uno dopo l'altro

|TransparentNetworkIPResolution|MultiSubnetFailover|Comportamento|
|:-:|:-:|:-:|
|(predefinito)|(predefinito)|0|
|(predefinito)|Abilitata|1|
|(predefinito)|Disabilitata|0|
|Abilitata|(predefinito)|0|
|Abilitata|Abilitata|1|
|Abilitata|Disabilitata|0|
|Disabilitata|(predefinito)|2|
|Disabilitata|Abilitata|1|
|Disabilitata|Disabilitata|2|

La `TransparentNetworkIPResolution` stringa di connessione e la parola chiave DSN controllano questa impostazione a livello di stringa di connessione. Il valore predefinito è Enabled.

Parola chiave|Valori|Default
-|-|-
`TransparentNetworkIPResolution`|`Yes`, `No`|`Yes`

L' `SQL_COPT_SS_TNIR` attributo pre-Connection consente a un'applicazione di controllare questa impostazione a livello di codice:

Attributo di connessione|   Dimensioni/Tipo|  Default| valore| Descrizione
-|-|-|-|-
`SQL_COPT_SS_TNIR` (1249)| `SQL_IS_INTEGER` o `SQL_IS_UINTEGER`| `SQL_IS_ON`(1), `SQL_IS_OFF`(0)|`SQL_IS_ON`|Abilita o Disabilita TNIR.

<a name="for-more-information-about-multisubnetfailover-see-odbc-driver-on-linux-and-macos---high-availability-and-disaster-recoveryconnectodbclinux-macodbc-driver-on-linux-support-for-high-availability-disaster-recoverymd"></a>Per altre informazioni su MultiSubnetFailover, vedere [driver ODBC in Linux e MacOS-disponibilità elevata e ripristino di emergenza](../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md)
--------------------------------------------------
## <a name="see-also"></a>Vedere anche  
* [Microsoft ODBC Driver for SQL Server in Windows](../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)
* [Clustering su più subnet di SQL Server (SQL Server)](https://msdn.microsoft.com/library/ff878716.aspx#RelatedContent)
