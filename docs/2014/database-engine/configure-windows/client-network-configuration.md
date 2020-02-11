---
title: Configurazione di rete dei client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- client configuration [SQL Server], connections
- Database Engine [SQL Server], network configurations
- connections [SQL Server], client configuration
- client connections [SQL Server], about client network connections
- client computers [SQL Server]
- client connections [SQL Server]
- network connections [SQL Server], client configuration
ms.assetid: c382eacd-0a0c-40a4-958f-9b774eb2d734
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 862c13e61513b46b44ce55df9e66170bbb1ac219
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62787104"
---
# <a name="client-network-configuration"></a>Configurazione di rete dei client
  Il software client consente ai computer client di connettersi a un' [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] istanza di in una rete. Un client è un'applicazione front-end che utilizza i servizi forniti da un server quale [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Il computer nel quale è installata l'applicazione viene definito *computer client*.  
  
 Al livello più semplice, un client di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può risiedere nello stesso computer di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In genere tuttavia, un client si connette a uno o più server remoti in rete. L'architettura client/server di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di gestire più client e server in una rete. Le configurazioni client predefinite risultano adeguate nella maggior parte dei casi.  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] I client sono applicazioni di vario tipo, tra cui:  
  
-   Consumer OLE DB  
  
     Queste applicazioni usano il provider OLE DB di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client per connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il provider OLE DB funge da intermediario tra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e le applicazioni client che utilizzano dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sotto forma di set di righe OLE DB. L'utilità del prompt dei comandi **sqlcmd** e [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]sono esempi di applicazioni OLE DB.  
  
-   applicazioni ODBC  
  
     Queste applicazioni includono utilità client installate con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio l'utilità del prompt dei comandi **osql** , nonché altre applicazioni che usano il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client per connettersi a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Client DB-Library  
  
     Queste applicazioni includono l'utilità del prompt dei comandi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **isql** e client scritti in DB-Library. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]il supporto per le applicazioni client che usano DB-Library [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è limitato alle funzionalità di 7,0.  
  
> [!NOTE]  
>  Nonostante supporti connessioni da applicazioni esistenti tramite le API DB-Library ed Embedded SQL, il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] non include i file o la documentazione necessari per svolgere attività di programmazione per le applicazioni che utilizzano tali API. In una versione futura del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] verrà eliminato il supporto per le connessioni da applicazioni DB-Library o Embedded SQL. Non utilizzare pertanto DB-Library o Embedded SQL per sviluppare nuove applicazioni. Quando si modificano applicazioni esistenti, rimuovere tutte le dipendenze da DB-Library o Embedded SQL. Invece di queste API, usare lo spazio dei nomi SQLClient o un'API, ad esempio OLE DB o ODBC. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è inclusa la DLL DB-Library necessaria per eseguire queste applicazioni. Per eseguire applicazioni DB-Library o Embedded SQL è necessario disporre della DLL DB-Library di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versione 6.5, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 o [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)].  
  
 Indipendentemente dal tipo di applicazione, la gestione di un client consiste principalmente nel configurarne la connessione con i componenti server di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A seconda dei requisiti del sito, le attività di gestione dei client possono variare dalla semplice immissione del nome del server alla compilazione di una libreria di voci di configurazione personalizzate, destinate a un ambiente multiserver eterogeneo.  
  
 La DLL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client contiene le librerie di rete e viene installata dal programma di installazione. Durante una nuova installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], i protocolli di rete non vengono abilitati. Le installazioni di aggiornamento mantengono i protocolli abilitati in precedenza. I protocolli di rete sottostanti vengono installati durante l'installazione di Windows (o tramite Reti nel Pannello di controllo). Gli strumenti elencati di seguito consentono la gestione dei client di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Configuration Manager  
  
     I componenti di rete client e server vengono gestiti mediante Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , che combina l'utilità Configurazione di rete di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , l'utilità Configurazione di rete client di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Gestione servizi delle versioni precedenti. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gestione configurazione è uno snap-in di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console (MMC). Viene inoltre visualizzato come un nodo nello snap-in Gestione computer di Windows. È possibile abilitare, disabilitare, configurare e impostare la priorità delle singole librerie di rete utilizzando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gestione configurazione.  
  
-   Installazione  
  
     Eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per installare i componenti di rete in un computer client. Quando il programma di installazione viene avviato dal prompt dei comandi, è possibile abilitare o disabilitare singole librerie di rete.  
  
-   Amministratore origine dati ODBC  
  
     Amministrazione origine dati ODBC consente di creare e modificare origini dati ODBC in computer su cui è in esecuzione il sistema operativo Microsoft Windows.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 [Configurazione di protocolli client](configure-client-protocols.md)  
  
 [Creare o eliminare un alias server per l'uso da un client &#40;Gestione configurazione SQL Server&#41;](create-or-delete-a-server-alias-for-use-by-a-client.md)  
  
 [Accesso a SQL Server](logging-in-to-sql-server.md)  
  
 [Apertura di Amministratore origine dati ODBC](open-the-odbc-data-source-administrator.md)  
  
 [Verificare la versione dei driver ODBC di SQL Server &#40;Windows&#41;](check-the-odbc-sql-server-driver-version-windows.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 [Configurazione di rete del server](server-network-configuration.md)  
  
 [Gestire il servizio Motore di database](manage-the-database-engine-services.md)  
  
  
