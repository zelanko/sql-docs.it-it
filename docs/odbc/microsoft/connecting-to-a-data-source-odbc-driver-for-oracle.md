---
title: Connessione a un'origine dati (driver ODBC per Oracle) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6ef567c9e3c7b63e7f5044de699750de856f3e52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281301"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>Connessione a un'origine dati (driver ODBC per Oracle)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Un'applicazione ODBC può passare le informazioni di connessione in diversi modi. Ad esempio, l'applicazione potrebbe richiedere sempre all'utente le informazioni di connessione. In alternativa, l'applicazione potrebbe prevedere una stringa di connessione che specifica la connessione all'origine dati. La modalità di connessione a un'origine dati dipende dal metodo di connessione utilizzato dall'applicazione ODBC.  
  
 Un modo comune per connettersi a un'origine dati è tramite la finestra di dialogo Origine dati. Se l'applicazione ODBC è impostata per l'utilizzo di una finestra di dialogo, tale finestra di dialogo viene visualizzata e richiede le informazioni di connessione all'origine dati appropriate.  
  
 È inoltre possibile connettersi a un'origine dati utilizzando la stringa di [connessione](../../odbc/microsoft/connection-string-format-and-attributes.md).  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>Per connettersi a un'origine dati tramite una finestra di dialogoTo connect to a data source using a dialog box  
  
1.  Quando viene visualizzata la finestra di dialogo Origine dati, selezionare un'origine dati Oracle e quindi fare clic su OK. Viene visualizzata la finestra di dialogo Connetti.  
  
2.  Immettere le informazioni appropriate per la finestra di dialogo Connetti e quindi fare clic su OK.  
  
 Dopo la verifica delle informazioni di connessione, l'applicazione può utilizzare il driver ODBC per Oracle per accedere alle informazioni contenute nell'origine dati.
