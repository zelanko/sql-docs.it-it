---
title: Configurare le proprietà di un agente di raccolta dati | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.dc.datacollectionprop.general.f1
- sql13.swb.dc.datacollectionprop.advanced.f1
ms.assetid: cf98f57d-5a6d-4bc3-bf10-783e460fc63d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1da1a6aa4b7a98a7ac76c32effc116efdc7020d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140775"
---
# <a name="configure-properties-of-a-data-collector"></a>Configurare le proprietà di un agente di raccolta dati
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento viene descritto come configurare le proprietà di un agente di raccolta dati.  
  
## <a name="data-collection-properties-general-tab"></a>Proprietà raccolta dati (scheda Generale)  
 Utilizzare questa pagina per configurare le impostazioni per il data warehouse di gestione e specificare la posizione di archiviazione dei dati raccolti prima del caricamento nel data warehouse.  
  
 **Abilita raccolta dati**  
 Selezionare questa opzione per abilitare la raccolta dei dati. Questa impostazione equivale all'esecuzione della stored procedure sp_syscollector_enable_collector. La deselezione di questa casella di controllo disabilita la raccolta dei dati ed equivale all'esecuzione della stored procedure sp_syscollector_disable_collector.  
  
 **Server**  
 Visualizza il nome del server che ospiterà il data warehouse di gestione.  
  
 **Nome database**  
 Visualizza il nome del database relazionale utilizzato per il data warehouse di gestione.  
  
 **Test connessione**  
 Consente di testare la connessione al **Server** specificato utilizzando le informazioni fornite durante la configurazione della raccolta dati.  
  
 **Directory cache**  
 Specifica la directory in cui vengono archiviati i dati raccolti nel sistema prima di essere caricati nel data warehouse di gestione. Se la **Directory cache** non è specificata, l'agente di raccolta dati tenta di individuare le variabili di ambiente % TEMP% e % TMP% e utilizza una di queste posizioni come percorso predefinito per l'archiviazione temporanea. Se queste variabili di ambiente non sono configurate, si verifica un errore e viene chiesto di creare una directory della cache.  
  
## <a name="data-collection-properties-advanced-tab"></a>Proprietà raccolta dati (scheda Avanzate)  
 Utilizzare questa pagina per configurare le impostazioni relative ai tentativi per la connessione al data warehouse di gestione.  
  
 **Numero di tentativi se il caricamento ha esito negativo**  
 Consente di specificare il numero di volte in cui è possibile ritentare l'esecuzione di un caricamento non riuscito nel data warehouse di gestione. Il valore predefinito è 1.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire raccolta dati](../../relational-databases/data-collection/manage-data-collection.md)   
 [Configurazione del data warehouse di gestione &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
