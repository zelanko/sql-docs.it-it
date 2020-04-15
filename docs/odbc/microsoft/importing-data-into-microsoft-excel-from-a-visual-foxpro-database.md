---
title: Importazione di dati in Microsoft Excel da un database di Visual FoxPro Documenti Microsoft
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
ms.openlocfilehash: 1bfd86233e5a0a406febcb30bf7a4fae595e53d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287671"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Importazione di dati in Microsoft Excel da un database Visual FoxPro
È possibile importare dati di Visual FoxPro nel foglio di lavoro di Microsoft Excel se è stata definita un'origine dati per tali dati. Per informazioni sulla creazione di un'origine dati Visual FoxPro, vedere [Accesso a un'origine dati Visual FoxPro da Microsoft Excel](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md).  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Per importare dati di Visual FoxPro in un foglio di lavoro di Microsoft Excel  
  
1.  Aprire un foglio di calcolo di Microsoft Excel.  
  
2.  Scegliere Carica dati esterni dal menu Dati. Verrà aperto Microsoft Query.  
  
3.  Nella finestra di dialogo Seleziona origine dati selezionare un'origine dati Visual FoxPro e quindi fare clic su Usa.In the Select Data Source dialog box, select a Visual FoxPro data source and then click Use.  
  
4.  Se il database a cui si accede dall'origine dati include tabelle, selezionare una tabella nella finestra di dialogo Aggiungi tabelle. Microsoft Query visualizza la tabella aggiunta nella metà superiore di Progettazione query.  
  
    > [!NOTE]  
    >  L'elenco Proprietario non è disponibile in questa finestra di dialogo perché il driver non supporta i proprietari. L'elenco Database non è disponibile perché il driver non supporta più database in un'origine dati.  
  
5.  Selezionare i campi per la query trascinandoli dalla tabella nella metà inferiore della finestra di progettazione.  
  
6.  Chiudere Microsoft Query. I dati selezionati vengono importati nel foglio di calcolo di Microsoft Excel.
