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
ms.openlocfilehash: 2681ecd0fe6f586954236c4fb5fddcf576b206be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67988062"
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
