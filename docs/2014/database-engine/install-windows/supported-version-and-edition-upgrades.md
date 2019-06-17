---
title: Aggiornamenti di versione ed edizione supportati | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server], adding to existing installations
- versions [SQL Server], upgrading
- upgrading SQL Server, upgrades supported
- cross-language support
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a245aab71292e1482bd5a17bd32a27bded640ab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775222"
---
# <a name="supported-version-and-edition-upgrades"></a>Aggiornamenti di versione ed edizione supportati
  È possibile eseguire l'aggiornamento da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. In questo argomento sono elencati i percorsi di aggiornamento supportati da queste versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gli aggiornamenti di edizione supportati per [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
## <a name="pre-upgrade-checklist"></a>Elenco di controllo preliminare all'aggiornamento  
  
-   Prima di effettuare l'aggiornamento da un'edizione all'altra di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , verificare che le funzionalità attualmente utilizzate siano supportate nell'edizione da aggiornare.  
  
-   Prima di aggiornare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abilitare l'autenticazione di Windows per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e verificare la configurazione predefinita, ovvero che l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia membro del gruppo sysadmin di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Per effettuare l'aggiornamento a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], è necessario che nel computer sia in esecuzione un sistema operativo supportato. Per ulteriori informazioni, vedere [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   L'aggiornamento verrà bloccato se è un riavvio è sospeso.  
  
-   L'aggiornamento verrà bloccato se il servizio Windows Installer non è in esecuzione.  
  
## <a name="unsupported-scenarios"></a>Scenari non supportati  
  
-   La presenza di istanze di versioni diverse di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] non è supportata. I numeri di versione dei componenti del [!INCLUDE[ssDE](../../includes/ssde-md.md)], di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devono essere identici in un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   L'aggiornamento tra piattaforme diverse non è supportato. Non è possibile aggiornare un'istanza a 32 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un'istanza a 64 bit nativa tramite il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Tuttavia, è possibile eseguire il backup o scollegare database da un'istanza a 32 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quindi ripristinarli o collegarli a una nuova istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (64 bit) se i database non sono pubblicati in replica. È necessario ricreare tutti gli account di accesso e gli altri oggetti utente nei database di sistema master, msdb e model.  
  
-   Non è possibile aggiungere nuove funzionalità durante l'aggiornamento dell'istanza esistente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dopo aver aggiornato un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], è possibile aggiungere funzionalità tramite il programma di installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per altre informazioni, vedere [aggiungere funzionalità a un'istanza di SQL Server 2014 &#40;installazione&#41;](add-features-to-an-instance-of-sql-server-setup.md).  
  
-   I cluster di failover non sono supportati nella modalità WOW.  
  
-   L'aggiornamento da una qualsiasi versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è supportato.  
  
## <a name="upgrades-from-earlier-versions-to-includesssql14includessssql14-mdmd"></a>Aggiornamenti da versioni precedenti a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
> [!NOTE]  
>  Il supporto per [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] verrà descritto più dettagliatamente nella sezione successiva, "Supporto di[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] per [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]".  
  
-   Le edizioni a 32 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere aggiornate a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nel sottosistema a 32 bit (WOW64) di un server a 64 bit.  
  
-   Le versioni a 64 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere aggiornate solo a un server [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a 64 bit.  
  
> [!NOTE]  
>  Quando esegue l'aggiornamento a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise edition, scegliere tra Enterprise Edition: Gestione delle licenze basate su core ed Enterprise Edition. Queste due edizioni differiscono solo per le modalità di gestione delle licenze, nonché per il numero massimo di core supportati. Per altre informazioni, vedere [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
 La versione di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] supporta l'aggiornamento dalle versioni seguenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 o versioni successive  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 o versioni successive  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 o versioni successive  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 o versioni successive  
  
 Nella tabella seguente sono elencati gli scenari di aggiornamento supportati da versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
|Aggiornamento da|Percorso di aggiornamento supportato|  
|------------------|----------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express,<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Tools e<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express,<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Tools e<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Datacenter|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express,<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Tools e<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express,<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Tools e<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express Management Studio e<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
  
### <a name="includesssql14includessssql14-mdmd-support-for-includessversion2005includesssversion2005-mdmd"></a>Supporto di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] per [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
 In questa sezione viene illustrato il supporto di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] per [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. In [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]è possibile effettuare le operazioni seguenti:  
  
-   Aggiornare un'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] del motore di database a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] eseguendo l'installazione di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] utilizzando l'installazione guidata o dal prompt dei comandi.  
  
