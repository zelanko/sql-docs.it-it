---
title: Importare dati usando una query nativa (Analysis Services) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 37c313484b2ee7ff87668cbfdd0b87ed52cdaf98
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523967"
---
# <a name="import-data-by-using-a-native-query"></a>Importare dati con una query nativa
[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]
Per i modelli tabulari 1400, la nuova esperienza recupera dati nei progetti di Visual Studio Analysis Services fornisce un'enorme flessibilità come eseguire il mashup dei dati durante l'importazione. Questo articolo descrive la creazione di una connessione a un'origine dati e quindi creando una query SQL nativa per specificare l'importazione dei dati.

Per completare le attività descritte in questo articolo, assicurarsi che si usa la versione più recente di SSDT. Se si usa Visual Studio 2017, assicurarsi che è stata scaricata e installata settembre 2017 o versioni successive Microsoft Analysis Services progetti VSIX.

[Scaricare e installare SSDT](../../ssdt/download-sql-server-data-tools-ssdt.md)

[Download di Microsoft Analysis Services progetti VSIX](https://marketplace.visualstudio.com/items?itemName=ProBITools.MicrosoftAnalysisServicesModelingProjects)

## <a name="create-a-datasource-connection"></a>Creare una connessione origine dati
Se non si ha già una connessione per l'origine dati, è necessario crearne uno.

1. In Visual Studio > **Esplora modelli tabulari**, fare doppio clic su **Zdroje dat**, quindi fare clic su **nuova origine dati**.
2. Nelle **recupera dati**, selezionare il tipo di origine dati e quindi fare clic su **Connect**. Seguire eventuali altri passaggi necessari per connettere l'origine dati.


## <a name="enter-a-query-as-a-named-expression"></a>Immettere una query come un'espressione denominata
1. Nelle **Esplora modelli tabulari**, fare doppio clic su **espressioni** > **modificare espressioni**.
2. Nelle **Editor di Query**, fare clic su **Query** > **nuova Query** > **Query vuota**
3. Nella barra della formula, digitare
    ```
    = Value.NativeQuery(#"DATA SOURCE NAME", "SELECT * FROM ...")
    ```
4. Per creare una tabella, in **query**, fare doppio clic su query e quindi selezionare **creare una nuova tabella**. La nuova tabella avrà lo stesso nome della query.


## <a name="example"></a>Esempio
Questa query nativa crea una tabella Employee nel modello che include tutte le colonne dalla tabella Dimension.Employee nell'origine dati.

```
= Value.NativeQuery(#"SQL/myserver;WideWorldImportersDW", "SELECT * FROM Dimension.Employee")
```
![Editor di query](media/ssas-import-query-example.png)


Dopo l'importazione, viene creata una tabella denominata Employees nel modello.   

![Editor di query](media/ssas-import-query-example-table.png)


## <a name="see-also"></a>Vedere anche  
 [Value.NativeQuery](https://msdn.microsoft.com/library/mt736917.aspx)   
 [Rappresentazione](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   

  
