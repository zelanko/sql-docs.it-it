---
title: Oggetti creati nel server di pubblicazione Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], objects created
ms.assetid: c58a124b-4da7-46e2-9292-af8ce9e6664b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 405deb86567c596372777dff5e6ccb9dd2e95fb1
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85901231"
---
# <a name="objects-created-on-the-oracle-publisher"></a>Oggetti creati nel server di pubblicazione Oracle
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  La replica di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] installa oggetti di database nel server di pubblicazione Oracle in modo da abilitare il rilevamento e l'inoltro delle modifiche. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non installa file binari nel server di pubblicazione Oracle. Nella tabella seguente vengono elencati gli oggetti creati nel server di pubblicazione Oracle quando viene identificato come server di pubblicazione nel server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Le descrizioni degli oggetti hanno esclusivamente scopo informativo. Non modificare tali oggetti.  
  
|Nome oggetto|Tipo di oggetto|Descrizione|  
|-----------------|-----------------|-----------------|  
|HREPL_ArticleNlog_V|Tabella|Tabella di rilevamento delle modifiche utilizzata per archiviare informazioni quando vengono apportate modifiche alla tabella pubblicata. Viene creata una tabella di rilevamento delle modifiche per ogni tabella pubblicata.|  
|HREPL_Changes|Tabella|Tabella utilizzata internamente dal processo Xactset per determinare il numero di modifiche in attesa di assegnazione a un set di transazioni. Per altre informazioni su questo processo, vedere [Ottimizzazione delle prestazioni per i server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/performance-tuning-for-oracle-publishers.md).|  
|HREPL_Distributor|Tabella|Tabella dello stato del server di distribuzione utilizzata per gestire le informazioni relative al server di distribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] associato al server di pubblicazione Oracle.|  
|HREPL_Event|Tabella|Tabella di eventi utilizzata per sincronizzare snapshot e richieste di conteggio delle righe.|  
|HREPL_Mutex|Tabella|Tabella utilizzata per garantire che la procedura di package Oracle PopulatePollTable non venga eseguita simultaneamente dall'agente di lettura log e dal processo del database.|  
|HREPL_Poll|Tabella|Tabella utilizzata per identificare le voci della tabella di log associate a set di modifiche alle tabelle pubblicate.|  
|HREPL_PublishedTables|Tabella|Tabella contenente una voce per ogni articolo di una pubblicazione transazionale.|  
|HREPL_Publisher|Tabella|Tabella dello stato del server di pubblicazione utilizzata per gestire informazioni specifiche del server di pubblicazione.|  
|HREPL_SchemaFilter|Tabella|Tabella contenente schemi non visualizzati in caso di pubblicazione tramite la Creazione guidata nuova pubblicazione.|  
|HREPL_XactsetCreateTimes|Tabella|Tabella che identifica l'ora di creazione associata a ogni set di transazioni.|  
|HREPL_XactsetJob|Tabella|Tabella con le impostazioni dei parametri correnti per il processo Xactset.|  
|HREPL_Pollid|Sequenza|Sequenza utilizzata per generare ID di polling.|  
|HREPL_Seq|Sequenza|Sequenza utilizzata per ordinare i comandi di modifica.|  
|HREPL_Stmt|Sequenza|Sequenza utilizzata per generare ID di istruzione.|  
|HREPL|Package e corpo package|Package di codice di supporto del server di pubblicazione, creato nel server di pubblicazione.|  
|MSSQLSERVERDISTRIBUTOR|Sinonimo public|Sinonimo public per la tabella HREPL_Distributor. Se si configura un server di distribuzione da utilizzare con un server di pubblicazione Oracle e questo sinonimo è già presente nel database, viene eliminato e ricreato.<br /><br /> Eliminando il sinonimo public e l'utente di replica Oracle configurato con l'opzione CASCADE verranno rimossi tutti gli oggetti di replica dal server di pubblicazione Oracle.|  
|HREPL_Len_I_J_K|Funzione|Funzione definita all'esterno del codice del package di pubblicazione Oracle, utilizzata per eseguire query relative alla lunghezza di una colonna LONG (in caso di generazione di comandi con parametri per tabelle con colonne LONG pubblicate). Viene creata una funzione per ogni tabella pubblicata con una colonna LONG.|  
|HREPL_DropPublisher|Procedura|Procedura definita all'esterno del codice del package di pubblicazione Oracle, utilizzata per eliminare il server di pubblicazione Oracle.|  
|HREPL_ExecuteCommand|Procedura|Procedura definita all'esterno del codice del package di pubblicazione Oracle, utilizzata per eseguire un comando nel server di pubblicazione.|  
|HREPL_ArticleN_Trigger_Row|Trigger|Trigger generato per ogni tabella pubblicata, utilizzato per rilevare le modifiche alle righe.|  
|HREPL_ArticleN_Trigger_Stmt|Trigger|Trigger generato per ogni tabella pubblicata, utilizzato per rilevare le modifiche a livello di istruzione.|  
|HREPL_Article_I_J|Visualizza|Vista creata per ogni tabella pubblicata, utilizzata per eseguire query sulla tabella pubblicata.|  
|HREPL_Log_I_J_K|Visualizza|Vista creata per ogni tabella pubblicata, utilizzata per eseguire query sulla tabella di rilevamento delle modifiche.|  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un server di pubblicazione Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Glossario dei termini per la pubblicazione Oracle](../../../relational-databases/replication/non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Panoramica della pubblicazione Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
