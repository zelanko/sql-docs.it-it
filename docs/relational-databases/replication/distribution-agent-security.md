---
title: Sicurezza agente di distribuzione | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.DA.f1
helpviewer_keywords:
- Distribution Agent Security dialog box
ms.assetid: de40cc21-2e58-4464-9be7-b5b90c925e9b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: 08a4a90580a00e3ab4f2c38c7dfa3cf81b331d08
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768624"
---
# <a name="distribution-agent-security"></a>Sicurezza agente di distribuzione
::: moniker range=">=sql-server-2014||=sqlallproducts-allversions" 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
La finestra di dialogo **Sicurezza agente di distribuzione** consente di specificare l'account di Windows utilizzato per l'esecuzione dell'agente di distribuzione. L'agente di distribuzione viene eseguito nel server di distribuzione per le sottoscrizioni push e nel Sottoscrittore per le sottoscrizioni pull. L'account di Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] è detto anche *account di processo*, poiché si tratta dell'account con cui viene eseguito il processo dell'agente. Le opzioni aggiuntive disponibili in questa finestra di dialogo dipendono dalla modalità con cui si accede a tale finestra di dialogo:  
  
-   Se si accede alla finestra di dialogo dalla Creazione guidata nuova sottoscrizione, è possibile specificare il contesto in cui l'agente di distribuzione stabilisce le connessioni al Sottoscrittore (per le sottoscrizioni push) o al server di distribuzione (per le sottoscrizioni pull). La connessione può essere stabilita tramite la rappresentazione dell'account di Windows o nel contesto di un account di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificato dall'utente.  
  
