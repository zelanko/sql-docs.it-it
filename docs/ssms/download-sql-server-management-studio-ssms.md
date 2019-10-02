---
title: Scaricare SQL Server Management Studio (SSMS) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein, maghan
ms.technology: ssms
ms.topic: conceptual
keywords:
- installazione di ssms, download di ssms, ssms più recente
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- installazione di sql management studio
- scaricare sql management studio
- ms sql management studio
- installare sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
author: dnethi
ms.author: dinethi
ms.custom: ''
ms.date: 09/24/2019
ms.openlocfilehash: 21678d69305cbe01e1fed3b254da627e00eb60f1
ms.sourcegitcommit: c4875c097e3aae1b76233777d15e0a0ec8e0d681
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/27/2019
ms.locfileid: "71342052"
---
# <a name="download-sql-server-management-studio-ssms"></a>Scaricare SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SQL Server Management Studio (SSMS) è un ambiente integrato per la gestione di qualsiasi infrastruttura SQL, da SQL Server al database SQL di Azure. SSMS offre gli strumenti per configurare, monitorare e amministrare le istanze di SQL Server e i database. Usare SSMS per distribuire, monitorare e aggiornare i componenti del livello dati usati dalle applicazioni, nonché per creare query e script.

È possibile usare SSMS per eseguire query, progettare e gestire database e data warehouse in qualsiasi posizione, nel computer locale o nel cloud.

SSMS è gratuito.

## <a name="download-ssms-183"></a>Scaricare SSMS 18.3

**È ora disponibile SSMS 18.3, la nuova versione disponibile a livello generale di *SQL Server Management Studio* che offre il supporto per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].**

