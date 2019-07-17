---
title: Mapping dei tipi di dati SQL Server (DB2ToSQL) e DB2 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e7e939a8-5e76-4509-beaf-5acd1cab505e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1e9baab08f4295b2c51fd942f6153cc9425dd958
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68141014"
---
# <a name="mapping-db2-and-sql-server-data-types-db2tosql"></a>Mapping dei tipi di dati SQL Server (DB2ToSQL) e DB2
Tipi di database DB2 sono diversi da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di database. Quando si convertono oggetti di database DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti, è necessario specificare come eseguire il mapping di tipi di dati da DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile accettare i mapping dei tipi di dati predefinito, oppure è possibile personalizzare i mapping come illustrato nelle sezioni seguenti.  
  
## <a name="default-mappings"></a>Mapping predefiniti  
SSMA è un set predefinito di mapping dei tipi di dati. Per l'elenco di mapping predefiniti, vedere [impostazioni del progetto &#40;Mapping dei tipi&#41; &#40;DB2ToSQL&#41;](../../ssma/db2/project-settings-type-mapping-db2tosql.md).  
  
## <a name="type-mapping-inheritance"></a>Tipo di Mapping dell'ereditarietà  
È possibile personalizzare i mapping dei tipi a livello di progetto, a livello di categoria di oggetto (ad esempio, tutte le stored procedure) o a livello di oggetto. Le impostazioni vengono ereditate da un livello superiore, a meno che non vengano sostituiti a un livello inferiore. Ad esempio, se si esegue il mapping **smallmoney** al **denaro** a livello di progetto, tutti gli oggetti nel progetto userà questo mapping non è stato personalizzato il mapping a livello di oggetto o categoria.  
  
Quando si visualizza il **Mapping dei tipi** scheda in SSMA, lo sfondo è contraddistinte da colorata per mostrare il mapping dei tipi vengono ereditati. Lo sfondo di un mapping dei tipi è di colore giallo per dei mapping dei tipi ereditati e bianco per qualsiasi mapping specificato al livello corrente.  
  
## <a name="customizing-data-type-mappings"></a>Personalizzazione dei mapping dei tipi di dati  
La procedura seguente illustra come eseguire il mapping di tipi di dati nel progetto, database o a livello di oggetto:  
  
**Eseguire il mapping di tipi di dati**  
  
1.  Per personalizzare i mapping dei tipi di dati per l'intero progetto, aprire il **impostazioni del progetto** nella finestra di dialogo:  
  
    1.  Nel **degli strumenti** dal menu **le impostazioni del progetto**.  
  
    2.  Nel riquadro sinistro, selezionare **Mapping dei tipi**.  
  
        Il grafico di mapping di tipo e i pulsanti vengono visualizzati nel riquadro di destra.  
  
    In alternativa, per personalizzare il tipo di dati mapping al database, tabella, vista o a livello di stored procedure, selezionare il database, una categoria dell'oggetto o un oggetto nel Visualizzatore metadati DB2:  
  
    1.  Nel Visualizzatore metadati DB2, selezionare la cartella o un oggetto da personalizzare.  
  
    2.  Nel riquadro di destra, scegliere il **Mapping dei tipi** scheda.  
  
2.  Per aggiungere un nuovo mapping, procedere come segue:  
  
    1.  Fare clic su **Aggiungi**.  
  
    2.  Sotto **tipo di origine**, selezionare il tipo di dati DB2 per eseguire il mapping.  
  
    3.  Se il tipo richiede una lunghezza, specificare la lunghezza minima dei dati per il mapping nel **dal** finestra e la lunghezza massima dei dati nel **a** casella.  
  
        Ciò consente di personalizzare il mapping dei dati per i valori più piccoli e più grandi dello stesso tipo di dati.  
  
    4.  Sotto **tipo di destinazione**, selezionare la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati.  
  
        Alcuni tipi richiedono una lunghezza del tipo dati di destinazione. Se necessario, immettere la nuova lunghezza dei dati nel **sostituire con** casella.  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Per modificare un mapping dei tipi di dati, eseguire le operazioni seguenti:  
  
    1.  Fare clic su **Modifica**.  
  
    2.  Sotto **tipo di origine**, selezionare il tipo di dati DB2 per eseguire il mapping.  
  
    3.  Se il tipo richiede una lunghezza, specificare la lunghezza minima dei dati per il mapping nel **dal** finestra e la lunghezza massima dei dati nel **a** casella.  
  
        Ciò consente di personalizzare il mapping dei dati per i valori più piccoli e più grandi dello stesso tipo di dati.  
  
    4.  Sotto **tipo di destinazione**, selezionare la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati.  
  
        Alcuni tipi richiedono una lunghezza del tipo dati di destinazione. Se necessario, immettere la nuova lunghezza dei dati nel **sostituire con** casella e quindi [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Per rimuovere un mapping dei tipi di dati personalizzate, eseguire le operazioni seguenti:  
  
    1.  Selezionare la riga nell'elenco di mapping di tipo che contiene il mapping dei tipi di dati che si desidera rimuovere.  
  
    2.  Scegliere **Rimuovi**.  
  
        Non è possibile rimuovere i mapping ereditati. Tuttavia, i mapping ereditati vengono sottoposte a override dai mapping personalizzati di un oggetto specifico o per categoria dell'oggetto.  
  
## <a name="next-steps"></a>Passaggi successivi  
Il passaggio successivo del processo di migrazione consiste nel [Report di valutazione &#40;DB2ToSQL&#41; ](../../ssma/db2/assessment-report-db2tosql.md) oppure [conversione di schemi DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md). Se si crea un report di valutazione, gli oggetti DB2 vengono convertiti automaticamente durante la valutazione.  
  
## <a name="see-also"></a>Vedere anche  
[Database DB2 la migrazione a SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
