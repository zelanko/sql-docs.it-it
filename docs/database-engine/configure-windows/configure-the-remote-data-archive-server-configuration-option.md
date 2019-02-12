---
title: Configurare l'opzione di configurazione del server remote data archive | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b5817b5a-f39a-4faf-b11e-a47b54fd9f32
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0aa939d36a97f6d4b7f0587bd06470189b91ff3b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017993"
---
# <a name="configure-the-remote-data-archive-server-configuration-option"></a>Configurare l'opzione di configurazione del server remote data archive
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Usare l'opzione **remote data archive** per specificare se i database e le tabelle nel server possono essere abilitati per l'estensione. Per ulteriori informazioni, vedere [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md).  
  
 L'opzione **remote data archive** può avere i valori seguenti.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|0|I database e le tabelle nel server non possono essere abilitati per l'estensione.|  
|1|I database e le tabelle nel server possono essere abilitati per l'estensione.|  
  
 L'esecuzione di **sp_configure** per impostare il valore dell'opzione **remote data archive** richiede autorizzazioni sysadmin o serveradmin.  
  
## <a name="example"></a>Esempio  
 L'esempio seguente visualizza per prima l'impostazione corrente dell'opzione **remote data archive** . L'esempio abilita quindi l'opzione **remote data archive** impostandone il valore su 1.  
  
```  
EXEC sp_configure 'remote data archive';  
GO  
EXEC sp_configure 'remote data archive' , '1';  
GO  
RECONFIGURE;  
GO  
```  
  
 Per disabilitare l'opzione, impostare il valore su 0.  
  
## <a name="see-also"></a>Vedere anche  
 [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md)   
 [Estensione database](../../sql-server/stretch-database/stretch-database.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
