---
title: Replica di tipo merge | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], about merge replication
- merge replication [SQL Server replication]
ms.assetid: ff87c368-4c00-4e48-809d-ea752839551e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8617fcbc7204dfe29d3f6a02a0240812b5bd682c
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175820"
---
# <a name="merge-replication"></a>Replica di tipo merge
  In genere la replica di tipo merge, come la replica transazionale, inizia con uno snapshot degli oggetti e dei dati del database di pubblicazione. Eventuali modifiche dei dati e dello schema apportate successivamente nel server di pubblicazione e nei Sottoscrittori vengono rilevate tramite trigger. Al momento della connessione alla rete il Sottoscrittore esegue la sincronizzazione con il server di pubblicazione e scambia con esso le righe modificate dopo l'ultima sincronizzazione.

 In genere la replica di tipo merge è utilizzata in ambienti server-to-client. La replica di tipo merge è adatta alle seguenti situazioni:

-   Più Sottoscrittori potrebbero richiedere l'aggiornamento dei dati in ore diverse e la distribuzione delle modifiche al server di pubblicazione e ad altri Sottoscrittori.

-   I Sottoscrittori devono ricevere i dati, eseguire le modifiche offline e sincronizzarle successivamente con il server di pubblicazione e i Sottoscrittori.

-   Per ogni Sottoscrittore è necessaria una diversa partizione di dati.

-   È necessario essere in grado di individuare e risolvere tempestivamente eventuali conflitti che potrebbero verificarsi.

-   È necessario lo scambio di dati net piuttosto che l'accesso a stati di dati intermedi. Ad esempio, se una riga viene modificata cinque volte nel Sottoscrittore prima della sincronizzazione con un server di pubblicazione, la riga verrà modificata solo una volta nel server di pubblicazione per riflettere la modifica dei dati net, ovvero il quinto valore.

 La replica di tipo merge consente a vari siti di eseguire elaborazioni in modo autonomo e di unire quindi gli aggiornamenti in un unico risultato uniforme. Dato che gli aggiornamenti vengono eseguiti in più nodi, è possibile che dati uguali siano aggiornati dal server di pubblicazione e da più Sottoscrittori, con la conseguente possibilità di conflitti quando viene eseguito il merge degli aggiornamenti. La replica di tipo merge offre tuttavia diversi modi di risoluzione dei conflitti.

 La replica di tipo merge viene implementata dall'agente snapshot e dall'agente di merge di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Se la pubblicazione non è filtrata o utilizza filtri statici, l'agente snapshot crea un singolo snapshot. Se la pubblicazione utilizza filtri con parametri, l'agente snapshot crea uno snapshot per ogni partizione di dati. L'agente di merge applica gli snapshot iniziali ai Sottoscrittori e unisce le modifiche ai dati incrementali apportate nel server di pubblicazione o nei Sottoscrittori dopo la creazione dello snapshot iniziale, quindi rileva e risolve eventuali conflitti in base alle regole configurate.

 Per tener traccia delle modifiche, tramite la replica di tipo merge e la replica transazionale con sottoscrizioni ad aggiornamento in coda deve essere possibile identificare in modo univoco ogni riga di ogni tabella pubblicata. A tale scopo, tramite la replica di tipo merge la colonna `rowguid` viene aggiunta a ogni tabella, a meno che in essa non sia già inclusa una colonna di tipo di dati `uniqueidentifier` con il set di proprietà `ROWGUIDCOL`, in questo caso viene utilizzata la colonna in questione. Se la tabella viene rimossa dalla pubblicazione, la colonna `rowguid` viene eliminata; se per il rilevamento è stata utilizzata una colonna esistente, questa non viene eliminata. In un filtro non deve essere inclusa la colonna `rowguidcol` utilizzata dalla replica per identificare le righe. La funzione `newid()` è predefinita per la colonna `rowguid`, in ogni caso i clienti possono fornire un GUID per ogni riga, se necessario. Non specificare tuttavia il valore 00000000-0000-0000-0000-000000000000.

 Nella figura seguente vengono illustrati i componenti utilizzati nella replica di tipo merge.

 ![Componenti e flusso di dati per la replica di tipo merge](../media/merge.gif "Componenti e flusso di dati per la replica di tipo merge")


