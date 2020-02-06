---
title: Eseguire simultaneamente istruzioni su più server
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- executing queries against multiple servers
- queries [SQL Server], multiserver
ms.assetid: 197760f3-0a06-43de-8162-69c27d3fbe56
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 07/18/2016
ms.openlocfilehash: 89e6e64f4e4dc5f3ae7c8f9adf1db3a392530989
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75246557"
---
# <a name="execute-statements-against-multiple-servers-simultaneously"></a>Eseguire simultaneamente istruzioni su più server

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

In questo argomento viene descritto come eseguire una query su più server contemporaneamente in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]creando un gruppo di server locali, o un server di gestione centrale e uno o più gruppi di server, e uno o più server registrati all'interno dei gruppi, quindi eseguendo la query sul gruppo completo. 

I risultati restituiti dalla query possono essere riuniti in un unico riquadro dei risultati oppure possono essere restituiti in riquadri dei risultati separati. Il set di risultati può includere colonne aggiuntive per il nome del server e l'account di accesso usati dalla query in ciascun server. I server di gestione centrale e i server subordinati possono essere registrati solo tramite l'autenticazione di Windows. I server inclusi nei gruppi di server locali possono essere registrati tramite l'autenticazione di Windows o l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> **NOTA** Prima di eseguire le procedure seguenti, creare un server di gestione centrale e un gruppo di server. Per altre informazioni, vedere [Creazione di un server di gestione centrale e di un gruppo di server &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md).  

  
##  <a name="Permissions"></a> Autorizzazioni  
 Poiché le connessioni gestite da un server di gestione centrale vengono eseguite nel contesto dell'utente, l'utilizzo dell'autenticazione di Windows comporta la possibile variazione delle autorizzazioni effettive per i server registrati. L'utente, ad esempio, potrebbe essere un membro del ruolo predefinito del server sysadmin nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A, ma disporre di autorizzazioni limitate per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] B.  
  
 ## <a name="execute-statements-against-multiple-configuration-targets-simultaneously"></a>Eseguire istruzioni su più destinazioni di configurazione simultaneamente  

1.  In SQL Server Management Studio nel menu **Visualizza** fare clic su **Server registrati**.  
  
2.  Espandere un server di gestione centrale, fare clic con il pulsante destro del mouse su un gruppo di server, scegliere **Connetti**, quindi fare clic su **Nuova query**.  
  
3.  Nell'editor di query digitare ed eseguire un'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] , ad esempio la seguente:  
  
    ```  
    USE master  
    GO  
    SELECT * FROM sysdatabases;  
    GO  
    ```  
  
     Per impostazione predefinita, il riquadro dei risultati combinerà i risultati della query restituiti da tutti i server inclusi nel gruppo di server.  
  
#### <a name="to-change-the-multiserver-results-options"></a>Per modificare le opzioni dei risultati multiserver  
  
1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], scegliere **Opzioni** dal menu **Strumenti**.  
  
2.  Espandere **Risultati query**, espandere **SQL Server**, quindi fare clic su **Risultati multiserver**.  
  
3.  Nella pagina **Risultati multiserver** specificare le impostazioni desiderate per le opzioni, quindi scegliere **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrare più server tramite server di gestione centrale](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
