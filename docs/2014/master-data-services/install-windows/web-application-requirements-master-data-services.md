---
title: Requisiti dell'applicazione Web (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 9455d3cf-c1b7-4d48-8aff-7dc636ed5dc3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 15b394c836cb24229944f4e0775dfccad847a32b
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/09/2019
ms.locfileid: "65482879"
---
# <a name="web-application-requirements-master-data-services"></a>Requisiti dell'applicazione Web (Master Data Services)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] è un'applicazione Web ospitata da Internet Information Services (IIS). [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] funziona solo in Internet Explorer (IE) 7 o versioni successive. IE 7 e le versioni precedenti, Microsoft Edge e Chrome non sono supportati.  
  
 Utilizzare [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] per creare e configurare l'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] . [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] IIS viene configurato nel computer locale, rappresentando pertanto la soluzione ottimale per le attività di configurazione Web iniziali. Configurare ad esempio un ambiente [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] con una singola applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] oppure configurare la prima applicazione Web in una distribuzione con scalabilità orizzontale di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Utilizzare gli strumenti di IIS per eseguire le attività più complesse, ad esempio la configurazione di più server Web in una distribuzione con scalabilità orizzontale.  
  
> [!NOTE]  
>  Tutti i computer in cui si installano componenti di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] devono essere dotati di licenza appropriata. Per ulteriori informazioni, fare riferimento al Contratto di licenza.  
  
## <a name="requirements"></a>Requisiti  
  
### <a name="operating-system"></a>Sistema operativo  
 Nei seguenti sistemi operativi Windows sono incluse le funzionalità di Internet Information Services (IIS) necessarie per l'applicazione Web [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e il servizio Web.  
  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Developer (64-bit) x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Enterprise (64-bit) x64|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Business Intelligence (64-bit) x64|  
