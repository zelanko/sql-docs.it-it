---
title: Aggiornamenti di versione ed edizione supportati (SQL Server 2017)
description: Aggiornamenti di versione ed edizione supportati per SQL Server 2017.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server], adding to existing installations
- versions [SQL Server], upgrading
- upgrading SQL Server, upgrades supported
- cross-language support
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 5c0d8067de4a045d6884258f88c09947c27c09c0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463582"
---
# <a name="supported-version--edition-upgrades-sql-server-2017"></a>Aggiornamenti di versione ed edizione supportati (SQL Server 2017)

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
  È possibile eseguire l'aggiornamento da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]. In questo articolo sono elencati i percorsi di aggiornamento supportati da queste versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e gli aggiornamenti di edizione supportati per [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
## <a name="pre-upgrade-checklist"></a>Elenco di controllo preliminare all'aggiornamento  
  
-   Prima di effettuare l'aggiornamento da un'edizione all'altra di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] , verificare che le funzionalità attualmente utilizzate siano supportate nell'edizione da aggiornare.  
  
-   Prima di aggiornare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abilitare l'autenticazione di Windows per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e verificare la configurazione predefinita, ovvero che l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia membro del gruppo sysadmin di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Per effettuare l'aggiornamento a [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], è necessario che nel computer sia in esecuzione un sistema operativo supportato. Per altre informazioni, vedere [Requisiti hardware e software per l'installazione di SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   L'aggiornamento verrà bloccato se è un riavvio è sospeso.  
  
-   L'aggiornamento verrà bloccato se il servizio Windows Installer non è in esecuzione.  
  
## <a name="unsupported-scenarios"></a>Scenari non supportati  
  
-   La presenza di istanze di versioni diverse di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] non è supportata. I numeri di versione dei componenti del [!INCLUDE[ssDE](../../includes/ssde-md.md)] devono essere identici in un'istanza di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] è disponibile solo per piattaforme a 64 bit. L'aggiornamento tra piattaforme diverse non è supportato. Non è possibile aggiornare un'istanza a 32 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a un'istanza a 64 bit nativa tramite il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Tuttavia, è possibile eseguire il backup o scollegare database da un'istanza a 32 bit di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quindi ripristinarli o collegarli a una nuova istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (64 bit) se i database non sono pubblicati in replica. È necessario ricreare tutti gli account di accesso e gli altri oggetti utente nei database di sistema master, msdb e model.  
  
-   Non è possibile aggiungere nuove funzionalità durante l'aggiornamento dell'istanza esistente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dopo aver aggiornato un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], è possibile aggiungere funzionalità tramite il programma di installazione di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]. Per altre informazioni, vedere [Aggiungere funzionalità a un'istanza di SQL Server &#40;programma di installazione&#41;](./add-features-to-an-instance-of-sql-server-setup.md).  
 
-   I cluster di failover non sono supportati nella modalità WOW.  
    
## <a name="upgrades-from-earlier-versions-to-sssqlv14-md"></a>Aggiornamenti da versioni precedenti a [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]  
 
[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] supporta l'aggiornamento dalle versioni di SQL Server seguenti:
 
- SQL Server 2008 SP4 o versioni successive
- SQL Server 2008 R2 SP3 o versioni successive
- SQL Server 2012 SP2 o versione successiva
- SQL Server 2014 o versione successiva 
- SQL Server 2016 o versione successiva
 

  
> [!NOTE]  
>  Per aggiornare i database in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] vedere [il supporto per la versione 2005](#SupportFor2005).  
  
 Nella tabella seguente sono elencati gli scenari di aggiornamento supportati da versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
|Aggiornamento da|Percorso di aggiornamento supportato|  
|:------|:------|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Small Business|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Workgroup|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Datacenter|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Small Business|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Workgroup|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Business Intelligence|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Valutazione di SP2|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Copia di valutazione <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Copia di valutazione|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Copia di valutazione <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Enterprise|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Developer|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Standard|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Express |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Business Intelligence|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Copia di valutazione|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Copia di valutazione <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer|
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] versione finale candidata* |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise |  
|[!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)] Developer |[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise | 

 \* Il supporto Microsoft per l'aggiornamento da software con versioni finali candidate è destinato ai clienti che hanno partecipato al programma TAP (Technology Adoption Program). 

   
###  <a name="sssqlv14-md-support-for-ssversion2005"></a><a name="SupportFor2005"></a>Supporto di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] per [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
 In questa sezione viene illustrato il supporto di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] per [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. In [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]è possibile effettuare le operazioni seguenti:  
  
-   Collegare un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (file ldf/mdf) all'istanza di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] del motore di database.  
  
-   Ripristinare un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] all'istanza di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] del motore di database da un backup.  
  
