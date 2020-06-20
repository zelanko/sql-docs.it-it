---
title: Database delle risorse | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- system objects [SQL Server]
- read-only databases
- mssqlsystemresource.mdf file
- Resource database [SQL Server]
ms.assetid: d592b2b4-bc36-4eb9-9385-8fe4dff0dced
author: stevestein
ms.author: sstein
ms.openlocfilehash: cca2f9e1ff6069a608beb1df1880b37e15f4e869
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965791"
---
# <a name="resource-database"></a>Database Resource
  Il database Resource è un database di sola lettura che contiene tutti gli oggetti di sistema inclusi in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gli oggetti di sistema, ad esempio sys.objects, sono archiviati fisicamente nel database Resource in modo persistente, ma nello schema sys di ogni database ne è presente un'implementazione logica. Il database Resource non contiene dati o metadati degli utenti.  
  
 Il database delle risorse consente di semplificare e rendere più rapida la procedura di aggiornamento a una nuova versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]la procedura di aggiornamento prevede l'eliminazione e la creazione di oggetti di sistema. Dal momento che il file del database Resource contiene tutti gli oggetti di sistema, l'aggiornamento viene ora eseguito semplicemente copiando il singolo file del database Resource sul server locale.  
  
## <a name="physical-properties-of-resource"></a>Proprietà fisiche del database Resource  
 I nomi di file fisici del database Resource sono mssqlsystemresource.mdf e mssqlsystemresource.ldf. Questi file si trovano in \<*drive*> : \Programmi\Microsoft SQL Server\MSSQL \<version> . \<*instance_name*> \MSSQL\Binn\ e non devono essere spostati. A ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è associato un solo file mssqlsystemresource.mdf e istanze diverse non condividono il file.  
  
> [!WARNING]  
>  Gli aggiornamenti e i Service Pack forniscono talvolta un nuovo database delle risorse che viene installato nella cartella BINN. Non è consigliabile né possibile modificare il percorso del database delle risorse.  
  
## <a name="backing-up-and-restoring-the-resource-database"></a>Backup e ripristino del database Resource  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è in grado di eseguire il backup del database delle risorse. È possibile eseguire un backup basato su file o basato su disco gestendo il file mssqlsystemresource.mdf come un file binario (con estensione exe), anziché come un file di database, ma non è possibile utilizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ripristinare i backup. Il ripristino di una copia di backup di mssqlsystemresource.mdf può essere eseguito solo manualmente, prestando attenzione a non sovrascrivere il database Resource corrente con una versione non aggiornata e potenzialmente non sicura.  
  
> [!IMPORTANT]  
>  Dopo aver ripristinato un backup di mssqlsystemresource.mdf, è necessario riapplicare eventuali aggiornamenti successivi.  
  
## <a name="accessing-the-resource-database"></a>Accesso al database Resource  
 È consigliabile che il database Resource venga modificato esclusivamente da o dietro indicazione di uno specialista del Servizio Supporto Tecnico Clienti Microsoft (CSS, Client Support Services). L'ID del database Resource è sempre 32767. Altri importanti valori associati al database Resource sono il numero di versione e la data e ora del suo ultimo aggiornamento.  
  
 **Per determinare il numero di versione del database delle** risorse **, usare**:  
  
```  
SELECT SERVERPROPERTY('ResourceVersion');  
GO  
```  
  
 **Per determinare data e ora dell'ultimo aggiornamento del database delle** risorse **, usare**:  
  
```  
SELECT SERVERPROPERTY('ResourceLastUpdateDateTime');  
GO  
```  
  
 **Per accedere a definizioni SQL di oggetti di sistema, utilizzare la funzione OBJECT_DEFINITION:**  
  
```  
SELECT OBJECT_DEFINITION(OBJECT_ID('sys.objects'));  
GO  
```  
  
## <a name="related-content"></a>Contenuto correlato  
 [Database di sistema.](system-databases.md)  
  
 [Connessione di diagnostica per gli amministratori di database](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](/sql/t-sql/functions/object-definition-transact-sql)  
  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)  
  
 [Avvio di SQL Server in modalità utente singolo](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md)  
  
  
