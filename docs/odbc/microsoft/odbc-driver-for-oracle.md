---
title: Driver ODBC per Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fc15968501fed6b94a7ccddb984cbdf76bcbcb0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915799"
---
# <a name="odbc-driver-for-oracle"></a>Driver ODBC per Oracle
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. In alternativa, usare il driver ODBC fornito da Oracle.  
  
 Microsoft® ODBC Driver per Oracle consente di connettere l'applicazione compatibile con ODBC a un database Oracle. Il Driver ODBC per Oracle è conforme alla specifica Open Database Connectivity (ODBC) descritto nel *riferimento per programmatori ODBC*. Consente di accedere al package PL/SQL, l'integrazione di XA/DTC e l'accesso di Oracle all'interno di Internet Information Services (IIS).  
  
 Oracle RDBMS è un sistema di gestione di database relazionale multiutente che viene eseguito con diversi sistemi operativi minicomputer e workstation. I computer compatibili con IBM che eseguono Microsoft Windows possono comunicare con i server di database Oracle in una rete. Le reti supportate includono Microsoft LAN Manager, NetWare, VINES, DECnet e qualsiasi rete che supporta TCP/IP.  
  
 Il Driver ODBC per Oracle consente a un'applicazione accedere ai dati in un database Oracle tramite l'interfaccia ODBC. Il driver può accedere a database Oracle locali o che possa comunicare con la rete tramite SQL * Net. Il diagramma seguente illustra in dettaglio questa architettura di applicazioni e driver.  
  
 ![Driver ODBC per Oracle app&#47;architettura del driver](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 Il Driver ODBC per Oracle è conforme con API conformità al livello 1 e SQL di base di livello la conformità. Supporta inoltre alcune funzioni nell'API conformità al livello 2 e la maggior parte della grammatica nei livelli di conformità di Core e SQL estesa. Il driver è compatibile con ODBC 2.5 e supporta sistemi a 32 bit. Oracle 7.3 x è supportata completamente; Include supporto limitato per Oracle8. Il Driver ODBC per Oracle non supporta uno qualsiasi dei nuovi tipi di dati Oracle8 - Unicode i tipi di dati, i BLOB, CLOB e così via, e non supporta nuovo modello del Oracle a oggetti relazionali. Per altre informazioni sui tipi di dati supportati, vedere [Supported Data Types](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) in questa Guida.  
  
 Per accedere ai dati di Oracle, sono necessari i componenti seguenti:  
  
-   Il Driver ODBC per Oracle  
  
-   Un database Oracle RDBMS  
  
-   Software Client Oracle  
  
 Inoltre, per le connessioni remote:  
  
-   Una rete che connette i computer che eseguono il driver e il database. La rete deve supportare SQL * Net connessioni.  
  
## <a name="component-documentation"></a>Documentazione relativa al componente  
 Questa guida contiene informazioni dettagliate sull'impostazione e configurazione del Driver ODBC di Microsoft per Oracle e aggiunta di funzionalità a livello di codice. Contiene inoltre materiale di riferimento tecnico.  
  
 Per informazioni sui comportamenti del prodotto Oracle specifici, consultare la documentazione che accompagna il prodotto Oracle.  
  
 Per informazioni sull'installazione o configurazione del Driver ODBC di Microsoft per Oracle con l'amministratore dell'origine dati ODBC, vedere la [Amministrazione origine dati ODBC](../../odbc/admin/odbc-data-source-administrator.md) documentazione.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Guida dell'utente del driver ODBC per Oracle](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Guida di riferimento per i programmatori del driver ODBC per Oracle](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
