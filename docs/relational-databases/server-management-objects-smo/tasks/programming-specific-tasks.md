---
title: Programmazione di attività specifiche | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SQL Server Management Objects, tasks
- SMO [SQL Server], programming
- SMO [SQL Server], tasks
ms.assetid: a15949ef-88d9-4205-892e-0b66588b4fcc
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f23b7844bcff234594db87875e89a89f0f073be9
ms.sourcegitcommit: f3f83ef95399d1570851cd1360dc2f072736bef6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/13/2019
ms.locfileid: "70148402"
---
# <a name="programming-specific-tasks"></a>Programmazione di attività specifiche
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Tra le attività specifiche della programmazione tramite oggetti SMO sono incluse operazioni complesse richieste esclusivamente dai programmi che hanno una funzione specifica, ad esempio il backup, il monitoraggio delle statistiche, la replica, la gestione di istanze di oggetti e l'impostazione di opzioni di configurazione.  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Uso di server collegati in SMO](../../../relational-databases/server-management-objects-smo/tasks/using-linked-servers-in-smo.md)|Viene descritto l'utilizzo in SMO dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> per collegare server OLE-DB.|  
|[Configurazione di SQL Server in SMO](../../../relational-databases/server-management-objects-smo/tasks/configuring-sql-server-in-smo.md)|Viene descritto come visualizzare e modificare le impostazioni di configurazione per l'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in SMO.|  
|[Uso del partizionamento di tabelle e indici](../../../relational-databases/server-management-objects-smo/tasks/using-table-and-index-partitioning.md)|Viene descritto come utilizzare il partizionamento di indici e tabelle in SMO.|  
|[Uso di filegroup e file per archiviare dati](../../../relational-databases/server-management-objects-smo/tasks/using-filegroups-and-files-to-store-data.md)|Viene descritto come utilizzare filegroup in SMO.|  
|[Gestione di servizi e di impostazioni di rete con il provider WMI](../../../relational-databases/server-management-objects-smo/tasks/managing-services-and-network-settings-by-using-wmi-provider.md)|Vengono descritti diversi modi per tenere traccia dell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando l'oggetto <xref:Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer> che rappresenta il provider WMI per la gestione della configurazione.|  
|[Uso degli oggetti di database](../../../relational-databases/server-management-objects-smo/tasks/creating-altering-and-removing-database-objects.md)|Viene descritto come creare classi di istanze che rappresentano oggetti nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Gestione di utenti, ruoli e account di accesso](../../../relational-databases/server-management-objects-smo/tasks/managing-users-roles-and-logins.md)|Viene descritto come utilizzare i ruoli di sicurezza in SMO.|  
|[Concessione, revoca e negazione delle autorizzazioni](../../../relational-databases/server-management-objects-smo/tasks/granting-revoking-and-denying-permissions.md)|Viene descritto come utilizzare SMO per concedere, revocare e negare autorizzazioni a utenti o membri di un ruolo.|  
|[Uso della crittografia](../../../relational-databases/server-management-objects-smo/tasks/using-encryption.md)|Viene descritto come proteggere i dati utilizzando la crittografia in SMO.|  
|[Pianificazione delle attività amministrative automatiche in SQL Server Agent](../../../relational-databases/server-management-objects-smo/tasks/scheduling-automatic-administrative-tasks-in-sql-server-agent.md)|Viene descritto come utilizzare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent per monitorare, segnalare in report e pianificare processi in SMO.|  
|[Backup e ripristino dei log dei database e delle transazioni](../../../relational-databases/server-management-objects-smo/tasks/backing-up-and-restoring-databases-and-transaction-logs.md)|Viene descritto come eseguire il backup e il ripristino di database e log delle transazioni in SMO.|  
|[Scripting](../../../relational-databases/server-management-objects-smo/tasks/scripting.md)|Viene descritto come generare script di oggetti e individuare dipendenze tra oggetti in SMO.|  
|[Trasferimento di dati](../../../relational-databases/server-management-objects-smo/tasks/transferring-data.md)|Viene descritto come trasferire dati in SMO.|  
|[Uso di Posta elettronica database](../../../relational-databases/server-management-objects-smo/tasks/using-database-mail.md)|Viene descritto l'utilizzo dei servizi di posta elettronica da parte di SMO.|  
|[Gestione di Service Broker](../../../relational-databases/server-management-objects-smo/tasks/managing-service-broker.md)|Viene descritto come configurare Service Broker tramite SMO.|  
|[Uso di XML Schema](../../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md)|Viene descritto come utilizzare il tipo di dati XML in SMO.|  
|[Uso dei sinonimi](../../../relational-databases/server-management-objects-smo/tasks/using-synonyms.md)|Viene descritto come creare sinonimi in SMO.|  
|[Uso di messaggi](../../../relational-databases/server-management-objects-smo/tasks/using-messages.md)|Viene descritto come utilizzare i messaggi di sistema e come specificare messaggi definiti dall'utente.|  
|[Implementazione della ricerca full-text](../../../relational-databases/server-management-objects-smo/tasks/implementing-full-text-search.md)|Viene descritto come implementare cataloghi e indici di ricerca full-text in SMO.|  
|[Implementazione di endpoint](../../../relational-databases/server-management-objects-smo/tasks/implementing-endpoints.md)|Viene descritto come creare endpoint per gestire payload per il mirroring di database, le richieste SOAP e Service Broker.|  
|[Creazione e aggiornamento delle statistiche](../../../relational-databases/server-management-objects-smo/tasks/creating-and-updating-statistics.md)|Viene descritto come configurare e monitorare statistiche su un database in SMO.|  
|[Traccia e riproduzione di eventi](../../../relational-databases/server-management-objects-smo/tasks/tracing-and-replaying-events.md)|Viene descritto come utilizzare gli oggetti **Trace** e replay in SMO per tracciare e riprodurre gli eventi.|  
  
  
