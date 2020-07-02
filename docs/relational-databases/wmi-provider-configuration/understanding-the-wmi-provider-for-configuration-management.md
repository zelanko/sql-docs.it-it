---
title: provider WMI per Gestione configurazione
description: Informazioni sul modo in cui il provider WMI per la gestione della configurazione utilizza WMI per gestire i servizi, gli alias del server e le impostazioni di rete client/server in SQL Server.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management, operations supported
ms.assetid: 92323972-7943-4208-bbf4-050774fb6027
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d517a674840f9115a80600838f5c401c5d586a9a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729989"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>Informazioni sul provider WMI per la gestione della configurazione
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]fornisce il provider WMI per la gestione della configurazione. Consente di utilizzare WMI (Strumentazione gestione Windows) per gestire i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e impostazioni di rete server e alias del server. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]i servizi, le impostazioni di rete e gli alias sono rappresentati da oggetti WMI nello spazio dei nomi root\Microsoft\SqlServer\ComputerManagement*nn* del computer. Una volta stabilita una connessione con il provider WMI nel computer specificato, è possibile eseguire query su servizi, impostazioni di rete e alias utilizzando WQL o un linguaggio di scripting.  
  
 Il provider WMI è un provider di istanze Fornisce istanze delle [classi WMI](../../relational-databases/wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md) e supporta le operazioni asincrone seguenti.  
  
 Recupero di istanze  
 Recupero di un'istanza di un tipo di classe specifica.  
  
 Enumerazione  
 Enumerazione di tutte le istanze di un tipo di classe.  
  
 Modifica  
 Modifica di una determinata istanza di un tipo di classe.  
  
 Le classi includono metodi che consentono la modifica delle relative proprietà.  
  
 Eliminazione  
 Rimozione di una determinata istanza di un tipo di classe.  
  
 Elaborazione di query  
 Enumerazione di istanze di un tipo di classe basata su un filtro.  
  
 Per esempi di applicazioni di gestione che utilizzano il provider WMI per la gestione della configurazione, vedere [utilizzo di WQL e di linguaggi di scripting con il provider WMI per la gestione della configurazione](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md).  
  
 Per ulteriori informazioni sulla programmazione di applicazioni di gestione utilizzando il provider WMI, vedere la documentazione di WMI in [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework SDK.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo del provider WMI per la gestione della configurazione](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [Uso di WQL e di linguaggi di scripting con il provider WMI per la gestione della configurazione](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
