---
title: Proprietà di MSReportServer_ConfigurationSetting | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Properties
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: bf1d2d6a884f3751cd2d252bbba38d62aeea5bf9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023722"
---
# <a name="msreportserverconfigurationsetting-properties"></a>Proprietà MSReportServer_ConfigurationSetting
  La classe MSReportServer_ConfigurationSetting rappresenta i parametri di installazione e runtime di un'istanza del server di report. Tali impostazioni sono archiviate nel file di configurazione RSReportServer.config.  
  
## <a name="public-properties"></a>Proprietà pubbliche  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|Restituisce le dimensioni del pool di connessioni utilizzato dal server di report per comunicare con l'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ospita il database del server di report. Di sola lettura.|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|Specifica l'account di accesso utilizzato dal server di report per connettersi all'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ospita il database del server di report. Di sola lettura.|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|Specifica il numero di secondi di attesa prima che un tentativo di accesso al database del server di report abbia esito negativo. Di sola lettura.|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|Specifica se il server di report utilizza un account del servizio Windows, un account utente di Windows o un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per accedere al database del server di report. Di sola lettura.|  
|[DatabaseName](configurationsetting-property-databasename.md)|Specifica il nome dell'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospita il database del server di report.|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|Specifica il numero di secondi che devono trascorrere prima che il comando non riesca o che si verifichi il timeout. Il server di report calcola il tempo del processo rispetto al catalogo di SQL Server e non rispetto a un'origine dati per il report.|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|Specifica il nome del server in cui è installato il database del server di report.|  
|[Proprietà InstallationID](configurationsetting-property-installationid.md)|Restituisce un identificatore univoco per un'istanza del server di report specifica.|  
|[InstanceName](configurationsetting-property-instancename.md)|Specifica il nome di un'istanza del server di report in un determinato computer.|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|Indica se l'istanza del server di report è inizializzata.  Di sola lettura.|  
|[IsSharePointIntegrated](configurationsetting-property-issharepointintegrated.md)|Indica se il server di report è configurato per la modalità integrata SharePoint.|  
|[IsWebServiceEnabled](configurationsetting-property-iswebserviceenabled.md)|Indica se il servizio Web ReportServer è abilitato. Di sola lettura.|  
|[IsWindowsServiceEnabled](configurationsetting-property-iswindowsserviceenabled.md)|Indica se il servizio Windows ReportServer è abilitato. Di sola lettura.|  
|[Proprietà MachineAccountIdentity &#40;WMI&#41;](configurationsetting-property-machineaccountidentity.md)|Ottiene l'identità dell'account del computer in cui è installato il server di report.|  
|[PathName](configurationsetting-property-pathname.md)|Specifica il percorso di installazione per un'istanza del server di report.|  
|[SecureConnectionLevel](configurationsetting-property-secureconnectionlevel.md)|Restituisce il livello di connessione protetta specificato nel file RSReportServer.config.|  
|[SenderEmailAddress](configurationsetting-property-senderemailaddress.md)|Ottiene l'indirizzo utilizzato per inviare messaggi di posta elettronica dal server di report. Di sola lettura.|  
|[SendUsingSMTPServer](configurationsetting-property-sendusingsmtpserver.md)|Specifica se la proprietà SendUsing nella configurazione della posta elettronica è impostata su TRUE.|  
|[SMTPServer](configurationsetting-property-smtpserver.md)|Ottiene la proprietà del server SMTP dal file RSReportServer.config. Di sola lettura.|  
|[UnattendedExecutionAccount](configurationsetting-property-unattendedexecutionaccount.md)|Specifica l'account utente di accesso rappresentato dal server di report per l'esecuzione automatica dei report. Di sola lettura.|  
|[Version](configurationsetting-property-version.md)|Restituisce la versione del server di report.|  
|[Proprietà VirtualDirectoryReportManager &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-property-virtualdirectoryreportmanager.md)|Restituisce la directory virtuale per Gestione report.|  
|[Proprietà VirtualDirectoryReportServer &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-property-virtualdirectoryreportserver.md)|Restituisce la directory virtuale per il servizio Web ReportServer.|  
|[WindowsServiceIdentityActual](configurationsetting-property-windowsserviceidentityactual.md)|Restituisce l'identità con cui il servizio Windows ReportServer è effettivamente in esecuzione. Di sola lettura.|  
|[WindowsServiceIdentityConfigured](windowsserviceidentityconfigured-property.md)|Restituisce l'ultima identità con cui il servizio Windows ReportServer è stato configurato per l'esecuzione. Di sola lettura.|  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
