---
title: Server di pubblicazione Oracle | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.selectoraclepublisher.f1
ms.assetid: 019b7c49-dcca-445d-8969-5982a8ccbc1a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b38b397c0a2128aed5ebaba0b1367ca14ebdcd09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63022035"
---
# <a name="oracle-publisher"></a>Server di pubblicazione Oracle
  A partire da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di pubblicare i dati di un database Oracle mediante la replica transazionale o snapshot. Per altre informazioni, vedere [Panoramica della pubblicazione Oracle](non-sql/oracle-publishing-overview.md).  
  
 Il server di pubblicazione Oracle deve utilizzare un server di distribuzione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remoto nel quale deve essere eseguita la procedura guidata dopo che il software di rete Oracle necessario è stato installato e testato. Per altre informazioni, vedere [Configurare un server di pubblicazione Oracle](non-sql/configure-an-oracle-publisher.md).  
  
> [!IMPORTANT]  
>  Se un altro amministratore ha configurato il database Oracle come database di pubblicazione, dopo aver fatto clic su **Avanti** verrà richiesto di digitare la password per l'accesso alla replica utilizzata per connettersi al database Oracle. In[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà quindi definito il mapping tra l'account di accesso utilizzato e la connessione del server collegato al database Oracle. Non sarà più necessario digitare la password per le connessioni successive al database Oracle.  
  
## <a name="options"></a>Opzioni  
 **Server di pubblicazione Oracle**  
 Consente di selezionare un server di pubblicazione Oracle nell'elenco. Nell'elenco sono inclusi i server di pubblicazione Oracle precedentemente configurati per l'utilizzo del server su cui viene eseguita la procedura guidata come server di distribuzione. Se l'elenco è vuoto oppure il server di pubblicazione Oracle desiderato non è presente, fare clic su **Aggiungi server di pubblicazione Oracle**.  
  
 **Aggiungi server di pubblicazione Oracle**  
 Fare clic su questo pulsante per visualizzare la finestra di dialogo **Proprietà server di distribuzione** . In questa finestra di dialogo fare clic su **Aggiungi**e quindi su **Aggiungi server di pubblicazione Oracle**. Nella finestra di dialogo **Connetti al server** specificare il nome del server Oracle, nonché l'account di accesso e la password per lo schema utente di amministrazione della replica. Per altre informazioni, vedere [Connetti al server &#40;Oracle&#41;, Account di accesso](connect-to-server-oracle-login.md).  
  
> [!NOTE]  
>  Se il server su cui viene eseguita la procedura guidata non è stato ancora configurato come server di distribuzione, viene richiesto di eseguire la configurazione adesso.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una pubblicazione da un database Oracle](publish/create-a-publication-from-an-oracle-database.md)   

  
  
