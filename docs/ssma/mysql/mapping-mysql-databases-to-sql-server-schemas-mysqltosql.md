---
title: Mapping di database MySQL a schemi SQL Server (MySQLToSQL) | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67908984"
---
# <a name="mapping-mysql-databases-to-sql-server-schemas-mysqltosql"></a>Mapping tra database MySQL e schemi di SQL Server (MySQLToSQL)
Per impostazione predefinita, SSMA per MySQL esegue la migrazione di tutti gli oggetti in uno [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schema MySQL in un database di o SQL Azure denominato per lo schema. Tuttavia, è possibile personalizzare il mapping tra gli schemi MySQL e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure database.  
  
## <a name="mysql-and-sql-server-or-sql-azure-schemas"></a>Schemi MySQL e SQL Server o SQL Azure  
Il concetto di MySQL di uno schema viene mappato al concetto di SQL Server di un database e di uno dei relativi schemi. SSMA fa riferimento alla combinazione SQL Server di database e schema come schema.  
  
Il concetto di MySQL di uno schema viene mappato al concetto di SQL Server di un database e di uno dei relativi schemi. Ad esempio, MySQL potrebbe avere uno schema denominato **HR**. Un'istanza di SQL Server potrebbe disporre di un database denominato **HR**e all'interno di tale database sono schemi. Uno schema è lo schema **dbo** (o Owner database). Per impostazione predefinita, viene eseguito **HR** il mapping di MySQL schema HR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al database e allo schema **HR. dbo**. SSMA fa riferimento alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] combinazione di database e schema come schema.  
  
È possibile modificare il mapping tra gli schemi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] MySQL e o Azure.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modifica del database di destinazione e dello schema  
In SSMA è possibile eseguire il mapping di uno schema MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qualsiasi schema disponibile o SQL Azure.  
  
**Per modificare il database e lo schema**  
  
1.  In MySQL Metadata Explorer selezionare **schemas**.  
  
    La scheda **mapping dello schema** è disponibile anche quando si selezionano singoli schemi. L'elenco nella scheda **mapping dello schema** è personalizzato per l'oggetto selezionato.  
  
2.  Nel riquadro di destra fare clic sulla scheda **mapping dello schema** .  
  
    Viene visualizzato un elenco di tutti gli schemi MySQL, seguiti da un valore di destinazione. Questa destinazione è indicata in una notazione in due parti (*database. Schema*) in o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure in cui verrà eseguita la migrazione degli oggetti e dei dati.  
  
3.  Selezionare la riga che contiene il mapping che si desidera modificare, quindi fare clic su **modifica**.  
  
    Nella finestra di dialogo **Scegli schema di destinazione** è possibile cercare il database e lo schema di destinazione disponibili oppure digitare il nome del database e dello schema nella casella di testo in una notazione in due parti (database. Schema), quindi fare clic su **OK**.  
  
4.  La destinazione cambia nella scheda **mapping dello schema** .  
  
**Modalità di mapping**  
  
-   Mapping a SQL Server  
  
È possibile eseguire il mapping del database di origine a qualsiasi database di destinazione. Per impostazione predefinita, il database di origine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene mappato al database di destinazione con il quale è stata effettuata la connessione tramite SSMA. Se il database di destinazione di cui è stato eseguito il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mapping non è presente in, verrà visualizzato un messaggio che indica che **il database e/o lo schema non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esiste nei metadati di destinazione. Verrà creata durante la sincronizzazione. Continuare? "** Fare clic su Sì. Analogamente, è possibile eseguire il mapping dello schema a uno schema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non esistente nel database di destinazione che verrà creato durante la sincronizzazione.  
  
-   Mapping a SQL Azure  
  
È possibile eseguire il mapping del database di origine al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database di destinazione connesso o a qualsiasi schema nel database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione connesso. Se si esegue il mapping dello schema di origine a qualsiasi schema non esistente nel database di destinazione connesso, verrà visualizzato un messaggio in cui viene visualizzato il messaggio **"lo schema non esiste nei metadati di destinazione. Verrà creata durante la sincronizzazione. Continuare? "** Fare clic su Sì.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Ripristino del database e dello schema predefiniti  
Se si Personalizza il mapping tra uno schema di MySQL e uno schema di SQL Server, è possibile ripristinare i valori predefiniti del mapping.  
  
**Per ripristinare il database e lo schema predefiniti**  
  
1.  Nella scheda mapping dello schema selezionare una riga qualsiasi e fare clic su **Reimposta per impostazione predefinita** per ripristinare il database e lo schema predefiniti.  
  
## <a name="next-steps"></a>Passaggi successivi  
Se si vuole analizzare la conversione degli oggetti MySQL in oggetti SQL Server o SQL Azure, è possibile [creare un report di conversione](assessing-mysql-databases-for-conversion-mysqltosql.md) in caso contrario, è possibile [convertire le definizioni degli oggetti di database mysql](converting-mysql-databases-mysqltosql.md) in schemi SQL Server o SQL Azure  
  
## <a name="see-also"></a>Vedi anche  
[Impostazioni progetto &#40;conversione&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-conversion-mysqltosql.md)  
[Connessione al database SQL di Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
[Migrazione di database MySQL a SQL Server-database SQL di Azure &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
[Connessione a SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
