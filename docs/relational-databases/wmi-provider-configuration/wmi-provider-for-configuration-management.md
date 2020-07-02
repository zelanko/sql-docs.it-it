---
title: Concetti relativi al provider WMI per Gestione configurazione
description: Informazioni sul provider WMI, utilizzato con Gestione configurazione SQL Server in Microsoft Management Console e Microsoft SQL Server Configuration Manager.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- WMI Provider for Configuration Management
- SQL Server WMI Provider
- configuration management [WMI]
- WMI Provider for Configuration Management, about WMI Provider for Configuration Management
ms.assetid: 7e41db24-b915-4eb8-a1d6-e6948ee915b7
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 7789f78cb4f79a537aef3ae5071498fae4cc439f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775648"
---
# <a name="wmi-provider-for-configuration-management"></a>provider WMI per Gestione configurazione
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]
  Il provider WMI è un livello pubblicato utilizzato con lo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] snap-in Configuration Manager per [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC) e il [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Viene fornita una modalità unificata per l'interfaccia con le chiamate API che gestiscono le operazioni del Registro di sistema richieste da Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e vengono offerte funzioni avanzate di controllo e manipolazione sui servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionati.  
  
 Il provider WMI di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un file DLL e un file MOF, compilati automaticamente dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Il provider WMI di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene un set di classi di oggetti utilizzati per controllare i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] attraverso i metodi seguenti:  
  
-   Un linguaggio di scripting come VBScript, [!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)] o Perl, in cui è possibile incorporare Windows Query Language (WQL).  
  
-   L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> in un programma di codice gestito SMO.  
  
-   Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o MMC con lo snap-in del provider WMI di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="using-a-script-language"></a>Utilizzo di un linguaggio di scripting  
 I vantaggi dell'utilizzo di un linguaggio di scripting sono i seguenti:  
  
-   Non è necessario un ambiente di sviluppo.  
  
-   I file che supportano il linguaggio di scripting sono ampiamente disponibili.  
  
 Lo script può funzionare anche con altri provider WMI oltre a quello di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un amministratore di dominio può utilizzare uno script per configurare i servizi, le impostazioni di rete e le impostazioni dell'alias in più computer di una rete.  
  
 In questa sezione viene illustrato in modo più approfondito l'accesso al provider WMI per Gestione configurazione dagli script.  
  
## <a name="using-the-smo-managedcomputer-object"></a>Utilizzo dell'oggetto ManagedComputer SMO   
 L'oggetto <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> è un oggetto SMO gestito che consente di accedere al provider WMI per Gestione configurazione. Tramite un programma SMO, l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> può essere utilizzato per visualizzare e modificare i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], le impostazioni di rete e le impostazioni dell'alias. Per ulteriori informazioni, vedere [gestione dei servizi e delle impostazioni di rete tramite il provider WMI](../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md).  
  
## <a name="using-the-microsoft-management-console-or-sql-server-configuration-manager"></a>Utilizzo di Microsoft Management Console o Gestione configurazione SQL Server  
 Microsoft Management Console (MMC) offre un'interfaccia per la gestione dei servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a differenza di un linguaggio di scripting o di un programma di codice gestito. Lo snap-in MMC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere utilizzato per arrestare e avviare servizi e modificare gli account di servizio.  
  
 Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere utilizzato anche per gestire protocolli client e server, alias del server e servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sul provider WMI per la gestione della configurazione](../../relational-databases/wmi-provider-configuration/understanding-the-wmi-provider-for-configuration-management.md)   
 [Utilizzo del provider WMI per la gestione della configurazione](../../relational-databases/wmi-provider-configuration/working-with-the-wmi-provider-for-configuration-management.md)   
 [Uso di WQL e di linguaggi di scripting con il provider WMI per la gestione della configurazione](../../relational-databases/wmi-provider-configuration/using-wql-and-scripting-languages-with-the-wmi-provider.md)  
  
  
