---
title: Finestra di dialogo Crea sito Web (Gestione configurazione Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.createsite.f1
ms.assetid: 179c9c1e-3b06-421b-b71b-1cb64d104f5e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 63e18bfd9c907e5604f82d0e5462b80d07279556
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971671"
---
# <a name="create-website-dialog-box-master-data-services-configuration-manager"></a>Finestra di dialogo Crea sito Web (Gestione configurazione Master Data Services)
  Usare la finestra di dialogo **Crea sito Web** per creare un nuovo sito Web nel computer locale. Quando si crea un sito Web in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], il sito viene aggiunto a Internet Information Services (IIS) nel computer locale con un'applicazione radice configurata come applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] . Viene inoltre creato un nuovo pool di applicazioni in cui viene inserita l'applicazione Web.  
  
## <a name="web-site"></a>Sito Web  
  
|Nome del controllo|Description|  
|------------------|-----------------|  
|**Nome sito Web**|Digitare un nome per il sito Web oppure utilizzare il nome predefinito. Si tratta di un nome descrittivo utilizzato solo per identificare il sito in IIS. Non viene utilizzato per accedere al sito da un Web browser.<br /><br /> Il nome deve essere univoco in tutti i siti inclusi in IIS nel computer locale.|  
|**Protocollo**|Consente di visualizzare **http**. Utilizzare il protocollo HTTP (Hypertext Transfer Protocol) quando non è necessario che la comunicazione tra client e server avvenga su un canale crittografato.<br /><br /> Nota: non è possibile creare un sito HTTPS in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. HTTPS è il protocollo HTTP che utilizza SSL (Secure Sockets Layer) e risulta particolarmente utile nello scambio di dati riservati o personali oppure quando si desidera che gli utenti confermino l'identità del server prima della trasmissione di informazioni personali. Se è necessario trasferire informazioni tra il server e un client su un canale crittografato, è necessario utilizzare un strumento IIS, ad esempio Gestione IIS, configurare il sito con un'associazione HTTPS e associare l'associazione del sito Web a un certificato server. È necessario effettuare queste operazioni prima che sia possibile aprire correttamente il sito Web in un Web browser. Per altre informazioni sui certificati server, vedere [Configuring Server Certificates in IIS 7](https://go.microsoft.com/fwlink/?LinkId=163220) (Configurazione dei certificati server in IIS 7) nel sito [!INCLUDE[msCoName](../includes/msconame-md.md)] TechNet.|  
|**Indirizzo IP**|Selezionare un indirizzo IP che può essere utilizzato dagli utenti per accedere al sito. Per impostazione predefinita, è selezionata l'opzione **Non assegnati** . A meno che non esista un motivo particolare per utilizzare un indirizzo IPv4 o un indirizzo IPv6 specifico, è consigliabile utilizzare il valore predefinito.<br /><br /> Con l'opzione **Non assegnati**, il sito risponde alle richieste per tutti gli indirizzi IP sulla porta e il nome host facoltativo specificato. Se un altro sito nel server ha un'associazione sulla stessa porta ma con un indirizzo IP specifico, il sito riceverà le richieste HTTP sulla porta e all'indirizzo IP specifico, mentre il sito con l'indirizzo IP impostato su **Non assegnati** riceverà tutte le altre richieste HTTP sulla porta e sugli altri indirizzi IP.|  
|**Porta**|Digitare la porta per le richieste effettuate al sito Web. Se si seleziona il protocollo HTTP, la porta predefinita è 80. Se si specifica una porta diversa dalle porte predefinite, per connettersi al sito Web è necessario che i client specifichino il numero di porta.<br /><br /> Nota: il **sito Web predefinito** in IIS è configurato per usare il protocollo HTTP sulla porta 80 con tutti gli indirizzi IP non assegnati. Se si tenta di creare il sito Web in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] con le informazioni di associazione predefinite, si riceve un errore di associazione duplicata esistente. In tal caso, è necessario modificare le informazioni di associazione per il sito in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]oppure modificare le informazioni di associazione per il sito Web predefinito tramite uno strumento di IIS, ad esempio Gestione IIS. In alternativa, è possibile specificare un'intestazione host per consentire a IIS di identificare in modo univoco il sito Web. Assicurarsi di configurare il firewall in modo che il traffico venga accettato sulla porta specificata.|  
|**Intestazione host**|Valore facoltativo. Digitare un nome per l'intestazione host. Utilizzare questa opzione quando si desidera assegnare un nome host, noto anche come nome di dominio, a un computer che utilizza un singolo indirizzo IP o una singola porta. Quando si specifica un nome host, per accedere al sito Web è necessario che i client utilizzino tale nome anziché l'indirizzo IP. Quando si configura un nome host, non è possibile aprire il sito in un Web browser, a meno che il server DNS non disponga di una voce per tale nome host.<br /><br /> Se ad esempio si vuole che gli utenti accedano al sito all'indirizzo `http://www.contoso.com/` è necessario specificare www.contoso.com come nome host e il server DNS deve avere una voce corrispondente.<br /><br /> Se il sito Web è disponibile in una Intranet, non è necessario specificare un nome host se gli utenti digitano il nome del server in un browser, ad esempio `http://server_name`. Tuttavia, se il server DNS nell'ambiente in uso è configurato per archiviare altri nomi per il server Web, sarà possibile creare un'associazione distinta per ogni nome host, in modo che gli utenti possano utilizzare gli altri nomi archiviati dal server DNS. Se è necessario configurare più nomi host per il sito, utilizzare uno strumento di IIS, ad esempio Gestione IIS, per aggiungere ulteriori associazioni di sito.|  
  
