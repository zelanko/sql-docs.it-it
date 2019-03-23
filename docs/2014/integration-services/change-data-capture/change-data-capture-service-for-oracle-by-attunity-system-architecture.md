---
title: Architettura di sistema di Change Data Capture Service per Oracle di Attunity | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1db6c737-3c60-4066-a0a3-3611e1c83e4e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 84ac0e6065fa3fb4845e0e3a47ce56816705e80d
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58389399"
---
# <a name="change-data-capture-service-for-oracle-by-attunity-system-architecture"></a>Architettura di sistema del servizio Change Data Capture per Oracle di Attunity
  Con il servizio CDC per Oracle è possibile acquisire le modifiche apportate alle tabelle selezionate in uno o più database Oracle di origine nei database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC presenti in un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Nel diagramma seguente vengono illustrati i componenti che costituiscono il servizio CDC per Oracle.  
  
 ![Architettura dei servizi](../media/service-architecture.gif "Architettura dei servizi")  
  
 In questa figura sono illustrate quattro piattaforme utilizzate. Sebbene in molti casi queste piattaforme possano sovrapporsi, il diagramma rappresenta un caso di utilizzo standard. Ad esempio, è logico che il database Oracle e il database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] vengano eseguiti ciascuno in un computer separato e non vengano condivisi con la piattaforma del servizio Oracle CDC o la piattaforma da cui viene progettato il servizio CDC. Nella figura sono illustrate le piattaforme seguenti:  
  
-   Il servizio Oracle CDC: Può trattarsi di qualsiasi computer Windows supportato in cui è installato ed eseguire il servizio Oracle CDC. Questa piattaforma può inoltre rappresentare un nodo del cluster in un cluster di failover Microsoft (le configurazioni di disponibilità elevata vengono discusse più avanti in questo documento).  
  
-   Il Database Oracle: Può trattarsi di qualsiasi computer in cui è in esecuzione una versione supportata del database Oracle. Sono inclusi i computer in cui viene eseguito un sistema operativo Windows, Linux o di altro tipo supportato dalla versione del database Oracle installato. Si noti che nel diagramma questa piattaforma è illustrata al plurale perché un solo servizio Oracle CDC può acquisire modifiche da più database Oracle di origine.  
  
-   Il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Può trattarsi di qualsiasi computer in cui la destinazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] database (una SKU supportata di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]) viene eseguito. Un servizio Oracle CDC supporta un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di destinazione in cui sono archiviate le tabelle delle modifica e la configurazione del servizio. La piattaforma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] può inoltre rappresentare un'istanza cluster di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] o un'istanza con mirroring di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] utilizzando la funzionalità **AlwaysOn** .  
  
-   Oracle CDC Designer: Può trattarsi di qualsiasi computer Windows supportato che è possibile accedere al database Oracle di origine e destinazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] database.  
  
 Nella tabella seguente vengono descritti i componenti eseguiti nelle quattro piattaforme descritte in precedenza.  
  
|Componente/Descrizione|Il componente è costituito da:|  
|----------------------------|----------------------------|  
|Servizio Oracle CDC: Si tratta di un servizio Windows in cui l'attività di change data capture viene eseguita.|Istanza di Oracle CDC: Sottoprocesso del servizio Oracle CDC che gestisce attività change data capture per un database Oracle di origine singolo (è presente un'istanza di Oracle CDC per database Oracle di origine).<br /><br /> Agente di lettura Log Oracle: Legge il log delle transazioni Oracle tramite il Client Oracle.<br /><br /> Client Oracle: Oracle Instant Client utilizzata per la comunicazione con Oracle. Si tratta di un prerequisito che è necessario ottenere da Oracle e installare prima dell'installazione del servizio Oracle CDC.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Change Writer: Scrive le modifiche sottoposte al commit apportate alla tabella Oracle acquisita per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]nelle tabelle delle modifiche. Questo componente gestisce inoltre lo stato di acquisizione all'interno del database [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di destinazione.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Client ODBC: Il Client nativo Microsoft per [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Si tratta di un componente prerequisito che è necessario ottenere da Microsoft e installare prima dell'installazione del servizio Oracle CDC.|  
|Oracle CDC Service Configuration: Questo è uno snap-in Microsoft Management Console che crea il servizio di Windows e impostata la relativa configurazione.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client: Il client SQL ADO.NET fornito con la versione 4 di .NET framework.|  
|Database Oracle: Un database Oracle di origine da cui le modifiche per selezionare le tabelle vengono acquisiti.|Log Miner: Un componente Oracle tramite cui vengono letti i log delle transazioni Oracle.<br /><br /> Log delle transazioni: Online e archiviati log Oracle di rollforward che vengono usati da Oracle per garantire che il database può eseguire il rollback delle transazioni e correggere gli errori (in questo caso, il database Oracle deve funzionare in modalità archivelog).|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Istanza di: Oggetto [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] istanza in cui sono ospitati i database CDC. può trattarsi di un'istanza cluster di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (cluster di failover) o di un database con mirroring (AlwaysOn).|Il Database MSXDBCDC: Un database in cui le informazioni sui servizi CDC che interagisce con questo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] istanza viene mantenuta. Sono inoltre presenti informazioni sulle istanze di Oracle CDC gestite da ogni servizio CDC. Questo database viene creato come parte del processo di creazione del servizio CDC.<br /><br /> Database CDC: database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui sono archiviate le modifiche apportate a uno dei database Oracle di origine. I database CDC sono abilitati per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC pertanto dispongono di tabelle e funzioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC. Ciò semplifica l'utilizzo delle modifiche che hanno origine in Oracle.|  
|Oracle CDC Designer: Snap-in Microsoft Management Console che facilita la creazione di istanze di Oracle CDC. Può essere utilizzato per selezionare le tabelle e le colonne da acquisire, fornire informazioni relative alla connessione Oracle e gestire il ciclo di vita delle istanze di CDC.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client: Il client SQL ADO.NET fornito con la versione 4 di .NET framework.<br /><br /> Client Oracle: Oracle Instant Client utilizzata per la comunicazione con Oracle. Si tratta di un componente prerequisito che è necessario ottenere da Oracle e installare prima dell'installazione del servizio Oracle CDC.|  
  
 Il servizio Oracle CDC e le istanze figlio di Oracle CDC sono in grado di comunicare solo con il o i database Oracle di origine e l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di destinazione come client. Non sono attivamente in ascolto su alcun protocollo di rete e di altro tipo. Tramite il servizio Oracle CDC vengono monitorati i database CDC per le modifiche della configurazione e l'operazione del servizio stesso viene aggiornata in base alla configurazione aggiornata.  
  
  
