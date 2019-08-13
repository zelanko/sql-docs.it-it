---
title: Limitazioni di sicurezza per SQL Server in Linux
description: Questo articolo descrive le limitazioni di SQL Server in Linux.
author: VanMSFT
ms.author: vanto
ms.date: 01/30/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 64da74cc-14bf-4636-a55e-8cc1fce2aaff
ms.openlocfilehash: 9f54197c8613293b36c1eb1ec362a8ed4db835e4
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/25/2019
ms.locfileid: "68065121"
---
# <a name="security-limitations-for-sql-server-on-linux"></a>Limitazioni di sicurezza per SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server in Linux presenta attualmente le limitazioni seguenti:

* Sono disponibili criteri password standard. MUST_CHANGE è l'unica opzione che è possibile configurare.  
* Extensible Key Management non è supportato. 
* L'uso di chiavi archiviate in Azure Key Vault non è supportato.
* SQL Server genera un certificato autofirmato personalizzato per la crittografia delle connessioni. È possibile configurare SQL Server per l'uso di un certificato fornito dall'utente per TLS. 

Per altre informazioni sulle funzionalità di sicurezza disponibili in SQL Server, vedere [il Centro di sicurezza per il motore di database di SQL Server e il database SQL di Azure](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md).

## <a name="next-steps"></a>Passaggi successivi

Per le attività di sicurezza comuni, vedere [Introduzione alle funzionalità di sicurezza di SQL Server in Linux](sql-server-linux-security-get-started.md). Per uno script di modifica del numero di porta TCP e delle directory di SQL Server e per configurare flag di traccia o regole di confronto, vedere [Configurare SQL Server in Linux con mssql-conf](sql-server-linux-configure-mssql-conf.md).
