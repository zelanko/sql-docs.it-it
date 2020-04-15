---
title: Importazione di dati di Visual FoxPro in Microsoft Access Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 90ac16bbdbaf7f4dd29e14e66cf5b9dc666057f4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302450"
---
# <a name="importing-visual-foxpro-data-into-microsoft-access"></a>Importazione di dati Visual FoxPro in Microsoft Access
È possibile importare i dati memorizzati in un database Visual FoxPro in un database di Microsoft Access utilizzando l'opzione Importa.  
  
### <a name="to-import-visual-foxpro-data-into-a-microsoft-access-database"></a>Per importare dati di Visual FoxPro in un database di Microsoft Access  
  
1.  Aprire un database di Microsoft Access.  
  
2.  Scegliere Carica dati esterni dal menu File, quindi Importa.  
  
3.  Nella finestra di dialogo Importa selezionare Database ODBC nell'elenco Tipo file.  
  
4.  Nella finestra di dialogo Origini dati SQL selezionare l'origine dati Visual FoxPro che si connette ai dati FoxPro su cui si desidera eseguire una query e fare clic su OK.  
  
5.  Nella finestra di dialogo Importa oggetti, selezionare una o più tabelle da importare e fare clic su OK. I nomi delle tabelle di Visual FoxPro importate vengono visualizzati nella scheda Tabelle del database di Microsoft Access.  
  
 È ora possibile utilizzare Microsoft Access per modificare i dati nelle tabelle di Visual FoxPro importate. I dati importati sono un'istantanea dei dati archiviati in Visual FoxPro; le modifiche apportate ai dati importati non vengono inviate all'origine dati Visual FoxPro.  
  
 Se si desidera apportare modifiche in Microsoft Access per modificare i dati nell'origine dati Visual FoxPro, vedere Esecuzione di query e aggiornamento dei dati di [Visual FoxPro da Microsoft Access](../../odbc/microsoft/querying-and-updating-visual-foxpro-data-from-microsoft-access.md).
