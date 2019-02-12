---
title: Metodi di MSReportServer_ConfigurationSetting | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Methods
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: a08c2476-5b8e-4792-94da-1360fe231c6e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d726e3982636b89819afed3a8500a581eebffc13
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56019622"
---
# <a name="msreportserverconfigurationsetting-methods"></a>Metodi di MSReportServer_ConfigurationSetting
  La classe MSReportServer_ConfigurationSetting del provider WMI del server di report fornisce i seguenti metodi pubblici.  
  
## <a name="public-methods"></a>Metodi pubblici  
  
|||  
|-|-|  
|[BackupEncryptionKey](configurationsetting-method-backupencryptionkey.md)|Esegue il backup della chiave di crittografia per l'istanza. Tale chiave viene archiviata crittografata con una password.|  
|[Metodo CreateSSLCertificateBinding &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-createsslcertificatebinding.md)|Crea un'associazione certificato SSL.|  
|[DeleteEncryptedInformation](configurationsetting-method-deleteencryptedinformation.md)|Elimina le informazioni crittografate dal database del server di report.|  
|[DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md)|Elimina le chiavi di crittografia dal database del server di report.|  
|[GenerateDatabaseCreationScript](configurationsetting-method-generatedatabasecreationscript.md)|Genera uno script SQL che può essere utilizzato per creare il database del server di report.|  
|[GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md)|Genera uno script SQL che può essere utilizzato per concedere a un utente le autorizzazioni per il database del server di report.|  
|[GenerateDatabaseUpgradeScript](configurationsetting-method-generatedatabaseupgradescript.md)|Genera uno script SQL che può essere utilizzato per aggiornare un database del server di report.|  
|[Metodo GetAdminSiteUrl &#40;WMI&#41;](configurationsetting-method-getadminsiteurl.md)|Ottiene l'URL assoluto del sito Web di Amministrazione centrale.|  
|[GetDatabaseVersionDisplayName](configurationsetting-method-getdatabaseversiondisplayname.md)|Ottiene il nome visualizzato di una stringa di versione di un database del server di report specifico.|  
|[InitializeReportServer](configurationsetting-method-initializereportserver.md)|Inizializza l'istanza del server di report specificata.|  
|[Metodo ListInstalledSharePointVersions &#40;WMI&#41;](configurationsetting-method-listinstalledsharepointversions.md)|Restituisce un set di token che rappresentano le versioni di Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] installate nello stesso computer del server di report.|  
|[Metodo ListIPAddresses &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-listipaddresses.md)|Elenca gli indirizzi IP per il computer.|  
|[ListReportServersInDatabase](configurationsetting-method-listreportserversindatabase.md)|Restituisce un elenco di installazioni del server di report presenti nel database del server di report, indipendentemente dal fatto che tali installazioni accedano o meno a informazioni protette.|  
|[Metodo ListReservedURLs &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-listreservedurls.md)|Elenca gli URL riservati per tutte le applicazioni presenti nel server di report.|  
|[Metodo ListSSLCertificateBindings &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-listsslcertificatebindings.md)|Elenca le associazioni certificato SSL presenti in HTTP.SYS e quelle previste da RSReportServer.config.|  
|[Metodo ListSSLCertificate &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-listsslcertificates.md)|Elenca i certificati SSL installati nel computer.|  
|[ReencryptSecureInformation](configurationsetting-method-reencryptsecureinformation.md)|Genera una nuova chiave di crittografia e la utilizza per crittografare nuovamente tutte le informazioni protette nel database del server di report.|  
|[Metodo RemoveSSLCertificateBindings &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-removesslcertificatebinding.md)|Rimuove un'associazione certificato SSL.|  
|[RemoveUnattendedExecutionAccount](configurationsetting-method-removeunattendedexecutionaccount.md)|Elimina la voce relativa all'account di esecuzione automatica dalla configurazione del server di report.|  
|[Metodo RemoveURL &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-removeurl.md)|Rimuove un URL riservato per il server di report.|  
|[Metodo ReserveURL &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-reserveurl.md)|Aggiunge una prenotazione URL per un'applicazione specifica.|  
|[RestoreEncryptionKey](configurationsetting-method-restoreencryptionkey.md)|Riapplica la chiave di crittografia specificata al database del server di report.|  
|[SetDatabaseConnection](configurationsetting-method-setdatabaseconnection.md)|Imposta la connessione al database del server di report su un database del server di report specifico.|  
|[SetDatabaseLogonTimeout](configurationsetting-method-setdatabaselogontimeout.md)|Specifica il valore di timeout predefinito per i tentativi di accesso al database del server di report.|  
|[SetDatabaseQueryTimeout](configurationsetting-method-setdatabasequerytimeout.md)|Specifica il valore di timeout predefinito per le query sul database del server di report.|  
|[SetEmailConfiguration](configurationsetting-method-setemailconfiguration.md)|Configura l'estensione per il recapito tramite posta elettronica utilizzata dal server di report per l'invio di messaggi di posta elettronica.|  
|[SetSecureConnectionLevel](configurationsetting-method-setsecureconnectionlevel.md)|Imposta il livello di connessione protetta del server di report.|  
|[SetServiceState](configurationsetting-method-setservicestate.md)|Attiva e disattiva il servizio ReportServer.|  
|[SetUnattendedExecutionAccount](configurationsetting-method-setunattendedexecutionaccount.md)|Specifica l'account utilizzato per l'esecuzione automatica dei report.|  
|[Metodo SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-setvirtualdirectory.md)|Imposta la directory virtuale per un'applicazione.|  
|[SetWindowsServiceIdentity](configurationsetting-method-setwindowsserviceidentity.md)|Consente l'esecuzione del servizio ReportServer in base all'utente di Windows specificato e concede a tale account autorizzazioni per il file system sufficienti, in modo da consentire il funzionamento del server di report.|  
  
## <a name="see-also"></a>Vedere anche  
 [MSReportServer_ConfigurationSetting Class](msreportserver-configurationsetting-class.md)  
  
  
