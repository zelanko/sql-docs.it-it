---
title: Mapping di Sybase ASE e tipi di dati SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping Sybase ASE Schemas to SQL Server Schemas
- Type Mapping Settings
ms.assetid: 784365d3-df4e-47ab-8ee0-d8392b52f510
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8e50253b7c7fb6c59b4303c528c1ef7267ccf644
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62706075"
---
# <a name="mapping-sybase-ase-and-sql-server-data-types-sybasetosql"></a>Mapping dei tipi di dati di Sybase ASE e SQL Server (SybaseToSQL)
Tipi di database di Sybase Adaptive Server Enterprise (ASE) sono diversi dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tipi di database di SQL Azure. Quando si convertono oggetti di database ambiente del servizio app [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di SQL Azure, è necessario specificare come eseguire il mapping di tipi di dati dall'ambiente del servizio app [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. È possibile accettare i mapping dei tipi di dati predefinito, oppure è possibile personalizzare i mapping come illustrato nelle sezioni seguenti.  
  
## <a name="default-mappings"></a>Mapping predefiniti  
SSMA è un set predefinito di mapping dei tipi di dati. Per l'elenco di mapping predefiniti, vedere [impostazioni del progetto &#40;Mapping dei tipi&#41; &#40;SybaseToSQL&#41;](../../ssma/sybase/project-settings-type-mapping-sybasetosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo di Mapping dell'ereditarietà  
È possibile personalizzare i mapping dei tipi a livello di progetto, a livello di categoria di oggetto (ad esempio, tutte le stored procedure) o a livello di oggetto. Le impostazioni vengono ereditate da un livello superiore, a meno che a un livello inferiore viene sottoposto a override. Ad esempio, se si esegue il mapping **smallmoney** al **denaro** a livello di progetti, tutti gli oggetti nel progetto userà questo mapping non è stato personalizzato il mapping a livello di oggetto categoria oppure a livello di oggetto.  
  
Quando si visualizza il **Mapping dei tipi** scheda in SSMA, lo sfondo è contraddistinte da colorata per mostrare il mapping dei tipi vengono ereditati. Lo sfondo di un mapping dei tipi è di colore giallo per dei mapping dei tipi ereditati e bianco per qualsiasi mapping specificato al livello corrente.  
  
## <a name="customizing-data-type-mappings"></a>Personalizzazione dei mapping dei tipi di dati  
La procedura seguente illustra come eseguire il mapping di tipi di dati nel progetto, database o a livello di oggetto.  
  
**Eseguire il mapping di tipi di dati**  
  
1.  Per personalizzare i mapping dei tipi di dati per l'intero progetto, aprire il **impostazioni del progetto** nella finestra di dialogo:  
  
    1.  Nel **degli strumenti** dal menu **le impostazioni del progetto**.  
  
    2.  Nel riquadro sinistro, selezionare **Mapping dei tipi**.  
  
        Il grafico di mapping di tipo e i pulsanti vengono visualizzati nel riquadro di destra.  
  
    In alternativa, per personalizzare il tipo di dati mapping al database, tabella, vista o a livello di stored procedure, selezionare il database, una categoria dell'oggetto o un oggetto nel Visualizzatore metadati Sybase:  
  
    1.  Nel Visualizzatore metadati Sybase, selezionare la cartella o un oggetto che si desidera personalizzare.  
  
    2.  Nel riquadro di destra, scegliere il **Mapping dei tipi** scheda.  
  
2.  Per aggiungere un nuovo mapping, procedere come segue:  
  
    1.  Scegliere **Aggiungi**.  
  
    2.  Sotto **tipo di origine**, selezionare il tipo di dati di ambiente del servizio App per eseguire il mapping.  
  
    3.  Se il tipo richiede una lunghezza, specificare la lunghezza minima dei dati per il mapping nel **dal** casella e specificare la lunghezza massima dei dati per il mapping nel **a** casella.  
  
        Ciò consente di personalizzare il mapping dei dati per i valori più piccoli e più grandi dello stesso tipo di dati.  
  
    4.  Sotto **tipo di destinazione**, selezionare la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tipo di dati di SQL Azure.  
  
        Alcuni tipi richiedono una lunghezza del tipo dati di destinazione. Se necessario, immettere la nuova lunghezza dei dati nel **sostituire con** casella.  
  
    5.  Fare clic su **OK**.  
  
3.  Per modificare un mapping dei tipi di dati, eseguire le operazioni seguenti:  
  
    1.  Fare clic su **Modifica**.  
  
    2.  Sotto **tipo di origine**, selezionare il tipo di dati di ambiente del servizio App per eseguire il mapping.  
  
    3.  Se il tipo richiede una lunghezza, specificare la lunghezza minima dei dati per il mapping nel **dal** casella e specificare la lunghezza massima dei dati per il mapping nel **a** casella.  
  
        Ciò consente di personalizzare il mapping dei dati per i valori più piccoli e più grandi dello stesso tipo di dati.  
  
    4.  Sotto **tipo di destinazione**, selezionare la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tipo di dati di SQL Azure.  
  
        Alcuni tipi richiedono una lunghezza del tipo dati di destinazione. Se necessario, immettere la nuova lunghezza dei dati nel **sostituita** casella e quindi fare clic su **OK**.  
  
4.  Per rimuovere un mapping dei tipi di dati personalizzate, eseguire le operazioni seguenti:  
  
    1.  Selezionare la riga nell'elenco di mapping di tipo che contiene il mapping dei tipi di dati che si desidera rimuovere.  
  
    2.  Scegliere **Rimuovi**.  
  
        Non è possibile rimuovere i mapping ereditati. Tuttavia, i mapping ereditati vengono sottoposte a override dai mapping personalizzati di un oggetto specifico o per categoria dell'oggetto.  
  
## <a name="next-steps"></a>Passaggi successivi  
Il passaggio successivo del processo di migrazione consiste nel [creare un report di valutazione](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) oppure [gli oggetti di database di Sybase ASE converte alla sintassi di SQL Server o SQL Azure](converting-sybase-ase-database-objects-sybasetosql.md). Se si crea un report di valutazione, gli oggetti di Sybase ASE vengono convertiti automaticamente durante la valutazione.  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Sybase ASE a SQL Server - Azure SQL database &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
