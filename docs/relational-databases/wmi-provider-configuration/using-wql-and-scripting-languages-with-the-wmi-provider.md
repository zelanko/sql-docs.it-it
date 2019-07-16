---
title: Utilizzo di WQL e linguaggi di Scripting con il Provider WMI | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- scripts [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Configuration Management, WQL
- WMI Provider for Configuration Management, scripts
ms.assetid: c1e64905-3c2b-4974-88f4-abf17cf7e289
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bf93c737a19f890df33c978f3feccfc6bd826105
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139732"
---
# <a name="using-wql-and-scripting-languages-with-the-wmi-provider"></a>Uso di WQL e di linguaggi di scripting con il provider WMI
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Le applicazioni di gestione accedono a servizi e impostazioni di rete di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando il provider di Strumentazione gestione Windows (WMI, Windows Management Instrumentation) per gli oggetti di gestione della configurazione in due modi diversi:  
  
-   Utilizzando un editor WQL o un strumento di query, ad esempio WBEMTest.exe, per eseguire una query sul set di oggetti con WQL.  
  
-   Utilizzando un linguaggio di scripting, ad esempio VBScript.  
  
 In alternativa, i servizi e le impostazioni di rete di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere gestiti a livello di programmazione utilizzando oggetti gestiti WMI in SMO. Per ulteriori informazioni sulla programmazione WMI gestiti gli oggetti, vedere [la gestione dei servizi e le impostazioni di rete dal Provider WMI utilizzando](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md).  
  
 È possibile accedere al provider WMI per la gestione della configurazione utilizzando Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console. Per altre informazioni sull'accesso al provider WMI da un'interfaccia utente, vedere [gestione dei servizi di argomenti relativi alle procedure &#40;Gestione configurazione SQL Server&#41;](https://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6).  
  
## <a name="see-also"></a>Vedere anche  
 [Accedere al Provider WMI per Gestione configurazione usando WQL](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-wql.md)   
 [Modificare le proprietà avanzate del servizio SQL Server usando VBScript](../../relational-databases/wmi-provider-configuration/access-wmi-provider-for-configuration-management-using-vbscript.md)  
  
  
