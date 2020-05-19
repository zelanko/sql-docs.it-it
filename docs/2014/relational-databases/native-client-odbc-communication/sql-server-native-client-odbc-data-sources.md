---
title: SQL Server Native Client origini dati ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, about data sources
- ODBC data sources, names
- data sources [SQL Server Native Client]
- names [ODBC]
- ODBC applications, data sources
- SQL Server Native Client ODBC driver, data sources
- ODBC data sources
ms.assetid: a6a50fd0-d439-43fd-b76f-16ec02f478c5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9b7a5ea06fb2b720e635f5d8310cefa425aa1646
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705693"
---
# <a name="sql-server-native-client-odbc-data-sources"></a>Origini dati ODBC di SQL Server Native Client
  Un nome di origine dati (DSN, Data Source Name) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identifica un'origine dati ODBC che contiene tutte le informazioni necessarie a un'applicazione ODBC per connettersi a un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un server specifico. Per definire un nome di origine dati ODBC, è possibile procedere in due modi diversi:  
  
-   In un computer client, aprire strumenti di amministrazione nel pannello di controllo e fare doppio clic su **origini dati (ODBC)**. Verrà visualizzato Amministratore origine dati ODBC, in cui è possibile creare un nome di origine dati.  
  
-   In un'applicazione ODBC, chiamare [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md).  
  
 Un'origine dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene gli elementi seguenti:  
  
-   Nome dell'origine dati.  
  
-   Tutte le informazioni necessarie per connettersi a un'istanza specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Database predefinito da utilizzare in un'istanza specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (facoltativo).  
  
-   Impostazioni quali le opzioni ANSI da utilizzare, la registrazione o meno delle statistiche sulle prestazioni e così via (facoltativo).  
  
 Un'applicazione ODBC non è necessaria per connettersi tramite un'origine dati. L'applicazione, tuttavia, deve fornire le stesse informazioni sulla connettività a una funzione di connessione ODBC altrimenti individuate dal driver in un nome di origine dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Comunicazione con SQL Server &#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
