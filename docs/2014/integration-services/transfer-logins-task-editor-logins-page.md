---
title: Editor attività Trasferisci account di accesso (pagina account di accesso) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins Task Editor
ms.assetid: bf244c24-bd45-4ece-b66b-78b488f35c5b
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 67c81901e454c4e7a47e5d448f2aa17d6a8820fa
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972811"
---
# <a name="transfer-logins-task-editor-logins-page"></a>Editor attività Trasferisci account di accesso (pagina Account di accesso)
  Usare la pagina **Account di accesso** della finestra di dialogo **Editor attività Trasferisci account di accesso** per impostare le proprietà per la copia di uno o più account di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a un altra. Per altre informazioni su questa attività, vedere [Attività Trasferisci account di accesso](control-flow/transfer-logins-task.md).  
  
> [!IMPORTANT]  
>  Durante l'esecuzione di questa attività, sul server di destinazione vengono creati gli account di accesso con password casuali e le password vengono disabilitate. Per usare questi account di accesso, è necessario che un membro del ruolo predefinito del server **sysadmin** cambi le password e quindi le attivi. L'account di accesso **sa** non può essere trasferito.  
  
## <a name="options"></a>Opzioni  
 **SourceConnection**  
 Selezionare una gestione connessione SMO nell'elenco oppure fare clic su **\<New connection...>** per creare una nuova connessione al server di origine.  
  
 **DestinationConnection**  
 Selezionare una gestione connessione SMO nell'elenco oppure fare clic su **\<New connection...>** per creare una nuova connessione al server di destinazione.  
  
 **LoginsToTransfer**  
 Consente di selezionare gli account di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da copiare dal server di origine a quello di destinazione. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Description|  
|-----------|-----------------|  
|**AllLogins**|Tutti gli account di accesso di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nel server di origine verranno copiati in quello di destinazione.|  
|**SelectedLogins**|Solo gli account di accesso specificati in **LoginsList** verranno copiati nel server di destinazione.|  
|**AllLoginsFromSelectedDatabases**|Tutti gli account di accesso nel database specificato in **DatabasesList** verranno copiati nel server di destinazione.|  
  
 **LoginsList**  
 Consente di selezionare gli account di accesso nel server di origine da copiare in quello di destinazione. Questa opzione è disponibile solo se è selezionata **SelectedLogins** per **LoginsToTransfer**.  
  
 **DatabasesList**  
 Consente di selezionare i database nel server di origine contenenti gli account di accesso da copiare sul server di destinazione. Questa opzione è disponibile solo se è selezionata **AllLoginsFromSelectedDatabases** per **LoginsToTransfer**.  
  
 **IfObjectExists**  
 Consente di selezionare la modalità di gestione dei nomi già esistenti nel server di destinazione da parte dell'attività  
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente:  
  
|valore|Description|  
|-----------|-----------------|  
|**FailTask**|L'attività ha esito negativo se esistono già account di accesso con lo stesso nome nel server di destinazione.|  
|**Sovrascrivere**|L'attività sovrascrive gli account di accesso con lo stesso nome nel server di destinazione.|  
|**Ignora**|L'attività ignora gli account di accesso con lo stesso nome nel server di destinazione.|  
  
 **CopySids**  
 Consente di indicare se gli identificatori di sicurezza associati agli account di accesso devono essere copiati sul server di destinazione. L'opzione**CopySids** deve essere impostata su **True** se l'attività Trasferisci account di accesso viene usata contestualmente all'attività Trasferisci database. In caso contrario, gli account di accesso copiati non verranno riconosciuti dal database trasferito.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Attività Integration Services](control-flow/integration-services-tasks.md)   
 [Editor attività Trasferisci account di accesso &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Pagina espressioni](expressions/expressions-page.md)   
 [Gestione connessione SMO](connection-manager/smo-connection-manager.md)   
 [Password complesse](../relational-databases/security/strong-passwords.md)   
 [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  
