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
manager: shamikg
ms.openlocfilehash: e375c07ceddc995b599930c14f00710af040d6c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68262906"
---
# <a name="mapping-oracle-schemas-to-sql-server-schemas-oracletosql"></a>Mapping di schemi Oracle a schemi SQL Server (OracleToSQL)
In Oracle ogni database dispone di uno o più schemi. Per impostazione predefinita, SSMA esegue la migrazione di tutti gli oggetti in uno [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schema Oracle a un database denominato per lo schema. Tuttavia, è possibile personalizzare il mapping tra gli schemi e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] i database Oracle.  
  
## <a name="oracle-and-sql-server-schemas"></a>Schemi Oracle e SQL Server  
Un database Oracle contiene schemi. Un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene più database, ognuno dei quali può disporre di più schemi.  
  
Il concetto Oracle di uno schema viene mappato [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al concetto di database e di uno dei relativi schemi. Ad esempio, Oracle potrebbe avere uno schema denominato **HR**. Un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] potrebbe disporre di un database denominato **HR**e all'interno di tale database sono schemi. Uno schema è lo schema **dbo** (o Owner database). Per impostazione predefinita, verrà eseguito il mapping dell' **ora** dello schema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Oracle al database e allo schema **HR. dbo**. SSMA fa riferimento alla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] combinazione di database e schema come schema.  
  
È possibile modificare il mapping tra Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli schemi.  
  
## <a name="modifying-the-target-database-and-schema"></a>Modifica del database di destinazione e dello schema  
In SSMA è possibile eseguire il mapping di uno schema Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qualsiasi schema disponibile.  
  
**Per modificare il database e lo schema**  
  
1.  In Esplora metadati Oracle selezionare **schemi**.  
  
    La scheda **mapping dello schema** è disponibile anche quando si seleziona un singolo database, la cartella **schemi** o singoli schemi. L'elenco nella scheda **mapping dello schema** è personalizzato per l'oggetto selezionato.  
  
2.  Nel riquadro di destra fare clic sulla scheda **mapping dello schema** .  
  
    Viene visualizzato un elenco di tutti gli schemi Oracle, seguiti da un valore di destinazione. Questa destinazione è indicata in una notazione in due parti (*database. Schema*) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cui verrà eseguita la migrazione degli oggetti e dei dati.  
  
3.  Selezionare la riga che contiene il mapping che si desidera modificare, quindi fare clic su **modifica**.  
  
    Nella finestra di dialogo **Scegli schema di destinazione** è possibile cercare il database e lo schema di destinazione disponibili oppure digitare il nome del database e dello schema nella casella di testo in una notazione in due parti (database. Schema), quindi fare clic su **OK**.  
  
4.  La destinazione cambia nella scheda **mapping dello schema** .  
  
**Modalità di mapping**  
  
-   Mapping a SQL Server  
  
È possibile eseguire il mapping del database di origine a qualsiasi database di destinazione. Per impostazione predefinita, il database di origine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene mappato al database di destinazione con il quale è stata effettuata la connessione tramite SSMA. Se il database di destinazione di cui è stato eseguito il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mapping non è presente in, verrà visualizzato un messaggio che indica che **il database e/o lo schema non [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esiste nei metadati di destinazione. Verrà creata durante la sincronizzazione. Continuare? "** Fare clic su Sì. Analogamente, è possibile eseguire il mapping dello schema a uno schema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non esistente nel database di destinazione che verrà creato durante la sincronizzazione.  
  
## <a name="reverting-to-the-default-database-and-schema"></a>Ripristino del database e dello schema predefiniti  
Se si Personalizza il mapping tra uno schema Oracle e uno [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] schema, è possibile ripristinare i valori predefiniti del mapping.  
  
**Per ripristinare il database e lo schema predefiniti**  
  
1.  Nella scheda mapping dello schema selezionare una riga qualsiasi e fare clic su **Reimposta per impostazione predefinita** per ripristinare il database e lo schema predefiniti.  
  
## <a name="next-steps"></a>Passaggi successivi  
Se si desidera analizzare la conversione degli oggetti Oracle in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti, è possibile [creare un report di conversione](assessing-oracle-schemas-for-conversion-oracletosql.md). In caso contrario, è possibile [convertire le definizioni degli oggetti di database Oracle](converting-oracle-schemas-oracletosql.md) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definizioni di oggetti.  
  
## <a name="see-also"></a>Vedere anche  
[Connessione a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)  
[Migrazione di database Oracle a SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
