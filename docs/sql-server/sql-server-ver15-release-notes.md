---
title: Note sulla versione di SQL Server 2019 | Microsoft Docs
ms.date: 08/21/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: d9d6f1f0bdf1a0e38bf26fdc18bc91c5825ca412
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653053"
---
# <a name="sql-server-2019-preview-release-notes"></a>Note sulla versione di anteprima di SQL Server 2019
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Questo articolo descrive le limitazioni e i problemi noti relativi a [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]. Per informazioni correlate, vedere:

>[Novità di SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)

>[!NOTE]
>Il contenuto è pubblicato per [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Release Candidate. La versione finale candidata è costituita da software provvisorio. Le informazioni sono soggette a modifiche. Per informazioni sugli scenari di supporto, vedere la sezione [Supporto](#support).

## <a name="includesql-server-2019includessssqlv15-mdmd-release-candidate-rc"></a>[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] Release Candidate (RC)

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC è la versione pubblica più recente di [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC è disponibile solo come edizione di valutazione. Non sono disponibili altre edizioni.

Dettagli completi sul supporto e sulle licenze per il software di una versione finale candidata sono disponibili in `license_Eval.rtf` nel supporto di installazione.

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

## <a name="documentation"></a>Documentazione

- **Problema e impatto per i clienti**: la documentazione di SQL Server 2019 (15.x) è limitata e il contenuto è incluso nel set di documentazione di [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Il contenuto negli articoli specifico di SQL Server 2019 (15.x) è indicato con **Si applica a**.

- **Problema e impatto per i clienti**: la documentazione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] può essere filtrata in base alla versione. Usare il controllo nell'angolo superiore sinistro di ogni pagina della documentazione per filtrare in base ai requisiti.

- **Problema e impatto per i clienti**: non è disponibile contenuto offline per SQL Server 2019 (15.x).

## <a name="hardware-and-software-requirements"></a>Requisiti hardware e software

- **Problema e impatto per i clienti**: i requisiti hardware e software sono ancora in fase di revisione e non sono finali per la versione del prodotto.

  - **Hardware**
    - [Windows - Requisiti del processore, della memoria e del sistema operativo](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux - Requisiti di sistema](../linux/sql-server-linux-setup.md#system)
  - **Software**
    - Windows Server 2016 o versione successiva. Per requisiti aggiuntivi, vedere [Requisiti per l'installazione di SQL Server](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - Microsoft .NET Framework 4.6.2. Disponibile dall'[Area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53344).
    - Per Linux, vedere [Linux - Piattaforme supportate](../linux/sql-server-linux-setup.md#supportedplatforms)

## <a name = "release-notes"></a>Funzionalità escluse dal supporto

- **Problema e impatto per i clienti**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] esclude il supporto per i componenti, le funzionalità e gli scenari seguenti:
  - SQL Server Analysis Services
  - SQL Server Reporting Services
  - Gruppi di disponibilità Always On in Kubernetes

- **Soluzione alternativa**: Nessuna. L'esclusione si applica a tutti i clienti, inclusi i partecipanti al Programma SQL Early Adopter.

- **Si applica a**: Release Candidate

## <a name="updated-compiler"></a>Compilatore aggiornato

- **Problema e impatto per i clienti**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] viene compilato con un compilatore aggiornato. In CTP 2.1 si verificava un problema noto per cui i risultati con numeri a virgola mobile e altri scenari di conversione potevano restituire valori diversi rispetto a quelli delle versioni precedenti, a causa dell'aggiornamento del compilatore. CTP 2.2 è stato aggiornato per garantire che gli scenari interessati restituiscano gli stessi risultati delle versioni precedenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Al momento del rilascio della versione finale candidata non sono noti altri problemi. Si prega di segnalare quanto prima eventuali anomalie nei risultati rispetto a [!INCLUDE[ss2017](../includes/sssqlv14-md.md)] al [team [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]](https://aka.ms/sqlfeedback).

- **Soluzione alternativa**: N/D

- **Si applica a**: Release Candidate

## <a name="installation-wizard-may-wait-between-eula-pages"></a>Possibile attesa tra le pagine delle condizioni di licenza durante l'installazione guidata

- **Problema e impatto per i clienti**: durante l'installazione mediante la procedura guidata, è possibile che sia necessario attendere un periodo di tempo prolungato tra il contratto di licenza con l'utente finale (EULA) per R Services e il contratto di licenza per Python.

- **Soluzione alternativa**: attendere che l'installazione guidata proceda. Il tempo di attesa può superare i 30 minuti.

- **Si applica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.0

## <a name="utf-8-collations"></a>Regole di confronto UTF-8

- **Problema e impatto per i clienti**: le regole di confronto che supportano UTF-8 non possono essere usate con altre funzionalità di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. UTF-8 non è supportato quando sono in uso le caratteristiche [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] seguenti:

  - OLTP in memoria
  - Tabella esterna per PolyBase ([!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC 1)
  - Always Encrypted (fino a [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] RC 1)
  - Server collegati (fino a [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2)

  > [!Note]
  > Attualmente non è disponibile il supporto dell'interfaccia utente per la scelta di regole di confronto con supporto UTF-8 in Azure Data Studio o SQL Server Data Tools (SSDT). [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) versione 18 supporta la scelta di regole di confronto abilitate per UTF-8 nell'interfaccia utente.
 
- **Soluzione alternativa**: nessuna soluzione alternativa per le versioni [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP.


- **Si applica a**: tutte le versioni CTP.

## <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted con enclave sicuri

- **Problema e impatto per i clienti**: i calcoli avanzati sono in attesa di ottimizzazioni delle prestazioni e miglioramenti alla gestione degli errori e sono attualmente disabilitati per impostazione predefinita.

- **Soluzione alternativa**: per abilitare i calcoli avanzati, eseguire `DBCC traceon(127,-1)`. Per informazioni dettagliate, vedere [Abilitare i calcoli avanzati](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

- **Si applica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2, CTP 3.1

## <a name="sql-server-configuration-manager-may-not-start"></a>L'avvio di Gestione configurazione SQL Server potrebbe non riuscire

- **Problema e impatto per i clienti**: Gestione configurazione SQL Server (SSCM) non viene avviato in un computer privo di VCRuntime 140. All'avvio di SSCM è possibile che all'utente sia presentata la finestra di dialogo seguente: 


  `MMC could not create the snap-in. The snap-in might not have been installed correctly.`

- **Soluzione alternativa**:  installare la versione VC Runtime 2013 (x86) più recente:

  - [Verbose](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)
  - [Diretta](https://support.microsoft.com/en-us/help/4032938/update-for-visual-c-2013-redistributable-package)

- **Si applica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.1, CTP 3.0, CTP 2.5.

## <a name="always-on-availability-group-kubernetes-operator-not-supported"></a>Operatore Kubernetes per gruppi di disponibilità Always On non supportato

- **Problema e impatto per i clienti**: l'operatore Kubernetes per gruppi di disponibilità Always On non è supportato in questa versione finale candidata e non sarà disponibile nella versione RTM. 

- **Soluzione alternativa**: None

- **Si applica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] Release Candidate

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