-   Eseguire il backup di un cubo di [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] e il ripristino in [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
Quando un database di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] viene aggiornato a [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)], il livello di compatibilità del database viene modificato da 90 a 100. In [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] i valori validi per il livello di compatibilità del database sono 100, 110, 120, 130 e 140. In [Livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) viene illustrato in che modo la modifica del livello di compatibilità possa influire sulle applicazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Tutti gli scenari non specificati nell'elenco sopra indicato non sono supportati, inclusi, a titolo esemplificativo, i seguenti:  
  
- Installazione di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] nello stesso computer (side-by-side).  
  
- Utilizzo di un'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] come membro della topologia di replica che implica un'istanza di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] .  
  
- Configurazione del mirroring del database tra istanze di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] e di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
- Backup del log delle transazioni con log shipping tra istanze di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] e di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
- Configurazione di server collegati tra istanze di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] e di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
- Gestione di un'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] da [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Management Studio.  
  
- Collegamento di un cubo di [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] in [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Management Studio.  
  
- Connessione a [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] da [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Management Studio.  
  
- Gestione di un servizio [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] da [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Management Studio.  
  
- Supporto per componenti personalizzati di terze parti di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Integration Services, ad esempio esecuzione e aggiornamento.  
  
## <a name="sssqlv14-md-edition-upgrade"></a>[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Aggiornamento delle edizioni  
Nella tabella seguente sono elencati gli scenari di aggiornamento delle edizioni supportati in [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)].  
  
Per istruzioni dettagliate sull'esecuzione di un aggiornamento dell'edizione, vedere [Eseguire l'aggiornamento a un'edizione diversa di SQL Server &#40;programma di installazione&#41;](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md).  
  
|Aggiornamento da|Aggiornamento a|  
|------------------|----------------|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+CAL e Core)**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise |  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation Enterprise**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (licenza Server+CAL o Core) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> L'aggiornamento da Evaluation (edizione gratuita) a qualsiasi edizione a pagamento è supportato per le installazioni autonome, ma non per le installazioni cluster. Questa limitazione non si applica alle istanze autonome installate in un cluster di failover Windows che partecipa a un gruppo di disponibilità.|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (licenza Server+CAL o Core)|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (licenza Server+CAL o Core) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (licenza Server+CAL o Core) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express*|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (licenza Server+CAL o Core) <br/><br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard <br/> <br/> [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Web|  
  
 È inoltre possibile inoltre eseguire un aggiornamento dell'edizione tra [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (Server+licenza CAL) e [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (licenza Core):  
  
|Aggiornamento dell'edizione da|Aggiornamento delle edizioni a|  
|--------------------------|------------------------|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (licenza Server+CAL)**|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (licenza Core)|  
|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (licenza Core)|[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Enterprise (licenza Server+CAL)|  
  
 \* Applicabile anche a [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express with Tools e [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Express with Advanced Services.  
  
 ** La modifica dell'edizione di un cluster di failover di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] prevede alcune limitazioni. Gli scenari seguenti non sono supportati per i cluster di failover di [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] :  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Da Enterprise a [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Developer, Standard o Evaluation.  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Da Developer a [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard o Evaluation.  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Da Standard a [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Evaluation.  
  
-   [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Da Evaluation a [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] Standard.  
  
## <a name="see-also"></a>Vedere anche  

 [Edizioni e funzionalità supportate per SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)
 
 [Requisiti hardware e software per l'installazione di SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 
 [Eseguire l'aggiornamento di SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
  
