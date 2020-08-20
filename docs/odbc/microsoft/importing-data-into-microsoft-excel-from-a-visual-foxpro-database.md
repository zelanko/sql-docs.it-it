---
description: Importazione di dati in Microsoft Excel da un database Visual FoxPro
title: Importazione di dati in Microsoft Excel da un database Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a4bd1cf7983ed0a552de4f9d0f491960b48f0d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500294"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Importazione di dati in Microsoft Excel da un database Visual FoxPro
È possibile importare dati Visual FoxPro nel foglio di lavoro di Microsoft Excel se è stata definita un'origine dati. Per informazioni sulla creazione di un'origine dati Visual FoxPro, vedere [accesso a un'origine dati Visual FoxPro da Microsoft Excel](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md).  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Per importare dati Visual FoxPro in un foglio di lavoro di Microsoft Excel  
  
1.  Aprire un foglio di calcolo di Microsoft Excel.  
  
2.  Scegliere Ottieni dati esterni dal menu dati. Viene aperta la query Microsoft.  
  
3.  Nella finestra di dialogo Seleziona origine dati selezionare un'origine dati Visual FoxPro, quindi fare clic su USA.  
  
4.  Se il database a cui si accede dall'origine dati include tabelle, selezionare una tabella nella finestra di dialogo Aggiungi tabelle. Microsoft query consente di visualizzare la tabella aggiunta nella parte superiore della finestra Progettazione query.  
  
    > [!NOTE]  
    >  L'elenco dei proprietari non è disponibile in questa finestra di dialogo perché il driver non supporta i proprietari. L'elenco di database non è disponibile perché il driver non supporta più database in un'origine dati.  
  
5.  Selezionare i campi per la query trascinandoli dalla tabella sulla metà inferiore della finestra di progettazione.  
  
6.  Chiudere la query Microsoft. I dati selezionati vengono importati nel foglio di calcolo di Microsoft Excel.
