---
title: Mapping dei tipi di dati SQL Server (OracleToSQL) e Oracle | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Type Mapping Inheritance
ms.assetid: 05da1495-63b9-47b7-86e2-6746394a2d8a
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 06e538ebbdab9d6438182eaa0b61d44818286547
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62796026"
---
# <a name="mapping-oracle-and-sql-server-data-types-oracletosql"></a>Mapping di tipi di dati Oracle e SQL Server (OracleToSQL)
Tipi di database Oracle sono diversi da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di database. Quando si convertono oggetti di database Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti, è necessario specificare come eseguire il mapping di tipi di dati da Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile accettare i mapping dei tipi di dati predefinito, oppure è possibile personalizzare i mapping come illustrato nelle sezioni seguenti.  
  
## <a name="default-mappings"></a>Mapping predefiniti  
SSMA è un set predefinito di mapping dei tipi di dati. Per l'elenco di mapping predefiniti, vedere [impostazioni del progetto &#40;Mapping dei tipi&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-type-mapping-oracletosql.md).  
  
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
  
    In alternativa, per personalizzare il tipo di dati mapping al database, tabella, vista o a livello di stored procedure, selezionare il database, una categoria dell'oggetto o un oggetto nel Visualizzatore metadati Oracle:  
  
    1.  Nel Visualizzatore metadati Oracle, selezionare la cartella o un oggetto da personalizzare.  
  
    2.  Nel riquadro di destra, scegliere il **Mapping dei tipi** scheda.  
  
2.  Per aggiungere un nuovo mapping, procedere come segue:  
  
    1.  Scegliere **Aggiungi**.  
  
    2.  Sotto **tipo di origine**, selezionare il tipo di dati Oracle per eseguire il mapping.  
  
    3.  Se il tipo richiede una lunghezza, specificare la lunghezza minima dei dati per il mapping nel **dal** finestra e la lunghezza massima dei dati nel **a** casella.  
  
        Ciò consente di personalizzare il mapping dei dati per i valori più piccoli e più grandi dello stesso tipo di dati.  
  
    4.  Sotto **tipo di destinazione**, selezionare la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati.  
  
        Alcuni tipi richiedono una lunghezza del tipo dati di destinazione. Se necessario, immettere la nuova lunghezza dei dati nel **sostituire con** casella.  
  
    5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
3.  Per modificare un mapping dei tipi di dati, eseguire le operazioni seguenti:  
  
    1.  Fare clic su **Modifica**.  
  
    2.  Sotto **tipo di origine**, selezionare il tipo di dati Oracle per eseguire il mapping.  
  
    3.  Se il tipo richiede una lunghezza, specificare la lunghezza minima dei dati per il mapping nel **dal** finestra e la lunghezza massima dei dati nel **a** casella.  
  
        Ciò consente di personalizzare il mapping dei dati per i valori più piccoli e più grandi dello stesso tipo di dati.  
  
    4.  Sotto **tipo di destinazione**, selezionare la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati.  
  
        Alcuni tipi richiedono una lunghezza del tipo dati di destinazione. Se necessario, immettere la nuova lunghezza dei dati nel **sostituire con** casella e quindi [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
4.  Per rimuovere un mapping dei tipi di dati personalizzate, eseguire le operazioni seguenti:  
  
    1.  Selezionare la riga nell'elenco di mapping di tipo che contiene il mapping dei tipi di dati che si desidera rimuovere.  
  
    2.  Scegliere **Rimuovi**.  
  
        Non è possibile rimuovere i mapping ereditati. Tuttavia, i mapping ereditati vengono sottoposte a override dai mapping personalizzati di un oggetto specifico o per categoria dell'oggetto.  
  
## <a name="next-steps"></a>Passaggi successivi  
Il passaggio successivo del processo di migrazione consiste nel [creare un report di valutazione](assessing-oracle-schemas-for-conversion-oracletosql.md) oppure [convertire gli oggetti di database Oracle in sintassi SQL Server](converting-oracle-schemas-oracletosql.md). Se si crea un report di valutazione, gli oggetti Oracle vengono convertiti automaticamente durante la valutazione.  
  
## <a name="see-also"></a>Vedere anche  
[La migrazione da Oracle database in SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
