---
title: Scaricare SQL Server Management Studio (SSMS)
description: Scaricare la versione più recente di SQL Server Management Studio (SSMS).
ms.prod: sql
ms.prod_service: sql-tools
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
ms.reviewer: sstein, maghan
ms.custom: seo-lt-2019
ms.date: 04/07/2020
ms.openlocfilehash: 294a1ee5cf728498f9564f93ac1f61815ed574f1
ms.sourcegitcommit: e922721431d230c45bbfb5dc01e142abbd098344
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2020
ms.locfileid: "82138265"
---
# <a name="download-sql-server-management-studio-ssms"></a>Scaricare SQL Server Management Studio (SSMS)

[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md.md](../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

SQL Server Management Studio (SSMS) è un ambiente integrato per la gestione di qualsiasi infrastruttura SQL, da SQL Server al database SQL di Azure. SSMS offre gli strumenti per configurare, monitorare e amministrare le istanze di SQL Server e i database. Usare SSMS per distribuire, monitorare e aggiornare i componenti del livello dati usati dalle applicazioni, nonché per creare query e script.

È possibile usare SSMS per eseguire query, progettare e gestire database e data warehouse in qualsiasi posizione, nel computer locale o nel cloud.

SSMS è gratuito.

## <a name="download-ssms"></a>Scaricare SSMS

**[![download](media/download-icon.png) Scaricare SQL Server Management Studio (SSMS)](https://aka.ms/ssmsfullsetup)**

SSMS 18.5 è la versione con disponibilità generale più recente di SSMS. Se è installata una versione di SSMS 18 con disponibilità generale precedente, l'installazione di SSMS 18.5 esegue l'aggiornamento alla versione 18.5.

### <a name="version-information"></a>Informazioni sulla versione

- Numero di versione: 18.5  
- Numero di build: 15.0.18330.0  
- Data di rilascio: 7 aprile 2020  

Per commenti, suggerimenti o per segnalare problemi, il canale migliore per contattare il team SSMS è [UserVoice](https://aka.ms/sqlfeedback).

L'installazione di SSMS 18.x non aggiorna o sostituisce SSMS 17.x o le versioni precedenti. SSMS 18.x viene installato side-by-side con le versioni precedenti, in modo che entrambe le versioni siano disponibili per l'uso. Se tuttavia è stata installata una versione di *anteprima* di SSMS 18.x, è necessario disinstallarla prima di installare SSMS 18.5. Per verificare se è presente la versione di anteprima, passare alla finestra **Guida > Informazioni su**.

Se un computer contiene installazioni affiancate di SQL Server Management Studio, assicurarsi di avviare la versione corretta per le specifiche esigenze. La versione più recente è denominata **Microsoft SQL Server Management Studio 18**.

> [!Note]
> Se si accede a questa pagina da una versione non in lingua inglese e si vuole visualizzare il contenuto più aggiornato, visitare la [versione in inglese del sito](https://aka.ms/downloadssmsusenglish). È possibile scaricare una versione del sito diversa da quella in lingua inglese selezionando [available languages](#available-languages) (lingue disponibili).

## <a name="available-languages"></a>Lingue disponibili

Questa versione di SSMS può essere installata nelle lingue seguenti:

SQL Server Management Studio 18.5:  
[Cinese (semplificato)](https://go.microsoft.com/fwlink/?linkid=2125901&clcid=0x804) | [Cinese (tradizionale)](https://go.microsoft.com/fwlink/?linkid=2125901&clcid=0x404) | [Inglese (Stati Uniti)](https://go.microsoft.com/fwlink/?linkid=2125901&clcid=0x409) | [Francese](https://go.microsoft.com/fwlink/?linkid=2125901&clcid=0x40c) | [Tedesco](https://go.microsoft.com/fwlink/?linkid=2125901&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2125901&clcid=0x410) | [Giapponese](https://go.microsoft.com/fwlink/?linkid=2125901&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2125901&clcid=0x412) | [Portoghese (Brasile)](https://go.microsoft.com/fwlink/?linkid=2125901&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2125901&clcid=0x419) | [Spagnolo](https://go.microsoft.com/fwlink/?linkid=2125901&clcid=0x40a)

> [!NOTE]
> Il modulo SQL Server PowerShell è ora un'installazione separata tramite PowerShell Gallery. Per altre informazioni, vedere [Scaricare il modulo SQL Server PowerShell](download-sql-server-ps-module.md).

## <a name="whats-new"></a>Novità

Per informazioni dettagliate e altre informazioni sulle novità di questa versione, vedere [Note sulla versione di SSMS](release-notes-ssms.md).

Sono presenti alcuni [problemi noti](release-notes-ssms.md#known-issues-185) in questa versione.

## <a name="previous-versions"></a>Versioni precedenti

Questo articolo è solo per la versione più recente di SSMS. Per scaricare le versioni precedenti di SSMS, vedere [Versioni precedenti di SSMS](../ssms/release-notes-ssms.md#previous-ssms-releases).

## <a name="unattended-install"></a>Installazione automatica

È anche possibile installare SSMS usando uno script del prompt dei comandi.

Se si vuole installare SSMS in background senza richieste dell'interfaccia utente grafica, seguire questa procedura.

1. Avviare il prompt dei comandi con autorizzazioni elevate.

2. Digitare il comando seguente nel prompt dei comandi.

    ```console
    start "" <path where SSMS-ENU.exe file is located> /Quiet SSMSInstallRoot=<path where you want to install SSMS>
    ```

    Esempio:

    ```console
    start "" %systemdrive%\SSMSfrom\SSMS-Setup-ENU.exe /Quiet SSMSInstallRoot=%systemdrive%\SSMSto
    ```

    È anche possibile passare */Passive* invece di */Quiet* per visualizzare l'interfaccia utente del programma di installazione.

3. Se l'operazione ha esito positivo, SSMS viene installato in %systemdrive%\SSMSto\Common7\IDE\Ssms.exe in base all'esempio. Se si verificano errori, è possibile verificare il codice di errore restituito nel file di log in %TEMP%\SSMSSetup.

## <a name="supported-sql-offerings-ssms-185"></a>Offerte di SQL supportate (SSMS 18.5)

- Questa versione di SSMS funziona con tutte le [versioni supportate di SQL Server 2008 -[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) e offre il massimo livello di supporto per l'uso con le funzionalità cloud più recenti nel database SQL di Azure e in Azure SQL Data Warehouse.
- È supportata anche l'installazione side-by-side di SSMS 18.x con SSMS 17.x, SSMS 16.x o SQL Server 2014 SSMS e versioni precedenti.
- SQL Server Integration Services (SSIS) - SQL Server Management Studio versione 17.x o successive non supporta la connessione al servizio legacy SQL Server Integration Services. Per connettersi a una versione precedente di Integration Services, usare la versione di SQL Server Management Studio allineata alla versione di SQL Server. Ad esempio, usare SQL Server Management Studio 16.x per connettersi al servizio SQL Server 2016 Integration Services. SSMS 17.x e SSMS 16.x possono essere installati affiancati nello stesso computer. A partire dalla versione di SQL Server 2012, è consigliabile usare il database Catalogo SSIS, SSISDB, per memorizzare, gestire, eseguire e monitorare i pacchetti Integration Services. Per informazioni dettagliate, vedere [Catalogo SSIS](../integration-services/catalog/ssis-catalog.md).

## <a name="supported-operating-systems-ssms-185"></a>Sistemi operativi supportati (SSMS 18.5)

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
> SSMS viene eseguito solo in Windows (AMD o Intel). Se è necessario uno strumento da eseguire su piattaforme diverse da Windows, considerare Azure Data Studio. Azure Data Studio è un nuovo strumento multipiattaforma che può essere eseguito su macOS, Linux e Windows. Per informazioni dettagliate, vedere [Azure Data Studio](../azure-data-studio/what-is.md).

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="see-also"></a>Vedere anche

- [Esercitazione: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Documentazione di SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Aggiornamenti più recenti](../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)
- [Azure Data Studio](../azure-data-studio/what-is.md)
- [Scaricare la versione più recente di SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md)
- [Guida all'architettura dei dati di Azure](https://docs.microsoft.com/azure/architecture/data-guide/)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]