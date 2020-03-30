---
title: Eseguire una query parziale
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
ms.assetid: af04ab37-6cbb-4185-9382-e5922fa5b1df
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: “”
ms.custom: seo-lt-2019
ms.date: 02/09/2017
ms.openlocfilehash: 5786127626a655e47e2f6eb4ba96f0a16b740258
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75241423"
---
# <a name="how-to-execute-a-partial-query"></a>Procedura: Esecuzione di una query parziale

L'Editor Transact\-SQL consente di evidenziare un segmento specifico dello script ed eseguirlo come una singola query. In questo modo è più semplice eseguire il debug di sezioni di query complesse.  
  
> [!WARNING]  
> Nella procedura seguente vengono usate entità create nelle procedure precedenti nelle sezioni [Sviluppo del database connesso](../ssdt/connected-database-development.md) e [Sviluppo di database offline orientato ai progetti](../ssdt/project-oriented-offline-database-development.md).  
  
## <a name="to-partially-execute-a-query"></a>Per eseguire parzialmente una query  
  
1. In **Esplora oggetti di SQL Server** fare doppio clic su **PerishableFruits** in **Viste** per aprirlo nell'Editor Transact\-SQL.  
  
2. Evidenziare il segmento `SELECT p.Id, p.Name FROM dbo.Product p` nel codice, fare clic con il pulsante destro del mouse e scegliere **Esegui query**.  
  
3. Si noti che tutte le righe con i campi specificati nella tabella `Products` vengono restituite nel riquadro dei**risultati**.