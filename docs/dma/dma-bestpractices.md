---
title: Procedura consigliate per Data Migration Assistant
description: Informazioni sulle procedure consigliate per la migrazione di database SQL Server con Data Migration Assistant
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Best Practices
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: ef953aa369e831e47d38db403b982919bd4bd830
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056551"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Procedure consigliate per l'esecuzione di Data Migration Assistant
In questo articolo vengono fornite alcune informazioni sulle procedure consigliate per l'installazione, la valutazione e la migrazione.

## <a name="installation"></a>Installation
Non installare ed eseguire il Data Migration Assistant direttamente nel computer host SQL Server.

## <a name="assessment"></a>Valutazione
- Eseguire valutazioni nei database di produzione durante gli orari non di punta.
- Per ridurre la durata della valutazione, è possibile eseguire separatamente i **problemi di compatibilità** e le nuove valutazioni dei **consigli sulle funzionalità** .

## <a name="migration"></a>Migrazione
- Eseguire la migrazione di un server durante gli orari non di punta.

- Quando si esegue la migrazione di un database, fornire un singolo percorso di condivisione accessibile al server di origine e al server di destinazione e, se possibile, evitare un'operazione di copia. Un'operazione di copia può presentare un ritardo in base alle dimensioni del file di backup. Anche l'operazione di copia aumenta le probabilità che una migrazione abbia esito negativo a causa di un passaggio aggiuntivo. Quando viene fornita una singola posizione, Data Migration Assistant ignora l'operazione di copia.
 
    Assicurarsi inoltre di fornire le autorizzazioni corrette per la cartella condivisa per evitare errori di migrazione. Le autorizzazioni corrette sono specificate nello strumento. Se un'istanza di SQL Server viene eseguita con le credenziali del servizio di rete, assegnare le autorizzazioni corrette per la cartella condivisa all'account del computer per l'istanza di SQL Server.

- Abilitare la connessione Encrypt durante la connessione ai server di origine e di destinazione. L'utilizzo della crittografia SSL aumenta la protezione dei dati trasmessi attraverso le reti tra Data Migration Assistant e l'istanza SQL Server, che risulta particolarmente utile in caso di migrazione degli account di accesso SQL. Se la crittografia SSL non viene usata e la rete viene compromessa da un utente malintenzionato, gli account di accesso SQL di cui è in corso la migrazione potrebbero essere intercettati e/o modificati immediatamente dall'autore dell'attacco.

    Tuttavia, se tutti accedono attraverso una configurazione di Intranet sicura, la crittografia potrebbe non essere necessaria. L'abilitazione della crittografia rallenta le prestazioni perché il sovraccarico aggiuntivo necessario per crittografare e decrittografare i pacchetti. Per ulteriori informazioni, vedere Crittografia delle [connessioni a SQL Server](https://go.microsoft.com/fwlink/?linkid=832513).
