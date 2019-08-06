---
title: Database host in un'istanza gestita | Microsoft Docs
description: Viene descritto come configurare un database MDS in un'istanza gestita.
ms.custom: ''
ms.date: 07/01/2019
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19519697-c219-44a8-9339-ee1b02545445
author: v-redu
ms.author: lle
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b4ca791a1a0ce46929f4d409d234f8dbc7efdec3
ms.sourcegitcommit: bcc3b2c7474297aba17b7a63b17c103febdd0af9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/05/2019
ms.locfileid: "68794926"
---
# <a name="host-database-on-managed-instance"></a>Database host nell'istanza gestita

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Questo articolo illustra come configurare un database MDS in un'istanza gestita.
  
## <a name="preparation"></a>Preparazione

Per la preparazione, è necessario completare i passaggi seguenti.
- Terminare la creazione e la configurazione dell'istanza gestita. Includere la rete virtuale e la VPN da punto a sito.
- Completare la configurazione del computer dell'applicazione Web.
  - Includere la VPN da punto a sito di installazione.
  - Installare ruoli e funzionalità.

**Lato database:**

1. Creare un'istanza gestita di database SQL di Azure include rete virtuale. [Avvio rapido: Creare un'istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-get-started)
2. Configurare una connessione da punto a sito. [Configurare una connessione da punto a sito a una VNet usando l'autenticazione del certificato nativa di Azure: portale di Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
3. Configurare Azure Active Directory autenticazione con istanza gestita di database SQL. [Configurare e gestire l'autenticazione Azure Active Directory con SQL](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)

**Lato computer applicazione Web:**

1. Installare il certificato di connessione da punto a sito e la VPN per assicurarsi che il computer possa accedere all'istanza gestita di database SQL. [Configurare una connessione da punto a sito a una VNet usando l'autenticazione del certificato nativa di Azure: portale di Azure](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal)
2. Installare il ruolo e le funzionalità. Sono necessarie le funzionalità seguenti.

- Ruoli

      Internet Information Services
      Web Management Tools
      IIS Management Console
      World Wide Web Services
      Application Development
      .NET Extensibility 3.5
      .NET Extensibility 4.5
      ASP.NET 3.5
      ASP.NET 4.5
      ISAPI Extensions
      ISAPI Filters
      Common HTTP Features
      Default Document
      Directory Browsing
      HTTP Errors
      Static Content
      [Note: Do not install WebDAV Publishing]
      Health and Diagnostics
      HTTP Logging
      Request Monitor
      Performance
      Static Content Compression
      Security
      Request Filtering
      Windows Authentication

- Funzionalità:

      .NET Framework 3.5 (includes .NET 2.0 and 3.0)
      .NET Framework 4.5 Advanced Services
      ASP.NET 4.5
      WCF Services
      HTTP Activation [Note: This is required.]
      TCP Port Sharing
      Windows Process Activation Service
      Process Model
      .NET Environment
      Configuration APIs
      Dynamic Content Compression

## <a name="install-and-configure-includessmdsshort_mdincludesssmdsshort-mdmd-web-application"></a>Installare e configurare [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] l'applicazione Web

Per installare e configurare [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)], è necessario completare i passaggi seguenti.

1. Installare la funzionalità di [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] inclusione SQL Server 2019.
2. Creare un [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] database nell'istanza di gestione.
3. Creare e configurare l'applicazione Web [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]per.
  
**Installare SQL Server 2019**

Utilizzare l'installazione guidata di SQL Server o un prompt dei comandi per installare [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)].

1. Fare doppio clic su Setup.exe e seguire i passaggi dell'installazione guidata.

2. Selezionare [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] nella pagina Selezione funzionalità in funzionalità condivise.
Vengono installati [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], gli assembly, uno snap-in di Windows PowerShell, nonché cartelle e file per i servizi e le applicazioni Web.

    ![MDS-SQLServer2019-config-mi-SQLFeatureSelection](../master-data-services/media/mds-sqlserver2019-config-mi-sqlfeatureselection.png "MDS-SQLServer2019-config-MI_SQLFeatureSelection")  

**Impostazione del database e del sito Web**

1. Connettere la rete virtuale di Windows Azure per assicurarsi che sia possibile connettersi all'istanza gestita.

    ![MDS-SQLServer2019-config-mi-P2SVPNConnect](../master-data-services/media/mds-sqlserver2019-config-mi-p2svpnconnect.png "MDS-SQLServer2019-config-MI_P2SVPNConnect")  

