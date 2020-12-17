---
description: Impostazione delle opzioni di crittografia nei server di destinazione
title: Impostazione delle opzioni di crittografia nei server di destinazione
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, encryption
- target servers [SQL Server], encryption
- multiserver environments [SQL Server], setting encryption options on target servers
ms.assetid: 1a9fd539-e166-4ea8-9f21-ac400ca74dee
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 09454c54f5c0f66201df1bf1968b6dfd3aaa2705
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464352"
---
# <a name="set-encryption-options-on-target-servers"></a>Impostazione delle opzioni di crittografia nei server di destinazione
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di SQL di Azure e SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Se non è possibile usare un certificato per le comunicazioni crittografate TLS (Transport Layer Security), protocollo noto in precedenza come SSL (Secure Sockets Layer), tra server master e alcuni o tutti i server di destinazione e si vuole crittografare il canale di comunicazione, configurare i server di destinazione per l'uso del livello di sicurezza necessario.  
  
Per configurare il livello di sicurezza appropriato necessario per uno specifico canale di comunicazione tra server master e server di destinazione, impostare la sottochiave del Registro di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\** \<*instance_name*> **\SQLServerAgent\MsxEncryptChannelOptions(REG_DWORD)** nel server di destinazione su uno dei valori seguenti. Il valore di \<*instance_name*> è **MSSQL.** _n_. Ad esempio, **MSSQL.1** o **MSSQL.3**.  
  
|valore|Descrizione|  
|---------|---------------|  
|**0**|Disabilita la crittografia tra il server di destinazione e il server master. Selezionare questa opzione solo quando il canale tra il server di destinazione e il server master è protetto in altro modo.|  
|**1**|Attiva solo la crittografia tra il server di destinazione e il server master senza la convalida del certificato.|  
|**2**|Attiva la crittografia TLS completa, inclusa la convalida del certificato, tra il server di destinazione e il server master. Questa è l'impostazione predefinita. A meno che non ci siano motivi specifici per scegliere un valore diverso, è consigliabile non modificarla.|  
  
Se si specifica **1** o **2**, è necessario abilitare la crittografia TLS sia nel server master sia nei server di destinazione. Se si specifica **2** , è necessario che nel server master sia presente un certificato firmato correttamente.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
[Procedura: Abilitare connessioni crittografate al Motore di database (Gestione configurazione SQL Server)](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)  
