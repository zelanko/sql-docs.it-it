---
title: Scaricare SQL Server Management Studio (SSMS) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
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
ms.date: 06/12/2019
ms.openlocfilehash: 0841379b0b64ebe81e4a23f76b21f6cf6abe0ec3
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68265165"
---
# <a name="download-sql-server-management-studio-ssms"></a>Scaricare SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SQL Server Management Studio (SSMS) è un ambiente integrato per la gestione di qualsiasi infrastruttura SQL, da SQL Server al database SQL di Azure. SSMS offre gli strumenti per configurare, monitorare e amministrare le istanze di SQL Server e i database. SSMS permette di distribuire, monitorare e aggiornare i componenti livello dati usati dalle applicazioni, nonché creare query e script.

È possibile usare SSMS per eseguire query, progettare e gestire database e data warehouse in qualsiasi posizione, nel computer locale o nel cloud.

SSMS è gratuito.

## <a name="download-ssms-181"></a>Scaricare SSMS 18.1

**È ora disponibile SSMS 18.1, la nuova versione GA (General Availability, disponibilità generale) di *SQL Server Management Studio* che offre il supporto per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]** .

**[![download](../ssdt/media/download.png) Scaricare SQL Server Management Studio 18.1](https://go.microsoft.com/fwlink/?linkid=2094583)**

SSMS 18.1 è la versione GA più recente di SSMS. Se si ha SSMS 18.0 (GA) già installato, l'installazione di SQL Server Management Studio 18.1 esegue l'aggiornamento alla versione 18.1. Se si ha una versione *precedente* di SSMS 18.0, è necessario disinstallarla prima di installare SSMS 18.1.

**Informazioni sulla versione**

- Numero di versione: 18.1<br>
- Numero di build: 15.0.18131.0<br>
- Data di rilascio: 11 giugno 2019

Per commenti, suggerimenti o per segnalare problemi, il canale migliore per contattare il team SSMS è [UserVoice](https://aka.ms/sqlfeedback).

L'installazione di SSMS 18.x non aggiorna o sostituisce SSMS 17.x o le versioni precedenti. SSMS 18.x viene installato side-by-side con le versioni precedenti, in modo che entrambe le versioni siano disponibili per l'uso.

Se un computer contiene installazioni side-by-side di SSMS, assicurarsi di avviare la versione corretta per le esigenze specifiche. La versione più recente è denominata **Microsoft SQL Server Management Studio 18**.

## <a name="available-languages-ssms-181"></a>Lingue disponibili (SSMS 18.1)

Questa versione di SSMS può essere installata nelle lingue seguenti:

SQL Server Management Studio 18.1:<br>
[Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2094583&clcid=0x40a)

> [!NOTE]
> Il modulo SQL Server PowerShell è ora un'installazione separata tramite PowerShell Gallery. Per altre informazioni, vedere [Scaricare il modulo SQL Server PowerShell](download-sql-server-ps-module.md).

## <a name="new-in-this-release-ssms-181"></a>Novità della versione (SSMS 18.1)

- **Diagrammi di database**: i diagrammi di database sono stati nuovamente aggiunti a SSMS. Per informazioni dettagliate, vedere [Diagrammi di database](https://feedback.azure.com/forums/908035/suggestions/37507828).
- **SSBDIAGNOSE.EXE**: lo strumento da riga di comando di diagnostica di SQL Server è stato nuovamente aggiunto al pacchetto di SSMS.
- **Integration Services (SSIS)** : supporto per la pianificazione del pacchetto SSIS, che si trova nel catalogo SSIS in Azure o nel file system, in Azure. Esistono tre voci di menu per l'avvio della finestra di dialogo Nuova pianificazione: *Nuova pianificazione* che viene visualizzata quando si fa clic con il pulsante destro del mouse sul pacchetto SSIS nel catalogo SSIS in Azure, *Schedule SSIS Package in Azure* (Pianifica pacchetto SSIS in Azure) in *Esegui migrazione ad Azure* nel menu *Strumenti* e "Schedule SSIS in Azure" (Pianifica SSIS in Azure) che viene visualizzata quando si fa clic con il pulsante destro del mouse sulla cartella Processi in SQL Server Agent dell'Istanza gestita del database SQL di Azure.

Per informazioni dettagliate sulle novità introdotte in questa versione, vedere le [note sulla versione di SSMS](release-notes-ssms.md).

## <a name="supported-sql-offerings-ssms-181"></a>Offerte di SQL supportate (SSMS 18.1)

* Questa versione di SSMS funziona con tutte le [versioni supportate di SQL Server 2008 -[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) e offre il massimo livello di supporto per l'uso con le funzionalità cloud più recenti nel database SQL di Azure e in Azure SQL Data Warehouse.
* È supportata anche l'installazione side-by-side di SSMS 18.x con SSMS 17.x, SSMS 16.x o SQL Server 2014 SSMS e versioni precedenti.
* SQL Server Integration Services (SSIS) - SQL Server Management Studio versione 17.x o successive non supporta la connessione al servizio legacy SQL Server Integration Services. Per connettersi a una versione precedente di Integration Services, usare la versione di SQL Server Management Studio allineata alla versione di SQL Server. Ad esempio, usare SQL Server Management Studio 16.x per connettersi al servizio SQL Server 2016 Integration Services. SQL Server Management Studio 17.x e SQL Server Management Studio 16.x possono essere installati side-by-side nello stesso computer. A partire dalla versione di SQL Server 2012, è consigliabile usare il database Catalogo SSIS, SSISDB, per memorizzare, gestire, eseguire e monitorare i pacchetti Integration Services. Per informazioni dettagliate, vedere [Catalogo SSIS](../integration-services/catalog/ssis-catalog.md).

## <a name="supported-operating-systems-ssms-181"></a>Sistemi operativi supportati (SSMS 18.1)

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

## <a name="release-notes-ssms-181"></a>Note sulla versione (SSMS 18.1)

Sono presenti alcuni [problemi noti](release-notes-ssms.md#known-issues-181) in questa versione.

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
