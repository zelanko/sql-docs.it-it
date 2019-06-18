---
title: Membri di MSReportServer_ConfigurationSetting | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- MSReportServer_ConfigurationSetting Members
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: 5e21a53a-a2f8-4b35-a8d9-5483519e3857
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 134c115e48bd578f794ecce28d770ce955622f0b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65569171"
---
# <a name="msreportserverconfigurationsetting-members"></a>Membri di MSReportServer_ConfigurationSetting
  La classe MSReportServer_ConfigurationSetting contiene le proprietà e i metodi seguenti.  
  
## <a name="public-properties"></a>Proprietà pubbliche  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-connectionpoolsize.md)|Restituisce le dimensioni del pool di connessioni utilizzato dal server di report per comunicare con l'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ospita il database del server di report. Di sola lettura.|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md)|Specifica l'account di accesso utilizzato dal server di report per connettersi all'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] che ospita il database del server di report. Di sola lettura.|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontimeout.md)|Specifica il numero di secondi di attesa prima che un tentativo di accesso al database del server di report abbia esito negativo. Di sola lettura.|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md)|Specifica se il server di report utilizza un account del servizio Windows, un account utente di Windows o un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per accedere al database del server di report. Di sola lettura.|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasename.md)|Specifica il nome dell'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che ospita il database del server di report.|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasequerytimeout.md)|Specifica il numero di secondi che devono trascorrere prima che il comando non riesca o che si verifichi il timeout. Il server di report calcola il tempo del processo rispetto al database del server di report e non rispetto a un'origine dati per il report.|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaseservername.md)|Specifica il nome del server in cui è installato il database del server di report.|  
|[Proprietà InstallationID](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-installationid.md)|Restituisce un identificatore univoco per un'istanza del server di report specifica.|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-instancename.md)|Specifica il nome di un'istanza del server di report in un determinato computer.|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md)|Indica se l'istanza del server di report è inizializzata. Di sola lettura.|  
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
|[Version](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-version.md)|Restituisce la versione del server di report.|  
|[Proprietà VirtualDirectoryReportManager &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportmanager.md)|Restituisce la directory virtuale per Gestione report.|  
|[Proprietà VirtualDirectoryReportServer &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportserver.md)|Restituisce la directory virtuale per il servizio Web ReportServer.|  
|[WindowsServiceIdentityActual](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-windowsserviceidentityactual.md)|Restituisce l'identità con cui il servizio Windows ReportServer è effettivamente in esecuzione. Di sola lettura.|  
|[WindowsServiceIdentityConfigured](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityconfigured-property.md)|Restituisce l'ultima identità con cui il servizio Windows ReportServer è stato configurato per l'esecuzione. Di sola lettura.|  
  
## <a name="public-methods"></a>Metodi pubblici  
  
|||  
|-|-|  
|[BackupEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md)|Esegue il backup della chiave di crittografia per l'istanza. Tale chiave viene archiviata crittografata con una password.|  
|[Metodo CreateSSLCertificateBinding &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-createsslcertificatebinding.md)|Crea un'associazione certificato SSL.|  
|[DeleteEncryptedInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptedinformation.md)|Elimina le informazioni crittografate dal database del server di report.|  
|[DeleteEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptionkey.md)|Elimina le chiavi di crittografia dal database del server di report.|  
|[GenerateDatabaseCreationScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)|Genera uno script SQL che può essere utilizzato per creare il database del server di report.|  
|[GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)|Genera uno script SQL che può essere utilizzato per concedere a un utente le autorizzazioni per il database del server di report.|  
|[GenerateDatabaseUpgradeScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)|Genera uno script SQL che può essere utilizzato per aggiornare un database del server di report.|  
|[Metodo GetAdminSiteUrl &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getadminsiteurl.md)|Ottiene l'URL assoluto del sito Web di Amministrazione centrale.|  
|[GetDatabaseVersionDisplayName](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getdatabaseversiondisplayname.md)|Ottiene il nome visualizzato di una stringa di versione di un database del server di report specifico.|  
|[InitializeReportServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-initializereportserver.md)|Inizializza l'istanza del server di report specificata.|  
|[Metodo ListInstalledSharePointVersions &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listinstalledsharepointversions.md)|Restituisce un set di token che rappresentano le versioni di [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] installate nello stesso computer del server di report.|  
|[Metodo ListIPAddresses &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listipaddresses.md)|Elenca gli indirizzi IP per il computer.|  
|[ListReportServersInDatabase](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreportserversindatabase.md)|Restituisce un elenco di installazioni del server di report presenti nel database del server di report, indipendentemente dal fatto che tali installazioni accedano o meno a informazioni protette.|  
|[Metodo ListReservedURLs &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreservedurls.md)|Elenca gli URL riservati per tutte le applicazioni presenti nel server di report.|  
|[Metodo ListSSLCertificateBindings &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificatebindings.md)|Elenca le associazioni certificato SSL presenti in HTTP.SYS e quelle previste da rsreportserver.config.|  
|[Metodo ListSSLCertificate &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificates.md)|Elenca i certificati SSL installati nel computer.|  
|[ReencryptSecureInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reencryptsecureinformation.md)|Genera una nuova chiave di crittografia e la utilizza per crittografare nuovamente tutte le informazioni protette nel database del server di report.|  
|[Metodo RemoveSSLCertificateBindings &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removesslcertificatebinding.md)|Rimuove un'associazione certificato SSL.|  
|[RemoveUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeunattendedexecutionaccount.md)|Elimina la voce relativa all'account di esecuzione automatica dalla configurazione del server di report.|  
|[Metodo RemoveURL &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeurl.md)|Rimuove un URL riservato per il server di report.|  
|[Metodo ReserveURL &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md)|Aggiunge una prenotazione URL per un'applicazione specifica.|  
|[RestoreEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-restoreencryptionkey.md)|Riapplica la chiave di crittografia specificata al database del server di report.|  
|[SetDatabaseConnection](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaseconnection.md)|Imposta la connessione al database del server di report su un database del server di report specifico.|  
|[SetDatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaselogontimeout.md)|Specifica il valore di timeout predefinito per i tentativi di accesso al database del server di report.|  
|[SetDatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabasequerytimeout.md)|Specifica il valore di timeout predefinito per le connessione al database del server di report.|  
|[SetEmailConfiguration](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setemailconfiguration.md)|Configura l'estensione per il recapito tramite posta elettronica utilizzata dal server di report per l'invio di messaggi di posta elettronica.|  
|[SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)|Imposta il livello di connessione protetta del server di report.|  
|[SetServiceState](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setservicestate.md)|Attiva e disattiva i servizi Windows ReportServer e Web ReportServer.|  
|[SetUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setunattendedexecutionaccount.md)|Specifica l'account utilizzato per l'esecuzione automatica dei report.|  
|[Metodo SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md)|Imposta la directory virtuale per un'applicazione.|  
|[SetWindowsServiceIdentity](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setwindowsserviceidentity.md)|Consente l'esecuzione del servizio Windows ReportServer in base all'utente di Windows specificato e concede a tale account autorizzazioni per il file system sufficienti, in modo da consentire il funzionamento del server di report.|  
  
## <a name="see-also"></a>Vedere anche  
 [MSReportServer_ConfigurationSetting Class](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
