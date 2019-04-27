---
title: Mapping di origine e i tipi di dati di destinazione (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- customizing data type mappings
- data types, mapping
- mapping, data types
- source data types
- target data types
ms.assetid: b362a075-16e7-423f-b63f-e1e9f02844a9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a32f7f321baa17dbcdaf557bb7de033422a02dbc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740981"
---
# <a name="mapping-source-and-target-data-types-accesstosql"></a>Mapping di origine e i tipi di dati di destinazione (AccessToSQL)
Tipi di database di Access sono diversi dal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di database. Quando si convertono oggetti di database di Access da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oggetti, è necessario specificare come eseguire il mapping di tipi di dati da Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. È possibile accettare i mapping dei tipi di dati predefinito, oppure è possibile personalizzare i mapping come illustrato nelle procedure seguenti.  
  
## <a name="default-mappings"></a>Mapping predefiniti  
SSMA è un set predefinito di mapping dei tipi di dati. Per l'elenco di mapping predefiniti, vedere [impostazioni progetto (Mapping dei tipi)](https://msdn.microsoft.com/b87b9683-abed-4677-8c50-18bdba704655).  
  
## <a name="customizing-data-type-mappings"></a>Personalizzazione dei mapping dei tipi di dati  
Tramite il **impostazioni del progetto** nella finestra di dialogo è possibile personalizzare la modalità di mapping dei tipi per tutti i database e oggetti di database in un progetto. I mapping dei tipi per un progetto si applicano a tutti i database e oggetti di database che sono privi di mapping dei tipi personalizzati.  
  
È anche possibile personalizzare i mapping dei tipi di dati a livello di database o tabella.  
  
La procedura seguente illustra come eseguire il mapping di tipi di dati nel progetto, database o a livello di oggetto di database.  
  
**Eseguire il mapping di tipi di dati**  
  
1.  Per personalizzare i mapping dei tipi di dati per l'intero progetto, aprire il **impostazioni del progetto** nella finestra di dialogo:  
  
    1.  Nel **degli strumenti** dal menu **le impostazioni del progetto**.  
  
    2.  Nel riquadro sinistro, selezionare **Mapping dei tipi**.  
  
        Il grafico di mapping di tipo e i pulsanti vengono visualizzati nel riquadro di destra.  
  
    In alternativa, per personalizzare i mapping dei tipi di dati a livello di database o una tabella, selezionare il database o una tabella nel riquadro di esplorazione di metadati di accesso:  
  
    1.  Nel riquadro di esplorazione di metadati di accesso, espandere **accesso metabase**, quindi espandere **database**.  
  
    2.  Selezionare il database o una tabella per cui si desidera personalizzare il mapping dei tipi di dati.  
  
    3.  Nel riquadro di destra, fare clic su **Mapping dei tipi**.  
  
2.  Per aggiungere un nuovo mapping, procedere come segue:  
  
    1.  Nel riquadro di mapping tra i tipi, fare clic su **Add**.  
  
    2.  Nel **nuovi mapping tra i tipi** nella finestra di dialogo **tipo di origine**, selezionare il tipo di dati di accesso per eseguire il mapping.  
  
    3.  Se il tipo richiede una lunghezza, specificare le lunghezze minima e massima dei dati per il mapping, selezionare la **dal** e **a** caselle di controllo e quindi immettere i valori.  
  
        Ciò consente di personalizzare il mapping dei dati per i valori più piccoli e più grandi dello stesso tipo di dati.  
  
    4.  Sotto **tipo di destinazione**, selezionare la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati.  
  
        Alcuni tipi richiedono una lunghezza del tipo dati di destinazione. Se necessario, immettere la nuova lunghezza dei dati nel **Sostituisci con** e quindi scegliere **OK**.  
  
3.  Per modificare un mapping dei tipi di dati, eseguire le operazioni seguenti:  
  
    1.  Nel riquadro di mapping tra i tipi, fare clic su **modifica**.  
  
    2.  Nel **elenco di Mapping di tipo** nella finestra di dialogo **tipo di origine**, selezionare il tipo di dati di accesso per eseguire il mapping.  
  
    3.  Se il tipo richiede una lunghezza, specificare le lunghezze minima e massima dei dati per il mapping, selezionare la **dal** e **a** caselle di controllo e quindi immettere i valori.  
  
        Ciò consente di personalizzare il mapping dei dati per i valori più piccoli e più grandi dello stesso tipo di dati.  
  
    4.  Sotto **tipo di destinazione**, selezionare la destinazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo di dati.  
  
        Alcuni tipi richiedono una lunghezza del tipo dati di destinazione. Se necessario, immettere la nuova lunghezza dei dati nel **Sostituisci con** e quindi scegliere **OK**.  
  
4.  Per rimuovere un mapping dei tipi di dati, eseguire le operazioni seguenti:  
  
    1.  Nel riquadro di Mapping dei tipi, selezionare la riga nell'elenco di mapping di tipo che contiene il mapping dei tipi di dati che si desidera rimuovere.  
  
    2.  Scegliere **Rimuovi**.  
  
## <a name="next-steps"></a>Passaggi successivi  
Il passaggio successivo del processo di migrazione consiste [convertire gli oggetti di database di access in oggetti di SQL Server](converting-access-database-objects-accesstosql.md)  
  
## <a name="see-also"></a>Vedere anche  
[Migrazione dei database di Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
