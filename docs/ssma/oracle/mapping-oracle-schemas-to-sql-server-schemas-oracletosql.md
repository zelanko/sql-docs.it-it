---
title: Mapping di schemi Oracle a schemi SQL Server (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 0edeaa08-9c5d-4e3a-bc15-b9a1f0c8a9dc
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 61b706145f708e9b2e8a04ba4e7bc574c503a742
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52407873"
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>Mapping di schemi Oracle a schemi SQL Server (OracleToSQL)
In Oracle, ogni database dispone di uno o più schemi. Per impostazione predefinita, SSMA esegue la migrazione di tutti gli oggetti in uno schema Oracle per un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominato per lo schema di database. Tuttavia, è possibile personalizzare il mapping tra schemi Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database.  
  
## <a name="oracle-and-sql-server-schemas"></a>Oracle e schemi SQL Server  
Un database Oracle contiene gli schemi. Un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene più database, ognuno dei quali può disporre di più schemi.  
  
Il concetto di Oracle di uno schema esegue il mapping al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] concetto di un database e uno dei relativi schemi. Ad esempio, Oracle può avere uno schema denominato **HR**. Un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe disporre di un database denominato **HR**, e all'interno del database sono gli schemi. Uno schema è il **dbo** (o proprietario del database) dello schema. Per impostazione predefinita, lo schema di Oracle **HR** verrà mappato al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schema e il database **HR.dbo**. SSMA si intende il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] combinazione di database e nello schema come schema.  
  
È possibile modificare il mapping tra Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schemi.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modifica il Database di destinazione e lo Schema  
In SSMA, è possibile mappare uno schema Oracle per eventuale [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dello schema.  
  
**Per modificare il database e dello schema**  
  
1.  Nel Visualizzatore metadati Oracle, selezionare **schemi**.  
  
    Il **dello Schema di Mapping** della scheda è disponibile anche quando si seleziona un singolo database, il **schemi** cartelle o singoli schemi. Nell'elenco il **Schema di Mapping** scheda personalizzata per l'oggetto selezionato.  
  
2.  Nel riquadro di destra, scegliere il **Schema di Mapping** scheda.  
  
    Verrà visualizzato un elenco di tutti gli schemi di Oracle, seguito da un valore di destinazione. Questa destinazione è identificata in una notazione di due parti (*database.schema*) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui verranno migrati i dati e oggetti.  
  
3.  Selezionare la riga che contiene il mapping che si desidera modificare e quindi fare clic su **Modify**.  
  
    Nel **scegliere lo Schema di destinazione** della finestra di dialogo è possibile esplorare per database di destinazione disponibili e dello schema o un tipo di database e lo schema assegnare un nome nella casella di testo in una notazione di due parti (database.schema) e quindi fare clic su **OK**.  
  
4.  La destinazione viene modificato nel **Schema di Mapping** scheda.  
  
**Modalità di Mapping**  
  
-   Mapping a SQL Server  
  
È possibile eseguire il mapping del database di origine a qualsiasi database di destinazione. Per impostazione predefinita viene eseguito il mapping di database di origine alla destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database con cui si è connessi con SSMA. Se il database di destinazione in corso il mapping è inesistente nel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quindi verrà richiesto con un messaggio **"il Database e/o schema non esiste nella destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei metadati. Ne verrà creato uno durante la sincronizzazione. Si desidera continuare?"** Fare clic su Sì. Analogamente, è possibile mappare lo schema allo schema non esistente nella destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database che verrà creato durante la sincronizzazione.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Viene ripristinato il Database predefinito e lo Schema  
Se si personalizza il mapping tra uno schema Oracle e un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dello schema, è possibile ripristinare il mapping ai valori predefiniti.  
  
**Per ripristinare il database predefinito e lo schema**  
  
1.  Nella scheda mapping dello schema, selezionare una riga qualsiasi e fare clic su **Ripristina predefinito** per ripristinare il database predefinito e lo schema.  
  
## <a name="next-steps"></a>Passaggi successivi  
Se si desidera analizzare la conversione degli oggetti Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti, è possibile [creare un report di conversione](assessing-oracle-schemas-for-conversion-oracletosql.md). In caso contrario, è possibile [convertire le definizioni degli oggetti di database Oracle](converting-oracle-schemas-oracletosql.md) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definizioni di oggetto.  
  
## <a name="see-also"></a>Vedere anche  
[La connessione a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[La migrazione da Oracle database in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
