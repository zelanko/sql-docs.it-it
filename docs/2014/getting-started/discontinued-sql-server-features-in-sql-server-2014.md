---
title: Funzionalità di SQL Server sospese in SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 0678bfbc-5d3f-44f4-89c0-13e8e52404da
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b8f7ab6cdbc1b6e0e3dc7d26fb579943a0c8fa95
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637776"
---
# <a name="discontinued-sql-server-features-in-sql-server-2014"></a>Funzionalità di SQL Server obsolete in SQL Server 2014
  In questo argomento vengono descritte le funzionalità non più disponibili dopo l'aggiornamento a [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="discontinued-features-in-includesssql14includessssql14-mdmd"></a>Funzionalità non più disponibili in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Nessuna funzionalità non più disponibile in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
## <a name="discontinued-features-in-includesssql11includessssql11-mdmd"></a>Funzionalità non più disponibili in [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="discontinued-active-directory-helper-service"></a>Servizi Active Directory Helper obsoleti  
 Il servizio Active Directory Helper e i componenti correlati sono stati rimossi. Nella tabella seguente sono elencati i componenti associati rimossi:  
  
|Category|Funzionalità non più utilizzata|Sostituzione|  
|--------------|--------------------------|-----------------|  
|Stored procedure di sistema|sp_ActiveDirectory_Obj<br /><br /> sp_ActiveDirectory_SCP<br /><br /> sp_ActiveDirectory_Start|Nessuna sostituzione disponibile|  
  
## <a name="discontinued-features-in-sql-server-2008-r2"></a>Funzionalità obsolete in SQL Server 2008 R2  
  
### <a name="64-bit-platform-support-in-reporting-services"></a>Supporto della piattaforma a 64 bit in Reporting Services  
 A partire da [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)], il componente [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] non supporta più server basati su Itanium che eseguono Windows Server 2003 o Windows Server 2003 R2. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] continua a supportare gli altri sistemi operativi a 64 bit, ad esempio Windows Server°2008 per sistemi basati su Itanium e Windows Server°2008°R2 per sistemi basati su Itanium. Per eseguire l'aggiornamento a [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] da un'installazione di [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in un'edizione del sistema basata su Itanium di Windows Server 2003 o Windows Server 2003 R2, è necessario prima aggiornare il sistema operativo.  
  
## <a name="discontinued-features-in-sql-server-2008"></a>Funzionalità obsolete in SQL Server 2008  
  
### <a name="discontinued-sql-dmo-from-sql-server-express-installation"></a>Eliminazione di SQL-DMO dall'installazione di SQL Server Express  
 SQL-DMO for [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è stato rimosso da [!INCLUDE[ssExpressEd10](../includes/ssexpressed10-md.md)]. È consigliabile modificare il prima possibile le applicazioni che utilizzano questa funzionalità. Se è necessario supportare SQL-DMO per [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express, installare i componenti per la compatibilità con le versioni precedenti da [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] Feature Pack dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=24793). Utilizzare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Objects (SMO) per i nuovi progetti di sviluppo.  
  
### <a name="discontinued-option-for-web-assistant"></a>Opzione rimossa per Pubblicazione guidata sul Web  
 L'opzione `sp_configure` per abilitare Pubblicazione guidata sul Web è stata rimossa da [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. È consigliabile utilizzare [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] in alternativa.  
  
### <a name="surface-area-configuration-tool"></a>strumento Configurazione superficie di attacco  
 Lo strumento Configurazione superficie di attacco non è più disponibile per [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Nella tabella seguente vengono illustrati gli elementi che è possibile utilizzare per configurare impostazioni, opzioni e funzionalità di componenti nella versione corrente.  
  
|Impostazioni di sostituzione e funzionalità del componente|Modalità di configurazione|  
|-------------------------------------------------|----------------------|  
|Protocolli, opzioni di connessione e di avvio|Utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|Funzionalità di [!INCLUDE[ssDE](../includes/ssde-md.md)]|Utilizzare la gestione basata su criteri, le impostazioni delle proprietà in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] oppure sp_Configure.|  
|Funzionalità di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Utilizzare le impostazioni delle proprietà in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].|  
|Proprietà di sicurezza [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]-proprietà EnableIntegratedSecurity|Utilizzare le impostazioni delle proprietà in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]: "Pianifica Eventi e recapito report" e "accesso HTTP e servizi Web"|Modificare il file di configurazione RSReportServer.config.|  
|Opzioni della riga di comando|Supporto non disponibile in questa versione.|  
|Endpoint SOAP e [!INCLUDE[ssSB](../includes/sssb-md.md)]|Utilizzare [create endpoint](/sql/t-sql/statements/create-endpoint-transact-sql)e [ALTER endpoint](/sql/t-sql/statements/alter-endpoint-transact-sql).|  
  
### <a name="discontinued-command-prompt-parameters-for-sql-server-setup"></a>Parametri del prompt dei comandi non più supportati nell'installazione di SQL Server  
 Nella tabella seguente sono illustrati i parametri del prompt dei comandi dell'installazione di versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non più sono supportati in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
|Parametro non più supportato|Parametro sostitutivo|  
|----------------------------|---------------------------|  
|ADDLOCAL|/ACTION=Uninstall e /FEATURES|  
|DISABLENETWORKPROTOCOLS|/TCPENABLED per TCP/IP<sup>1</sup>|  
|DISABLENETWORKPROTOCOLS|/NPENABLED per Named Pipes<sup>1</sup>|  
|INSTALLSQLDATADIR|/SQLUSERDBDIR<br /><br /> /SQLUSERDBLOGDIR<br /><br /> /SQLBACKUPDIR<br /><br /> /SQLTEMPDBDIR<br /><br /> /SQLTEMPDBLOGDIR|  
|REINSTALL|Nessun parametro equivalente in questa versione.|  
|REINSTALLMODE|Nessun parametro equivalente in questa versione.|  
|REMOVE|/ACTION=Uninstall e /FEATURES|  
|SAMPLEDATABASE|Nessun parametro equivalente in questa versione.|  
|SAVESYSDB|Nessun parametro equivalente in questa versione.|  
|SKUUPGRADE<sup>2</sup>|Nessun parametro equivalente in questa versione.|  
|UPGRADE|/ACTION=Upgrade e /FEATURES|  
|USESYSDB|Nessun parametro equivalente in questa versione.|  
  
 <sup>1</sup> Questi parametri sono validi solo per l'installazione.  
  
 <sup>2</sup> A partire da [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], specificare/Action = EditionUpgrade per aggiornare un'edizione esistente di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a un'edizione diversa in qualsiasi momento senza usare il supporto di installazione originale. Per ulteriori informazioni sugli aggiornamenti di versione ed edizione supportati, vedere [Supported Version and Edition Upgrades](../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
 Per altre informazioni, vedere [Installare SQL Server 2014 dal prompt dei comandi](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
  