## <a name="application-pool"></a>Pool di applicazioni  
  
|Nome del controllo|Descrizione|  
|------------------|-----------------|  
|**Nome**|Digitare un nome univoco descrittivo per un nuovo pool di applicazioni oppure utilizzare il nome predefinito fornito. L'applicazione Web radice per il sito Web è in esecuzione in questo pool di applicazioni.<br /><br /> I pool di applicazioni definiscono limiti che impediscono alle applicazioni incluse in un pool di applicazioni di influire sulle applicazioni incluse in un altro pool di applicazioni.|  
|**Nome utente**|Digitare un dominio e il nome utente di Active Directory. Questo account è l'identità del pool di applicazioni in cui viene eseguita l'applicazione Web.<br /><br /> Questo account viene aggiunto al ruolo del database mds_exec nel database [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] per l'accesso al database. Per altre informazioni, vedere [Account di accesso, utenti e ruoli di database &#40;Master Data Services&#41;](database-logins-users-and-roles-master-data-services.md). Viene inoltre aggiunto a un gruppo di Windows [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , **MDS_ServiceAccounts**, a cui viene concessa l'autorizzazione per la directory di compilazione temporanea, **MDSTempDir**, nel file system. Per altre informazioni, vedere [Autorizzazioni per file e cartelle &#40;Master Data Services&#41;](../../2014/master-data-services/folder-and-file-permissions-master-data-services.md).|  
|**Password**|Digitare la password per l'account utente specificato.|  
|**Conferma password**|Ridigitare la password per l'account utente specificato. I campi **Password** e **Conferma password** devono contenere la stessa password.|  
  
## <a name="see-also"></a>Vedere anche  
 [Pagina di configurazione Web &#40;Gestione configurazione Master Data Services&#41;](../../2014/master-data-services/web-configuration-page-master-data-services-configuration-manager.md)   
 [Configurare il database e il sito Web per Master Data Services](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Requisiti delle applicazioni Web &#40;Master Data Services&#41;](install-windows/web-application-requirements-master-data-services.md)   
 [Creare un'applicazione Web Gestione dati master &#40;Master Data Services&#41;](install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
