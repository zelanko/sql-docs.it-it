---
title: Opzione di configurazione del server Ole Automation Procedures | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Ole Automation Procedures option
ms.assetid: e8982e05-4984-4406-9760-285e8c028ddf
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f00c238dfb32089261c51936b3937b0657c58b08
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62782029"
---
# <a name="ole-automation-procedures-server-configuration-option"></a>Opzione di configurazione del server Ole Automation Procedures
  Utilizzare l'opzione `Ole Automation Procedures` per specificare se è possibile creare un'istanza degli oggetti di automazione OLE all'interno di batch [!INCLUDE[tsql](../../includes/tsql-md.md)]. Questa opzione può essere configurata usando anche la gestione basata su criteri o la stored procedure **sp_configure** . Per ulteriori informazioni, vedere [Surface Area Configuration](../../relational-databases/security/surface-area-configuration.md).  
  
 L'opzione `Ole Automation Procedures` può essere impostata su uno dei valori seguenti.  
  
 0  
 L'opzione Ole Automation Procedures è disabilitata. Impostazione predefinita per le nuove istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 1  
 L'opzione Ole Automation Procedures è abilitata.  
  
 Quando l'opzione Ole Automation Procedures è abilitata, l'ambiente di esecuzione condiviso OLE viene avviato mediante una chiamata a **sp_OACreate** .  
  
 Il valore corrente dell' `Ole Automation Procedures` opzione può essere visualizzato e modificato utilizzando il **sp_configure** stored procedure di sistema.  
  
## <a name="examples"></a>Esempi  
 Nell'esempio seguente viene illustrata la procedura per la visualizzazione dell'impostazione corrente dell'opzione Ole Automation Procedures.  
  
```  
EXEC sp_configure 'Ole Automation Procedures';  
GO  
```  
  
 Nell'esempio seguente viene illustrata la procedura per l'abilitazione dell'opzione Ole Automation Procedures.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Ole Automation Procedures', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Configurazione superficie di attacco](../../relational-databases/security/surface-area-configuration.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
  
