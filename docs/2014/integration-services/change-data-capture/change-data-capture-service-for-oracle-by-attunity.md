---
title: Servizio Change Data Capture per Oracle di Attunity | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 22ec8a5c-9550-4d38-8a4a-485ec3e53ea8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: a01524acf4fc72cb50732650f1f2e6f58b4ff74d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62771527"
---
# <a name="change-data-capture-service-for-oracle-by-attunity"></a>Servizio Change Data Capture per Oracle di Attunity
  Il servizio CDC per Oracle è un servizio Windows tramite cui vengono analizzati i log delle transazioni Oracle e acquisite le modifiche apportate alle tabelle Oracle di interesse nelle tabelle delle modifiche di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Le tabelle delle modifiche SQL in cui vengono archiviate le modifiche acquisite da Oracle sono dello stesso tipo delle tabelle delle modifiche usate nella funzionalità Change Data Capture nativa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . In questo modo l'utilizzo delle modifiche è facile quanto l'utilizzo delle modifiche apportate ai database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="installation"></a>Installazione  
 È possibile installare il servizio CDC per Oracle in qualsiasi computer Windows supportato con accesso al o ai database Oracle di origine che vengono acquisiti e all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione in cui si trova il database CDC di destinazione. Per il servizio CDC non è necessaria un'installazione locale del database Oracle o del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ma solo dei relativi client supportati. Per altre informazioni sul percorso di installazione dei componenti di database richiesti, vedere **Prerequisiti del database** in questo argomento.  
  
 Con l'installazione del servizio CDC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per Oracle l'interfaccia utente della configurazione del servizio e il programma del servizio vengono posizionati nel percorso selezionato. Il servizio CDC per Oracle viene configurato separatamente tramite Oracle CDC Service Configuration Console. Per altre informazioni sulla configurazione del servizio Oracle CDC, vedere [Guida del servizio Change Data Capture per Oracle di Attunity](change-data-capture-service-for-oracle-by-attunity-f1-help.md).  
  
 Per installare il servizio CDC per Oracle, eseguire manualmente **AttunityOracleCdcService. msi** dal supporto di installazione di SQL Server. I pacchetti di installazione per x86 e x64 si trovano in **.\Tools\AttunityCDCOracle\\ ** sul supporto di installazione di SQL Server.  
  
 È possibile installare il servizio CDC per Oracle in qualsiasi computer Windows supportato in cui sia installato il client nativo di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ; non è necessario che sia installato nello stesso computer in cui si trova l'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione.  
  
## <a name="supported-windows-environments"></a>Ambienti Windows supportati  
 È possibile eseguire il servizio Change Data Capture per Oracle di Attunity negli ambienti Windows seguenti:  
  
-   Windows 8  
  
-   Windows 7 a 32 bit (x86) e a 64 bit (x64)  
  
-   Windows Server 2012  
  
-   Windows Server 2008 R2 con Service Pack 1  
  
-   Windows Server 2008 a 32 bit (x86) e a 64 bit (x64) con Service Pack 2  
  
## <a name="database-prerequisites"></a>Prerequisiti del database  
 Per usare il servizio CDC per Oracle, è necessario installare il software Oracle [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client. Si tratta di un prerequisito che è necessario ottenere da Oracle e installare prima dell'installazione del servizio Oracle CDC. Inoltre, è necessario installare il client ODBC di SQL Server usando il programma di installazione di SQL Server.  
  
 Il servizio CDC per Oracle supporta le versioni seguenti:  
  
### <a name="source-oracle-database"></a>Database Oracle di origine  
  
-   Oracle Database 11x, qualsiasi versione  
  
-   Oracle Database 10x, qualsiasi versione  
  
### <a name="target-sql-server-database"></a>Database di SQL Server di destinazione  
 Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="running-the-installation-program"></a>Esecuzione del programma di installazione  
 Per installare il servizio CDC per Oracle, aprire l'Installazione guidata per la piattaforma Windows in uso (32/64 bit) e attenersi alle indicazioni visualizzate sullo schermo.  
  
## <a name="uninstalling-change-data-capture-service-for-oracle-by-attunity"></a>Disinstallazione del servizio Change Data Capture per Oracle di Attunity  
 Per disinstallare il servizio CDC per Oracle, scegliere Pannello di controllo, Programmi e funzionalità.  
  
 Con la disinstallazione del servizio CDC, non vengono eliminati i database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] creati. Per la rimozione completa dello strumento, è necessario rimuovere il database MSXDBCDC e i database CDC specifici creati nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione usata.  
  
 Se si disinstalla il software del servizio CDC da un computer e lo si installa in un altro computer, è sufficiente fornire le definizioni seguenti:  
  
-   Account servizio  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] - Stringa di connessione e credenziali  
  
-   Master password  
  
 Tutte le altre definizioni vengono archiviate in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e sono disponibile dall'installazione precedente in un altro computer.  
  
## <a name="in-this-documentation"></a>Contenuto della documentazione  
  
-   [Architettura di sistema del servizio Change Data Capture per Oracle di Attunity](change-data-capture-service-for-oracle-by-attunity-system-architecture.md)  
  
-   [Servizio Oracle CDC](the-oracle-cdc-service.md)  
  
-   [Guida del servizio Change Data Capture per Oracle di Attunity](change-data-capture-service-for-oracle-by-attunity-f1-help.md)  
  
-   [Guida procedurale del servizio Change Data Capture per Oracle di Attunity](change-data-capture-service-for-oracle-by-attunity-how-to-guide.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Uso del servizio Oracle CDC](working-with-the-oracle-cdc-service.md)  
  
  