|-------------------------------------------------------|--------------------------------------------------------|-------------------------------------------------------------------|  
|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows 7 Professional, Enterprise e Ultimate<br /><br /> Windows 8.0 Professional, Enterprise e Ultimate|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|[!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2<br /><br /> Windows Server 2008 R2 SP1<br /><br /> Windows Server 2012|  
  
 Per un elenco completo dei sistemi operativi Windows supportati per l'edizione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
### <a name="microsoft-silverlight"></a>Microsoft Silverlight  
 Per funzionare nell'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , è necessario installare Silverlight 5 nel computer client. Se non si dispone della versione richiesta di Silverlight, sarà necessario installarla quando si passa a un'area dell'applicazione Web in cui è necessaria. Silverlight 5 può essere installato da [qui](https://go.microsoft.com/fwlink/?LinkId=243096).  
  
### <a name="role-and-role-services-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>Ruolo e servizi ruolo (sistemi operativi Windows Server 2008 o Windows Server 2008 R2, Windows 7)  
 In Windows Server 2008 R2 è possibile utilizzare **Server Manager**, disponibile in Microsoft Management Console (MMC), per installare il ruolo **Server Web (IIS)** e i seguenti servizi ruolo necessari:  
  
> [!NOTE]  
>  Nei sistemi operativi [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] e Windows 7 utilizzare **Programmi e funzionalità** nel Pannello di controllo per abilitare queste opzioni nella finestra di dialogo **Funzionalità Windows** .  
  
||  
|-|  
|Server Web<br /><br /> Funzionalità HTTP comuni<br /><br /> Contenuto statico<br /><br /> Documento predefinito<br /><br /> Esplorazione directory<br /><br /> Errori HTTP<br /><br /> Sviluppo applicazioni<br /><br /> ASP.NET<br /><br /> Estendibilità .NET<br /><br /> Estensioni ISAPI<br /><br /> Filtri ISAPI<br /><br /> Integrità e diagnostica<br /><br /> Registrazione HTTP<br /><br /> Monitoraggio richieste<br /><br /> Sicurezza<br /><br /> Autenticazione di Windows<br /><br /> Filtro richieste<br /><br /> Prestazioni<br /><br /> Compressione contenuto statico<br /><br /> Strumenti di gestione<br /><br /> Console di gestione IIS|  
  
### <a name="role-and-role-services-windows-server-2012-or-windows-8-operating-systems"></a>Ruolo e servizi ruolo (sistemi operativi Windows Server 2012 o Windows 8)  
 In Windows Server 2012 è possibile utilizzare **Server Manager**, disponibile in Microsoft Management Console (MMC), per installare il ruolo **Server Web (IIS)** e i seguenti servizi ruolo necessari:  
  
> [!NOTE]  
>  Nel sistema operativo Windows 8 utilizzare **Programmi e funzionalità** nel Pannello di controllo per abilitare queste opzioni nella finestra di dialogo **Funzionalità Windows** .  
  
||  
|-|  
|Internet Information Services<br /><br /> Strumenti di gestione Web<br /><br /> Console di gestione IIS<br /><br /> Servizi Web<br /><br /> Sviluppo applicazioni<br /><br /> Estendibilità .NET 3.5<br /><br /> Estendibilità .NET 4.5<br /><br /> ASP.NET 3.5<br /><br /> ASP.NET 4.5<br /><br /> Estensioni ISAPI<br /><br /> Filtri ISAPI<br /><br /> Funzionalità HTTP comuni<br /><br /> Documento predefinito<br /><br /> Esplorazione directory<br /><br /> Errori HTTP<br /><br /> Contenuto statico<br /><br /> [Nota: Installare la pubblicazione WebDAV]<br /><br /> Integrità e diagnostica<br /><br /> Registrazione HTTP<br /><br /> Monitoraggio richieste<br /><br /> Prestazioni<br /><br /> Compressione contenuto statico<br /><br /> Sicurezza<br /><br /> Filtro richieste<br /><br /> Autenticazione di Windows|  
  
### <a name="features-windows-server-2008-or-windows-server-2008-r2-windows-7-operating-systems"></a>Funzionalità (sistemi operativi Windows Server 2008 o Windows Server 2008 R2, Windows 7)  
 In [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] o Windows Server 2008 R2 è possibile utilizzare **Server Manager** per installare le seguenti funzionalità necessarie:  
  
> [!NOTE]  
>  Nei sistemi operativi [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] e Windows 7 utilizzare **Programmi e funzionalità** nel Pannello di controllo per abilitare queste opzioni nella finestra di dialogo **Funzionalità Windows** .  
  
||  
|-|  
|Funzionalità di .NET Framework 3.0<br /><br /> Attivazione di WCF<br /><br /> Attivazione HTTP<br /><br /> Attivazione non HTTP<br /><br /> Servizio Attivazione processo Windows<br /><br /> Modello di processo<br /><br /> Ambiente .NET<br /><br /> API di configurazione|  
  
### <a name="features-windows-server-2012-or-windows-8-operating-systems"></a>Funzionalità (sistemi operativi Windows Server 2012 o Windows 8)  
 In Windows Server 2012 è possibile utilizzare **Server Manager** per installare le seguenti funzionalità necessarie:  
  
> [!NOTE]  
>  Nel sistema operativo Windows 8 utilizzare **Programmi e funzionalità** nel Pannello di controllo per abilitare queste opzioni nella finestra di dialogo **Funzionalità Windows** .  
  
||  
|-|  
|.NET Framework 3.5 (inclusi .NET 2.0 e 3.0)<br /><br /> .NET Framework 4.5 Advanced Services<br /><br /> ASP.NET 4.5<br /><br /> WCF Services<br /><br /> Attivazione HTTP [Nota: È necessaria.]<br /><br /> Condivisione porta TCP<br /><br /> Servizio Attivazione processo Windows<br /><br /> Modello di processo<br /><br /> Ambiente .NET<br /><br /> API di configurazione|  
  
### <a name="accounts-and-permissions"></a>Account e autorizzazioni  
  
|Type|Descrizione|  
|----------|-----------------|  
|Account di Windows|È necessario accedere al computer server Web con un account di Windows che disponga dell'autorizzazione per configurare ruoli di Windows, servizi ruolo e funzionalità e per creare e gestire pool di applicazioni, siti Web e applicazioni Web in IIS sul computer locale.|  
|Account servizio|Quando si crea l'applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] in [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)], è necessario specificare un'identità per il pool di applicazioni in cui viene eseguita l'applicazione. Questo account può essere diverso dall'account del servizio che è stato specificato durante la creazione del database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .<br /><br /> Questa identità deve essere un account utente di dominio e viene aggiunta al ruolo di database mds_exec nel database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] per consentirne l'accesso. Per altre informazioni, vedere [Account di accesso, utenti e ruoli di database &#40;Master Data Services&#41;](../database-logins-users-and-roles-master-data-services.md). Questo account viene aggiunto anche a un gruppo di Windows [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], **MDS_ServiceAccounts**, a cui viene concessa l'autorizzazione per la directory di compilazione temporanea, **MDSTempDir**, nel file system. Per altre informazioni, vedere [Autorizzazioni per file e cartelle &#40;Master Data Services&#41;](../folder-and-file-permissions-master-data-services.md).<br /><br /> Per evitare errori del server, l'account del pool di applicazioni richiede l'autorizzazione VIEW SERVER STATE. Ad esempio, il comando Convalida versione di MDS avrà esito negativo con un errore del server. Per altre informazioni, vedere [Il comando Convalida versione di MDS ha esito negativo con un errore del server in SQL Server 2012 e SQL Server 2014](https://go.microsoft.com/fwlink/p/?LinkId=526304).|  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione di Master Data Services](install-master-data-services.md)   
 [Creare un'applicazione Web Gestione dati master &#40;Master Data Services&#41;](create-a-master-data-manager-web-application-master-data-services.md)   
 [Pagina Configurazione Web &#40;Gestione configurazione Master Data Services&#41;](../web-configuration-page-master-data-services-configuration-manager.md)  
  
  
