---
title: Informazioni parametri (IntelliSense) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Parameter Info option [IntelliSense]
- stored function parameter completion [Intellisense]
- language references [SQL Server]
- IntelliSense [SQL Server], Parameter Info option
ms.assetid: 56c2aac9-c65c-4679-b62c-d9f689876dde
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 015e0708b9e43340918bbf4d6d207c2b12a34c64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65821291"
---
# <a name="parameter-info-intellisense"></a>Informazioni parametri (IntelliSense)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  L'opzione [!INCLUDE[msCoName](../../includes/msconame-md.md)] Informazione sul parametro **di** IntelliSense consente di aprire un elenco di parametri che include informazioni relative a numero, nomi e tipi dei parametri necessari per una funzione o per una stored procedure. Il parametro in grassetto indica il parametro successivo necessario quando viene digitata una funzione o una stored procedure.  
  
 L'elenco dei parametri è visualizzato anche per le funzioni nidificate. Se si digita una funzione come parametro per un'altra funzione, nell'elenco dei parametri verranno visualizzati i parametri per la funzione interna. Quando l'elenco dei parametri della funzione interna è completo, verranno quindi visualizzati i parametri della funzione esterna.  
  
#### <a name="to-view-parameter-info-for-functions-or-stored-procedures"></a>Per visualizzare le informazioni sul parametro per le funzioni o le stored procedure  
  
1.  Dopo il nome di una funzione, digitare una normale parentesi aperta per aprire l'elenco dei parametri. Dopo avere digitato il nome di una stored procedure, digitare un normale spazio per ottenere informazioni sui parametri della procedura.  
  
     In IntelliSense viene visualizzata la dichiarazione completa per la funzione o per i parametri di una stored procedure in una finestra popup subito al di sotto del punto di inserimento. Il primo parametro dell'elenco viene visualizzato in grassetto.  
  
2.  Durante l'immissione dei parametri, il grassetto cambia per indicare il parametro successivo da immettere.  
  
3.  Premere ESC in qualsiasi momento per chiudere l'elenco oppure continuare a digitare fino a completare la funzione.  
  
     Nel caso di una funzione, se viene digitata la parentesi di chiusura viene chiuso anche l'elenco dei parametri.  
  
#### <a name="to-manually-start-parameter-info"></a>Per avviare manualmente l'opzione Informazioni sul parametro  
  
1.  Scegliere **IntelliSense** dal menu **Modifica** , quindi selezionare **Informazioni parametri**.  
  
2.  Utilizzare i tasti di scelta rapida CTRL+MAIUSC+BARRA SPAZIATRICE.  
  
 Per altre informazioni, vedere [Configurare IntelliSense &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/configure-intellisense-sql-server-management-studio.md).  
  
> [!NOTE]  
>  L'opzione **Informazioni parametri** è disponibile solo per l'editor di query di [!INCLUDE[ssDE](../../includes/ssde-md.md)] e per l'editor di query XML.  
  
  
