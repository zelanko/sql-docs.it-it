---
description: Metodi di MSReportServer_ConfigurationSetting
title: Metodi di MSReportServer_ConfigurationSetting | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- MSReportServer_ConfigurationSetting Methods
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: a08c2476-5b8e-4792-94da-1360fe231c6e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7b51e79a99f47886627f6479f58b7a2980629d88
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472609"
---
# <a name="msreportserver_configurationsetting-methods"></a>Metodi di MSReportServer_ConfigurationSetting
  La classe MSReportServer_ConfigurationSetting del provider WMI del server di report fornisce i seguenti metodi pubblici.  
  
## <a name="public-methods"></a>Metodi pubblici  
  
|Metodo|Descrizione|  
|-|-|  
|[BackupEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md)|Esegue il backup della chiave di crittografia per l'istanza. Tale chiave viene archiviata crittografata con una password.|  
|[Metodo CreateSSLCertificateBinding &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-createsslcertificatebinding.md)|Crea un'associazione di certificati TLS/SSL.|  
|[DeleteEncryptedInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptedinformation.md)|Elimina le informazioni crittografate dal database del server di report.|  
|[DeleteEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptionkey.md)|Elimina le chiavi di crittografia dal database del server di report.|  
|[GenerateDatabaseCreationScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)|Genera uno script SQL che può essere utilizzato per creare il database del server di report.|  
|[GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)|Genera uno script SQL che può essere utilizzato per concedere a un utente le autorizzazioni per il database del server di report.|  
|[GenerateDatabaseUpgradeScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)|Genera uno script SQL che può essere utilizzato per aggiornare un database del server di report.|  
|[Metodo GetAdminSiteUrl &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getadminsiteurl.md)|Ottiene l'URL assoluto del sito Web di Amministrazione centrale.|  
|[GetDatabaseVersionDisplayName](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getdatabaseversiondisplayname.md)|Ottiene il nome visualizzato di una stringa di versione di un database del server di report specifico.|  
|[InitializeReportServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-initializereportserver.md)|Inizializza l'istanza del server di report specificata.|  
|[Metodo ListInstalledSharePointVersions &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listinstalledsharepointversions.md)|Restituisce un set di token che rappresentano le versioni di Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] installate nello stesso computer del server di report.|  
|[Metodo ListIPAddresses &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listipaddresses.md)|Elenca gli indirizzi IP per il computer.|  
|[ListReportServersInDatabase](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreportserversindatabase.md)|Restituisce un elenco di installazioni del server di report presenti nel database del server di report, indipendentemente dal fatto che tali installazioni accedano o meno a informazioni protette.|  
|[Metodo ListReservedURLs &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreservedurls.md)|Elenca gli URL riservati per tutte le applicazioni presenti nel server di report.|  
|[Metodo ListSSLCertificateBindings &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificatebindings.md)|Elenca le associazioni di certificati TLS/SSL presenti in HTTP.SYS e quelle previste da RSReportServer.config.|  
|[Metodo ListSSLCertificate &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificates.md)|Elenca i certificati TLS/SSL installati nel computer.|  
|[ReencryptSecureInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reencryptsecureinformation.md)|Genera una nuova chiave di crittografia e la utilizza per crittografare nuovamente tutte le informazioni protette nel database del server di report.|  
|[Metodo RemoveSSLCertificateBindings &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removesslcertificatebinding.md)|Rimuove un'associazione di certificati TLS/SSL.|  
|[RemoveUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeunattendedexecutionaccount.md)|Elimina la voce relativa all'account di esecuzione automatica dalla configurazione del server di report.|  
|[Metodo RemoveURL &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeurl.md)|Rimuove un URL riservato per il server di report.|  
|[Metodo ReserveURL &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md)|Aggiunge una prenotazione URL per un'applicazione specifica.|  
|[RestoreEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-restoreencryptionkey.md)|Riapplica la chiave di crittografia specificata al database del server di report.|  
|[SetDatabaseConnection](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaseconnection.md)|Imposta la connessione al database del server di report su un database del server di report specifico.|  
|[SetDatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaselogontimeout.md)|Specifica il valore di timeout predefinito per i tentativi di accesso al database del server di report.|  
|[SetDatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabasequerytimeout.md)|Specifica il valore di timeout predefinito per le query sul database del server di report.|  
|[SetEmailConfiguration](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setemailconfiguration.md)|Configura l'estensione per il recapito tramite posta elettronica utilizzata dal server di report per l'invio di messaggi di posta elettronica.|  
|[SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)|Imposta il livello di connessione protetta del server di report.|  
|[SetServiceState](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setservicestate.md)|Attiva e disattiva il servizio ReportServer.|  
|[SetUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setunattendedexecutionaccount.md)|Specifica l'account utilizzato per l'esecuzione automatica dei report.|  
|[Metodo SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md)|Imposta la directory virtuale per un'applicazione.|  
|[SetWindowsServiceIdentity](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setwindowsserviceidentity.md)|Consente l'esecuzione del servizio ReportServer in base all'utente di Windows specificato e concede a tale account autorizzazioni per il file system sufficienti, in modo da consentire il funzionamento del server di report.|  
  
## <a name="see-also"></a>Vedere anche  
 [Classe MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
