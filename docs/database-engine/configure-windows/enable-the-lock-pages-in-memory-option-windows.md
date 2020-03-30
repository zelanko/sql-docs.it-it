---
title: Abilitare l'opzione Blocco di pagine in memoria (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Lock Pages in Memory option
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8041f5f057962af79d75f121423233d3d6a3a806
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68011770"
---
# <a name="enable-the-lock-pages-in-memory-option-windows"></a>Abilitazione dell'opzione Blocco di pagine in memoria (Windows)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questi criteri di Windows determinano gli account autorizzati a usare un processo per mantenere i dati nella memoria fisica, impedendo al sistema di eseguire il paging dei dati nella memoria virtuale su disco.  
  
> [!NOTE]  
>  Bloccando le pagine in memoria è possibile migliorare le prestazioni nei casi in cui è previsto il paging della memoria su disco.  
  
 Utilizzare lo strumento Criteri di gruppo di Windows (gpedit.msc) per abilitare questi criteri per l'account utilizzato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per modificare i criteri, è necessario essere un amministratore di sistema.  
  
### <a name="to-enable-the-lock-pages-in-memory-option"></a>Per abilitare l'opzione Blocco di pagine in memoria  
  
1.  Fare clic sul menu **Start** e scegliere **Esegui**. Nella casella **Apri** digitare **gpedit.msc**.  
  
2.  Nella console **Editor Criteri di gruppo locali** espandere **Configurazione computer**, quindi **Impostazioni di Windows**.  
  
3.  Espandere **Impostazioni sicurezza**e quindi espandere **Criteri locali**.  
  
4.  Selezionare la cartella **Assegnazione diritti utente** .  
  
     I criteri verranno visualizzati nel riquadro dei dettagli.  
  
5.  Nel riquadro fare doppio clic su **Blocco di pagine in memoria**.  
  
6.  Nella finestra di dialogo **Impostazioni di sicurezza locali - Blocco di pagine in memoria** fare clic su **Aggiungi utente o gruppo**.  
  
7.  Nella finestra di dialogo **Select Users, Service Accounts, or Groups** (Selezione utenti, account di servizio o gruppi) selezionare l'account del servizio SQL Server.  
  
8.  Riavviare il servizio SQL Server per rendere effettiva questa impostazione.
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server Server Memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
  
