---
title: Abilitare l'opzione Blocco di pagine in memoria (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Lock Pages in Memory option
ms.assetid: cd581fbc-4747-439e-87f9-2f18e39c5bb9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0f6e938e3212e519ab51be1faf3f18e28957ef3e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62782279"
---
# <a name="enable-the-lock-pages-in-memory-option-windows"></a>Abilitazione dell'opzione Blocco di pagine in memoria (Windows)
  Questi criteri di Windows determinano gli account autorizzati a usare un processo per mantenere i dati nella memoria fisica, impedendo al sistema di eseguire il paging dei dati nella memoria virtuale su disco.  
  
> [!NOTE]  
>  Bloccando le pagine in memoria è possibile migliorare le prestazioni nei casi in cui è previsto il paging della memoria su disco.  
  
 Utilizzare lo strumento Criteri di gruppo di Windows (gpedit.msc) per abilitare questi criteri per l'account utilizzato da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per modificare i criteri, è necessario essere un amministratore di sistema.  
  
### <a name="to-enable-the-lock-pages-in-memory-option"></a>Per abilitare l'opzione Blocco di pagine in memoria  
  
1.  Fare clic sul menu **Start** e scegliere **Esegui**. Nel **aperto** , digitare `gpedit.msc`.  
  
2.  Nella console **Editor Criteri di gruppo locali** espandere **Configurazione computer**, quindi **Impostazioni di Windows**.  
  
3.  Espandere **Impostazioni sicurezza**e quindi espandere **Criteri locali**.  
  
4.  Selezionare la cartella **Assegnazione diritti utente** .  
  
     I criteri verranno visualizzati nel riquadro dei dettagli.  
  
5.  Nel riquadro fare doppio clic su **Blocco di pagine in memoria**.  
  
6.  Nella finestra di dialogo **Impostazioni di sicurezza locali - Blocco di pagine in memoria** fare clic su **Aggiungi utente o gruppo**.  
  
7.  Nella finestra di dialogo **Selezione utenti, computer, account del servizio o gruppi** aggiungere un account con privilegi per l'esecuzione di sqlservr.exe.  
  
8.  Effettuare la disconnessione e nuovamente l'accesso per rendere operativa questa modifica.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzioni di configurazione del server Server Memory](server-memory-server-configuration-options.md)  
  
  
