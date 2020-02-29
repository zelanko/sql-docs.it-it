---
title: Panoramica del modello di pubblicazione della replica | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], publishing model
- subscriptions [SQL Server replication], about subscriptions
- articles [SQL Server replication]
- publications [SQL Server replication]
- Publishers [SQL Server replication], about Publishers
- Subscribers [SQL Server replication]
- Distributors [SQL Server replication], about Distributors
- Subscribers [SQL Server replication], about Subscribers
- articles [SQL Server replication], about articles
- publications [SQL Server replication], about publications
- Distributors [SQL Server replication]
ms.assetid: b9567832-e6a8-45b2-a3ed-ea12aa002f4b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9c5e1eb0a35081cd9392178412db990308efcd0b
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176731"
---
# <a name="replication-publishing-model-overview"></a>Panoramica del modello di pubblicazione della replica
  Nella replica viene utilizzata una metafora basata sul settore dell'editoria per rappresentare i componenti di una topologia di replica: server di pubblicazione, server di distribuzione, sottoscrittori, pubblicazioni, articoli e sottoscrizioni. Il processo di replica in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è paragonabile a quello di pubblicazione e distribuzione di una rivista:

-   Un editore di riviste produce una o più pubblicazioni

-   Una pubblicazione contiene articoli

-   L'editore distribuisce la rivista direttamente o tramite un distributore

-   I sottoscrittori ricevono le pubblicazioni per le quali hanno effettuato una sottoscrizione

 Sebbene la metafora della rivista si riveli utile per comprendere il concetto di replica, è importante osservare che in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] la replica include funzionalità non rappresentate nella metafora, in particolare la possibilità per un Sottoscrittore di apportare aggiornamenti e per un server di pubblicazione di inviare modifiche incrementali agli articoli di una pubblicazione.

 Una *topologia di replica* definisce la relazione tra i server e le copie di dati, nonché la logica che determina il flusso dei dati tra server. Sono disponibili diversi processi di replica, denominati *agenti*, responsabili della copia e del trasferimento di dati tra il server di pubblicazione e i Sottoscrittori. Nella figura seguente viene offerta una panoramica dei componenti e dei processi coinvolti nella replica.

 ![Componenti e flusso di dati per la replica](../media/replintro1.gif "Componenti e flusso di dati per la replica")

## <a name="publisher"></a>Editore
 Il server di pubblicazione è un'istanza di database che rende i dati disponibili in altre posizioni tramite la replica. Può disporre di una o più pubblicazioni, ognuna delle quali definisce un set logicamente correlato di dati e oggetti da replicare.

## <a name="distributor"></a>Database di distribuzione
 Il server di distribuzione è un'istanza di database che funge da archivio per i dati specifici della replica associati a uno o più server di pubblicazione. Ogni server di pubblicazione è associato a un singolo database, denominato database di distribuzione, nel server di distribuzione. Nel database di distribuzione vengono archiviati i dati relativi allo stato di replica e i metadati sulla pubblicazione. In alcuni casi, il database funge inoltre da coda per i dati trasferiti dal server di pubblicazione ai Sottoscrittori. Frequentemente, una singola istanza di server di database funge sia da server di pubblicazione che da server di distribuzione. Questa configurazione viene denominata *server di distribuzione locale*. In caso di configurazione del server di pubblicazione e del server di distribuzione in istanze di server di database separate, il server di distribuzione è noto come *server di distribuzione remoto*.

## <a name="subscribers"></a>Sottoscrittori
 Un Sottoscrittore è un'istanza di database che riceve i dati replicati da uno o più server di pubblicazione e una o più pubblicazioni. A seconda del tipo di replica selezionato, il Sottoscrittore può inoltre passare modifiche di dati al server di pubblicazione oppure ripubblicare i dati per altri Sottoscrittori.

## <a name="article"></a>Articolo
 Un articolo identifica un oggetto di database incluso in una pubblicazione. Una pubblicazione può contenere diversi tipi di articoli, tra cui tabelle, viste, stored procedure e altri oggetti. In caso di pubblicazione delle tabelle come articoli, è possibile utilizzare filtri per limitare le colonne e le righe di dati inviate ai Sottoscrittori.

## <a name="publication"></a>Pubblicazione
 Una pubblicazione è una raccolta di uno o più articoli di un database. Il raggruppamento di più articoli in una pubblicazione semplifica la selezione di un set logicamente correlato di dati e oggetti di database replicati come unità.

## <a name="subscription"></a>Subscription
 Una sottoscrizione è una richiesta di recapito di una copia di una pubblicazione a un Sottoscrittore. Una sottoscrizione definisce la pubblicazione che verrà ricevuta, insieme alla posizione e al momento in cui l'operazione verrà eseguita. Esistono due tipi di sottoscrizioni: push e pull. Per altre informazioni sulle sottoscrizioni push e pull, vedere [Sottoscrizione delle pubblicazioni](../subscribe-to-publications.md).

## <a name="see-also"></a>Vedere anche
 [Panoramica degli agenti di replica](../agents/replication-agents-overview.md) [tipi di replica configurazione della](../types-of-replication.md) [replica per gruppi di disponibilità AlwaysOn (SQL Server)](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) [gestione di un database di pubblicazione AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/maintaining-an-always-on-publication-database-sql-server.md)


