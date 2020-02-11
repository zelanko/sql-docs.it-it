---
title: Proprietà replica di disponibilità (Pagina Generale) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilityreplicaproperties.general.f1
ms.assetid: 8318fefb-e045-4fab-8507-e1951fc7cec6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07652cec7b3b7a17c4b994eb68afd939e15244a3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62791905"
---
# <a name="availability-replica-properties-general-page"></a>Proprietà replica di disponibilità (Pagina Generale)
  Usare questa finestra di dialogo per visualizzare le proprietà di una replica di disponibilità.  
  
## <a name="task-list"></a>Elenco attività  
 **Per visualizzare le proprietà della replica di disponibilità**  
  
-   [Visualizzazione delle proprietà della replica di disponibilità &#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [Usare il dashboard AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Nome gruppo di disponibilità**  
 Nome del gruppo di disponibilità. Si tratta di un nome specificato dall'utente che deve essere univoco all'interno del cluster di failover di Windows Server (WSFC).  
  
 **Istanza del server**  
 Nome del server dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che ospita la replica corrente e, per un'istanza non predefinita, il nome dell'istanza.  
  
 **Ruolo**  
 **Server/istanza primaria**  
 Attualmente la replica primaria.  
  
 **Secondari**  
 Attualmente una replica secondaria.  
  
 **Risoluzione**  
 È in corso la risoluzione del ruolo della replica nel ruolo primario o secondario.  
  
 **Modalità di disponibilità**  
 Modalità di disponibilità della replica. I valori possibili sono:  
  
 **Commit asincrono**  
 La replica primaria può eseguire il commit delle transazioni senza attendere che la replica secondaria salvi il log su disco.  
  
 **Commit sincrono**  
 La replica primaria attende che la replica secondaria salvi la transazione su disco prima di eseguirne il commit.  
  
 Per ulteriori informazioni, vedere [modalità di disponibilità (gruppi di disponibilità AlwaysOn)](availability-modes-always-on-availability-groups.md).  
  
 **Modalità di failover**  
 Modalità di failover della replica. I valori possibili sono:  
  
 **Automatico**  
 Failover automatico. La replica è una destinazione per i failover automatici. Questa opzione è supportata solo se la modalità di disponibilità è impostata sul commit sincrono.  
  
 **Manuale**  
 Failover manuale. Il failover della replica può essere eseguito solo manualmente dall'amministratore di database.  
  
 **Connessioni nel ruolo primario**  
 Tipo di connessioni client supportate quando la replica detiene il ruolo primario.  
  
 **Consenti tutte le connessioni**  
 Sono consentite tutte le connessioni ai database nella replica primaria. Si tratta dell'impostazione predefinita.  
  
 **Consenti connessioni in lettura/scrittura**  
 Non sono consentite le connessioni in cui la proprietà di connessione Finalità dell'applicazione è impostata su **ReadOnly** . Se la proprietà finalità dell'applicazione è impostata su **ReadWrite** o se la proprietà di connessione finalità dell'applicazione non è impostata, la connessione è consentita.  
  
 **Secondario leggibile**  
 Specifica se una replica di disponibilità che esegue il ruolo secondario, ovvero una replica secondaria, può accettare connessioni dai client. I valori possibili sono:  
  
 **No**  
 Non sono consentite connessioni dirette ai database secondari di questa replica. I database non sono disponibili per l'accesso in lettura. Si tratta dell'impostazione predefinita.  
  
 **Solo con finalità di lettura**  
 Sono consentite solo connessioni dirette di sola lettura ai database secondari di questa replica. Il database o i database secondari sono tutti disponibili per l'accesso in lettura.  
  
 **Sì**  
 Sono consentite tutte le connessioni ai database secondari di questa replica, ma solo per l'accesso in lettura. Il database o i database secondari sono tutti disponibili per l'accesso in lettura.  
  
 Per ulteriori informazioni, vedere [repliche secondarie attive: repliche secondarie leggibili (gruppi di disponibilità AlwaysOn)](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 **Timeout sessione (secondi)**  
 Periodo di timeout in secondi. Il periodo di timeout è il tempo di attesa massimo rispettato dalla replica per la ricezione di un messaggio da un'altra replica, prima di considerare la connessione tra la replica primaria e secondaria non riuscita. Il timeout della sessione rileva se le repliche secondarie sono connesse alla replica primaria. Se viene rilevata una connessione non riuscita con una replica secondaria, la replica primaria considera la replica secondaria come NOT_SYNCHRONIZED. Se viene rilevata una connessione non riuscita con una replica primaria, una replica secondaria tenta di riconnettersi.  
  
> [!NOTE]  
>  I timeout della sessione non provocano failover automatici.  
  
 **URL endpoint**  
 Rappresentazione di stringa dell'endpoint del mirroring di database specificato dall'utente usato dalle connessioni tra repliche primarie e secondarie per la sincronizzazione dei dati. Per informazioni sulla sintassi degli URL dell'endpoint, vedere [Specificare l'URL dell'endpoint quando si aggiunge o si modifica una replica di disponibilità &#40;SQL Server&#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
