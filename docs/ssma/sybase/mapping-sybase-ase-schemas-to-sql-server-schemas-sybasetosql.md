---
title: Mapping di schemi di Sybase ASE a schemi SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Schema Mapping
ms.assetid: 2c927003-c49d-4fe1-8e3e-5b2899166268
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2a27b2e7c915a1ac13050d0ed188002cd42746c8
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52400434"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Mapping degli schemi di Sybase ASE per gli schemi di SQL Server (SybaseToSQL)
In Sybase Adaptive Server Enterprise (ASE), ogni database dispone di uno o più schemi. Per impostazione predefinita, SSMA esegue la migrazione di tutti gli oggetti all'interno di un database e dello schema nel database e schema nel stesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. Tuttavia, è possibile personalizzare il mapping tra l'ambiente del servizio App e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database di SQL Azure e schemi.  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>Ambiente del servizio App e SQL Server o SQL Azure schemi  
Ambiente del servizio App e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure sia specificare i database e i relativi schemi usando la notazione parte due come *database.schema*. Ad esempio, in un ambiente del servizio app **demo** del database, potrebbe esserci un **dbo** dello schema. È specificati come coppia di database e nello schema **demo.dbo**. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure ha lo stesso database e dello schema, la coppia è specificata anche come **demo.dbo**.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modifica il Database di destinazione e lo Schema  
In SSMA, è possibile eseguire il mapping dello schema un ambiente del servizio App per le [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o lo schema di SQL Azure.  
  
**Per modificare il database e dello schema**  
  
1.  Nel Visualizzatore metadati Sybase, selezionare **database**.  
  
    Il **dello Schema di Mapping** della scheda è disponibile anche quando si seleziona un singolo database, il **schemi** cartelle o singoli schemi. Nell'elenco il **Schema di Mapping** scheda personalizzata per l'oggetto selezionato.  
  
2.  Nel riquadro di destra, scegliere il **Schema di Mapping** scheda.  
  
    Verrà visualizzato un elenco di tutti i database di ambiente del servizio App con i relativi schemi, seguiti da un valore di destinazione. Questa destinazione è identificata in una notazione di due parti (*database.schema*) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure in cui verranno migrati i dati e oggetti.  
  
3.  Selezionare la riga che contiene il mapping che si desidera modificare e quindi fare clic su **Modify**.  
  
4.  Nel **scegliere lo Schema di destinazione** della finestra di dialogo è possibile esplorare per database di destinazione disponibili e dello schema o un tipo di database e lo schema assegnare un nome nella casella di testo in una notazione di due parti (database.schema) e quindi fare clic su **OK**.  
  
5.  La destinazione viene modificato nel **Schema di Mapping** scheda.  
  
**Modalità di Mapping**  
  
-   Mapping a SQL Server  
  
È possibile eseguire il mapping del database di origine a qualsiasi database di destinazione. Per impostazione predefinita viene eseguito il mapping di database di origine alla destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database con cui si è connessi con SSMA. Se il database di destinazione in corso il mapping è inesistente nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quindi verrà richiesto con un messaggio **"il Database e/o schema non esiste nella destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei metadati. Ne verrà creato uno durante la sincronizzazione. Si desidera continuare?"** Fare clic su Sì. Analogamente, è possibile mappare lo schema allo schema non esistente nella destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database che verrà creato durante la sincronizzazione.  
  
-   Il mapping a SQL Azure  
  
È possibile eseguire il mapping del database di origine al database di SQL Azure di destinazione connessi o per qualsiasi schema nel database di SQL Azure di destinazione connessi. Se si esegue il mapping dello Schema di origine ad alcuno schema non esistente nel database di destinazione connesso, quindi verrà richiesto con un messaggio **"dello Schema non esiste nei metadati di destinazione. Ne verrà creato uno durante la sincronizzazione. Si desidera continuare? "** Fare clic su Sì.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Viene ripristinato il Database predefinito e lo Schema  
Se si personalizza il mapping tra uno schema di ambiente del servizio App e un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o schema di SQL Azure, è possibile ripristinare il mapping ai valori predefiniti.  
  
**Per ripristinare il database predefinito e lo schema**  
  
1.  Nella scheda mapping dello schema, selezionare una riga qualsiasi e fare clic su **Ripristina predefinito** per ripristinare il database predefinito e lo schema.  
  
## <a name="next-steps"></a>Passaggi successivi  
Se si desidera analizzare la conversione di oggetti di Sybase ASE in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di SQL Azure, è possibile [creare un report di conversione](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md). In caso contrario, è possibile [convertire le definizioni degli oggetti di database di ASE](converting-sybase-ase-database-objects-sybasetosql.md) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o le definizioni degli oggetti di SQL Azure.  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Sybase ASE a SQL Server - Azure SQL database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
