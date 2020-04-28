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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 093cb7352a7f509b0afcc061e2691311bb183169
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298131"
---
# <a name="odbc-driver-for-oracle"></a>Driver ODBC per Oracle
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Il driver ODBC di Microsoft® per Oracle consente di connettere l'applicazione conforme a ODBC a un database Oracle. Il driver ODBC per Oracle è conforme alla specifica Open Database Connectivity (ODBC) descritta in *ODBC Programmer ' s Reference*. Consente l'accesso ai pacchetti PL/SQL, all'integrazione XA/DTC e all'accesso Oracle dall'interno di Internet Information Services (IIS).  
  
 Oracle RDBMS è un sistema di gestione di database relazionali multiutente eseguito con vari sistemi operativi workstation e minicomputer. I computer compatibili con IBM che eseguono Microsoft Windows possono comunicare con i server di database Oracle in una rete. Le reti supportate includono Microsoft LAN Manager, NetWare, Vines, DECnet e qualsiasi rete che supporta TCP/IP.  
  
 Il driver ODBC per Oracle consente a un'applicazione di accedere ai dati in un database Oracle tramite l'interfaccia ODBC. Il driver può accedere ai database Oracle locali oppure può comunicare con la rete tramite SQL * NET. Il diagramma seguente illustra l'architettura dell'applicazione e del driver.  
  
 ![Architettura del driver ODBC per&#47;app Oracle](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 Il driver ODBC per Oracle è conforme al livello di conformità API 1 e al livello di conformità SQL di base. Supporta anche alcune funzioni nel livello di conformità dell'API 2 e la maggior parte della grammatica nei livelli di conformità di base e SQL esteso. Il driver è conforme a ODBC 2,5 e supporta i sistemi a 32 bit. Oracle 7.3 x è supportato completamente; Oracle8 ha un supporto limitato. Il driver ODBC per Oracle non supporta alcuno dei nuovi tipi di dati Oracle8, ovvero tipi di dati Unicode, BLOB, CLOB e così via, né supporta il nuovo modello a oggetti relazionale di Oracle. Per ulteriori informazioni sui tipi di dati supportati, vedere [tipi di dati supportati](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) in questa guida.  
  
 Per accedere ai dati Oracle, sono necessari i componenti seguenti:  
  
-   Driver ODBC per Oracle  
  
-   Un database Oracle RDBMS  
  
-   Software client Oracle  
  
 Inoltre, per le connessioni remote:  
  
-   Rete che connette i computer che eseguono il driver e il database. La rete deve supportare le connessioni SQL * NET.  
  
## <a name="component-documentation"></a>Documentazione del componente  
 In questa guida vengono fornite informazioni dettagliate sulla configurazione e sulla configurazione del driver ODBC Microsoft per Oracle e sull'aggiunta della funzionalità a livello di codice. Contiene inoltre materiale di riferimento tecnico.  
  
 Per informazioni relative al comportamento specifico del prodotto Oracle, consultare la documentazione che accompagna il prodotto Oracle.  
  
 Per informazioni sull'impostazione o sulla configurazione del driver ODBC Microsoft per Oracle tramite Amministrazione origine dati ODBC, vedere la documentazione relativa all' [amministratore dell'origine dati](../../odbc/admin/odbc-data-source-administrator.md) ODBC.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Guida dell'utente del driver ODBC per Oracle](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [Guida di riferimento per i programmatori del driver ODBC per Oracle](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
