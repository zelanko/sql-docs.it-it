---
title: Mapping di MySQL e tipi di dati SQL Server (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Mapping, customize data type mapping
- Mapping, Type mapping
ms.assetid: 14f98054-13b4-4231-a6b0-2452f3b9941d
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 99e86d99a4214b1ccdf317e75218fe22bb2c7af7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67908996"
---
# <a name="mapping-mysql-and-sql-server-data-types-mysqltosql"></a>Mapping dei tipi di dati MySQL e SQL Server (MySQLToSQL)
Tipi di database MySQL sono diversi dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tipi di database di SQL Azure. Quando si convertono oggetti di database MySQL [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o gli oggetti di SQL Azure, è necessario specificare come eseguire il mapping di tipi di dati da MySQL a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o SQL Azure. È possibile accettare i mapping dei tipi di dati predefinito, oppure è possibile personalizzare i mapping come illustrato nelle procedure seguenti.  
  
## <a name="default-mappings"></a>Mapping predefiniti  
SSMA è un set predefinito di mapping dei tipi di dati. Per l'elenco di mapping predefiniti, vedere [impostazioni del progetto &#40;Mapping dei tipi&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-type-mapping-mysqltosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo di Mapping dell'ereditarietà  
È possibile personalizzare i mapping dei tipi a livello di progetto, a livello di categoria di oggetto (ad esempio, tutte le stored procedure) o a livello di oggetto. Le impostazioni vengono ereditate da un livello superiore, a meno che non vengano sostituiti a un livello inferiore. Ad esempio, se si esegue il mapping **smallint** al **int** a livello di progetto, tutti gli oggetti nel progetto userà questo mapping non è stato personalizzato il mapping a livello di oggetto o categoria.  
  
Quando si visualizza il **Mapping dei tipi** scheda in SSMA, lo sfondo è contraddistinte da colorata per mostrare il mapping dei tipi vengono ereditati. Lo sfondo di un mapping dei tipi è di colore giallo per dei mapping dei tipi ereditati e bianco per qualsiasi mapping specificato al livello corrente.  
  
## <a name="customizing-data-type-mappings"></a>Personalizzazione dei mapping dei tipi di dati  
  
-   **Eseguire il mapping di tipi di dati:**  
  
    Le procedure seguenti illustrano come eseguire il mapping di tipi di dati nel progetto, database o a livello di oggetto di database:  
  
    1.  Per personalizzare i mapping dei tipi di dati per l'intero progetto, aprire il **impostazioni del progetto** nella finestra di dialogo. Nel menu Strumenti, selezionare **impostazioni del progetto**.  
  
        Nel riquadro sinistro, selezionare **Mapping dei tipi**. Il grafico di mapping di tipo e i pulsanti vengono visualizzati nel riquadro di destra.  
  
    2.  Per personalizzare i mapping dei tipi di dati a livello di database o una tabella, selezionare il database o la tabella nella finestra di esplorazione di metadati di MySQL. Nel Visualizzatore metadati MySQL, selezionare la cartella o un oggetto da personalizzare.  
  
        Nel riquadro di destra, fare clic su **Mapping dei tipi**.  
  
-   **Per aggiungere un nuovo mapping, procedere come segue:**  
  
    1.  Nel riquadro di mapping tra i tipi, fare clic su **Add** .  
  
    2.  Nel nuovo tipo di finestra di dialogo Mapping, in **tipo di origine**, selezionare il tipo di dati di MySQL per eseguire il mapping.  
  
    3.  Se il tipo richiede una lunghezza, specificare le lunghezze minima e massima dei dati per il mapping, selezionare la **dal** e **a** caselle di controllo e quindi immettere i valori.  
  
    4.  Ciò consente di personalizzare il mapping dei dati per i valori più piccoli e più grandi dello stesso tipo di dati. Sotto **tipo di destinazione**, selezionare la destinazione di SQL Server o un tipo di dati di SQL Azure.  
  
        1.  Alcuni tipi richiedono una lunghezza del tipo dati di destinazione. Se richiesto, immettere la nuova lunghezza dei dati nel **Sostituisci con** e quindi scegliere **OK**.  
  
        2.  Alcuni tipi richiedono un tipo di dati di destinazione **precisione** e **scalabilità**. Se richiesto, immettere la nuova precisione e la scalabilità nel **Sostituisci con** e quindi scegliere **OK**.  
  
-   **Per modificare un mapping dei tipi, eseguire le operazioni seguenti:**  
  
    1.  Nel riquadro di mapping tra i tipi, fare clic su **modifica**.  
  
    2.  Nel Mapping dei tipi di elenco della finestra di dialogo sotto **tipo di origine**, selezionare il tipo di dati di MySQL per eseguire il mapping.  
  
    3.  Se il tipo richiede una lunghezza, specificare le lunghezze minima e massima dei dati per il mapping, selezionare la **dal** e **a** caselle di controllo e quindi immettere i valori.  
  
    Ciò consente di personalizzare il mapping dei dati per i valori più piccoli e più grandi dello stesso tipo di dati. Sotto **tipo di destinazione**, selezionare la destinazione di SQL Server o un tipo di dati di SQL Azure.  
  
    1.  Alcuni tipi richiedono una lunghezza del tipo dati di destinazione. Se richiesto, immettere la nuova lunghezza dei dati nel **Sostituisci con** e quindi scegliere **OK**.  
  
    2.  Alcuni tipi richiedono un tipo di dati di destinazione **precisione** e **scalabilità** . Se richiesto, immettere la nuova precisione e la scalabilità nel **Sostituisci con** e quindi scegliere **OK** .  
  
-   **Per rimuovere un mapping dei tipi di dati, eseguire le operazioni seguenti:**  
  
    1.  Nel riquadro di Mapping dei tipi, selezionare la riga nell'elenco di mapping di tipo che contiene il mapping dei tipi di dati che si desidera rimuovere.  
  
    2.  Scegliere **Rimuovi**.  
  
## <a name="next-step"></a>Passaggio successivo  
Il passaggio successivo del processo di migrazione consiste nel [creare un report di valutazione](assessing-mysql-databases-for-conversion-mysqltosql.md) oppure [MySQL convertire gli oggetti di database in SQL Server o SQL Azure sintassi](converting-mysql-databases-mysqltosql.md). Se si crea un report, gli oggetti di MySQL vengono convertiti automaticamente durante la valutazione.  
  
## <a name="see-also"></a>Vedere anche  
[Database di migrazione da MySQL a SQL Server - Azure SQL database &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
