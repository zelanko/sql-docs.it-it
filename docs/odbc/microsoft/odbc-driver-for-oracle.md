---
title: 'Driver ODBC per Oracle : Documenti Microsoft'
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
ms.openlocfilehash: 2b5f1aabd23a587e681c33aed4b4119523444219
ms.sourcegitcommit: fc5b757bb27048a71bb39755648d5cefe25a8bc6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "80402609"
---
# <a name="odbc-driver-for-oracle"></a>Driver ODBC per Oracle
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il [driver ODBC fornito da Oracle](https://www.oracle.com/database/technologies/releasenote-odbc-ic.html).  
  
 Microsoft® ODBC Driver per Oracle consente di connettere l'applicazione conforme a ODBC a un database Oracle. Il driver ODBC per Oracle è conforme alla specifica ODBC (Open Database Connectivity) descritta in *ODBC Programmer's Reference*. Consente l'accesso ai pacchetti PL/SQL, all'integrazione XA/DTC e all'accesso Oracle da Internet Information Services (IIS).  
  
 Oracle RDBMS è un sistema di gestione di database relazionali multiutente che viene eseguito con vari sistemi operativi per workstation e minicomputer. I computer compatibili con IBM che eseguono Microsoft Windows possono comunicare con i server di database Oracle attraverso una rete. Le reti supportate includono Microsoft LAN Manager, NetWare, VINES, DECnet e qualsiasi rete che supporti TCP/IP.  
  
 Il driver ODBC per Oracle consente a un'applicazione di accedere ai dati in un database Oracle tramite l'interfaccia ODBC. Il driver può accedere ai database Oracle locali o può comunicare con la rete tramite SQL.Net. Il diagramma seguente descrive in dettaglio questa architettura dell'applicazione e del driver.  
  
 ![Driver ODBC per l'architettura dei driver di&#47;dell'applicazione OracleODBC Driver for Oracle app&#47;driver architecture](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 Il driver ODBC per Oracle è conforme a API Conformance Level 1 e SQL Conformance Level Core. Supporta inoltre alcune funzioni in API Conformance Level 2 e la maggior parte della grammatica nei livelli di conformità Core ed Extended SQL. Il driver è conforme a ODBC 2.5 e supporta sistemi a 32 bit. Oracle 7.3x è supportato completamente; Oracle8 ha un supporto limitato. Il driver ODBC per Oracle non supporta nessuno dei nuovi tipi di dati Oracle8 ( tipi di dati Unicode, BLOB, CLOB e così via) né supporta il nuovo modello a oggetti relazionale di Oracle. Per altre informazioni sui tipi di dati supportati, vedere [Tipi di dati supportati](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) in questa guida.  
  
 Per accedere ai dati Oracle, sono necessari i seguenti componenti:  
  
-   Il driver ODBC per Oracle  
  
-   Un database Oracle RDBMS  
  
-   Oracle Client Software  
  
 Inoltre, per le connessioni remote:  
  
-   Rete che connette i computer che eseguono il driver e il database. La rete deve supportare le connessioni SQL-Net.  
  
## <a name="component-documentation"></a>Documentazione dei componenti  
 Questa guida contiene informazioni dettagliate sull'impostazione e la configurazione del driver Microsoft ODBC per Oracle e sull'aggiunta di funzionalità a livello di codice. Contiene anche materiale di riferimento tecnico.  
  
 Per informazioni sul comportamento specifico del prodotto Oracle, consultare la documentazione fornita con il prodotto Oracle.  
  
 Per informazioni sull'impostazione o la configurazione del driver Microsoft ODBC per Oracle mediante l'Amministratore origine dati ODBC, vedere la documentazione [Amministratore origine dati ODBC.](../../odbc/admin/odbc-data-source-administrator.md)  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Guida dell'utente del driver ODBC per Oracle](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Guida di riferimento per i programmatori del driver ODBC per Oracle](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
