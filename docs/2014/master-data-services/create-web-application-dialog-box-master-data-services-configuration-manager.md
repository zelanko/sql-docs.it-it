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
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 65e057224a8456f893b38e106e6b7f75d03d237a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483229"
---
# <a name="create-web-application-dialog-box-master-data-services-configuration-manager"></a>Finestra di dialogo Crea applicazione Web (Gestione configurazione Master Data Services)
  Usare la finestra di dialogo **Crea applicazione Web** per creare l'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . L'applicazione Web viene creata nel sito selezionato nella pagina **Configurazione Web** .  
  
## <a name="web-application"></a>Applicazione Web  
 Il server Web risponde alle richieste di contenuto per l'applicazione Web inclusa nella cartella [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] **WebApplication** folder in the file system. Questo percorso viene specificato durante l'installazione e per impostazione predefinita il percorso è *unità*: \Programmi\microsoft SQL Server\120\Master Data Services\WebApplication.  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|Percorso virtuale|Selezionare il percorso virtuale in cui si vuole creare l'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Un percorso virtuale fa parte dell'URL utilizzato per accedere a un'applicazione Web.<br /><br /> Questo elenco viene filtrato per visualizzare solo i percorsi virtuali delle applicazioni in cui è possibile creare l'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Non è possibile creare un'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] in un'altra applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .|  
|Alias|Digitare un nome per l'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] o usare il nome predefinito. Questo nome viene utilizzato in un URL per l'accesso all'applicazione Web da un browser.|  
  
## <a name="application-pool"></a>Pool di applicazioni  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**Nome**|Digitare un nome univoco descrittivo per un nuovo pool di applicazioni oppure utilizzare il nome predefinito. L'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] verrà aggiunta a questo pool di applicazioni.<br /><br /> I pool di applicazioni definiscono limiti che impediscono alle applicazioni incluse in un pool di applicazioni di influire sulle applicazioni incluse in un altro pool di applicazioni.|  
|**Nome utente**|Digitare un dominio e il nome utente di Active Directory. Questo account è l'identità del pool di applicazioni in cui viene eseguita l'applicazione Web. L'account deve corrispondere all'account del servizio specificato alla creazione del database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> Questo account viene aggiunto al ruolo del database mds_exec nel database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] per l'accesso al database. Per altre informazioni, vedere [Account di accesso, utenti e ruoli di database &#40;Master Data Services&#41;](database-logins-users-and-roles-master-data-services.md). Viene inoltre aggiunto a un gruppo di Windows [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , **MDS_ServiceAccounts**, a cui viene concessa l'autorizzazione per la directory di compilazione temporanea, **MDSTempDir**, nel file system. Per altre informazioni, vedere [Autorizzazioni per file e cartelle &#40;Master Data Services&#41;](../../2014/master-data-services/folder-and-file-permissions-master-data-services.md).|  
|**Password**|Digitare la password per l'account utente specificato.|  
|**Conferma password**|Ridigitare la password per l'account utente specificato. I campi **Password** e **Conferma password** devono contenere la stessa password.|  
  
## <a name="see-also"></a>Vedere anche  
 [Pagina di configurazione Web &#40;Gestione configurazione Master Data Services&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
 [Configurare il database e il sito Web per Master Data Services](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Requisiti delle applicazioni Web &#40;Master Data Services&#41;](install-windows/web-application-requirements-master-data-services.md)   
 [Creare un'applicazione Web Gestione dati master &#40;Master Data Services&#41;](install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
