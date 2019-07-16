---
title: Mapping tra i database MySQL a schemi SQL Server (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, Modifying target database and schema
- Mapping, reverting to default database and schema
ms.assetid: 5c6fb445-92ae-4933-b77d-80230931c024
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 215833c96fae02ae7877e00173fb5a920a47ee0c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908984"
---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>Mapping tra database MySQL e schemi di SQL Server (MySQLToSQL)
Per impostazione predefinita, SSMA per MySQL consente di migrare tutti gli oggetti in uno schema di MySQL a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database di SQL Azure denominato per lo schema. Tuttavia, è possibile personalizzare il mapping tra gli schemi di MySQL e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o i database di SQL Azure.  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>MySQL e SQL Server o SQL Azure schemi  
Il concetto di MySQL di uno schema viene eseguito il mapping al concetto di un database e uno dei relativi schemi di SQL Server. SSMA si intende la combinazione di SQL Server di database e nello schema come schema.  
  
Il concetto di MySQL di uno schema viene eseguito il mapping al concetto di un database e uno dei relativi schemi di SQL Server. Ad esempio, MySQL potrebbe avere uno schema denominato **HR**. Un'istanza di SQL Server potrebbe essere un database denominato **HR**, e all'interno del database sono gli schemi. Uno schema è il **dbo** (o proprietario del database) dello schema. Per impostazione predefinita, gli schemi di MySQL **HR** verrà mappato il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schema e il database **HR.dbo**. SSMA si intende il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] combinazione di database e nello schema come schema.  
  
È possibile modificare il mapping tra MySQL e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o schemi di Azure.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modifica il Database di destinazione e lo Schema  
In SSMA, è possibile mappare uno schema di MySQL per eventuale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o lo schema di SQL Azure.  
  
**Per modificare il database e dello schema**  
  
1.  Nel Visualizzatore metadati di MySQL, selezionare **schemi**.  
  
    Il **Schema di Mapping** scheda è disponibile anche quando si seleziona singoli schemi. Nell'elenco il **Schema di Mapping** scheda personalizzata per l'oggetto selezionato.  
  
2.  Nel riquadro di destra, scegliere il **Schema di Mapping** scheda.  
  
    Verrà visualizzato un elenco di tutti gli schemi di MySQL, seguito da un valore di destinazione. Questa destinazione è identificata in una notazione di due parti (*database.schema*) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure in cui verranno migrati i dati e oggetti.  
  
3.  Selezionare la riga che contiene il mapping che si desidera modificare e quindi fare clic su **Modify**.  
  
    Nel **scegliere lo Schema di destinazione** della finestra di dialogo è possibile esplorare per database di destinazione disponibili e dello schema o un tipo di database e lo schema assegnare un nome nella casella di testo in una notazione di due parti (database.schema) e quindi fare clic su **OK**.  
  
4.  La destinazione viene modificato nel **Schema di Mapping** scheda.  
  
**Modalità di Mapping**  
  
-   Mapping a SQL Server  
  
È possibile eseguire il mapping del database di origine a qualsiasi database di destinazione. Per impostazione predefinita viene eseguito il mapping di database di origine alla destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database con cui si è connessi con SSMA. Se il database di destinazione in corso il mapping è inesistente nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quindi verrà richiesto con un messaggio **"il Database e/o schema non esiste nella destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei metadati. Ne verrà creato uno durante la sincronizzazione. Si desidera continuare?"** Fare clic su Sì. Analogamente, è possibile mappare lo schema allo schema non esistente nella destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database che verrà creato durante la sincronizzazione.  
  
-   Il mapping a SQL Azure  
  
È possibile eseguire il mapping del database di origine alla destinazione connessa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database o per qualsiasi schema nel database di destinazione connessi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database. Se si esegue il mapping dello Schema di origine ad alcuno schema non esistente nel database di destinazione connesso, quindi verrà richiesto con un messaggio **"dello Schema non esiste nei metadati di destinazione. Ne verrà creato uno durante la sincronizzazione. Si desidera continuare? "** Fare clic su Sì.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Viene ripristinato il Database predefinito e lo Schema  
Se si personalizza il mapping tra uno schema di MySQL e uno schema di SQL Server, è possibile ripristinare il mapping ai valori predefiniti.  
  
**Per ripristinare il database predefinito e lo schema**  
  
1.  Nella scheda mapping dello schema, selezionare una riga qualsiasi e fare clic su **Ripristina predefinito** per ripristinare il database predefinito e lo schema.  
  
## <a name="next-steps"></a>Passaggi successivi  
Se si desidera analizzare la conversione di oggetti di MySQL in oggetti di SQL Server o SQL Azure, puoi [creare un report di conversione](assessing-mysql-databases-for-conversion-mysqltosql.md) in caso contrario, è possibile [convertire le definizioni degli oggetti di database MySQL](converting-mysql-databases-mysqltosql.md) in SQL Schemi di server o SQL Azure  
  
## <a name="see-also"></a>Vedere anche  
[Le impostazioni di progetto &#40;conversione&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[La connessione al database SQL di Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[Database di migrazione da MySQL a SQL Server - Azure SQL database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[La connessione a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
