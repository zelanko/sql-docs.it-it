---
title: Impostare l'account del servizio per l'Utilità di avvio del daemon filtri full-text
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], FDHOST Launcher (MSSQLFDLauncher) service account
- FDHOST Launcher (MSSQLFDLauncher) [SQL Server]
ms.assetid: 3ab1d101-7ae0-488f-9b57-468e2517b737
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-lt-2019
ms.openlocfilehash: eed8020872b3d2a3babc0581054bef0dbed64a4d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "74055944"
---
# <a name="set-the-service-account-for-the-full-text-filter-daemon-launcher"></a>Impostazione dell'account del servizio dell'Utilità di avvio del daemon di filtri full-text
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
 Questo argomento descrive come impostare o modificare l'account del servizio Utilità di avvio del daemon filtri full-text di SQL (MSSQLFDLauncher) tramite Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'account di servizio predefinito usato dal programma di installazione di SQL Server è `NT Service\MSSQLFDLauncher`.
  
  
## <a name="about-the-sql-full-text-filter-daemon-launcher-service"></a>Informazioni sul servizio Utilità di avvio del daemon filtri full-text di SQL
Il servizio Utilità di avvio del daemon filtri full-text di SQL viene usato dalla ricerca full-text di SQL Server per avviare il processo host del daemon di filtri che gestisce il word breaking e l'applicazione di filtri per la ricerca full-text. Per usare la ricerca full-text, questo servizio deve essere in esecuzione.  
  
Il servizio Utilità di avvio del daemon filtri full-text di SQL è un servizio specifico dell'istanza associato a una determinata istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Tale servizio propaga le informazioni sull'account del servizio a ogni processo host del daemon di filtri che avvia.  

##  <a name="setting"></a> Impostare l'account del servizio  
  
1.  Nel menu **Start** scegliere **Tutti i programmi**, espandere [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)] e quindi fare clic su **Gestione configurazione SQL Server 2016**.  
  
2.  In **Gestione configurazione SQL Server**, fare clic su **Servizi di SQL Server**, fare clic con il pulsante destro del mouse su **Utilità di avvio del daemon filtri full-text di SQL (** _nome istanza_ **)** , quindi scegliere **Proprietà**.  
  
3.  Fare clic sulla scheda **Accesso** della finestra di dialogo e quindi selezionare o immettere l'account con il quale eseguire i processi avviati dal servizio Utilità di avvio del daemon filtri full-text di SQL.  
  
4.  Dopo avere chiuso la finestra di dialogo, fare clic su **Riavvia** per riavviare il servizio Utilità di avvio del daemon filtri full-text di SQL.  
  
![Proprietà del processo di avvio del daemon filtri full-text di SQL](../../relational-databases/search/media/sql-full-text-filter-daemon-launch-process-properties.png)
  
##  <a name="error"></a> Risolvere i problemi di avvio del servizio Utilità di avvio del daemon filtri full-text di SQL  
 Se il servizio Utilità di avvio del daemon filtri full-text di SQL non viene avviato, verificare le possibili cause seguenti:  
  
### <a name="permissions-issues"></a>Problemi con le autorizzazioni
-   Il gruppo di servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non dispone dell'autorizzazione necessaria per avviare il servizio Utilità di avvio del daemon filtri full-text di SQL.  

     Assicurarsi che il gruppo di servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] abbia le autorizzazioni necessarie per l'account del servizio Utilità di avvio del daemon filtri full-text di SQL. Durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], al gruppo di servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene concessa l'autorizzazione predefinita per gestire, eseguire query sul e avviare il servizio Utilità di avvio del daemon filtri full-text di SQL. Se le autorizzazioni del gruppo di servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per l'account del servizio Utilità di avvio del daemon filtri full-text sono state rimosse dopo l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , questo servizio non viene avviato e la ricerca full-text viene disabilitata.     

-   L'account utilizzato per accedere al servizio non dispone di privilegi.  
  
     È possibile che sia in uso un account senza i privilegi di accesso nel computer in cui è installata l'istanza del server. Assicurarsi di accedere con un account che disponga di diritti e autorizzazioni utente nel computer locale.  

### <a name="service-account-and-password-issues"></a>Problemi relativi ad account del servizio e password
-   La password o l'account utente dell'account del servizio non è corretto.  
  
     In Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 assicurarsi che il servizio usi l'account del servizio e la password corretti.  
  
-   La password associata all'account del servizio Utilità di avvio del daemon filtri full-text di SQL è scaduta.  
  
     Se si usa un account utente locale per il servizio Utilità di avvio del daemon filtri full-text di SQL e la password scade, è necessario:  
  
    1.  Impostare una nuova password di Windows per l'account.  
  
    2.  Aggiornare il servizio Utilità di avvio del daemon filtri full-text di SQL per usare la nuova password in Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016.  
  
### <a name="named-pipes-configuration-issues"></a>Problemi relativi alla configurazione delle named pipe
-   Il servizio Utilità di avvio del daemon filtri full-text di SQL non è configurato correttamente.  
  
     Se la funzionalità delle named pipe è stata disabilitata nel computer locale o se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è stato configurato per l'utilizzo di una named pipe diversa da quella predefinita, il servizio Utilità di avvio del daemon filtri full-text di SQL potrebbe non essere avviato.  
  
-   Un'altra istanza della stessa named pipe è già in esecuzione.  
  
     Il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funge da server named pipe per il client del servizio Utilità di avvio del daemon filtri full-text di SQL. Se la named pipe è già stata creata da un altro processo prima dell'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , viene registrato un errore nel log degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e nel registro eventi di Windows e la ricerca full-text non è disponibile.  Individuare il processo o l'applicazione che tenta di utilizzare la stessa named pipe e arrestare l'applicazione.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per la gestione dei servizi &#40;Gestione configurazione SQL Server&#41;](https://msdn.microsoft.com/library/78dee169-df0c-4c95-9af7-bf033bc9fdc6)   
 [Aggiornare la ricerca full-text](../../relational-databases/search/upgrade-full-text-search.md)  
  
  
