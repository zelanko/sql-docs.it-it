---
title: Finestra di dialogo Crea applicazione Web (Gestione configurazione Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.createapp.f1
ms.assetid: e045b41a-4836-47f6-8e78-2b09494b461f
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: dac7b74969c341b7f68c7dfbf56d2314d9ab4427
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52788363"
---
# <a name="create-web-application-dialog-box-master-data-services-configuration-manager"></a>Finestra di dialogo Crea applicazione Web (Gestione configurazione Master Data Services)
  Usare la finestra di dialogo **Crea applicazione Web** per creare l'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . L'applicazione Web viene creata nel sito selezionato nella pagina **Configurazione Web** .  
  
## <a name="web-application"></a>Applicazione Web  
 Il server Web risponde alle richieste di contenuto per l'applicazione Web inclusa nella cartella [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] **WebApplication** folder in the file system. Questa posizione viene specificata durante l'installazione e per impostazione predefinita è il percorso *unità*: \Programmi\Microsoft SQL Server\120\Master Data services\webapplication.  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|Percorso virtuale|Selezionare il percorso virtuale in cui si vuole creare l'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Un percorso virtuale fa parte dell'URL utilizzato per accedere a un'applicazione Web.<br /><br /> Questo elenco viene filtrato per visualizzare solo i percorsi virtuali delle applicazioni in cui è possibile creare l'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Non è possibile creare un'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] in un'altra applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .|  
|Alias|Digitare un nome per l'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] o usare il nome predefinito. Questo nome viene utilizzato in un URL per l'accesso all'applicazione Web da un browser.|  
  
## <a name="application-pool"></a>Pool di applicazioni  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**Name**|Digitare un nome univoco descrittivo per un nuovo pool di applicazioni oppure utilizzare il nome predefinito. L'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] verrà aggiunta a questo pool di applicazioni.<br /><br /> I pool di applicazioni definiscono limiti che impediscono alle applicazioni incluse in un pool di applicazioni di influire sulle applicazioni incluse in un altro pool di applicazioni.|  
|**Nome utente**|Digitare un dominio e il nome utente di Active Directory. Questo account è l'identità del pool di applicazioni in cui viene eseguita l'applicazione Web. L'account deve corrispondere all'account del servizio specificato alla creazione del database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> Questo account viene aggiunto al ruolo del database mds_exec nel database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] per l'accesso al database. Per altre informazioni, vedere [Account di accesso, utenti e ruoli di database &#40;Master Data Services&#41;](database-logins-users-and-roles-master-data-services.md). Viene inoltre aggiunto a un gruppo di Windows [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], **MDS_ServiceAccounts**, a cui viene concessa l'autorizzazione per la directory di compilazione temporanea, **MDSTempDir**, nel file system. Per altre informazioni, vedere [Autorizzazioni per file e cartelle &#40;Master Data Services&#41;](../../2014/master-data-services/folder-and-file-permissions-master-data-services.md).|  
|**Password**|Digitare la password per l'account utente specificato.|  
|**Conferma password**|Ridigitare la password per l'account utente specificato. I campi **Password** e **Conferma password** devono contenere la stessa password.|  
  
## <a name="see-also"></a>Vedere anche  
 [Pagina Configurazione Web &#40;Gestione configurazione Master Data Services&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
 [Configurare il Database e il sito Web per Master Data Services](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Requisiti dell'applicazione Web &#40;Master Data Services&#41;](install-windows/web-application-requirements-master-data-services.md)   
 [Creare un'applicazione Web Gestione dati master &#40;Master Data Services&#41;](install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
