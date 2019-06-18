---
title: Informazioni sulla gestione delle finestre di SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- autohide [SQL Server Management Studio]
- SQL Server Management Studio [SQL Server], tool windows
- push pin [SQL Server Management Studio]
- tool windows [SQL Server Management Studio]
ms.assetid: bebf8383-dcaf-466e-84f5-63b81c9cfe52
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: b9bd9f0a6698b5af88d7a8bf86752f6d1c11bd6b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65090035"
---
# <a name="understand-sql-server-management-studio-windows-management"></a>Informazioni sulla gestione delle finestre di SQL Server Management Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Le finestre degli strumenti in [!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] costituiscono un sistema efficiente, flessibile e funzionale che consente di eseguire le operazioni seguenti:  
  
-   Ingrandire l'area di lavoro dell'utente per facilitare lo sviluppo e la gestione.  
  
-   Ridurre il numero di finestre inutilizzate visualizzate contemporaneamente.  
  
-   Personalizzare con facilità l'ambiente utente.  
  
La capacità di gestire le finestre è fondamentale per l'ambiente [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] . Gli utenti possono accedere con facilità alle finestre e agli strumenti utilizzati con maggiore frequenza. Possono controllare la quantità di spazio da allocare a diverse informazioni, mentre l'ambiente ottimizza di conseguenza lo spazio disponibile per la modifica di query. È possibile spostare finestre in posizioni diverse sullo schermo. Molte finestre possono essere disancorate e trascinate all'esterno della cornice di [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] , un'opzione che risulta particolarmente utile quando si utilizzano più monitor.  
  
Per aumentare le dimensioni dell'area di modifica mantenendo la funzionalità, in tutte le finestre è disponibile la caratteristica Nascondi automaticamente che consente di visualizzare la finestra come una scheda su una barra lungo il bordo dell'ambiente [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] principale. Quando si posiziona il puntatore su una scheda, viene visualizzata la finestra sottostante. Per attivare o disattivare la funzionalità Nascondi automaticamente, fare clic sul pulsante **Nascondi automaticamente** rappresentato dall'icona di una puntina da disegno nell'angolo superiore destro della finestra. È inoltre disponibile l'opzione **Nascondi tutto automaticamente** nel menu **Finestra** .  
  
Alcuni componenti possono essere configurati in modalità a schede, per visualizzare i componenti sotto forma di schede nella stessa posizione di ancoraggio, oppure in modalità a più documenti (MDI, Multiple Document Interface) per visualizzare ogni documento in una finestra separata. Per configurare questa funzionalità, scegliere **Opzioni** dal menu **Strumenti**, fare clic su **Ambiente**e quindi su **Generale**.  
  
> [!IMPORTANT]  
> Quando un account di accesso (o un utente di database indipendente) si connette e viene autenticato, tramite la connessione vengono archiviate le informazioni relative all'identità sull'account di accesso. In caso di un account di accesso con l'autenticazione di Windows, sono incluse informazioni sull'appartenenza ai gruppi di Windows. L'identità dell'account di accesso rimane autenticata, a condizione che la connessione venga mantenuta. Per forzare le modifiche nell'identità, ad esempio una reimpostazione della password o una modifica dell'appartenenza al gruppo di Windows, l'account di accesso deve disconnettersi dall'autorità di autenticazione (Windows o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]) e accedere di nuovo. Un membro del ruolo predefinito del server **sysadmin** o qualsiasi account di accesso con l'autorizzazione **ALTER ANY CONNECTION** può usare il comando **KILL** per terminare una connessione e forzare la riconnessione di un account di accesso. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] è possibile usare di nuovo le informazioni di connessione quando si aprono più connessioni alle finestre Esplora oggetti ed Editor di query. Chiudere tutte le connessioni per forzare la riconnessione.  
  
> [!IMPORTANT]  
> Quando un account di accesso (o un utente di database indipendente) si connette e viene autenticato, tramite la connessione vengono memorizzate nella cache le informazioni relative all'identità sull'account di accesso. In caso di un account di accesso con l'autenticazione di Windows, sono incluse informazioni sull'appartenenza ai gruppi di Windows. L'identità dell'account di accesso rimane autenticata, a condizione che la connessione venga mantenuta. Per forzare le modifiche nell'identità, ad esempio una reimpostazione della password o una modifica dell'appartenenza al gruppo di Windows, l'account di accesso deve disconnettersi dall'autorità di autenticazione (Windows o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]) e accedere di nuovo. Un membro del ruolo predefinito del server **sysadmin** o qualsiasi account di accesso con l'autorizzazione **ALTER ANY CONNECTION** può usare il comando **KILL** per terminare una connessione e forzare la riconnessione di un account di accesso. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] è possibile usare di nuovo le informazioni di connessione quando si aprono più connessioni alle finestre Esplora oggetti ed Editor di query. Chiudere tutte le connessioni per forzare la riconnessione.  
  
## <a name="see-also"></a>Vedere anche  
[Utilizzo di SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[Ambiente di SQL Server Management Studio](../ssms/the-sql-server-management-studio-environment.md)  
  
