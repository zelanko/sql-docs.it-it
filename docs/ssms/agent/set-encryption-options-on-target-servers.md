---
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
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d03b187b3af7778d4c574c41661aa4cb9ed39838
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253239"
---
# <a name="set-encryption-options-on-target-servers"></a>Impostazione delle opzioni di crittografia nei server di destinazione
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Se non è possibile utilizzare un certificato per le comunicazioni crittografate SSL (Secure Sockets Layer) tra server master e alcuni o tutti i server di destinazione e si desidera crittografare il canale di comunicazione, configurare i server di destinazione per l'utilizzo del livello di sicurezza necessario.  
  
Per configurare il livello di sicurezza appropriato necessario per uno specifico canale di comunicazione tra server master e server di destinazione, impostare la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sottochiave del Registro di sistema di Agent **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\** \<*nome_istanza*> **\SQLServerAgent\MsxEncryptChannelOptions(REG_DWORD)** nel server di destinazione su uno dei valori seguenti. Il valore di \<*nome_istanza*> è **MSSQL.** _n_. Ad esempio, **MSSQL.1** o **MSSQL.3**.  
  
|valore|Descrizione|  
|---------|---------------|  
|**0**|Disabilita la crittografia tra il server di destinazione e il server master. Selezionare questa opzione solo quando il canale tra il server di destinazione e il server master è protetto in altro modo.|  
|**1**|Attiva solo la crittografia tra il server di destinazione e il server master senza la convalida del certificato.|  
|**2**|Attiva la crittografia SSL completa, inclusa la convalida del certificato, tra il server di destinazione e il server master. Questa è l'impostazione predefinita. A meno che non ci siano motivi specifici per scegliere un valore diverso, è consigliabile non modificarla.|  
  
Se si specifica **1** o **2** , è necessario attivare la crittografia SSL sia nel server master sia nei server di destinazione. Se si specifica **2** , è necessario che nel server master sia presente un certificato firmato correttamente.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
[Procedura: Abilitazione di connessioni crittografate al Motore di database (Gestione configurazione SQL Server)](https://msdn.microsoft.com/e1e55519-97ec-4404-81ef-881da3b42006)  
  
