---
title: Proprietà di MSReportServer_ConfigurationSetting | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- MSReportServer_ConfigurationSetting Properties
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 634c5065730ea58905f89ac0454cdda53552a126
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "65569092"
---
# <a name="msreportserver_configurationsetting-properties"></a>Proprietà MSReportServer_ConfigurationSetting
  La classe MSReportServer_ConfigurationSetting rappresenta i parametri di installazione e runtime di un'istanza del server di report. Tali impostazioni sono archiviate nel file di configurazione RSReportServer.config.  
  
## <a name="public-properties"></a>Proprietà pubbliche  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-connectionpoolsize.md)|Restituisce le dimensioni del pool di connessioni usato dal server di report per comunicare con l'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ospita il database del server di report. Di sola lettura.|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md)|Specifica l'account di accesso usato dal server di report per connettersi all'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ospita il database del server di report. Di sola lettura.|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontimeout.md)|Specifica il numero di secondi di attesa prima che un tentativo di accesso al database del server di report abbia esito negativo. Di sola lettura.|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md)|Specifica se il server di report utilizza un account del servizio Windows, un account utente di Windows o un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per accedere al database del server di report. Di sola lettura.|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasename.md)|Specifica il nome dell'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospita il database del server di report.|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasequerytimeout.md)|Specifica il numero di secondi che devono trascorrere prima che il comando non riesca o che si verifichi il timeout. Il server di report calcola il tempo del processo rispetto al catalogo di SQL Server e non rispetto a un'origine dati per il report.|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaseservername.md)|Specifica il nome del server in cui è installato il database del server di report.|  
|[Proprietà InstallationID](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-installationid.md)|Restituisce un identificatore univoco per un'istanza del server di report specifica.|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-instancename.md)|Specifica il nome di un'istanza del server di report in un determinato computer.|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md)|Indica se l'istanza del server di report è inizializzata.  Di sola lettura.|  
|[IsSharePointIntegrated](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-issharepointintegrated.md)|Indica se il server di report è configurato per la modalità integrata SharePoint.|  
|[IsWebServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswebserviceenabled.md)|Indica se il servizio Web ReportServer è abilitato. Di sola lettura.|  
|[IsWindowsServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswindowsserviceenabled.md)|Indica se il servizio Windows ReportServer è abilitato. Di sola lettura.|  
|[Proprietà MachineAccountIdentity &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-machineaccountidentity.md)|Ottiene l'identità dell'account del computer in cui è installato il server di report.|  
|[PathName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-pathname.md)|Specifica il percorso di installazione per un'istanza del server di report.|  
|[SecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-secureconnectionlevel.md)|Restituisce il livello di connessione protetta specificato nel file RSReportServer.config.|  
|[SenderEmailAddress](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-senderemailaddress.md)|Ottiene l'indirizzo utilizzato per inviare messaggi di posta elettronica dal server di report. Di sola lettura.|  
|[SendUsingSMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-sendusingsmtpserver.md)|Specifica se la proprietà SendUsing nella configurazione della posta elettronica è impostata su TRUE.|  
|[SMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-smtpserver.md)|Ottiene la proprietà del server SMTP dal file RSReportServer.config. Di sola lettura.|  
|[UnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-unattendedexecutionaccount.md)|Specifica l'account utente di accesso rappresentato dal server di report per l'esecuzione automatica dei report. Di sola lettura.|  
|[Versione](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-version.md)|Restituisce la versione del server di report.|  
|[Proprietà VirtualDirectoryReportManager &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportmanager.md)|Restituisce la directory virtuale per Gestione report.|  
|[Proprietà VirtualDirectoryReportServer &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportserver.md)|Restituisce la directory virtuale per il servizio Web ReportServer.|  
|[WindowsServiceIdentityActual](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-windowsserviceidentityactual.md)|Restituisce l'identità con cui il servizio Windows ReportServer è effettivamente in esecuzione. Di sola lettura.|  
|[WindowsServiceIdentityConfigured](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityconfigured-property.md)|Restituisce l'ultima identità con cui il servizio Windows ReportServer è stato configurato per l'esecuzione. Di sola lettura.|  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  

  
