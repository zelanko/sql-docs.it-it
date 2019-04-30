---
title: Command Prompt Installation of Reporting Services SharePoint Mode e modalità nativa | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 048169b3-512c-41e4-895a-0416eff41268
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ec74b3d16830eff3c78a3b74e07bc017287defb5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63064618"
---
# <a name="command-prompt-installation-of-reporting-services-sharepoint-mode-and-native-mode"></a>Installazione dal prompt dei comandi delle modalità SharePoint e nativa di Reporting Services
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] supporta l'installazione da riga di comando dal programma di installazione di SQL Server. In questo argomento sono contenuti numerosi esempi di installazioni da riga di comando specifiche di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Per una descrizione completa delle opzioni della riga di comando disponibili per tutti i componenti di SQL Server, vedere [installare SQL Server 2014 dal Prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md). In questo argomento non vengono descritte le opzioni della riga di comando per il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per i prodotti SharePoint. Per informazioni sull'installazione dalla riga di comando del componente aggiuntivo, vedere [Installare il componente aggiuntivo utilizzando il file di installazione rssharepoint.msi](install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md#bkmk_install_rssharepoint).  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** Modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | Modalità nativa di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="rsinstallmode-native-mode"></a>RSINSTALLMODE (modalità nativa)  
 L'impostazione di input primaria per l'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è **/RSINSTALLMODE** . L'impostazione è disponibili due opzioni: **DefaultNativeMode** e **FilesOnlyMode**  
  
 Se l'installazione include il motore di database di SQL Server, l'opzione predefinita di RSINSTALLMODE è DefaultNativeMode. In caso contrario, l'opzione predefinita di RSINSTALLMODE è FilesOnlyMode. Se si sceglie DefaultNativeMode, ma nell'installazione non è incluso il motore di database di SQL Server, RSINSTALLMODE viene impostato automaticamente su FilesOnlyMode. Per altre informazioni sulle impostazioni di input, vedere [installare SQL Server 2014 dal Prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
## <a name="rsshpinstallmode-sharepoint-mode"></a>RSSHPINSTALLMODE (modalità SharePoint)  
 L'impostazione di input per installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint è **/RSSHPINSTALLMODE**. L'impostazione di input contiene un'opzione: SharePointFilesOnlyMode. che consente di installare tutti i file necessari per la modalità SharePoint. Dopo l'installazione sarà necessario procedere alla configurazione. I passaggi aggiuntivi della configurazione vengono completati utilizzando Amministrazione centrale SharePoint. Per altre informazioni, vedere [Installare la modalità SharePoint di Reporting Services per SharePoint 2010](../../sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md).  
  
## <a name="examples-of-sharepoint-mode-installation"></a>Esempi di installazione in modalità SharePoint  
 Nell'esempio seguente vengono installati SQL Server, il servizio del motore di database e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint, nonché il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per SharePoint (RS_SHPWFE).  
  
```  
setup /q /ACTION=install /FEATURES=SQL, RS_SHP, RS_SHPWFE,TOOLS /INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /SQLSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /AGTSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE"  
```  
  
 Nell'esempio seguente viene installata solo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint.  
  
```  
Setup.exe /q /ACTION="Install" /IACCEPTSQLSERVERLICENSETERMS /FEATURES="RS_SHP" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SECURITYMODE="SQL" /SAPWD="*****" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Name]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="[Account Name]" /UPDATEENABLED="False"  
  
```  
  
 Nell'esempio seguente vengono installate tutte le funzionalità di SQL Server, incluse le modalità nativa e Sharepoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
```  
Setup.exe /q /ACTION="Install" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Replication,SNAC,SNAC_SDK,Browser,Writer,AS,IS,MDS,Adv_SSMS,BC,BOL,Conn,SDK,DReplay_CTLR,DReplay_CLT, RS_SHP,RS_SHPWFE,DQC,BIDS,FullText, RS,DQ,SSMS" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SQLSVCACCOUNT="[Account Name]" /SQLSVCPASSWORD="********" /AGTSVCACCOUNT="[Account Nam]" /AGTSVCPASSWORD="********" /CTLRSVCACCOUNT="[Account Nam]" /CTLRSVCPASSWORD="********" /CLTSVCACCOUNT="[Account Nam]" /CLTSVCPASSWORD="********" /ASSVCACCOUNT="[Account Nam]" /ASSVCPASSWORD="********" /RSSVCACCOUNT="[Account Nam]" /RSSVCPASSWORD="********" /FTSVCACCOUNT="[Account Nam]" /FTSVCPASSWORD="********" /SECURITYMODE="SQL" /SAPWD="********" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Nam]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSSHPINSTALLMODE="SharePointFilesOnlyMode" /RSINSTALLMODE="DefaultNativeMode"  
```  
  
## <a name="examples-of-sharepoint-mode-upgrade"></a>Esempi di aggiornamento della modalità SharePoint  
 Nell'esempio seguente viene aggiornata la modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . **RSUPGRADEPASSWORD** è la password dell'account del servizio del server di report esistente. RSUPGRADEPASSWORD è un campo obbligatorio in un scenario di aggiornamento a meno che l'account del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sia un account predefinito.  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[PID value]" /FTSVCACCOUNT="[DOMAIN\ACCOUNT]" /FTSVCPASSWORD="[ACCOUNTPASSSWORD]" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSUPGRADEPASSWORD="******"  
```  
  
 L'esempio seguente può essere utilizzato per aggiornare un'installazione della modalità SharePoint basata sull'architettura del servizio di SharePoint condivisa. Nell'esempio viene utilizzata l'opzione ALLOWUPGRADEFORSSRSSHAREPOINTMODE, L'opzione non è necessaria per aggiornare le versioni precedenti che non sono basate sull'architettura di servizi condivisi:  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
```  
Setup.exe /q /ACTION="Upgrade" /INSTANCENAME="MSSQLSERVER" /PID="[Your PID Value]" /FTSVCACCOUNT="[ACCOUNT Name]" /FTSVCPASSWORD="****" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /ALLOWUPGRADEFORSSRSSHAREPOINTMODE="True"  
```  
  
## <a name="examples-of-native-mode-installation"></a>Esempi di installazione in modalità nativa  
  
```  
Setup.exe /q /ACTION="Install" /INSTANCENAME="MSSQLSERVER" /FEATURES="SQLEngine,Replication,SNAC,SNAC_SDK,Browser,Writer,AS,IS,MDS,Adv_SSMS,BC,BOL,Conn,SDK,DReplay_CTLR,DReplay_CLT,DQC,BIDS,FullText, RS,DQ,SSMS" /INSTANCEDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDDIR="C:\Program Files\Microsoft SQL Server" /INSTALLSHAREDWOWDIR="C:\Program Files (x86)\Microsoft SQL Server" /INSTALLSQLDATADIR="C:\Program Files\Microsoft SQL Server" /SQLSVCACCOUNT="[Account Name]" /SQLSVCPASSWORD="********" /AGTSVCACCOUNT="[Account Nam]" /AGTSVCPASSWORD="********" /CTLRSVCACCOUNT="[Account Nam]" /CTLRSVCPASSWORD="********" /CLTSVCACCOUNT="[Account Nam]" /CLTSVCPASSWORD="********" /ASSVCACCOUNT="[Account Nam]" /ASSVCPASSWORD="********" /RSSVCACCOUNT="[Account Nam]" /RSSVCPASSWORD="********" /FTSVCACCOUNT="[Account Nam]" /FTSVCPASSWORD="********" /SECURITYMODE="SQL" /SAPWD="********" /PID="[Your PID Value]" /SQLSYSADMINACCOUNTS="[Account Nam]" "AutoSql Admin Group" /ASSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /UPDATEENABLED="False" /IACCEPTSQLSERVERLICENSETERMS /RSINSTALLMODE="DefaultNativeMode"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Installare SQL Server 2014 dal Prompt dei comandi](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [Parametri SysPrep](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#SysPrep)   
 [Installazione di PowerPivot dal prompt dei comandi](../../sql-server/install/install-powerpivot-from-the-command-prompt.md)  
  
  
