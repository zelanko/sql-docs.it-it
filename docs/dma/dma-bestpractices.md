---
title: Procedure consigliate per Data Migration Assistant (SQL Server) | Microsoft Docs
description: Informazioni sulle procedure consigliate per la migrazione dei database di SQL Server con Data Migration Assistant
ms.custom: ''
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
manager: jroth
ms.openlocfilehash: b122c8dbd5e087ab8b871eb7a29e3bb2b330acaa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66794406"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Le procedure consigliate per l'esecuzione di Data Migration Assistant
Questo articolo fornisce alcune procedure consigliate per l'installazione, valutazione e migrazione.

## <a name="installation"></a>Installazione
Non è possibile installare ed eseguire Data Migration Assistant direttamente nel computer host SQL Server.

## <a name="assessment"></a>Valutazione
- Eseguire valutazioni su database di produzione durante i periodi non di punta.
- Eseguire la **problemi di compatibilità** e **nuove funzionalità consigliate** valutazioni separatamente per ridurre la durata della valutazione.

## <a name="migration"></a>Migrazione
- Eseguire la migrazione di un server durante i periodi non di punta.

- Durante la migrazione di un database, specificare una posizione singola condivisione accessibile dal server di origine e il server di destinazione e se possibile, evitare un'operazione di copia. Un'operazione di copia può introdurre ritardo in base alla dimensione del file di backup. L'operazione di copia aumenta anche la possibilità che la migrazione avrà esito negativo a causa di un passaggio aggiuntivo. Quando viene fornita un'unica posizione, Data Migration Assistant consente di ignorare l'operazione di copia.
 
    Inoltre, assicurarsi che per fornire le autorizzazioni corrette per la cartella condivisa per evitare errori durante la migrazione. Le autorizzazioni corrette vengono specificate nello strumento. Se un'istanza di SQL Server viene eseguito con le credenziali del servizio di rete, assegnare le autorizzazioni corrette per la cartella condivisa per l'account del computer per l'istanza di SQL Server.

- Abilita Crittografa connessione durante la connessione al server di origine e destinazione. Crittografia mediante SSL aumenta la sicurezza dei dati trasmessi tra le reti tra l'istanza di SQL Server, è utile soprattutto quando la migrazione di account di accesso SQL e Data Migration Assistant. Se non viene utilizzata la crittografia SSL e la rete è compromessa da un utente malintenzionato, l'account di accesso SQL migrato a è stato possibile ottenere intercettati e/o modificate in immediatamente dall'autore dell'attacco.

    Tuttavia, se tutti accedono attraverso una configurazione di Intranet sicura, la crittografia potrebbe non essere necessaria. Abilitazione della crittografia del rallentamento delle prestazioni perché il sovraccarico aggiuntivo che è necessario per crittografare e decrittografare i pacchetti. Per altre informazioni, consultare [crittografia delle connessioni a SQL Server](https://go.microsoft.com/fwlink/?linkid=832513).
