---
title: Mapping di schemi dell'ambiente del servizio app Sybase a schemi SQL Server (SybaseToSQL) | Microsoft Docs
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
ms.openlocfilehash: 5c39e81f8faffed606e6ca94315c47d383174c91
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028876"
---
# <a name="mapping-sybase-ase-schemas-to-sql-server-schemas-sybasetosql"></a>Mapping degli schemi di Sybase ASE per gli schemi di SQL Server (SybaseToSQL)
In Sybase Adaptive Server Enterprise (ASE) ogni database dispone di uno o più schemi. Per impostazione predefinita, SSMA esegue la migrazione di tutti gli oggetti all'interno di un database e di uno [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schema nello stesso database e nello stesso schema in o SQL Azure. Tuttavia, è possibile personalizzare il mapping tra l'ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del servizio app e o SQL Azure database e schemi.  
  
## <a name="ase-and-sql-server-or-sql-azure-schemas"></a>Schemi ASE e SQL Server o SQL Azure  
Ambiente del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio app e o SQL Azure specificano i database e i relativi schemi usando la notazione in due parti come *database. Schema*. Ad esempio, in un database **demo** dell'ambiente del servizio app potrebbe essere presente uno schema **dbo** . Il database e la coppia di schemi vengono specificati come **demo. dbo**. Se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure ha lo stesso database e lo stesso schema, la coppia viene specificata anche come **demo. dbo**.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modifica del database di destinazione e dello schema  
In SSMA è possibile eseguire il mapping di uno schema dell'ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del servizio app a qualsiasi schema disponibile o SQL Azure.  
  
**Per modificare il database e lo schema**  
  
1.  In Sybase Metadata Explorer selezionare **database**.  
  
    La scheda **mapping dello schema** è disponibile anche quando si seleziona un singolo database, la cartella **schemi** o singoli schemi. L'elenco nella scheda **mapping dello schema** è personalizzato per l'oggetto selezionato.  
  
2.  Nel riquadro di destra fare clic sulla scheda **mapping dello schema** .  
  
    Viene visualizzato un elenco di tutti i database dell'ambiente del servizio app con i rispettivi schemi, seguiti da un valore di destinazione. Questa destinazione è indicata in una notazione in due parti (*database. Schema*) in o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL Azure in cui verrà eseguita la migrazione degli oggetti e dei dati.  
  
3.  Selezionare la riga che contiene il mapping che si desidera modificare, quindi fare clic su **modifica**.  
  
4.  Nella finestra di dialogo **Scegli schema di destinazione** è possibile cercare il database e lo schema di destinazione disponibili oppure digitare il nome del database e dello schema nella casella di testo in una notazione in due parti (database. Schema), quindi fare clic su **OK**.  
  
5.  La destinazione cambia nella scheda **mapping dello schema** .  
  
**Modalità di mapping**  
  
-   Mapping a SQL Server  
  
È possibile eseguire il mapping del database di origine a qualsiasi database di destinazione. Per impostazione predefinita, il database di origine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene mappato al database di destinazione con il quale è stata effettuata la connessione tramite SSMA. Se il database di destinazione di cui è stato eseguito il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mapping non è presente in, verrà visualizzato un messaggio che indica che **il database e/o lo schema non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esiste nei metadati di destinazione. Verrà creata durante la sincronizzazione. Continuare? "** Fare clic su Sì. Analogamente, è possibile eseguire il mapping dello schema a uno schema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non esistente nel database di destinazione che verrà creato durante la sincronizzazione.  
  
-   Mapping a SQL Azure  
  
È possibile eseguire il mapping del database di origine alla destinazione connessa SQL Azure database o a qualsiasi schema nella destinazione connessa SQL Azure database. Se si esegue il mapping dello schema di origine a qualsiasi schema non esistente nel database di destinazione connesso, verrà visualizzato un messaggio in cui viene visualizzato il messaggio **"lo schema non esiste nei metadati di destinazione. Verrà creata durante la sincronizzazione. Continuare? "** Fare clic su Sì.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Ripristino del database e dello schema predefiniti  
Se si Personalizza il mapping tra uno schema dell'ambiente del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio app e uno schema o SQL Azure, è possibile ripristinare i valori predefiniti del mapping.  
  
**Per ripristinare il database e lo schema predefiniti**  
  
1.  Nella scheda mapping dello schema selezionare una riga qualsiasi e fare clic su **Reimposta per impostazione predefinita** per ripristinare il database e lo schema predefiniti.  
  
## <a name="next-steps"></a>Passaggi successivi  
Se si vuole analizzare la conversione degli oggetti di Sybase ASE in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure oggetti, è possibile [creare un report di conversione](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md). In caso contrario, è possibile [convertire le definizioni degli oggetti di database dell'ambiente del](converting-sybase-ase-database-objects-sybasetosql.md) servizio app in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure le definizioni  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database Sybase ASE a SQL Server-database SQL di Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
