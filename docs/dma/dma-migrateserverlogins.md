---
title: Eseguire la migrazione di account di accesso SQL Server con Data Migration Assistant
description: Informazioni su come eseguire la migrazione di SQL Server account di accesso con Data Migration Assistant
ms.date: 10/22/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, login migration
ms.assetid: ''
author: HJToland3
ms.author: jtoland
ms.custom: seo-lt-2019
ms.openlocfilehash: 368372ab7324b11e9f7fdaa6af94d5ba2c0534ad
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74056484"
---
# <a name="migrate-sql-server-logins-with-data-migration-assistant"></a>Eseguire la migrazione di account di accesso SQL Server con Data Migration Assistant

Questo articolo fornisce una panoramica della migrazione degli account di accesso SQL Server usando Data Migration Assistant.

> [!IMPORTANT]
> Questo argomento si applica a scenari che coinvolgono SQL Server aggiornamenti a versioni successive del prodotto locale o SQL Server in macchine virtuali di Azure.

## <a name="which-logins-are-migrated"></a>Gli account di accesso di cui viene eseguita la migrazione

- È possibile eseguire la migrazione degli account di accesso in base a un'entità di Windows, ad esempio un utente di dominio o un gruppo di dominio Windows. È inoltre possibile eseguire la migrazione di account di accesso creati in base all'autenticazione SQL, detti anche SQL Server account di accesso.

- Data Migration Assistant attualmente non supporta gli account di accesso associati a un certificato di sicurezza autonomo (account di accesso con mapping al certificato), una chiave asimmetrica autonoma (account di accesso di cui è stato eseguito il mapping a una chiave asimmetrica) e gli account di accesso con mapping a credenziali.

- Data Migration Assistant non sposta i principi di accesso e del server **sa** con i nomi racchiusi tra\#\#doppi segni di cancelletto (), che sono solo per uso interno.

- Per impostazione predefinita, Data Migration Assistant seleziona tutti gli account di accesso completi da migrare. Facoltativamente, è possibile selezionare account di accesso specifici per la migrazione. Quando Data Migration Assistant esegue la migrazione di tutti gli account di accesso qualificati, il mapping dell'utente di accesso rimane intatto nei database di cui viene eseguita la migrazione.

  Se si prevede di eseguire la migrazione di account di accesso specifici, assicurarsi di selezionare gli account di accesso di cui è stato eseguito il mapping a uno o più utenti nei database selezionati per la migrazione.

- Come parte della migrazione degli account di accesso, Data Migration Assistant sposta inoltre i ruoli del server definiti dall'utente e aggiunge le autorizzazioni a livello di server ai ruoli del server definiti dall'utente. Il proprietario del ruolo verrà impostato sull'entità **sa** .

## <a name="during-and-after-migration"></a>Durante e dopo la migrazione

- Come parte della migrazione degli account di accesso di, Data Migration Assistant assegna le autorizzazioni alle entità a protezione diretta nel SQL Server di destinazione come esistono nel SQL Server di origine.

  Se l'account di accesso esiste già nel SQL Server di destinazione, Data Migration Assistant esegue la migrazione solo delle autorizzazioni assegnate alle entità a protezione diretta e non creerà di nuovo l'intero account di accesso.

- Data Migration Assistant esegue il massimo sforzo per eseguire il mapping dell'account di accesso agli utenti del database, se l'account di accesso esiste già nel server di destinazione.

- È consigliabile esaminare i risultati della migrazione per comprendere lo stato complessivo della migrazione degli account di accesso e le azioni di post-migrazione consigliate.

## <a name="resources"></a>Risorse

[Data Migration Assistant (DMA)](../dma/dma-overview.md)

[Data Migration Assistant: impostazioni di configurazione](../dma/dma-configurationsettings.md)
