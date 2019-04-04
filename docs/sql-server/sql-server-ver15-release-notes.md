---
title: Note sulla versione di SQL Server 2019 | Microsoft Docs
ms.date: 03/27/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 6336e6ebc549d1be2787bb8a100efec1ea9b6836
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492853"
---
# <a name="sql-server-2019-preview-release-notes"></a>Note sulla versione di anteprima di SQL Server 2019
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive le limitazioni e i problemi noti per le versioni Community Technology Preview (CTP) di [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]. Per informazioni correlate, vedere:
- [Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)

> [!NOTE]
> Le versioni di anteprima di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] vengono rese disponibili per consentire di sperimentare le funzionalità della prossima versione. Non sono supportate o concesse in licenza per la produzione. In particolare non sono supportati gli scenari riportati di seguito:
>
> - Installazione side-by-side con altre versioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
> - Aggiornare un'istanza esistente di SQL Server da qualsiasi versione

**Provare[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]**
- [![Download da Evaluation Center](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101) [Scaricare [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] per l'installazione in Windows](https://go.microsoft.com/fwlink/?LinkID=862101)
- Installazione in Linux per [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md), [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) e [Ubuntu](../linux/quickstart-install-connect-ubuntu.md).
- [Esecuzione in SQL Server 2019 in Docker](../linux/quickstart-install-connect-docker.md).

## <a name="ctp-24"></a>CTP 2.4
[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4 è l'ultima versione pubblica di [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.3 è disponibile solo come edizione di valutazione. Non sono disponibili altre edizioni. Il supporto per le versioni CTP è descritto in `license_Eval.rtf` nel supporto di installazione.

Un supporto limitato può essere disponibile in una delle posizioni seguenti:

- Forum
  - [Commenti di SQL Server](https://aka.ms/sqlfeedback)
  - [Introduzione a SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [Documentazione di SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- Oppure inviando un tweet [@SQLServer](https://twitter.com/SQLServer) con [#sqlhelp](https://twitter.com/search?q=%23sqlhelp)

### <a name="documentation-ctp-24"></a>Documentazione (CTP 2.4)

- **Problema e impatto per i clienti**: la documentazione di SQL Server 2019 (15.x) è limitata e il contenuto è incluso nel set di documentazione di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il contenuto di articoli specifici per SQL Server 2019 (15.x) è indicato con **Si applica a**.

- **Problema e impatto per i clienti**: la documentazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] può essere filtrata in base alla versione. Usare il controllo nell'angolo superiore sinistro di ogni pagina della documentazione per filtrare in base ai requisiti.

- **Problema e impatto per i clienti**: non è disponibile contenuto offline per SQL Server 2019 (15.x).

### <a name="hardware-and-software-requirements-ctp-24"></a>Requisiti hardware e software (CTP 2.4)

- **Problema e impatto per i clienti**: i requisiti hardware e software sono ancora in fase di revisione e non sono finali per la versione del prodotto.

  - **Hardware**
    - [Windows - Requisiti del processore, della memoria e del sistema operativo](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux - Requisiti di sistema](../linux/sql-server-linux-setup.md#system)
  - **Software**
    - Windows Server 2016 o versione successiva. Per requisiti aggiuntivi, vedere [Requisiti per l'installazione di SQL Server](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - Microsoft .NET Framework 4.6.2. Disponibile dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53344).
    - Per Linux, vedere [Linux - Piattaforme supportate](../linux/sql-server-linux-setup.md#supportedplatforms)

### <a name="updated-compiler"></a>Compilatore aggiornato

- **Problema e impatto per i clienti**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] viene compilato con un compilatore aggiornato. In CTP 2.1 si verificava un problema noto per cui i risultati con numeri a virgola mobile e altri scenari di conversione potevano restituire valori diversi rispetto a quelli delle versioni precedenti, a causa dell'aggiornamento del compilatore. CTP 2.2 è stato aggiornato per garantire che gli scenari interessati restituiscano gli stessi risultati delle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Al momento del rilascio di CTP 2.3 non sono noti altri problemi. Si prega di segnalare quanto prima eventuali anomalie nei risultati rispetto a [!INCLUDE[ss2017](../includes/sssqlv14-md.md)] al [team [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](http://aka.ms/sqlfeedback).

- **Soluzione alternativa**: N/D

- **Si applica a**: SQL Server 2019 CTP 2.4, CTP 2.3, CTP 2.2, CTP 2.1

### <a name="utf-8-collations"></a>Regole di confronto UTF-8

- **Problema e impatto per i clienti**: le regole di confronto che supportano UTF-8 non possono essere usate con altre funzionalità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. UTF-8 non è supportato quando sono in uso le caratteristiche [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] seguenti:

  - Server collegato
  - OLTP in memoria
  - Tabella esterna per PolyBase
  - Always Encrypted

  > [!Note]
  > Attualmente non è disponibile il supporto dell'interfaccia utente per la scelta di regole di confronto con supporto UTF-8 in Azure Data Studio o SQL Server Data Tools (SSDT). La versione più recente di [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) supporta la scelta di regole di confronto con UTF-8 nell'interfaccia utente.
 
- **Soluzione alternativa**: nessuna soluzione alternativa per le versioni [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP.

- **Si applica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4, CTP 2.3, CTP 2.2, CTP 2.1, CTP 2.0.

### <a name="sql-graph"></a>SQL Graph

- **Problema e impatto per i clienti**: gli strumenti che dipendono da DacFx, come import-export, non funzionano per le nuove funzionalità dei grafi Edge Constraints (Vincoli di arco) o Merge DML (Unisci DML). La creazione di script in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] potrebbe non funzionare.

- **Soluzione alternativa**: la creazione di script [!INCLUDE[tsql](../includes/tsql-md.md)] e l'esecuzione di tali script sul server mediante [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o SQLCMD funziona correttamente. L'esportazione o l'importazione di oggetti database che creano vincoli di arco, usano la nuova sintassi DML di unione o creano tabelle o viste derivate su oggetti grafo non funzionano. Gli utenti devono creare manualmente questi oggetti nel database usando gli script [!INCLUDE[tsql](../includes/tsql-md.md)]. 

- **Si applica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4, CTP 2.3, CTP 2.2, CTP 2.1, 2.0.

### <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted con enclave sicuri

- **Problema e impatto per i clienti**: i calcoli avanzati sono in attesa di varie ottimizzazioni delle prestazioni, includono funzionalità limitate (nessuna indicizzazione e altro) e sono attualmente disabilitati per impostazione predefinita.

- **Soluzione alternativa**: per abilitare i calcoli avanzati, eseguire `DBCC traceon(127,-1)`. Per informazioni dettagliate, vedere [Enable rich computations](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave) (Abilitare i calcoli avanzati).

- **Si applica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4, CTP 2.3, 2.2, CTP 2.1, 2.0.

### <a name="system-dynamic-management-views"></a>Viste a gestione dinamica (DMV) di sistema

- **Problema e impatto per i clienti**: La funzione di sistema con valori di tabella [sys.dm_db_objects_disabled_on_compatibility_level_change](../relational-databases/system-dynamic-management-views/spatial-data-sys-dm-db-objects-disabled-on-compatibility-level-change.md) restituisce valori casuali nella colonna `dependency`.

- **Si applica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.4, CTP 2.3.

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
