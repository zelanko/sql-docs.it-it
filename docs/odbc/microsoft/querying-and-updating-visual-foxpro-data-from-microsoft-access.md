---
description: Esecuzione di query e aggiornamento dei dati Visual FoxPro da Microsoft Access
title: Esecuzione di query e aggiornamento dei dati Visual FoxPro da Microsoft Access | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 82232cfa3c0bb32ccd87231f139e9aecf8342450
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340427"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>Esecuzione di query e aggiornamento dei dati Visual FoxPro da Microsoft Access
È possibile eseguire una query e aggiornare i dati archiviati in un database Visual FoxPro da un database di Microsoft Access utilizzando l'opzione della tabella di collegamento.  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>Per collegare un database Visual FoxPro a un database di Microsoft Access  
  
1.  Aprire un database di Microsoft Access.  
  
2.  Nella scheda tabelle fare clic su nuovo.  
  
3.  Nella finestra di dialogo nuova tabella selezionare collega tabella, quindi fare clic su OK.  
  
4.  Nella finestra di dialogo collegamento selezionare database ODBC nell'elenco tipo file.  
  
5.  Nella finestra di dialogo origini dati SQL selezionare l'origine dati che si connette ai dati Visual FoxPro su cui si desidera eseguire la query e fare clic su OK.  
  
6.  Nella finestra di dialogo tabelle di collegamento selezionare le tabelle su cui si desidera eseguire la query e aggiornare e fare clic su OK. Le tabelle collegate di Visual FoxPro vengono visualizzate nella scheda tabelle del database di Microsoft Access.  
  
 È ora possibile usare Microsoft Access per eseguire query e aggiornare i dati nelle tabelle collegate di Visual FoxPro. Le modifiche apportate ai dati collegati vengono restituite all'origine dati Visual FoxPro.  
  
 Se non si desidera che le modifiche apportate in Microsoft Access influiscano sui dati nell'origine dati Visual FoxPro, vedere [importazione di dati Visual FoxPro in Microsoft Access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md).
