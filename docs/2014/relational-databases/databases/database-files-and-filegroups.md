---
title: Filegroup e file di database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 91e22e536a91878609feedf2977ffa7d78a54d61
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970201"
---
# <a name="database-files-and-filegroups"></a>Filegroup e file di database
  Ogni database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene almeno due file del sistema operativo: un file di dati e un file di log. I file di dati contengono dati e oggetti come tabelle, indici, stored procedure e viste. I file di log contengono le informazioni necessarie per il recupero di tutte le transazioni del database. I file di dati possono essere raggruppati in filegroup ai fini dell'allocazione e dell'amministrazione.  
  
## <a name="database-files"></a>File di database  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i database contengono tre tipi di file, come illustrato nella tabella seguente.  
  
|File|Descrizione|  
|----------|-----------------|  
|Primaria|Il file di dati primario contiene le informazioni di avvio del database e punta agli altri file del database. I dati e gli oggetti degli utenti possono essere archiviati in questo file o nei file di dati secondari. In ogni database è disponibile un unico file di dati primario. L'estensione consigliata per i file di dati primari è mdf.|  
|Secondari|I file di dati secondari sono facoltativi e definiti dall'utente e vengono utilizzati per archiviare i dati dell'utente. Possono essere utilizzati per suddividere i dati su più dischi, memorizzandoli in unità disco distinte. Se un database supera le dimensioni massime consentite per un singolo file di Windows, è inoltre possibile utilizzare i file di dati secondari per consentire l'aumento di dimensioni del database.<br /><br /> L'estensione consigliata per i file di dati secondari è ndf.|  
|Log delle transazioni|I file di log delle transazioni contengono le informazioni necessarie per il recupero del database. È necessario che sia disponibile almeno un file di log per ogni database. L'estensione consigliata per i file di log è ldf.|  
  
 Ad esempio, è possibile creare un database semplice, denominato **Sales** , con un file primario che include tutti i dati e gli oggetti e un file di log che include le informazioni del log delle transazioni. In alternativa, è possibile creare un database più complesso, denominato **Orders** , con un file primario e cinque file secondari. I dati e gli oggetti all'interno del database vengono suddivisi nei sei file e i quattro file di log includono le informazioni del log delle transazioni.  
  
 Per impostazione predefinita, i dati e i log delle transazioni vengono archiviati nella stessa unità e nello stesso percorso. Ciò consente la gestione nei sistemi a disco singolo, ma può non essere la soluzione ottimale per gli ambienti di produzione. È consigliabile archiviare i dati e i file di log in dischi separati.  
  
## <a name="filegroups"></a>Filegroup  
 Ogni database contiene un filegroup primario, che include il file di dati primario e gli eventuali file secondari non inclusi in altri filegroup. È possibile creare filegroup definiti dall'utente per raggruppare i file di dati a fini amministrativi e di allocazione e posizione dei dati.  
  
 Ad esempio, è possibile creare tre file, Data1.ndf, Data2.ndf e Data3.ndf su tre unità disco distinte e assegnarli al filegroup **fgroup1**. È quindi possibile creare una tabella specifica nel filegroup **fgroup1**. Le query sui dati della tabella verranno suddivise sui tre dischi con il conseguente miglioramento delle prestazioni. È possibile ottenere lo stesso risultato in termini di prestazioni utilizzando un singolo file creato su un set di striping RAID. File e filegroup, tuttavia, consentono di aggiungere nuovi file su nuovi dischi in modo semplice.  
  
 Tutti i file di dati vengono archiviati nei filegroup elencati nella tabella seguente.  
  
|Filegroup|Descrizione|  
|---------------|-----------------|  
|Primaria|Il filegroup che contiene il file primario. Tutte le tabelle di sistema vengono allocate al filegroup primario.|  
|Route definite dall'utente|Qualsiasi filegroup creato specificamente dall'utente in fase di creazione o di successiva modifica del database.|  
  
### <a name="default-filegroup"></a>Filegroup predefinito  
 Gli oggetti di database creati senza specificare un filegroup di appartenenza vengono assegnati al filegroup predefinito. Viene designato sempre e solo un filegroup predefinito. I file nel filegroup predefinito devono essere di dimensioni sufficienti a contenere tutti i nuovi oggetti non allocati ad altri filegroup.  
  
 A meno che non venga modificato tramite l'istruzione ALTER DATABASE, PRIMARY è il filegroup predefinito. Gli oggetti e le tabelle di sistema, tuttavia, restano allocati all'interno del filegroup PRIMARY e non all'interno del nuovo filegroup predefinito.  
  
## <a name="related-content"></a>Contenuto correlato  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
 [Opzioni per file e filegroup ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)  
  
 [Collegamento e scollegamento di un database &#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)  
  
  
