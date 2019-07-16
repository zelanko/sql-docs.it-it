---
title: Informazioni sul Provider WMI per Gestione configurazione | Microsoft Docs
ms.custom: ''
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
ms.openlocfilehash: de76b774083c6744e5bfad34aa0fed24952793be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139396"
---
# <a name="understanding-the-wmi-provider-for-configuration-management"></a>Informazioni sul provider WMI per la gestione della configurazione
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce il Provider WMI per Gestione configurazione. Consente di utilizzare WMI (Strumentazione gestione Windows) per gestire i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e impostazioni di rete server e alias del server. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizi, le impostazioni di rete e gli alias sono rappresentati dagli oggetti WMI nel root\Microsoft\SqlServer\ComputerManagement*nn* dello spazio dei nomi del computer. Una volta stabilita una connessione con il provider WMI nel computer specificato, è possibile eseguire query su servizi, impostazioni di rete e alias utilizzando WQL o un linguaggio di scripting.  
  
 Il provider WMI è un provider di istanze Che fornisce istanze delle [classi WMI](../../relational-databases/wmi-provider-configuration-classes/wmi-provider-for-configuration-management-classes.md) e supporta le operazioni asincrone seguenti.  
  
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
  
 Per esempi di applicazione di gestione utilizzando il Provider WMI per Gestione configurazione, vedere [utilizzo di WQL e linguaggi di Scripting con il Provider WMI per Gestione configurazione](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md).  
  
 Per altre informazioni sulla programmazione di applicazioni di gestione tramite il Provider WMI, vedere la documentazione di WMI nel [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework SDK.  
  
## <a name="see-also"></a>Vedere anche  
 [Uso del Provider WMI per Gestione configurazione](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [Uso di WQL e di linguaggi di scripting con il provider WMI per la gestione della configurazione](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
