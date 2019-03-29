---
title: SQL Server in Linux domande frequenti | Microsoft Docs
description: Questo articolo offre risposte alle domande frequenti su SQL Server in esecuzione su Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 01/10/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: e0f1b8a425e3b21ac1e36e0f301f3b380d791d1a
ms.sourcegitcommit: a9a03f9a7ec4dad507d2dfd5ca33571580114826
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/28/2019
ms.locfileid: "58566580"
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>Domande frequenti su SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Le sezioni seguenti forniscono domande e risposte comuni per SQL Server in esecuzione su Linux.

## <a name="general-questions"></a>Domande generali

1. **Quali piattaforme Linux sono supportati?**

   SQL Server è attualmente supportato in Red Hat Enterprise Server, SUSE Linux Enterprise Server e Ubuntu. Anche supportato in esecuzione in un contenitore con Docker. Per informazioni aggiornate sulle versioni supportate, vedere [piattaforme supportate](sql-server-linux-setup.md#supportedplatforms).

1. **SQL Server su Linux funzionerà su altre piattaforme**?

   SQL Server viene testato e supportato in Linux per le distribuzioni elencate in precedenza. Altre distribuzioni Linux sono strettamente correlati e potrebbero essere in grado di eseguire SQL Server (ad esempio CentOS è strettamente correlato a Red Hat Enterprise Server). Ma se si sceglie di installare SQL Server in un sistema operativo non supportato, vedere il **criteri di supporto** sezione del [dei criteri di supporto tecnico per Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) per comprendere il supporto implicazioni. Si noti inoltre che alcune gestite dalla community-distribuzioni di Linux non è un sistema formale per ricevere supporto se il sistema operativo sottostante è il problema.

1. **È anche in Windows Server SQL in Linux?**

   Il motore di Database per SQL Server core è lo stesso in Linux come in Windows. Tuttavia, alcune funzionalità non sono attualmente supportate in Linux. Per un elenco delle funzionalità non supportate in Linux, vedere la [non è supportato servizi e funzionalità in](sql-server-linux-release-notes.md#Unsupported). Vedere anche il [problemi noti](sql-server-linux-release-notes.md#known-issues). Se non diversamente specificato in questi elenchi, altri servizi e funzionalità di SQL Server sono supportati in Linux.

1. **Quali sono i criteri di supporto per SQL Server?**

   Per comprendere i criteri di supporto, vedere la [tecniche dei criteri di supporto per SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

1. **Sto provenienti da un background di Windows SQL Server. Sono disponibili risorse per apprendere come usare SQL Server in Linux?**

   Il [guide introduttive](sql-server-linux-setup.md#platforms) forniscono istruzioni dettagliate su come installare SQL Server in Linux ed eseguire query Transact-SQL. Altre esercitazioni forniscono istruzioni aggiuntive sull'uso di SQL Server in Linux. Per un elenco di terze parti dei suggerimenti, vedere la [elenco MSSQLTIPS di SQL Server in Linux suggerimenti](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/).

## <a name="licensing"></a>Gestione delle licenze

1. **Come funziona la gestione delle licenze in Linux?**

   SQL Server viene concesso in licenza allo stesso modo per Windows e Linux. In effetti, concedere in licenza SQL Server e quindi è possibile scegliere di utilizzare la licenza per la piattaforma di propria scelta. Per altre informazioni, vedere [licenza di SQL Server come](https://www.microsoft.com/sql-server/sql-server-2017-pricing).

1. **Quale edizione di SQL Server scegliere quando ho già acquistato?**

   Quando si esegue il programma di installazione mssql-conf viene visualizzata con le opzioni seguenti:
   
   ```
   Choose an edition of SQL Server:
      1. Evaluation (free, no production use rights, 180-day limit)
      2. Developer (free, no production use rights)
      3. Express (free)
      4. Web (PAID)
      5. Standard (PAID)
      6. Enterprise (PAID)
      7. Enterprise Core (PAID)
      8. I bought a license through a retail sales channel and have a product key to enter.
   ```
     
   Se si è ottenuto la licenza tramite i contratti multilicenza come parte di un contratto Enterprise Agreement o tramite l'abbonamento MSDN, è necessario selezionare le opzioni di 4 a 7. Questo passaggio non viene chiesto di immettere la licenza, ma è necessario aver precedentemente acquistato la licenza appropriata per la configurazione. Se è stato acquistato Standard edition tramite un canale di vendita al dettaglio, selezionare l'opzione 8. Questa opzione viene visualizzata una richiesta di immettere una chiave. 

1. **Come verificare la versione installata e l'edizione di SQL Server in Linux?**

   Connettersi all'istanza di SQL Server con uno strumento client, ad esempio **sqlcmd**, **mssql-cli**, o Visual Studio Code. Quindi eseguire la query Transact-SQL seguente per verificare la versione ed edizione di SQL Server in esecuzione: 

   ```sql
   SELECT @@VERSION
   SELECT SERVERPROPERTY('Edition')
   ```

## <a name="installation"></a>Installazione

1. **Come ottenere SQL Server installata nel server Linux?**

   Microsoft gestisce i repository dei pacchetti per l'installazione di SQL Server e supporta l'installazione tramite strumenti di gestione di pacchetti nativi, ad esempio yum, zypper e apt. Per installare rapidamente, vedere uno del [guide introduttive](sql-server-linux-setup.md#platforms).

1. **È possibile installare SQL Server nel sottosistema di Linux per Windows 10?**

   No. Linux in esecuzione in Windows 10 non è attualmente una piattaforma supportata per SQL Server e strumenti correlati.

1. **Il file System di Linux può usare SQL Server per i file di dati?**

   SQL Server in Linux supporta attualmente ext4 e XFS. Verrà aggiunto il supporto per altri sistemi di file in base alle esigenze in futuro.

1. **È possibile scaricare i pacchetti di installazione per installare SQL Server non in linea?**

   Sì. Per altre informazioni, vedere il pacchetto i collegamenti nel download il [note sulla versione](sql-server-linux-release-notes.md). Inoltre, esaminare i [istruzioni per le installazioni offline](sql-server-linux-setup.md#offline).

1. **È possibile eseguire un'installazione automatica di SQL Server in Linux?**

   Sì. Per una discussione di installazione automatica, vedere [informazioni aggiuntive sull'installazione per SQL Server in Linux](sql-server-linux-setup.md#unattended). Vedere gli script di esempio per [Red Hat](sample-unattended-install-redhat.md), [SUSE Linux Enterprise Server](sample-unattended-install-suse.md), e [Ubuntu](sample-unattended-install-ubuntu.md). È anche possibile esaminare [questo script di esempio](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/) creati da SQL Server Customer Advisory Team.

## <a name="tools"></a>Strumenti

1. **È possibile usare il client di SQL Server Management Studio in Windows per accedere a SQL Server in Linux?**

   Sì, è possibile usare tutti gli strumenti esistenti eseguiti in Windows per accedere a SQL Server in Linux. Sono inclusi strumenti forniti da Microsoft, ad esempio SQL Server Management Studio (SSMS), SQL Server Data Tools (SSDT) e sistemi operativi e gli strumenti di terze parti.

1. **È disponibile uno strumento come SQL Server Management Studio che viene eseguito in Linux?**

   Il nuovo Studio dati Azure è uno strumento multipiattaforma per la gestione di SQL Server. Per altre informazioni, vedere [che cos'è Azure Data Studio](../azure-data-studio/what-is.md).

1. **Sono disponibili in Linux comandi, ad esempio sqlcmd e bcp?**

   Sì, [sqlcmd e bcp](sql-server-linux-setup-tools.md) sono disponibili in modo nativo su Linux, macOS e Windows. Inoltre, usare il nuovo [mssql-scripter](https://github.com/Microsoft/mssql-scripter) lo strumento da riga di comando in Linux, macOS o Windows per generare script T-SQL per il database SQL in esecuzione ovunque. Vedere anche l'anteprima per rilasciare [mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/).

1. **È possibile visualizzare Monitoraggio attività quando è connesso tramite SSMS in Windows per un'istanza in esecuzione in Linux?**

   Sì, è possibile usare SQL Server Management Studio in Windows per connettersi in remoto e usare strumenti / funzionalità quali comandi di Monitoraggio attività in un'istanza di Linux.

1. **Quali strumenti sono disponibili per monitorare le prestazioni di SQL Server in Linux?**

   È possibile usare [viste a gestione dinamica (DMV) del sistema](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) per raccogliere tipi diversi di informazioni su SQL Server, incluse le informazioni sul processo Linux. È possibile usare [Query Store](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md) per migliorare le prestazioni delle query. Altri strumenti, ad esempio l'oggetto incorporato [Performance Dashboard](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/), funzionano in modalità remota in SQL Server Management Studio (SSMS) di Windows.

   > [!TIP]
   > Un modo per migliorare le prestazioni consiste nel configurare correttamente il insance di SQL Server e il sistema operativo Linux. Per altre informazioni, vedere [consigliate per le prestazioni e linee guida per la configurazione per SQL Server in Linux](sql-server-linux-performance-best-practices.md).

## <a name="administration"></a>Amministrazione

1. **Dispone di Microsoft ha creato un'app, ad esempio Gestione configurazione SQL Server in Linux?**

   Sì, è disponibile uno strumento di configurazione per SQL Server in Linux: [mssql-conf](sql-server-linux-configure-mssql-conf.md).

1. **SQL Server in Linux supporta più istanze nello stesso host?**

   È consigliabile eseguire più contenitori in un host a dispone di più istanze distinte. Questo avviene facilmente usando docker, ma ogni contenitore deve restare in ascolto su una porta diversa. Per altre informazioni, vedere [esecuzione di più contenitori di SQL Server](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers).

1. **Autenticazione di Active Directory è supportato in Linux?**

   Sì. Per altre informazioni, vedere [autenticazione di Active Directory con SQL Server in Linux](sql-server-linux-active-directory-authentication.md).

1. **Always On e clustering supportate in Linux?**

   Clustering di failover e la disponibilità elevata in Linux si ottengono con Pacemaker in Linux. Per altre informazioni, vedere [Business continuità e ripristino del database - SQL Server in Linux](sql-server-linux-business-continuity-dr.md).

1. **È possibile configurare la replica da Linux a Windows e viceversa?**

   Le repliche con scalabilità in lettura è utilizzabile tra Windows e Linux per la replica dei dati unidirezionale.

1. **È possibile eseguire la migrazione di database esistenti nelle versioni precedenti di SQL Server da Windows a Linux?**

   Sì, esistono [diversi metodi](sql-server-linux-migrate-overview.md) di raggiungere questo obiettivo.

1. **È possibile migrare i dati da Oracle e altri motori di database a SQL Server in Linux?**

   Sì. SSMA supporta la migrazione tra diversi tipi di motori di database: Microsoft Access, DB2, MySQL, Oracle e SAP ASE (noto in precedenza come SAP Sybase ASE). Per un esempio d'uso di SSMA, vedere [eseguire la migrazione di uno schema Oracle a SQL Server in Linux con SQL Server Migration Assistant](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json).

1. **Quali autorizzazioni sono necessarie per i file di SQL Server?**

   Tutti i file nel `/var/opt/mssql` cartella di file deve essere di proprietà di **mssql** utente e appartengono al **mssql** gruppo. Entrambi i **mssql** utente e gruppo deve avere autorizzazioni di lettura / scrittura di tutti i file e directory. Tenere presente i seguenti scenari speciali che interessa le autorizzazioni di file e directory:

   * Per il proprietario mssql e di gruppo sono necessarie autorizzazioni per le condivisioni di rete montate che vengono usate per archiviare i file di SQL Server.
   * Se i file di database o backup si trova in una directory non predefinito, è necessario impostare anche le autorizzazioni per tale directory.
   * Se si modifica la proprietà umask radice predefinito da 0022, configurazione di SQL Server non riesce dopo l'installazione. Quindi è necessario applicare manualmente le autorizzazioni necessarie all'account di avvio di SQL Server.

1. **È possibile modificare la proprietà dei file di SQL Server e delle directory dal gruppo e account mssql installata?**

   Non è supportata la modifica del proprietario del file e directory di SQL Server dall'installazione predefinita. L'account mssql e il gruppo viene usato in modo specifico per SQL Server e nessun accesso di accesso interattivo.

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
