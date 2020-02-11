---
title: Mapping dei database di origine e di destinazione (AccessToSQL) | Microsoft Docs
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
ms.openlocfilehash: 192db2e6c074305ca258d76652351175c8a82751
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67907154"
---
# <a name="mapping-source-and-target-databases-accesstosql"></a>Mapping dei database di origine e di destinazione (AccessToSQL)
Quando ci si connette [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a o SQL Azure, è necessario specificare un database di destinazione per la migrazione. Se si dispone di più database di Access, è possibile eseguirne il mapping a più [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database (o schemi) o a più schemi nel database di SQL Azure connesso.  
  
## <a name="sql-server-or-sql-azure-database-schemas"></a>Schemi di database SQL Server o SQL Azure  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]i database utilizzano il concetto di schemi per separare gli oggetti all'interno di un database in gruppi logici. Ad esempio, un database di libreria può utilizzare tre schemi denominati **libri**, **audio**e **video** per separare gli oggetti book, audio e video tra loro. Per impostazione predefinita, il database di Access viene mappato al database **Master** e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] allo schema **dbo** in e al database connesso e allo schema **dbo** in SQL Azure.  
  
A meno che non si Personalizza il mapping tra ogni database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Access e il database e lo schema, SSMA eseguirà la migrazione di tutti gli schemi e i dati associati al database di Access al database predefinito mappato.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modifica del database di destinazione e dello schema  
SSMA consente di eseguire il mapping di ogni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database di Access a o SQL Azure database e schema. Nella procedura riportata di seguito viene descritto come personalizzare il mapping per ogni database.  
  
**Per modificare il database e lo schema di destinazione**  
  
1.  Nel riquadro Access Metadata Explorer selezionare **Access-Metadata**.  
  
    Il mapping dello schema è disponibile anche quando si seleziona il nodo **database** o qualsiasi nodo del database. L'elenco di mapping dello schema è personalizzato per l'oggetto selezionato.  
  
2.  Nel riquadro di destra fare clic sulla scheda **mapping dello schema** .  
  
    Viene visualizzata una tabella contenente i nomi dei database di Access e il relativo schema ssNoVersion o SQL Azure corrispondente. Lo schema di destinazione è indicato in una notazione in due parti (database. Schema).  
  
3.  Selezionare la riga che contiene il mapping che si desidera personalizzare, quindi fare clic su **modifica**.  
  
4.  Nella finestra di dialogo **Scegli schema di destinazione** è possibile cercare il database e lo schema di destinazione disponibili oppure digitare il nome del database e dello schema nella casella di testo in una notazione in due parti (database. Schema), quindi fare clic su **OK**.  
  
**Modalità di mapping**  
  
-   Mapping a SQL Server  
  
È possibile eseguire il mapping del database di origine a qualsiasi database di destinazione. Per impostazione predefinita, il database di origine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene mappato al database di destinazione con il quale è stata effettuata la connessione tramite SSMA. Se il database di destinazione di cui è stato eseguito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]il mapping non esiste in, verrà visualizzato **il messaggio "il database e/o lo schema non esiste nei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadati di destinazione. Verrà creata durante la sincronizzazione. Continuare? "** Fare clic su Sì. Analogamente, è possibile eseguire il mapping dello schema a uno schema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non esistente nel database di destinazione che verrà creato durante la sincronizzazione.  
  
-   Mapping a SQL Azure  
  
È possibile eseguire il mapping del database di origine al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database di destinazione connesso o a qualsiasi schema nel database [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di destinazione connesso. Se si esegue il mapping dello schema di origine a qualsiasi schema non esistente nel database di destinazione connesso, verrà visualizzato un messaggio in cui viene visualizzato il messaggio **"lo schema non esiste nei metadati di destinazione. Verrà creata durante la sincronizzazione. Continuare? "** Fare clic su Sì.  
  
## <a name="reverting-to-your-initial-database-and-schema"></a>Ripristino del database e dello schema iniziali  
Se si Personalizza il mapping tra un database di Access e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uno o SQL Azure database e schema, è possibile ripristinare il mapping al database specificato quando si è connessi a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure.  
  
**Per ripristinare il database e lo schema predefiniti**  
  
1.  Nella scheda mapping dello schema selezionare una riga qualsiasi e fare clic su **Reimposta per impostazione predefinita** per ripristinare il database e lo schema predefiniti.  
  
## <a name="next-step"></a>passaggio successivo  
Il passaggio successivo del processo di migrazione consiste nella [conversione degli oggetti di database](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
