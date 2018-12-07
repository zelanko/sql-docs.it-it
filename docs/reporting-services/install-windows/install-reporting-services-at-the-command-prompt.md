---
title: Installare Reporting Services 2016 al prompt dei comandi - SSRS | Microsoft Docs
ms.date: 01/09/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- command line
ms.assetid: 048169b3-512c-41e4-895a-0416eff41268
author: markingmyname
ms.author: maghan
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 05519dae5377d1e58f6b8e47b91d898c0b67dc2f
ms.sourcegitcommit: c7febcaff4a51a899bc775a86e764ac60aab22eb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2018
ms.locfileid: "52710872"
---
# <a name="install-reporting-services-2016-at-the-command-prompt"></a>Installare Reporting Services 2016 al prompt dei comandi

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supporta l'installazione da riga di comando dal programma di installazione di SQL Server. In questo argomento sono contenuti numerosi esempi di installazioni da riga di comando specifiche di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per una descrizione completa delle opzioni della riga di comando disponibili per tutti i componenti di SQL Server, vedere [Installare SQL Server dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md). In questo argomento non vengono descritte le opzioni della riga di comando per il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per i prodotti SharePoint. Per informazioni sull'installazione dalla riga di comando del componente aggiuntivo, vedere [Installare il componente aggiuntivo utilizzando il file di installazione rssharepoint.msi](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md#bkmk_install_rssharepoint).

##  <a name="bkmk_native_mode"></a> Reporting Services in modalità nativa

### <a name="rsinstallmode-native-mode"></a>RSINSTALLMODE (modalità nativa)
 L'impostazione di input primaria per l'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è **/RSINSTALLMODE** . All'impostazione sono associate due opzioni: **DefaultNativeMode** e **FilesOnlyMode**  
  
 Se l'installazione include il motore di database di SQL Server, l'opzione predefinita di RSINSTALLMODE è DefaultNativeMode. In caso contrario, l'opzione predefinita di RSINSTALLMODE è FilesOnlyMode. Se si sceglie DefaultNativeMode, ma nell'installazione non è incluso il motore di database di SQL Server, RSINSTALLMODE viene impostato automaticamente su FilesOnlyMode. Per altre informazioni sulle impostazioni di input, vedere [Installazione di SQL Server dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).

### <a name="examples-of-native-mode-installation"></a>Esempi di installazione in modalità nativa

 Nell'esempio seguente viene installato quanto segue e vengono configurati gli account:  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa.  
  
-   [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
-   SQL Server Agent, necessario per le funzionalità di sottoscrizione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
```  
Setup.exe /q /IACCEPTSQLSERVERLICENSETERMS /ACTION="install" /ERRORREPORTING=1 /UPDATEENABLED="False" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Adv_SSMS,RS" /RSINSTALLMODE="DefaultNativeMode" /SQLSVCACCOUNT="[DOMAIN\ACCOUNT]" /SQLSVCPASSWORD="[PASSWORD]" /AGTSVCACCOUNT="[DOMAIN\ACCOUNT]" /AGTSVCPASSWORD="[PASSWORD]" /SQLSYSADMINACCOUNTS="[DOMAIN\ACCOUNT]"  
```  
  
##  <a name="bkmk_sharepoint_mode"></a> Reporting Services in modalità SharePoint  
  
### <a name="rsshpinstallmode-sharepoint-mode"></a>RSSHPINSTALLMODE (modalità SharePoint)  
 L'impostazione di input per installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint è **/RSSHPINSTALLMODE**. L'impostazione di input dispone di un'opzione, SharePointFilesOnlyMode che consente di installare tutti i file necessari per la modalità SharePoint. Dopo l'installazione sarà necessario procedere alla configurazione. I passaggi aggiuntivi della configurazione vengono completati utilizzando Amministrazione centrale SharePoint. Per altre informazioni, vedere [Installare il primo server di report in modalità SharePoint](install-the-first-report-server-in-sharepoint-mode.md).  
  
### <a name="examples-of-sharepoint-mode-installation"></a>Esempi di installazione in modalità SharePoint  
 Nell'esempio seguente vengono installati SQL Server, il servizio del motore di database e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint, nonché il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per SharePoint (RS_SHPWFE).  
  
```  
setup /q /ACTION=install /FEATURES=SQL, RS_SHP, RS_SHPWFE,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE"  
```  
  
 Nell'esempio seguente viene installata solo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint.  
  
```  
Setup.exe /q /ACTION="Install" /IACCEPTSQLSERVERLICENSETERMS /FEATURES="RS_SHP" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SECURITYMODE="SQL" /SAPWD="[PASSWORD]" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Name]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="[Account Name]" /UPDATEENABLED="False"  
  
```  
  
### <a name="examples-of-sharepoint-mode-upgrade"></a>Esempi di aggiornamento della modalità SharePoint  
 Nell'esempio seguente viene aggiornata la modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . **RSUPGRADEPASSWORD** è la password dell'account del servizio del server di report esistente. RSUPGRADEPASSWORD è un campo obbligatorio in un scenario di aggiornamento a meno che l'account del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sia un account predefinito.  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[PID value]" /FTSVCACCOUNT="[DOMAIN\ACCOUNT]" /FTSVCPASSWORD="[PASSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSUPGRADEPASSWORD="[PASSWORD]"  
```  
  
 L'esempio seguente può essere utilizzato per aggiornare un'installazione della modalità SharePoint basata sull'architettura del servizio di SharePoint condivisa. Nell'esempio viene utilizzata l'opzione ALLOWUPGRADEFORSSRSSHAREPOINTMODE, L'opzione non è necessaria per aggiornare le versioni precedenti che non sono basate sull'architettura di servizi condivisi:  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[Your PID Value]" /FTSVCACCOUNT="[ACCOUNT Name]" /FTSVCPASSWORD="[PASSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /ALLOWUPGRADEFORSSRSSHAREPOINTMODE="True"  
```

## <a name="next-steps"></a>Passaggi successivi

[Installare SQL Server dal prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
[Parametri SysPrep](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#SysPrep)   
[Installare PowerPivot dal prompt dei comandi](https://msdn.microsoft.com/7f1f2b28-c9f5-49ad-934b-02f2fa6b9328)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
