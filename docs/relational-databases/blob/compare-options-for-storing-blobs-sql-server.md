---
title: Confrontare opzioni per l'archiviazione di BLOB (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
ms.assetid: 6038697b-36a9-49e8-a02a-2ad9e2e60e5a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 20d392d5019bf643654bb3a0a6989f882a05b671
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2019
ms.locfileid: "65094223"
---
# <a name="compare-options-for-storing-blobs-sql-server"></a>Confrontare opzioni per l'archiviazione di BLOB (SQL Server)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Vengono descritte e confrontate le opzioni disponibili per l'archiviazione di file e documenti in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="Expectations"></a> Archiviazione di file nel database: vantaggi e comportamenti previsti

Nella realtà un'ampia percentuale di dati aziendali non è strutturata e generalmente viene archiviata come file e documenti in file system. La maggior parte di questi dati viene prodotta, gestita e utilizzata da applicazioni che accedono ai file tramite API Windows. Solitamente le aziende mantengono questi dati nel file system, archiviando i metadati correlati per i file in un database relazionale.

L'integrazione dei dati non strutturati nel database relazionale offre i seguenti vantaggi:

- Integrazione di archiviazione e funzionalità di gestione dei dati come ad esempio backup.
- Servizi integrati quali ricerca full-text e ricerca semantica su dati e metadati.
- Facilità di amministrazione e gestione dei criteri sui dati non strutturati.

È scomodo, in genere, archiviare dati non strutturati in un database relazionale. Non è pratico riscrivere applicazioni consolidate, come ad esempio Microsoft Word o Adobe Reader, al fine di farle interagire con le API del database relazionale. Tali applicazioni, infatti, prevedono l'accessibilità ai dati attraverso le API di Windows. Le applicazioni hanno le aspettative seguenti:

- Le transazioni di database non sono riconosciute né richieste dalle applicazioni di Windows.
- Le applicazioni di Windows richiedono compatibilità con le API del file system per i dati di file e directory.

Molti anni fa SQL Server non offriva modi diversi per archiviare i dati non strutturati in un database relazionale. Oggi, invece, offre vari modi per archiviare i dati non strutturati.

## <a name="Filestream"></a> FILESTREAM

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispone già della funzionalità FILESTREAM. La funzionalità FILESTREAM fornisce funzionalità di archiviazione, gestione e flusso efficienti per i dati non strutturati archiviati come file nel file system. Una soluzione FILESTREAM, tuttavia, richiede programmazione personalizzata e non soddisfa i requisiti per la piena compatibilità delle applicazioni Windows descritta sopra.

## <a name="FileTables"></a> FileTable

La funzionalità FileTable si basa sulle capacità FILESTREAM esistenti e consente ai clienti aziendali di archiviare i dati non strutturati dei file e le gerarchie di directory in un database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La funzionalità soddisfa i requisiti per l'accesso non transazionale e la compatibilità delle applicazioni Windows per i dati basati su file.

## <a name="CompareFileTable"></a> Confronto tra FILESTREAM e tabelle FileTable

|Funzionalità|Soluzione file server e database|Soluzione FILESTREAM|Soluzione FileTable|
|:------|:--------------------------------|:------------------|:-----------------|
|**Singola soluzione per le attività di gestione**|no|Sì|**Sì**|
|**Singolo set di servizi**: ricerca, creazione di report, esecuzione di query e così via|no|Sì|**Sì**|
|**Modello di sicurezza integrata**|no|Sì|**Sì**|
|**Aggiornamenti sul posto di dati FILESTREAM**|Sì|no|**Sì**|
|**Gerarchia di file e directory gestita nel database**|no|no|**Sì**|
|**Compatibilità delle applicazioni di Windows**|Sì|no|**Sì**|
|**Accesso relazionale agli attributi dei file**|no|no|**Sì**|

## <a name="CompareRBS"></a> Confronto tra FILESTREAM e Archivio BLOB remoti (Remote BLOB Store, RBS)

Un'altra opzione per l'archiviazione dei dati non strutturati implica l'utilizzo di un Archivio BLOB remoto. Per altre informazioni, vedere [Archivio Blob remoto (RBS) (SQL Server)](remote-blob-store-rbs-sql-server.md).

## <a name="more"></a> Ulteriori informazioni

[FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
[FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md)  
[Archivio BLOB remoto &#40;RBS&#41; &#40;SQL Server&#41;](../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)
