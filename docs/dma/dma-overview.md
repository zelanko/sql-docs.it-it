---
title: Panoramica di Data Migration Assistant (SQL Server) | Microsoft Docs
description: Informazioni su come usare Data Migration Assistant per eseguire la migrazione di database di SQL Server ad altri database di SQL Server o di Azure
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, overview
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.openlocfilehash: 64c8416a15afd685559fe2d05c436c2e5fc1382d
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632856"
---
# <a name="overview-of-data-migration-assistant"></a>Panoramica di Data Migration Assistant

Il Data Migration Assistant (DMA) consente di eseguire l'aggiornamento a una piattaforma dati moderna individuando i problemi di compatibilità che possono influito sulle funzionalità del database nella nuova versione di SQL Server o nel database SQL di Azure. DMA consiglia miglioramenti per le prestazioni e l'affidabilità per l'ambiente di destinazione e consente di spostare lo schema, i dati e gli oggetti non contenuti dal server di origine al server di destinazione.

> [!NOTE]
> Per migrazioni di grandi dimensioni (in termini di numero e dimensione dei database), è consigliabile usare il [servizio migrazione del database di Azure](/azure/dms/dms-overview), che consente di eseguire la migrazione dei database su larga scala.
  
## <a name="get-data-migration-assistant"></a>Ottenere Data Migration Assistant

Per installare DMA, scaricare la versione più recente dello strumento dall' [area download Microsoft](https://www.microsoft.com/download/details.aspx?id=53595), quindi eseguire il file **DataMigrationAssistant. msi** .

## <a name="capabilities"></a>Capabilities

- Valutare le istanze di SQL Server locali che eseguono la migrazione a database SQL di Azure. Il flusso di lavoro di valutazione consente di rilevare i seguenti problemi che possono influire sulla migrazione del database SQL di Azure e fornisce indicazioni dettagliate su come risolverli.

  - Problemi di blocco della migrazione: individua i problemi di compatibilità che bloccano la migrazione dei database di SQL Server locali ai database SQL di Azure. DMA fornisce consigli per risolvere tali problemi.

  - Funzionalità parzialmente supportate o non supportate: rileva le funzionalità parzialmente supportate o non supportate attualmente in uso nell'istanza di SQL Server di origine. DMA fornisce un set completo di indicazioni, approcci alternativi disponibili in Azure e procedure di mitigazione per poterli incorporare nei progetti di migrazione.

- Individuare i problemi che possono influire sull'aggiornamento a un SQL Server locale. Questi sono descritti come problemi di compatibilità e sono organizzati nelle categorie seguenti:

  - Modifiche di rilievo
  - Modifiche del comportamento
  - Funzionalità deprecate

- Individuare nuove funzionalità nella piattaforma di SQL Server di destinazione che il database può trarre vantaggio da dopo un aggiornamento. Questi sono descritti come raccomandazioni sulle funzionalità e sono organizzati nelle categorie seguenti:

  - Prestazioni
  - Sicurezza
  - Archiviazione

- Eseguire la migrazione di un'istanza di SQL Server locale a un'istanza di SQL Server moderna ospitata in locale o in una macchina virtuale (VM) di Azure accessibile dalla rete locale. È possibile accedere alla macchina virtuale di Azure tramite VPN o altre tecnologie. Il flusso di lavoro di migrazione consente di eseguire la migrazione dei componenti seguenti:

  - Schema dei database
  - Dati e utenti
  - Ruoli del server
  - SQL Server e account di accesso di Windows

- Al termine della migrazione, le applicazioni possono connettersi senza problemi ai database di destinazione SQL Server.

- Valutare i pacchetti di SQL Server Integration Services (SSIS) locali che eseguono la migrazione a un database SQL di Azure o a un'istanza gestita di database SQL di Azure. La valutazione consente di individuare problemi che possono influire sulla migrazione. Questi sono descritti come problemi di compatibilità e sono organizzati nelle categorie seguenti:

  - Blocchi per la migrazione: individua i problemi di compatibilità che bloccano la migrazione dei pacchetti di origine in Azure. DMA fornisce consigli per risolvere tali problemi.

  - Problemi di informazioni: rileva le funzionalità parzialmente supportate o deprecate utilizzate nei pacchetti di origine.

## <a name="prerequisites"></a>Prerequisiti

Per eseguire una valutazione, è necessario essere un membro del ruolo **sysadmin** SQL Server.

## <a name="supported-source-and-target-versions"></a>Versioni di origine e di destinazione supportate

DMA sostituisce tutte le versioni precedenti di SQL Server preparazione aggiornamento e deve essere utilizzato per gli aggiornamenti per la maggior parte delle SQL Server versioni. Le versioni di origine e di destinazione supportate sono:

**Fonti**

- SQL Server 2005
- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 in Windows

**Obiettivi**

- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- SQL Server 2017 in Windows e Linux
- SQL Server 2019
- Database singolo di database SQL di Azure
- Istanza gestita di database SQL di Azure
- SQL Server in esecuzione in una macchina virtuale di Azure

## <a name="see-also"></a>Vedere anche

[Valutare la migrazione del SQL Server](../dma/dma-assesssqlonprem.md)

[Data Migration Assistant: impostazioni di configurazione](../dma/dma-configurationsettings.md)

[Eseguire la migrazione di SQL Server locali con Data Migration Assistant](../dma/dma-migrateonpremsql.md)

[Data Migration Assistant: procedure consigliate](../dma/dma-bestpractices.md)
