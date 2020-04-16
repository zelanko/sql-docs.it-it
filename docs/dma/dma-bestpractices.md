---
title: Procedura consigliate per Data Migration Assistant
description: Informazioni sulle procedure consigliate per la migrazione dei database di SQL Server con Assistente migrazione dati
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
ms.openlocfilehash: f2bfbb79a8a4803bb56e3dce85f575e8cf257b4a
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388156"
---
# <a name="best-practices-for-running-data-migration-assistant"></a>Procedure consigliate per l'esecuzione di Data Migration Assistant
In questo articolo vengono fornite alcune informazioni sulle procedure consigliate per l'installazione, la valutazione e la migrazione.

## <a name="installation"></a>Installazione
Non installare ed eseguire l'Assistente migrazione dati direttamente nel computer host SQL Server.

## <a name="assessment"></a>Valutazione
- Eseguire valutazioni sui database di produzione durante le ore non di punta.
- Eseguire separatamente le valutazioni **relative ai problemi di compatibilità** e alle **nuove raccomandazioni sulle funzionalità** per ridurre la durata della valutazione.

## <a name="migration"></a>Migrazione
- Eseguire la migrazione di un server durante le ore non di punta.

- Quando si esegue la migrazione di un database, fornire un singolo percorso di condivisione accessibile dal server di origine e dal server di destinazione ed evitare un'operazione di copia, se possibile. Un'operazione di copia può introdurre un ritardo in base alle dimensioni del file di backup. L'operazione di copia aumenta anche le probabilità che una migrazione avrà esito negativo a causa di un passaggio aggiuntivo. Quando viene fornita una singola posizione, Assistente migrazione dati ignora l'operazione di copia.
 
    Inoltre, assicurarsi di fornire le autorizzazioni corrette per la cartella condivisa per evitare errori di migrazione. Nello strumento vengono specificate le autorizzazioni corrette. Se un'istanza di SQL Server viene eseguita in Credenziali del servizio di rete, assegnare le autorizzazioni corrette per la cartella condivisa all'account del computer per l'istanza di SQL Server.

- Abilitare la connessione crittografata quando ci si connette ai server di origine e di destinazione. L'utilizzo della crittografia TLS aumenta la sicurezza dei dati trasmessi tra le reti tra l'Assistente migrazione dati e l'istanza di SQL ServerSQL Server , il che è utile soprattutto quando si esegue la migrazione degli account di accesso SQL. Se la crittografia TLS non viene utilizzata e la rete è compromessa da un utente malintenzionato, gli account di accesso SQL di cui viene eseguita la migrazione potrebbero essere intercettati e/o modificati in tempo reale dall'utente malintenzionato.

    Tuttavia, se tutti accedono attraverso una configurazione di Intranet sicura, la crittografia potrebbe non essere necessaria. L'abilitazione della crittografia rallenta le prestazioni perché l'overhead aggiuntivo necessario per crittografare e decrittografare i pacchetti. Per ulteriori informazioni, fare riferimento a [Crittografia delle connessioni a SQL Server](https://go.microsoft.com/fwlink/?linkid=832513).
    
- Verificare la presenza di vincoli non attendibili nel database di origine e nel database di destinazione prima della migrazione dei dati. Dopo la migrazione, analizzare nuovamente il database di destinazione per verificare se eventuali vincoli non sono stati attendibili come parte dello spostamento dei dati. Correggere i vincoli non attendibili in base alle esigenze. L'esclusione dei vincoli non attendibili può comportare piani di esecuzione insufficienti e può influire sulle prestazioni.