**[![download](../ssdt/media/download.png) Scaricare SQL Server Management Studio 18.3](https://go.microsoft.com/fwlink/?linkid=2104251)**

SSMS 18.3 è la versione disponibile a livello generale più recente di SSMS. Se è installata una versione di SSMS 18 con disponibilità generale precedente, l'installazione di SSMS 18.3 esegue l'aggiornamento alla versione 18.3. Se è stata installata una versione di *anteprima* precedente di SSMS 18.x, è necessario disinstallarla prima di installare SSMS 18.3.

**Informazioni sulla versione**

- Numero di versione: 18.3  
- Numero di build: 15.0.18178.0  
- Data di rilascio: 23 settembre 2019  

Per commenti, suggerimenti o per segnalare problemi, il canale migliore per contattare il team SSMS è [UserVoice](https://aka.ms/sqlfeedback).

L'installazione di SSMS 18.x non aggiorna o sostituisce SSMS 17.x o le versioni precedenti. SSMS 18.x viene installato side-by-side con le versioni precedenti, in modo che entrambe le versioni siano disponibili per l'uso.

Se un computer contiene installazioni affiancate di SQL Server Management Studio, assicurarsi di avviare la versione corretta per le specifiche esigenze. La versione più recente è denominata **Microsoft SQL Server Management Studio 18**.

## <a name="available-languages-ssms-183"></a>Lingue disponibili (SSMS 18.3)

Questa versione di SSMS può essere installata nelle lingue seguenti:

SQL Server Management Studio 18.2:  
[Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2104251&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2104251&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2104251&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2104251&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2104251&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2104251&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2104251&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2104251&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2104251&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2104251&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2104251&clcid=0x40a)

> [!NOTE]
> Il modulo SQL Server PowerShell è ora un'installazione separata tramite PowerShell Gallery. Per altre informazioni, vedere [Scaricare il modulo SQL Server PowerShell](download-sql-server-ps-module.md).

## <a name="new-in-this-release-ssms-183"></a>Novità della versione (SSMS 18.3)

| Nuovo elemento | Dettagli |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Classificazione dei dati | Aggiunta delle informazioni di classificazione dei dati all'interfaccia utente delle proprietà della colonna (le opzioni *Tipo di informazioni*, *ID tipo di informazioni*, *Etichetta riservatezza* e *ID etichetta di riservatezza* non sono esposte nell'interfaccia utente di SSMS). |
| IntelliSense/editor | Aggiornamento del supporto per le funzionalità aggiunte di recente a SQL Server 2019 (ad esempio "ALTER SERVER CONFIGURATION"). |
| Integration Services | Aggiunta di una nuova voce del menu di selezione `Tools > Migrate to Azure > Configure Azure-enabled DTExec` per richiamare le esecuzioni del pacchetto SSIS in Azure-SSIS Integration Runtime come attività di esecuzione del pacchetto SSIS nelle pipeline ADF. |
| SMO/scripting | Aggiunta del supporto dello scripting del vincolo UNIQUE di Azure SQL Data Warehouse. |
| SMO/scripting | Classificazione dei dati - Aggiunta del supporto per SQL versione 10 (SQL 2008) e versioni successive.  - Aggiunta del nuovo attributo di riservatezza 'rank' per SQL versione 15 (SQL 2019) e versioni successive e il database SQL di Azure. |

Per informazioni dettagliate sulle novità introdotte in questa versione, vedere le [note sulla versione di SSMS](release-notes-ssms.md).

## <a name="supported-sql-offerings-ssms-183"></a>Offerte di SQL supportate (SSMS 18.3)

- Questa versione di SSMS funziona con tutte le [versioni supportate di SQL Server 2008 -[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) e offre il massimo livello di supporto per l'uso con le funzionalità cloud più recenti nel database SQL di Azure e in Azure SQL Data Warehouse.
- È supportata anche l'installazione side-by-side di SSMS 18.x con SSMS 17.x, SSMS 16.x o SQL Server 2014 SSMS e versioni precedenti.
- SQL Server Integration Services (SSIS) - SQL Server Management Studio versione 17.x o successive non supporta la connessione al servizio legacy SQL Server Integration Services. Per connettersi a una versione precedente di Integration Services, usare la versione di SQL Server Management Studio allineata alla versione di SQL Server. Ad esempio, usare SQL Server Management Studio 16.x per connettersi al servizio SQL Server 2016 Integration Services. SSMS 17.x e SSMS 16.x possono essere installati affiancati nello stesso computer. A partire dalla versione di SQL Server 2012, è consigliabile usare il database Catalogo SSIS, SSISDB, per memorizzare, gestire, eseguire e monitorare i pacchetti Integration Services. Per informazioni dettagliate, vedere [Catalogo SSIS](../integration-services/catalog/ssis-catalog.md).

## <a name="supported-operating-systems-ssms-183"></a>Sistemi operativi supportati (SSMS 18.3)

Se usata con l'ultimo Service Pack disponibile, questa versione di SSMS supporta le seguenti piattaforme a 64 bit:

- Windows 10 (64 bit) <sup>*</sup>
- Windows 8.1 (64 bit)
- Windows Server 2019 (64 bit)
- Windows Server 2016 (64 bit) <sup>*</sup>
- Windows Server 2012 R2 (64 bit)
- Windows Server 2012 (64 bit)
- Windows Server 2008 R2 (64 bit)

<sup>*</sup> Richiede la versione 1607 (10.0.14393) o una versione successiva

> [!NOTE]
> SSMS viene eseguito solo in Windows. Se è necessario uno strumento da eseguire su piattaforme diverse da Windows, considerare Azure Data Studio. Azure Data Studio è un nuovo strumento multipiattaforma che può essere eseguito su macOS, Linux e Windows. Per informazioni dettagliate, vedere [Azure Data Studio](../azure-data-studio/what-is.md).

## <a name="release-notes-ssms-183"></a>Note sulla versione (SSMS 18.3)

Sono presenti alcuni [problemi noti](release-notes-ssms.md#known-issues-183) in questa versione.

Per informazioni dettagliate su questa versione, vedere le [note sulla versione di SSMS](release-notes-ssms.md).

## <a name="previous-ssms-releases"></a>Versioni precedenti di SSMS

[Versioni precedenti di SQL Server Management Studio](../ssms/release-notes-ssms.md#previous-ssms-releases)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="see-also"></a>Vedere anche

- [Esercitazione: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Documentazione di SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Altri aggiornamenti e Service Pack](https://technet.microsoft.com/sqlserver/ff803383.aspx)
- [Scaricare SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
