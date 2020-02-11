---
title: Disinstallare e rimuovere Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: efc2431c-588b-42e7-b23b-c875145a33f6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e9bac4dba698af6e7f3dc57904da66a7fb15a08b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62989043"
---
# <a name="uninstall-and-remove-master-data-services"></a>Disinstallare e rimuovere Master Data Services
  Per disinstallare la funzionalità [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] da un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seguire i passaggi in [Disinstallare un'istanza esistente di SQL Server &#40;programma di installazione&#41;](../../../2014/sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md) e specificare [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] come funzionalità da rimuovere nella pagina **Seleziona funzionalità**. Il processo di disinstallazione rimuove cartelle e file di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] e disinstalla [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] dal computer locale.  
  
 Per impedire la perdita di dati ed evitare di influire su altri computer nel sistema, alcuni elementi non vengono rimossi o modificati dal processo di disinstallazione. Esaminare la tabella seguente per determinare se lasciare o rimuovere elementi.  
  
|Elemento|Descrizione|  
|----------|-----------------|  
|File e cartelle|Il processo di disinstallazione rimuove la maggior parte di file e cartelle dal percorso di installazione.<br /><br /> Il processo di disinstallazione non rimuove le cartelle Master Data Services e MDSTempDir dal percorso di installazione. Una volta completato il processo di disinstallazione, è possibile eliminare manualmente queste cartelle dal file system. Per altre informazioni, vedere [Autorizzazioni per file e cartelle &#40;Master Data Services&#41;](../../master-data-services/folder-and-file-permissions-master-data-services.md).|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] assembly|Il processo di disinstallazione rimuove gli assembly di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] dalla Global Assembly Cache (GAC).|  
|Database|Il processo di disinstallazione non influisce sul database [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] . Il database rimane invariato nell'istanza di [!INCLUDE[ssDE](../../includes/ssde-md.md)] in modo da evitare perdite di dati, inclusi dati master, oggetti modello, autorizzazioni per utenti e gruppi, regole business e così via.<br /><br /> È possibile eliminare il database dall'istanza di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] che lo ospita, se non è necessario e non si prevede di connetterlo in futuro a un altro sito Web o un'altra applicazione [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Per altre informazioni, vedere [Eliminare un database](../../relational-databases/databases/delete-a-database.md).|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] e Web.config|Il processo di disinstallazione rimuove la cartella WebApplication dal file system. La cartella WebApplication contiene i file dell'applicazione Web e il file Web.config per [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)].<br /><br /> **\*\* Importante \*\*** Prima di procedere alla disinstallazione, è possibile copiare il file Web.config in un altro percorso per mantenere eventuali impostazioni personalizzate o altre informazioni contenute nel file. Una volta completato il processo di disinstallazione, il file Web.config non potrà essere recuperato.|  
|Elementi di Internet Information Services (IIS)|Il processo di disinstallazione non influisce su pool di applicazioni, siti Web o applicazioni Web in IIS sul computer locale. Dal momento che il processo di disinstallazione rimuove la cartella WebApplication e il file Web.config per [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)], qualsiasi applicazione Web [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] che richieda tali file non renderà più disponibile alcun contenuto. Se gli utenti tentano di accedere all'applicazione Web, riceveranno il messaggio Errore HTTP 500.19 - Errore interno del server: "Impossibile accedere alla pagina richiesta perché i dati di configurazione per la pagina non sono validi".<br /><br /> Se il sito Web o l'applicazione e il pool di applicazioni che rende disponibile il sito o l'applicazione non sono più necessari, è possibile utilizzare un strumento di IIS per eliminarli. Per altre informazioni, vedere la [Guida operativa di IIS 7](https://go.microsoft.com/fwlink/?LinkId=184885) su [!INCLUDE[msCoName](../../includes/msconame-md.md)] TechNet.|  
|Gruppo**MDS_ServiceAccounts**|Una volta completato il processo di disinstallazione, rimangono nel sistema il gruppo di Windows **MDS_ServiceAccounts** e qualsiasi account di servizio aggiunto al gruppo. Se il gruppo e gli account sono più necessari, è possibile rimuoverli.|  
|Registro|Tramite il processo di disinstallazione vengono rimosse tutte le chiavi del Registro di sistema di [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] dal Registro di sistema di Windows.|  
  
## <a name="see-also"></a>Vedere anche  
 [Installazione di Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
