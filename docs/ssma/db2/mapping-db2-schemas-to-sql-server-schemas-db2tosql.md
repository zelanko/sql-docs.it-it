---
title: Mapping di schemi DB2 a schemi SQL Server (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 05ff7bd4-e60b-4f48-a893-bc2346aa9a8a
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: e9ccc7648be4915a68b798f314689d961113639a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298654"
---
# <a name="mapping-db2-schemas-to-sql-server-schemas-db2tosql"></a>Mapping di schemi DB2 a schemi SQL Server (DB2ToSQL)
In DB2, ogni database dispone di uno o più schemi. Per impostazione predefinita, SSMA esegue la migrazione di tutti gli oggetti in uno schema DB2 a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominato per lo schema di database. Tuttavia, è possibile personalizzare il mapping tra schemi DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
## <a name="db2-and-sql-server-schemas"></a>DB2 e degli schemi SQL Server  
Un database DB2 contiene gli schemi. Un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene più database, ognuno dei quali può disporre di più schemi.  
  
Il concetto di DB2 di uno schema esegue il mapping al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] concetto di un database e uno dei relativi schemi. Ad esempio, DB2 può avere uno schema denominato **HR**. Un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe disporre di un database denominato **HR**, e all'interno del database sono gli schemi. Uno schema è il **dbo** (o proprietario del database) dello schema. Per impostazione predefinita, lo schema DB2 **HR** verrà mappato il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schema e il database **HR.dbo**. SSMA si intende il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] combinazione di database e nello schema come schema.  
  
È possibile modificare il mapping tra DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schemi.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modifica il Database di destinazione e lo Schema  
In SSMA, è possibile mappare uno schema DB2 su qualsiasi disponibile [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dello schema.  
  
**Per modificare il database e dello schema**  
  
1.  Nel Visualizzatore metadati DB2, selezionare **schemi**.  
  
    Il **dello Schema di Mapping** della scheda è disponibile anche quando si seleziona un singolo database, il **schemi** cartelle o singoli schemi. Nell'elenco il **Schema di Mapping** scheda personalizzata per l'oggetto selezionato.  
  
2.  Nel riquadro di destra, scegliere il **Schema di Mapping** scheda.  
  
    Verrà visualizzato un elenco di tutti gli schemi DB2, seguito da un valore di destinazione. Questa destinazione è identificata in una notazione di due parti (*database.schema*) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui verranno migrati i dati e oggetti.  
  
3.  Selezionare la riga che contiene il mapping che si desidera modificare e quindi fare clic su **Modify**.  
  
    Nel **scegliere lo Schema di destinazione** della finestra di dialogo è possibile esplorare per database di destinazione disponibili e dello schema o un tipo di database e lo schema assegnare un nome nella casella di testo in una notazione di due parti (database.schema) e quindi fare clic su **OK**.  
  
4.  La destinazione viene modificato nel **Schema di Mapping** scheda.  
  
**Modalità di Mapping**  
  
-   Mapping a SQL Server  
  
È possibile eseguire il mapping del database di origine a qualsiasi database di destinazione. Per impostazione predefinita viene eseguito il mapping di database di origine alla destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database con cui si è connessi con SSMA. Se il database di destinazione in corso il mapping è inesistente nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quindi verrà richiesto con un messaggio **"il Database e/o schema non esiste nella destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei metadati. Ne verrà creato uno durante la sincronizzazione. Si desidera continuare?"** Fare clic su Sì. Analogamente, è possibile mappare lo schema allo schema non esistente nella destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database che verrà creato durante la sincronizzazione.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Viene ripristinato il Database predefinito e lo Schema  
Se si personalizza il mapping tra uno schema DB2 e un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dello schema, è possibile ripristinare il mapping ai valori predefiniti.  
  
**Per ripristinare il database predefinito e lo schema**  
  
1.  Nella scheda mapping dello schema, selezionare una riga qualsiasi e fare clic su **Ripristina predefinito** per ripristinare il database predefinito e lo schema.  
  
## <a name="next-steps"></a>Passaggi successivi  
Se si desidera analizzare la conversione di oggetti di DB2 in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti, è possibile [Report di migrazione dati (SSMA comuni)](https://msdn.microsoft.com/bbfb9d88-5a98-4980-8d19-c5d78bd0d241).  
  
## <a name="see-also"></a>Vedere anche  
[La connessione a SQL Server &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)  
[Database DB2 la migrazione a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
