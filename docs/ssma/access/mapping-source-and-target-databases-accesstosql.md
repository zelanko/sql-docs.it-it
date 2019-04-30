---
title: Mapping di origine e i database di destinazione (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- database schemas
- mapping, databases
- schemas, mapping to
- schemas, SQL Azure
- schemas, SQL Server
- source database
- target database
ms.assetid: 69bee937-7b2c-49ee-8866-7518c683fad4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: d2be7854240a52edd8f3308ea92e3ea7eb25924f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63299196"
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>Mapping di origine e i database di destinazione (AccessToSQL)
Quando ci si connette a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure, è necessario specificare un database di destinazione per la migrazione. Se si dispone di più database di Access è possibile eseguirne il mapping a più [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database (o gli schemi) o a più schemi inclusi nel database di SQL Azure connesso.  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>SQL Server o schemi del Database SQL Azure  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database utilizzano il concetto di schemi per separare gli oggetti all'interno di un database in gruppi logici. Ad esempio, un database di libreria è stato possibile usare tre schemi denominati **libri**, **audio**, e **video** per separare gli oggetti di audio e video libro intitolato uni dagli altri. Per impostazione predefinita, il database di access viene eseguito il mapping a **master** database e **dbo** schema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e in un database connesso e **dbo** dello schema in SQL Azure.  
  
Non è stato personalizzato il mapping tra ogni database di Access e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database e dello schema, verrà eseguita la migrazione di SSMA tutti gli schemi e dati associati al database l'accesso al database predefinito mappato.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modifica il Database di destinazione e lo Schema  
SSMA consente di eseguire il mapping di ogni database di Access per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database di SQL Azure e lo schema. La procedura seguente descrive come personalizzare il mapping per ogni database.  
  
**Per modificare il database di destinazione e lo schema**  
  
1.  Nel riquadro di esplorazione di metadati di accesso, selezionare **accedere ai metadati**.  
  
    Mapping dello schema è disponibile anche quando si seleziona il **database** nodo o un qualsiasi nodo del database. L'elenco di mapping dello schema viene personalizzato per l'oggetto selezionato.  
  
2.  Nel riquadro di destra, scegliere il **Schema di Mapping** scheda.  
  
    Si noterà una tabella che include l'accesso dello schema di Sql Azure e relativi ssNoVersion corrispondente o nomi di database. Lo schema di destinazione è identificato in una notazione di due parti (database.schema).  
  
3.  Selezionare la riga che contiene il mapping che si desidera personalizzare e quindi fare clic su **Modify**.  
  
4.  Nel **scegliere lo Schema di destinazione** della finestra di dialogo è possibile esplorare per database di destinazione disponibili e dello schema o un tipo di database e lo schema assegnare un nome nella casella di testo in una notazione di due parti (database.schema) e quindi fare clic su **OK**.  
  
**Modalità di Mapping**  
  
-   Mapping a SQL Server  
  
È possibile eseguire il mapping del database di origine a qualsiasi database di destinazione. Per impostazione predefinita viene eseguito il mapping di database di origine alla destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database con cui si è connessi con SSMA. Se il database di destinazione in corso il mapping non esiste sul [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], quindi verrà richiesto con un messaggio **"il Database e/o schema non esiste nella destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dei metadati. Ne verrà creato uno durante la sincronizzazione. Si desidera continuare?"** Fare clic su Sì. Analogamente, è possibile mappare lo schema allo schema non esistente nella destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database che verrà creato durante la sincronizzazione.  
  
-   Il mapping a SQL Azure  
  
È possibile eseguire il mapping del database di origine alla destinazione connessa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database o per qualsiasi schema nel database di destinazione connessi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database. Se si esegue il mapping dello Schema di origine ad alcuno schema non esistente nel database di destinazione connesso, quindi verrà richiesto con un messaggio **"dello Schema non esiste nei metadati di destinazione. Ne verrà creato uno durante la sincronizzazione. Si desidera continuare? "** Fare clic su Sì.  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>Viene ripristinato il Database iniziale e lo Schema  
Se si personalizza il mapping tra un database di Access e un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o database di SQL Azure e lo schema, è possibile ripristinare il mapping nel database specificato quando connesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
**Per reimpostare lo schema e il database predefinito**  
  
1.  Nella scheda mapping dello schema, selezionare una riga qualsiasi e fare clic su **Ripristina predefinito** per ripristinare il database predefinito e lo schema.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste [conversione di oggetti di database](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
