---
title: Architettura di sistema di Change Data Capture Service per Oracle di Attunity | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1db6c737-3c60-4066-a0a3-3611e1c83e4e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8c6c809aaa32bd8f953061c48bde6bf43d012aa4
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294846"
---
# <a name="change-data-capture-service-for-oracle-by-attunity-system-architecture"></a>Architettura di sistema del servizio Change Data Capture per Oracle di Attunity

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Con il servizio CDC per Oracle è possibile acquisire le modifiche apportate alle tabelle selezionate in uno o più database Oracle di origine nei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC presenti in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nel diagramma seguente vengono illustrati i componenti che costituiscono il servizio CDC per Oracle.  
  
 ![Architettura dei servizi](../../integration-services/change-data-capture/media/service-architecture.gif "Architettura dei servizi")  
  
 In questa figura sono illustrate quattro piattaforme utilizzate. Sebbene in molti casi queste piattaforme possano sovrapporsi, il diagramma rappresenta un caso di utilizzo standard. Ad esempio, è logico che il database Oracle e il database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengano eseguiti ciascuno in un computer separato e non vengano condivisi con la piattaforma del servizio Oracle CDC o la piattaforma da cui viene progettato il servizio CDC. Nella figura sono illustrate le piattaforme seguenti:  
  
-   Servizio Oracle CDC: può essere qualsiasi computer Windows supportato in cui viene installato ed eseguito il servizio Oracle CDC. Questa piattaforma può inoltre rappresentare un nodo del cluster in un cluster di failover Microsoft (le configurazioni di disponibilità elevata vengono discusse più avanti in questo documento).  
  
-   Oracle Database: può trattarsi di qualsiasi computer in cui viene eseguita una versione supportata del database Oracle. Sono inclusi i computer in cui viene eseguito un sistema operativo Windows, Linux o di altro tipo supportato dalla versione del database Oracle installato. Si noti che nel diagramma questa piattaforma è illustrata al plurale perché un solo servizio Oracle CDC può acquisire modifiche da più database Oracle di origine.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: può trattarsi di qualsiasi computer in cui viene eseguito il database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione (uno SKU supportato di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]). Un servizio Oracle CDC supporta un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione in cui sono archiviate le tabelle delle modifica e la configurazione del servizio. La piattaforma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può inoltre rappresentare un'istanza cluster di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] o un'istanza con mirroring di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] che usa la funzionalità **AlwaysOn** .  
  
-   Oracle CDC Designer: può trattarsi di qualsiasi computer Windows supportato in grado di accedere al database Oracle di origine e al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione.  
  
 Nella tabella seguente vengono descritti i componenti eseguiti nelle quattro piattaforme descritte in precedenza.  
  
|Componente/Descrizione|Il componente è costituito da:|  
|----------------------------|----------------------------|  
|Servizio Oracle CDC: si tratta di un servizio Windows in cui ha luogo l'attività Change Data Capture.|Istanza di Oracle CDC: sottoprocesso del servizio Oracle CDC che gestisce l'attività Change Data Capture per un solo database Oracle di origine (è presente un'istanza di Oracle CDC per ciascun database Oracle di origine).|  
||Agente di lettura log Oracle: legge i log delle transazioni Oracle tramite il client Oracle.|  
||Client Oracle: Oracle Instant Client usato per la comunicazione con Oracle. Si tratta di un prerequisito che è necessario ottenere da Oracle e installare prima dell'installazione del servizio Oracle CDC.|  
||[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Change Writer: scrive le modifiche di cui è stato eseguito il commit apportate alla tabella Oracle acquisita nelle tabelle delle modifiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo componente gestisce inoltre lo stato di acquisizione all'interno del database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione.|  
||[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Client ODBC: Microsoft Native Client per [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Si tratta di un componente prerequisito che è necessario ottenere da Microsoft e installare prima dell'installazione del servizio Oracle CDC.|  
|Configurazione del servizio Oracle CDC: si tratta di uno snap-in di Microsoft Management Console con cui viene creato il servizio Windows e impostata la relativa configurazione.|Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: client SQL ADO.NET fornito con la versione 4 di .NET Framework.|  
|Oracle Database: database Oracle di origine da cui vengono acquisite le modifiche apportate alle tabelle selezionate.|Log Miner: componente Oracle tramite il quale vengono letti i log delle transazioni Oracle.|  
||Log delle transazioni: log di ripristino Oracle online e archiviati usati da Oracle per garantire che il database sia in grado di eseguire il rollback delle transazioni e il recupero dagli errori (in questo caso, il database Oracle deve funzionare in modalità archive-log).|  
|Istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dove sono ospitati i database CDC. Può trattarsi di un'istanza cluster di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (cluster di failover) o di un database con mirroring (AlwaysOn).|Database MSXDBCDC: database in cui sono contenute le informazioni sui servizi CDC che usano quest'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sono inoltre presenti informazioni sulle istanze di Oracle CDC gestite da ogni servizio CDC. Questo database viene creato come parte del processo di creazione del servizio CDC.|  
||Database CDC: database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui sono archiviate le modifiche apportate a uno dei database Oracle di origine. I database CDC sono abilitati per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC pertanto dispongono di tabelle e funzioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC. Ciò semplifica l'utilizzo delle modifiche che hanno origine in Oracle.|  
|Oracle CDC Designer: snap-in di Microsoft Management Console che consente di creare istanze di Oracle CDC. Può essere utilizzato per selezionare le tabelle e le colonne da acquisire, fornire informazioni relative alla connessione Oracle e gestire il ciclo di vita delle istanze di CDC.|Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: client SQL ADO.NET fornito con la versione 4 di .NET Framework.|  
||Client Oracle: Oracle Instant Client usato per la comunicazione con Oracle. Si tratta di un componente prerequisito che è necessario ottenere da Oracle e installare prima dell'installazione del servizio Oracle CDC.|  
  
 Il servizio Oracle CDC e le istanze figlio di Oracle CDC sono in grado di comunicare solo con il o i database Oracle di origine e l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione come client. Non sono attivamente in ascolto su alcun protocollo di rete e di altro tipo. Tramite il servizio Oracle CDC vengono monitorati i database CDC per le modifiche della configurazione e l'operazione del servizio stesso viene aggiornata in base alla configurazione aggiornata.  
  
  
