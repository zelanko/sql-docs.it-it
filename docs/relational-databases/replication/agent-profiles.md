---
title: Profili agenti | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.profiles.perfprofiles.f1
helpviewer_keywords:
- Agent Profiles dialog box
ms.assetid: 0422e99c-e688-419b-bb4c-c7bebeef1d8d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: e90b24ea20076a8af4622c144358e50e7b998ad1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85739119"
---
# <a name="agent-profiles"></a>Profili agenti
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Utilizzare la finestra di dialogo **Profili agenti** per gestire i profili degli agenti. I profili agenti consentono di gestire facilmente i parametri di run-time per ogni agente. Ogni agente dispone di un profilo predefinito e alcuni agenti dispongono di profili predefiniti aggiuntivi. L'agente di merge, ad esempio, dispone di un profilo "collegamento lento" dedicato alle connessioni a larghezza di banda ridotta. I profili predefiniti sono sufficienti per la maggior parte delle applicazioni, ma è possibile creare profili definiti dall'utente, che consentono di personalizzare il funzionamento degli agenti.  
  
## <a name="options"></a>Opzioni  
 **Selezione pagina**  
 Consente di selezionare un agente nel riquadro sinistro in modo da visualizzare i rispettivi profili in quello destro.  
  
 **Predefinito per i nuovi agenti**  
 Consente di selezionare il profilo che verrà utilizzato durante la creazione dei processi per un dato tipo di agente. Se ad esempio si creano varie sottoscrizioni a una pubblicazione di tipo merge, il processo dell'agente di merge per ogni sottoscrizione utilizzerà il profilo selezionato. Per modificare il profilo di processi esistenti, selezionare un profilo e quindi fare clic su **Modifica agenti esistenti**.  
  
 **Nome**  
 Nome del profilo.  
  
 **Tipo**  
 Tipo di profilo: **Utente** (definito dall'utente) o **Sistema** (predefinito).  
  
 **Proprietà (...)**  
 Fare clic su questo pulsante per visualizzare i valori utilizzati per ogni parametro nel profilo agente.  
  
 **Nuovo**  
 Fare clic su questo pulsante per creare un nuovo profilo.  
  
 **Elimina**  
 Selezionare un profilo definito dall'utente e quindi fare clic su **Elimina** per eliminarlo. I profili predefiniti non possono essere eliminati.  
  
 **Modifica agenti esistenti**  
 Selezionare un profilo e quindi fare clic su **Modifica agenti esistenti** per specificare che tutti i processi esistenti per un dato tipo di agente devono utilizzare il profilo selezionato. Se ad esempio sono state create varie sottoscrizioni a una pubblicazione di tipo merge e si desidera modificare il profilo per specificare che il processo dell'agente di merge per ogni sottoscrizione deve utilizzare il **Profilo agente a collegamento lento**, selezionare tale profilo e quindi fare clic su **Modifica agenti esistenti**.  
  
## <a name="see-also"></a>Vedere anche  
 [Usare i profili agenti di replica](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Panoramica degli agenti di replica](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Profili degli agenti di replica](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  
