---
title: Esecuzione di query e aggiornamento dei dati di Visual FoxPro da Microsoft Access Documenti Microsoft
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
ms.openlocfilehash: f11b49ed099ba29d0e7e013af99a8ad96ca6825c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292871"
---
# <a name="querying-and-updating-visual-foxpro-data-from-microsoft-access"></a>Esecuzione di query e aggiornamento dei dati Visual FoxPro da Microsoft Access
È possibile eseguire query e aggiornare i dati archiviati in un database Visual FoxPro da un database di Microsoft Access utilizzando l'opzione Collega tabella.  
  
### <a name="to-link-a-visual-foxpro-database-to-a-microsoft-access-database"></a>Per collegare un database di Visual FoxPro a un database di Microsoft Access  
  
1.  Aprire un database di Microsoft Access.  
  
2.  Nella scheda Tabelle fare clic su Nuovo.  
  
3.  Nella finestra di dialogo Nuova tabella, selezionare Collega tabella e fare clic su OK.  
  
4.  Nella finestra di dialogo Collegamento selezionare Database ODBC nell'elenco Tipo file.  
  
5.  Nella finestra di dialogo Origini dati SQL selezionare l'origine dati che si connette ai dati di Visual FoxPro su cui si desidera eseguire la query e fare clic su OK.  
  
6.  Nella finestra di dialogo Collega tabelle, selezionare le tabelle su cui si desidera eseguire la query e aggiornare e fare clic su OK. Le tabelle Visual FoxPro collegate vengono visualizzate nella scheda Tabelle del database di Microsoft Access.  
  
 È ora possibile utilizzare Microsoft Access per eseguire query e aggiornare i dati nelle tabelle Visual FoxPro collegate. Le modifiche apportate ai dati collegati vengono inviate all'origine dati Visual FoxPro.  
  
 Se non si desidera che le modifiche apportate in Microsoft Access influiscano sui dati nell'origine dati Visual FoxPro, vedere [Importazione di dati di Visual FoxPro in Microsoft Access](../../odbc/microsoft/importing-visual-foxpro-data-into-microsoft-access.md).
