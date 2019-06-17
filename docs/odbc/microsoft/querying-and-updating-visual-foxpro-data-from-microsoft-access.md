---
title: L'esecuzione di query e aggiornamento dei dati Visual FoxPro da Microsoft Access | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- querying Visual FoxPro data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], querying and updating
- updating Visual FoxPro data [ODBC]
ms.assetid: 2d314e78-9edf-44b2-bd8b-96784236bcbe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1097e03c414d919a606ffd21ae50ffddf51173b7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316754"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>Esecuzione di query e aggiornamento dei dati Visual FoxPro da Microsoft Access
È possibile eseguire una query e aggiornare i dati archiviati in un database di Visual FoxPro da un database Microsoft Access usando l'opzione di tabella dei collegamenti.  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>Per collegare un database di Visual FoxPro a un database Microsoft Access  
  
1.  Aprire un database Microsoft Access.  
  
2.  Dalla scheda tabelle, fare clic su nuovo.  
  
3.  Nella finestra di dialogo nuova tabella, selezionare la tabella di collegamento e fare clic su OK.  
  
4.  Nella finestra di dialogo di collegamento, selezionare il Database ODBC nei file dell'elenco dei tipi.  
  
5.  Nella finestra di dialogo origini dei dati SQL, selezionare l'origine dati che si connette ai dati Visual FoxPro che si desidera eseguire una query e fare clic su OK.  
  
6.  Nella finestra di dialogo tabelle di collegamento, selezionare le tabelle a cui che si desidera eseguire una query e aggiornare e fare clic su OK. Le tabelle di Visual FoxPro collegate vengono visualizzate nella scheda delle tabelle del database Microsoft Access.  
  
 È ora possibile usare Microsoft Access per eseguire query e aggiornare i dati nelle tabelle di Visual FoxPro collegate. Le modifiche apportate ai dati collegati vengono inviate nuovamente all'origine dati Visual FoxPro.  
  
 Se non si desidera le modifiche apportate in Microsoft Access influisce sui dati nell'origine dati Visual FoxPro, vedere [importazione di dati Visual FoxPro in Microsoft Access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md).
