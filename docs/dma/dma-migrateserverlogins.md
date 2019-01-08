---
title: Eseguire la migrazione di account di accesso di SQL Server con Data Migration Assistant | Microsoft Docs
description: Informazioni su come eseguire la migrazione di account di accesso di SQL Server con Data Migration Assistant
ms.custom: ''
ms.date: 10/20/2018
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
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 20084c0fadbccab9c920cb81b29cf30cb2cf739c
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52392624"
---
# <a name="migrate-sql-server-logins-with-data-migration-assistant"></a>Eseguire la migrazione di account di accesso di SQL Server con Data Migration Assistant

Questo articolo offre una panoramica degli account di accesso di SQL Server la migrazione usando Data Migration Assistant. 

## <a name="which-logins-are-migrated"></a>Gli account di accesso viene eseguita la migrazione

- È possibile eseguire la migrazione degli account di accesso basato su un'entità di Windows (ad esempio, un utente di dominio o un gruppo di dominio di Windows). È anche possibile eseguire la migrazione di account di accesso creati in base sull'autenticazione di SQL, detto anche account di accesso di SQL Server.

- Data Migration Assistant non supporta attualmente gli account di accesso associato a un certificato di sicurezza autonomo (account di accesso mappato a certificato), una chiave asimmetrica autonoma (account di accesso mappato alla chiave asimmetrica) e gli account di accesso mappato alle credenziali.

- Data Migration Assistant non si sposta il **sa** principi di account di accesso e il server con nomi racchiusi tra simboli di cancelletto doppio (\#\#), che sono solo per uso interno.

- Per impostazione predefinita, Data Migration Assistant Seleziona tutti gli account di accesso completo per eseguire la migrazione. Facoltativamente, è possibile selezionare un account di accesso specifici per eseguire la migrazione. Quando Data Migration Assistant esegue la migrazione di tutti gli account di accesso completo, il mapping di account di accesso utente rimane nel database che vengono eseguita la migrazione. 

  Se si prevede di eseguire la migrazione di account di accesso specifici, assicurarsi di selezionare gli account di accesso viene eseguito il mapping a uno o più utenti nei database selezionati per la migrazione.

- Come parte della migrazione di account di accesso, Data Migration Assistant inoltre consente di spostare i ruoli server definiti dall'utente e aggiunge autorizzazioni a livello di server per i ruoli del server definito dall'utente. Il proprietario del ruolo verrà automaticamente impostato **sa** dell'entità.

## <a name="during-and-after-migration"></a>Durante e dopo la migrazione

- Come parte della migrazione di account di accesso, Data Migration Assistant assegna le autorizzazioni per entità a protezione diretta nella destinazione di SQL Server in cui si trovano in SQL Server di origine. 

  Se l'account di accesso esiste già nella destinazione di SQL Server, Data Migration Assistant viene eseguita la migrazione solo le autorizzazioni assegnate a entità a protezione diretta e non creare nuovamente l'intero account di accesso.

- Data Migration Assistant rende il migliore sforzo per associare l'account di accesso agli utenti di database se l'account di accesso esiste già nel server di destinazione.

- È consigliabile esaminare i risultati di migrazione per comprendere lo stato complessivo di tutte le azioni post-migrazione consigliate e la migrazione di account di accesso.

## <a name="resources"></a>Risorse

[Data Migration Assistant (DMA)](../dma/dma-overview.md)

[Data Migration Assistant: Impostazioni di configurazione](../dma/dma-configurationsettings.md)
