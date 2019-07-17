---
title: Importazione di dati Visual FoxPro in Microsoft Access | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], Access
- Visual FoxPro ODBC driver [ODBC], Access
- Visual FoxPro data [ODBC], importing
ms.assetid: a3591295-0a76-4e3c-b4fa-8bd4f1cde705
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 557b5505b9eb6a15080a7d0495df2e63aefd2d76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085539"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Importazione di dati Visual FoxPro in Microsoft Access
È possibile importare i dati archiviati in un database di Visual FoxPro in un database Microsoft Access utilizzando l'opzione di importazione.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Per importare dati Visual FoxPro in un database Microsoft Access  
  
1.  Aprire un database Microsoft Access.  
  
2.  Dal menu File, scegliere che quindi importare dati esterni.  
  
3.  Nella finestra di dialogo di importazione, selezionare i database ODBC nei file dell'elenco dei tipi.  
  
4.  Nella finestra di dialogo origini dei dati SQL, selezionare l'origine dati Visual FoxPro che si connette ai dati di FoxPro che si desidera eseguire una query e fare clic su OK.  
  
5.  Nella finestra di dialogo Importa oggetti, selezionare uno o più tabelle che si desidera importare e fare clic su OK. I nomi delle tabelle di Visual FoxPro importati vengono visualizzati nella scheda delle tabelle del database Microsoft Access.  
  
 È ora possibile usare Microsoft Access per manipolare i dati nelle tabelle di Visual FoxPro importati. I dati che si importano sono uno snapshot dei dati archiviati in Visual FoxPro; le modifiche apportate ai dati importati non vengono inviate nuovamente all'origine dati Visual FoxPro.  
  
 Se si desidera che le modifiche apportate in Microsoft Access per modificare i dati nell'origine dati Visual FoxPro, vedere [esecuzione di query e aggiornamento dei dati Visual FoxPro da Microsoft Access](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md).