-   Collegare un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (file ldf/mdf) all'istanza di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] del motore di database.  
  
-   Ripristinare un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] all'istanza di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] del motore di database da un backup.  
  
-   Aggiornare un pacchetto di [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Eseguire i pacchetti con l'aggiornamento automatico sul posto.  
  
-   Aggiornare [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] eseguendo l'installazione di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .  
  
-   Eseguire il backup di un cubo di [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] e il ripristino in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
-   Aggiornare [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] eseguendo l'installazione di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .  
  
-   Connettersi a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]usando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 2014.  
  
 Quando un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] viene aggiornato a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], il livello di compatibilità del database viene modificato da 90 a 100. (In [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], i valori validi per il livello di compatibilità del database sono 100, 110 e 120.) In [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) viene illustrato in che modo la modifica del livello di compatibilità possa influire sulle applicazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Tutti gli scenari non specificati nell'elenco sopra indicato non sono supportati, inclusi, a titolo esemplificativo, i seguenti:  
  
-   Installazione di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] nello stesso computer (side-by-side).  
  
-   Utilizzo di un'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] come membro della topologia di replica che implica un'istanza di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .  
  
-   Configurazione del mirroring del database tra istanze di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Backup del log delle transazioni con log shipping tra istanze di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Configurazione di server collegati tra istanze di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Gestione di un'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] da [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Management Studio.  
  
-   Collegamento di un cubo di [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Management Studio.  
  
-   Connessione a [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] da [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Management Studio.  
  
-   Gestione di un servizio [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] da [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Management Studio.  
  
-   Supporto per componenti personalizzati di terze parti di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Integration Services, ad esempio esecuzione e aggiornamento.  
  
## <a name="includesssql14includessssql14-mdmd-edition-upgrade"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Aggiornamento delle edizioni  
 Nella tabella seguente sono elencati gli scenari di aggiornamento delle edizioni supportati in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 Per istruzioni dettagliate su come eseguire un aggiornamento dell'edizione, vedere [esegue l'aggiornamento a una diversa versione di SQL Server 2014 &#40;installazione&#41;](upgrade-to-a-different-edition-of-sql-server-setup.md).  
  
|Aggiornamento da|Aggiornamento a|  
|------------------|----------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server + CAL e Core) <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licenza Server+CAL o Core)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise Evaluation <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licenza Server+CAL o Core)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> L'aggiornamento da Evaluation Enterprise (edizione gratuita) a qualsiasi edizione a pagamento è supportato per le installazioni autonome, ma non per le installazioni cluster.|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licenza Server+CAL o Core)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licenza Server+CAL o Core)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licenza Server+CAL o Core)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express <sup>1</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licenza Server+CAL o Core)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
  
 È inoltre possibile inoltre eseguire un aggiornamento dell'edizione tra [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+licenza CAL) e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licenza Core):  
  
|Aggiornamento dell'edizione da|Aggiornamento delle edizioni a|  
|--------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licenza Server + CAL) <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licenza Core)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licenza Core)|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licenza Server+CAL)|  
  
 <sup>1</sup> si applica anche alle [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express with Tools e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express with Advanced Services.  
  
 <sup>2</sup> modifica dell'edizione di un [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] cluster di failover è limitata. Gli scenari seguenti non sono supportati per i cluster di failover di [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] :  
  
-   Da SQL Server 2014 Enterprise a SQL Server 2014 Developer, Standard o Enterprise Evaluation.  
  
-   Da SQL Server 2014 Developer a SQL Server 2014 Standard o Enterprise Evaluation.  
  
-   Da SQL Server 2014 Standard a SQL Server 2014 Enterprise Evaluation.  
  
-   Da SQL Server 2014 Enterprise Evaluation a SQL Server 2014 Standard.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Requisiti hardware e Software per l'installazione di SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Eseguire l'aggiornamento a SQL Server 2014](upgrade-sql-server.md)   
 [Usare la Preparazione aggiornamento per preparare gli aggiornamenti](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
  