-   Se si accede alla finestra di dialogo dalla finestra di dialogo **Proprietà sottoscrizione** , è possibile specificare il contesto in cui l'agente di distribuzione stabilisce le connessioni facendo clic sul pulsante delle proprietà ( **...** ) nella riga **Connessione al Sottoscrittore** o **Connessione server di distribuzione** della finestra. Per altre informazioni sull'accesso alla finestra di dialogo **Proprietà sottoscrizione**, vedere [Visualizzare e modificare le proprietà delle sottoscrizioni push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e [Visualizzare e modificare le proprietà delle sottoscrizioni pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 Tutti gli account devono essere validi e per ogni account deve essere stata specificata la password corretta. Gli account e le password vengono convalidati solo dopo l'avvio dell'esecuzione di un agente.  
  
## <a name="options"></a>Opzioni  
 **Process Account**  
 Consente di immettere un account di Windows utilizzato per l'esecuzione dell'agente di distribuzione:  
  
-   Per le sottoscrizioni push, l'account deve:  
  
    -   Essere almeno un membro del ruolo predefinito del database **db_owner** nel database di distribuzione.  
  
    -   Essere un membro dell'elenco di accesso alla pubblicazione.  
  
    -   Disporre delle autorizzazioni di lettura per la condivisione snapshot.  
  
    -   Disporre delle autorizzazioni di lettura per la directory di installazione del provider OLE DB per il Sottoscrittore se la sottoscrizione riguarda un Sottoscrittore non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Per le sottoscrizioni pull, l'account deve essere almeno un membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione.  
  
 Sono necessarie autorizzazioni aggiuntive nel caso in cui l'account di processo sia rappresentato durante l'attivazione delle connessioni. Vedere le sezioni **Connetti al server di distribuzione** e **Connetti al Sottoscrittore** seguenti.  
  
 Non è possibile specificare **l'account di processo** per le sottoscrizioni pull di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], poiché l'agente di distribuzione non viene eseguito nelle istanze di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
 **Password** e **Conferma password**  
 Immettere la password per l'account di Windows.  
  
 **Connetti al server di distribuzione**  
 Per le sottoscrizioni push, le connessioni al server di distribuzione vengono stabilite sempre tramite la rappresentazione dell'account specificato nella casella di testo **Account processo** .  
  
 Per le sottoscrizioni pull, specificare se l'agente di distribuzione deve stabilire connessioni al server di distribuzione tramite la rappresentazione dell'account specificato nella casella di testo **Account processo** o tramite un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se si seleziona l'opzione per l'utilizzo di un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , immettere un account di accesso e una password di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  È consigliabile scegliere di rappresentare l'account di Windows anziché di utilizzare un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 L'account di Windows o l'account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato per la connessione deve:  
  
-   Essere un membro del ruolo PAL.  
  
-   Disporre delle autorizzazioni di lettura per la condivisione snapshot.  
  
 **Connetti al Sottoscrittore**  
 Per le sottoscrizioni pull, le connessioni al Sottoscrittore vengono sempre stabilite tramite la rappresentazione dell'account specificato nella casella di testo **Account processo** .  
  
 Per le sottoscrizioni push le opzioni sono diverse per i Sottoscrittori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   Per i Sottoscrittori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] selezionare se l'agente di distribuzione deve stabilire connessioni al Sottoscrittore tramite la rappresentazione dell'account specificato nella casella di testo **Account processo** o tramite un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se si seleziona l'opzione per l'utilizzo di un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , immettere un account di accesso e una password di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    > [!NOTE]  
    >  È consigliabile scegliere di rappresentare l'account di Windows anziché di utilizzare un account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     L'account di Windows o l'account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzato per la connessione deve essere almeno un membro del ruolo del database predefinito **db_owner** nel database di sottoscrizione.  
  
-   Per i Sottoscrittori non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare l'account di accesso al database nel Sottoscrittore da utilizzare quando l'agente di distribuzione si connette al Sottoscrittore. L'account di accesso deve disporre di autorizzazioni sufficienti per creare oggetti nel database di sottoscrizione. Per altre informazioni sulla configurazione di Sottoscrittori non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Creare una sottoscrizione per un Sottoscrittore non SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
 **Opzioni di connessione aggiuntive**  
 Solo per Sottoscrittori non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Specificare le opzioni di connessione per il Sottoscrittore sotto forma di una stringa di connessione (Oracle non richiede opzioni aggiuntive). Le opzioni devono essere separate dal punto e virgola. L'esempio seguente illustra una stringa di connessione IBM DB2 (le interruzioni di riga sono state inserite per favorire la leggibilità):  
  
```  
Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
Persist Security Info=False;Connection Pooling=True;  
```  
  
 La maggior parte delle opzioni nella stringa è specifica per il server DB2 configurato, ma è necessario che l'opzione **Process Binary as Character** sia sempre impostata su **False**. È necessario specificare un valore per l'opzione **Initial Catalog** per identificare il database di sottoscrizione. Per altre informazioni, vedere [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Controllo di identità e accesso (replica)](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Modello di sicurezza dell'agente di replica](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Panoramica degli agenti di replica](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Sottoscrizione delle pubblicazioni](../../relational-databases/replication/subscribe-to-publications.md)  
::: moniker-end
  
::: monikerRange="azuresqldb-mi-current"
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
La finestra di dialogo **Sicurezza agente di distribuzione** consente di specificare l'account di autenticazione di SQL Server usato per l'esecuzione dell'agente di distribuzione. L'agente di distribuzione viene eseguito nel server di distribuzione per le sottoscrizioni push e nel Sottoscrittore per le sottoscrizioni pull.  Le opzioni aggiuntive disponibili in questa finestra di dialogo dipendono dalla modalità con cui si accede a tale finestra di dialogo:  
  
-   Se si accede alla finestra di dialogo dalla Creazione guidata nuova sottoscrizione, è possibile specificare il contesto in cui l'agente di distribuzione stabilisce le connessioni al Sottoscrittore (per le sottoscrizioni push) o al server di distribuzione (per le sottoscrizioni pull). La connessione deve essere eseguita usando un account di autenticazione di SQL Server. 
  
-   Se si accede alla finestra di dialogo dalla finestra di dialogo **Proprietà sottoscrizione** , è possibile specificare il contesto in cui l'agente di distribuzione stabilisce le connessioni facendo clic sul pulsante delle proprietà ( **...** ) nella riga **Connessione al Sottoscrittore** o **Connessione server di distribuzione** della finestra. Per altre informazioni sull'accesso alla finestra di dialogo **Proprietà sottoscrizione**, vedere [Visualizzare e modificare le proprietà delle sottoscrizioni push](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) e [Visualizzare e modificare le proprietà delle sottoscrizioni pull](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 Tutti gli account devono essere validi e per ogni account deve essere stata specificata la password corretta. Gli account e le password vengono convalidati solo dopo l'avvio dell'esecuzione di un agente.  
  
## <a name="options"></a>Opzioni  
 **Process Account**  
 Immettere un account di autenticazione di SQL Server per l'esecuzione dell'agente di distribuzione:  
  
-   Per le sottoscrizioni push, l'account deve:  
  
    -   Essere almeno un membro del ruolo predefinito del database **db_owner** nel database di distribuzione.  
  
    -   Essere un membro dell'elenco di accesso alla pubblicazione.  
  
    -   Disporre delle autorizzazioni di lettura per la condivisione snapshot.  
  
    -   Disporre delle autorizzazioni di lettura per la directory di installazione del provider OLE DB per il Sottoscrittore se la sottoscrizione riguarda un Sottoscrittore non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Per le sottoscrizioni pull, l'account deve essere almeno un membro del ruolo predefinito del database **db_owner** nel database di sottoscrizione.  
  
    
**Password** e **Conferma password**  
Immettere la password per l'account di Windows.  
  
**Connetti al server di distribuzione**  
Per le sottoscrizioni push, le connessioni al server di distribuzione vengono stabilite sempre tramite la rappresentazione dell'account specificato nella casella di testo **Account processo** .  
  
Per le sottoscrizioni pull, specificare se l'agente di distribuzione deve stabilire connessioni al server di distribuzione tramite la rappresentazione dell'account specificato nella casella di testo **Account processo** o tramite un account di autenticazione di SQL Server. 
  
  
 **Connetti al Sottoscrittore**  
 Per le sottoscrizioni pull, le connessioni al Sottoscrittore vengono sempre stabilite tramite la rappresentazione dell'account specificato nella casella di testo **Account processo** .  
  
 Per le sottoscrizioni push le opzioni sono diverse per i Sottoscrittori [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :

  
-   Per i Sottoscrittori non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , specificare l'account di accesso al database nel Sottoscrittore da utilizzare quando l'agente di distribuzione si connette al Sottoscrittore. L'account di accesso deve disporre di autorizzazioni sufficienti per creare oggetti nel database di sottoscrizione. Per altre informazioni sulla configurazione di Sottoscrittori non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Creare una sottoscrizione per un Sottoscrittore non SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
 **Opzioni di connessione aggiuntive**  
 Solo per Sottoscrittori non[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Specificare le opzioni di connessione per il Sottoscrittore sotto forma di una stringa di connessione (Oracle non richiede opzioni aggiuntive). Le opzioni devono essere separate dal punto e virgola. L'esempio seguente illustra una stringa di connessione IBM DB2 (le interruzioni di riga sono state inserite per favorire la leggibilità):  
  
```  
Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
Persist Security Info=False;Connection Pooling=True;  
```  
  
 La maggior parte delle opzioni nella stringa è specifica per il server DB2 configurato, ma è necessario che l'opzione **Process Binary as Character** sia sempre impostata su **False**. È necessario specificare un valore per l'opzione **Initial Catalog** per identificare il database di sottoscrizione. Per altre informazioni, vedere [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Replica transazionale con il database SQL di Azure](/azure/sql-database/sql-database-managed-instance-transactional-replication) [Configurare la replica per un'istanza gestita](/azure/sql-database/replication-with-sql-database-managed-instance)
::: moniker-end


