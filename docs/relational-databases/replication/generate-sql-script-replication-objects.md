---
title: Genera script SQL (oggetti di replica) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.generatesqlscript.f1
helpviewer_keywords:
- Generate SQL Script dialog box
ms.assetid: b7ccc34e-1c22-44b8-8eb5-f6423af3164e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 474a65593b830e671a7a65557c4c5fec11aea07a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "76285863"
---
# <a name="generate-sql-script-replication-objects"></a>Genera script SQL (oggetti di replica)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  In uno script di replica sono incluse le stored procedure di sistema [!INCLUDE[tsql](../../includes/tsql-md.md)] necessarie per l'implementazione dei componenti di replica selezionati per lo script, ad esempio una pubblicazione o una sottoscrizione. Gli script di tutti i componenti di replica inclusi in una topologia devono essere creati come parte di un piano di ripristino di emergenza. Gli script possono inoltre essere utilizzati per automatizzare attività ripetitive. Sono disponibili due finestre di dialogo per lo script di oggetti di replica:  
  
-   **Genera script SQL**, disponibile dal menu di scelta rapida della cartella **Replica** e da tutte le sottocartelle in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Questa finestra di dialogo consente di creare lo script di tutti gli oggetti di replica in un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Genera script SQL \<NomeOggetto>** , disponibile dal menu di scelta rapida associato a pubblicazioni e sottoscrizioni. Questa finestra di dialogo consente di creare lo script di singoli oggetti.  
  
 Queste finestre di dialogo consentono di creare lo script di oggetti in una singola istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ma non di stabilire connessioni ad altre istanze per generare lo script degli oggetti correlati.  
  
## <a name="generate-sql-script-options"></a>Opzioni Genera script SQL  
 **Proprietà server di distribuzione**  
 Selezionare questa opzione per creare script di stored procedure che consentano di attivare o disabilitare il server di distribuzione, aggiungere o eliminare i server di pubblicazione associati a quello di distribuzione e creare o rimuovere il database di distribuzione.  
  
 **Pubblicazioni nelle origini dei dati seguenti**  
 Selezionare questa opzione per creare script di stored procedure che consentano di attivare o disabilitare la pubblicazione e creare o eliminare pubblicazioni, articoli, sottoscrizioni push e processi di replica.  
  
 **Sottoscrizioni nelle origini dei dati seguenti**  
 Selezionare questa opzione per creare lo script di stored procedure che consentano di creare o eliminare sottoscrizioni pull e processi di replica.  
  
 **Per creare o attivare i componenti** e **Per rimuovere o disabilitare i componenti**  
 Specificare se nello script devono essere inclusi i comandi per la creazione o la rimozione di un oggetto di replica. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di utilizzare questa finestra di dialogo per creare un set di script che consenta di attivare e disabilitare i componenti.  
  
 **Processi di replica**  
 Selezionare questa opzione per creare lo script dei processi di replica oltre a quello delle chiamate di stored procedure. Questa opzione è disponibile solo quando si crea lo script da un server di distribuzione.  
  
 Le stored procedure di replica creano i processi necessari al momento dell'esecuzione e non è pertanto necessario selezionare l'opzione. Può tuttavia risultare utile disporre di un record dei processi creati in caso sia necessario ricreare un singolo processo.  
  
## <a name="generate-sql-script-objectname-options"></a>Opzioni Genera script SQL \<NomeOggetto>  
 **Per creare o attivare i componenti** e **Per rimuovere o disabilitare i componenti**  
 Specificare se nello script devono essere inclusi i comandi per la creazione o la rimozione di un oggetto di replica. [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di utilizzare la finestra di dialogo, creando un set di script che consenta di attivare e disabilitare i componenti.  
  
 **Processi di replica**  
 Questa opzione è disponibile solo dalla finestra di dialogo **Genera script SQL** .  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di script di replica](../../relational-databases/replication/scripting-replication.md)  
  
  