2. Avviare il [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. E fare clic su **Configurazione database** nel riquadro sinistro.

3. Fare clic su **Crea database**, quindi fare clic su Avanti nella procedura guidata **Crea database** .

4. Nel **server di database** pagina, compilare l' **istanza di SQL Server** e selezionare il tipo di **autenticazione** , quindi fare clic su **Test connessione** per confermare che è possibile connettersi al database usando le credenziali per il tipo di autenticazione selezionato. Scegliere Avanti.

   > [!NOTE]
   > - Istanza di SQL Server per istanza gestita come "xxxxxxx.xxxxxxx.database.windows.net"
   > - Per istanza gestita, è supportato il tipo di autenticazione **"Account SQL Server"** e **"utente corrente – Active Directory integrato"** .
   > - Quando si seleziona **utente corrente-Active Directory integrato** come tipo di autenticazione, la casella **nome utente** è di sola lettura e visualizza il nome dell'account utente di Windows che ha eseguito l'accesso al computer. Se si esegue SQL Server 2019 [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] in una macchina virtuale (VM) di Azure, nella casella **nome utente** verranno visualizzati il nome della macchina virtuale e il nome utente per l'account amministratore locale nella VM.

    Assicurarsi che l'autenticazione contenga la regola **"sysadmin"** per l'istanza gestita.
![MDS-SQLServer2019-config-mi-CreateDBConnect](../master-data-services/media/mds-sqlserver2019-config-mi-createdbconnect.png "MDS-SQLServer2019-config-MI_CreateDBConnect")  

5. Digitare un nome nel campo **Nome database** . Facoltativamente, per selezionare regole di confronto di Windows, deselezionare la casella di controllo **Regole di confronto predefinite di SQL Server** e fare clic su una o più delle opzioni disponibili, ad esempio **Distinzione maiuscole/minuscole**. Fare clic su **Avanti**.

    ![MDS-SQLServer2019-config-mi-CreatedDBName](../master-data-services/media/mds-sqlserver2019-config-mi-createddbname.png "MDS-SQLServer2019-config-MI_CreatedDBName")  

6. Nel campo **nome utente** specificare l'account di Windows dell'utente che sarà l'utente con privilegi avanzati predefinito per [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]. L'utente con privilegi avanzati ha accesso a tutte le aree funzionali e può aggiungere, eliminare e aggiornare tutti i modelli.

    ![MDS-SQLServer2019-config-mi-CreateDBUserName](../master-data-services/media/mds-sqlserver2019-config-mi-createdbusername.png "MDS-SQLServer2019-config-MI_createDBUserName")

7. Fare clic su **Avanti** per visualizzare un riepilogo delle impostazioni per il database [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] e quindi fare di nuovo clic su **Avanti** per creare il database. Viene visualizzata la pagina **Continua e termina**.

8. Quando il database viene creato e configurato, fare clic su **Fine**.

    Per ulteriori informazioni sulle impostazioni della **procedura guidata Crea database**, vedere [creazione guidata &#40; [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] Database Configuration Manager&#41;](../master-data-services/create-database-wizard-master-data-services-configuration-manager.md).

9. Nella[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]pagina **Configurazione database** della fare clic su **Seleziona database**.

10. Fare clic su **Connetti**, [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] selezionare il database creato nel passaggio 8, quindi fare clic su **OK**.

    ![MDS-SQLServer2019-config-mi-connectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "MDS-SQLServer2019-config-MI_connectDBName")

11. In [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]fare clic su **Configurazione Web** nel riquadro sinistro.

12. Nella casella di riepilogo **Sito Web** fare clic su **Sito Web predefinito**e quindi fare clic su **Crea** per creare un'applicazione Web.
![MDS-SQLServer2019-config-mi-Webconfiguration](../master-data-services/media/mds-sqlserver2019-config-mi-webconfiguration.png "MDS-SQLServer2019-config-MI_WebConfiguration")

   > [!NOTE] 
   > Quando si seleziona **Sito Web predefinito**, è necessario creare un'applicazione Web. Se si seleziona **Crea nuovo sito Web** nella casella di riepilogo, l'applicazione viene creata automaticamente.

    

13. Nella sezione **pool di applicazioni** immettere un nome utente diverso, immettere la password e quindi fare clic su OK.
![MDS-SQLServer2019-config-mi-CreateWebApplication](../master-data-services/media/mds-sqlserver2019-config-mi-createwebapplication.png "MDS-SQLServer2019-config-MI_CreateWebApplication")

   > [!NOTE]
   > È necessario assicurarsi che l'utente possa accedere al database con Active Directory autenticazione integrata appena creata. In alternativa, è necessario modificare la connessione in Web. config in un secondo momento.

    

14. Per ulteriori informazioni sulla finestra di dialogo **Crea applicazione Web** , vedere finestra di [ &#40; [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] dialogo Crea applicazione Web&#41;Configuration Manager](../master-data-services/create-web-application-dialog-box-master-data-services-configuration-manager.md).

15. Nella pagina **configurazione Web** nella casella **applicazione Web** fare clic sull'applicazione creata e quindi fare clic su **Seleziona** nella sezione **associare l'applicazione al database** .

16. Fare clic su **Connetti**, selezionare il database [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] che si vuole associare all'applicazione Web e quindi fare clic su **OK**.

    L'impostazione del sito Web è stata completata. Nella pagina **configurazione Web** è ora visualizzato il sito Web selezionato, l'applicazione Web creata e il [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] database associato all'applicazione.

    ![MDS-SQLServer2019-config-mi-WebConfigSelectDB](../master-data-services/media/mds-sqlserver2019-config-mi-webconfigselectdb.png "MDS-SQLServer2019-config-MI_WebConfigSelectDB")

17. Fare clic su **Applica**. Viene visualizzata la finestra di messaggio **Configurazione completata**. Fare clic su **OK** nella finestra di messaggio per avviare l'applicazione Web. L'indirizzo del sito Web http://server è nome/applicazione Web/.

## <a name="other-authentication-type-to-connect-managed-instance-database-on-web-application"></a>Altro tipo di autenticazione per connettere il database dell'istanza gestita nell'applicazione Web

È possibile ottenere il file **Web. config** in C:\Programmi\Microsoft SQL Server\150\Master Data Services\WebApplication. È possibile modificare connectionString per modificare altro tipo di autenticazione per connettere il database dell'istanza gestita.

Il tipo di autenticazione predefinito è "**Active Directory Integrated**", che segue la stringa di connessione di esempio.

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Integrated&quot;" />
```

È supportata anche l'autenticazione Active Directory password e l'autenticazione SQL Server, che segue la stringa di connessione di esempio.

Autenticazione della password Active Directory

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;Authentication=&quot;Active Directory Password&quot; ; UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!" />
```

autenticazione di SQL Server

```xml
<add name="MDS1" connectionString="Data Source=*****.*****.database.windows.net;Initial Catalog=MasterDataServices;Integrated Security=False;Connect Timeout=60;User ID=UserName;Password=MyPassword!;" />
```

## <a name="upgrade-includessmdsshort_mdincludesssmdsshort-mdmd-and-database-version"></a>Aggiornamento [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] e versione del database

**Aggiornamento[!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)]**

Installare l' **aggiornamento cumulativo**di SQL Server 2019, [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] il verrà aggiornato automaticamente.

**Aggiornare la versione del database**

Se viene visualizzato il problema "la versione del client non è compatibile con la versione del database" dopo l'installazione SQL Server 2019 **aggiornamento cumulativo**, è necessario aggiornare la versione del database.

![MDS-SQLServer2019-config-mi-UpgradeDBPage](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbpage.png "MDS-SQLServer2019-config-MI_UpgradeDBPage")

1. Avviare il [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]. E fare clic su **Configurazione database** nel riquadro sinistro.

2. Nella[!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]pagina **Configurazione database** della fare clic su **Seleziona database**.

3. Fare clic su **Connetti**, [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] selezionare il database associato all'applicazione Web e quindi fare clic su **OK**.

    ![MDS-SQLServer2019-config-mi-ConnectDBName](../master-data-services/media/mds-sqlserver2019-config-mi-connectdbname.png "MDS-SQLServer2019-config-MI_ConnectDBName")

4. Fare clic su **Aggiorna database...** Pulsante

    ![MDS-SQLServer2019-config-mi-SelectUpgradeDB](../master-data-services/media/mds-sqlserver2019-config-mi-selectupgradedb.png "MDS-SQLServer2019-config-MI_SelectUpgradeDB")

5. In aggiornamento guidato database fare clic sul pulsante **Avanti** nella pagina **iniziale** e nella pagina **Verifica aggiornamento** .

    ![MDS-SQLServer2019-config-mi-UpgradeDBWizard](../master-data-services/media/mds-sqlserver2019-config-mi-upgradedbwizard.png "MDS-SQLServer2019-config-MI_UpgradeDBWizard")

6. Al termine di tutte le attività, fare clic sul pulsante **fine** .

## <a name="see-also"></a>Vedere anche

 [Database Master Data Services](../master-data-services/master-data-services-database.md) [Applicazione Web gestione dati master](../master-data-services/master-data-manager-web-application.md) [ &#40;Gestione configurazione Master Data Services&#41; pagina Configurazione database](../master-data-services/database-configuration-page-master-data-services-configuration-manager.md) [Novità di Master Data Services &#40;MDS&#41; ](../master-data-services/what-s-new-in-master-data-services-mds.md)
