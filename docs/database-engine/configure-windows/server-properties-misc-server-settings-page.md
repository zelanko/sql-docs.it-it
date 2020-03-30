---
title: Proprietà server - pagina Impostazioni varie | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.miscserversettings.f1
ms.assetid: b170c066-30cd-42dd-8d34-aa129ea09551
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 62a8af2e4a82a0a0bdeec231db62c2166ed030de
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68030835"
---
# <a name="server-properties---misc-server-settings-page"></a>Proprietà server - pagina Impostazioni varie
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilizzare questa pagina per visualizzare o modificare le impostazioni del server.  
  
## <a name="options"></a>Opzioni  
 **Lingua predefinita per l'utente**  
 Specifica la lingua predefinita per tutti i nuovi account di accesso creati.  
  
 **Consenti attivazione di trigger da altri trigger**  
 Consente di controllare l'esecuzione di un'azione da parte di un trigger per l'inizializzazione di un altro trigger. Quando questa opzione è deselezionata, i trigger non possono essere attivati da altri trigger. Quando questa opzione è selezionata, i trigger possono essere attivati da altri trigger fino a un massimo di 32 livelli.  
  
 **Usa Query Governor per evitare query con esecuzione prolungata**  
 Consente di specificare un limite di tempo massimo entro il quale può essere eseguita la query. Il costo della query equivale al tempo, in secondi, stimato per l'esecuzione di una query in una configurazione hardware specifica. Per impostazione predefinita, la funzionalità Query Governor è disattivata ed è consentita l'esecuzione di tutte le query. Se questa opzione è selezionata, è necessario immettere un limite di tempo nella casella di testo sottostante. Se si specifica un valore diverso da zero e positivo, Query Governor non consentirà l'esecuzione delle query il cui costo stimato supera tale valore.  
  
 **Interpreta l'immissione di un anno a due cifre come un anno compreso nell'intervallo dal**  
 Consente di specificare l'intervallo di date a 100 anni per l'interpretazione dei valori degli anni immessi con due cifre. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpreterà i valori delle date immesse con due cifre come riferiti all'anno che termina per tali cifre e rientra nell'intervallo specificato.  
  
 Impostare l'anno di fine nella casella a destra. Quando l'anno di fine viene salvato, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] popola automaticamente la casella a sinistra con l'anno di inizio.  
  
 **Valori configurati**  
 Consente di visualizzare i valori configurati per le opzioni nel riquadro. Se si modificano i valori, fare clic su **Valori correnti** per verificare se le modifiche sono diventate effettive. Se le modifiche non sono diventate effettive, è innanzitutto necessario riavviare l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Valori correnti**  
 Consente di visualizzare i valori correnti per le opzioni contenute nel riquadro. I valori sono di sola lettura.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
