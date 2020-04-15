---
title: Patch del software Oracle Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], Oraclesoftware patches
- Oracle software patches [ODBC]
ms.assetid: 1275157b-f4e1-4c24-b273-c02555e261c2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b1fb577e7b08f6ef332ed35f6d275a5f7ce543ba
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292951"
---
# <a name="oracle-software-patches"></a>Patch del software Oracle
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Le patch per i prodotti server Oracle e il relativo componente client sono necessarie per il corretto funzionamento di diversi prodotti e tecnologie Microsoft, tra cui Microsoft ODBC Driver for Oracle, Microsoft OLE DB Provider for Oracle, Internet Information Services (IIS), Component Services (o Microsoft Transaction Server, se si utilizza Windows NT) e così via.  
  
> [!NOTE]  
>  Le seguenti istruzioni potrebbero non essere completamente accurate perché il sito FTP Oracle è soggetto a modifiche.  
  
### <a name="to-download-the-oracle-software-patches"></a>Per scaricare le patch del software Oracle  
  
1.  Connettersi al sito FTP pubblico alloracle-ftp.oracle.com. L'ID utente è "anonimo" e la password è il tuo indirizzo e-mail.  
  
2.  Passare alla directory seguente: /server/wgt_tech/server/windowsNT.  
  
3.  Per scaricare le patch più rilevanti per Windows 95, Windows 98 e Windows NT/Windows 2000, passare alla sottodirectory della versione di Oracle in uso - 7.3 o 8.0. Le due sottodirectory sono /73patchsets e /80patchsets.  
  
4.  Per scaricare le patch per la tecnologia di rete di Oracle, SQL-Net o Net8, passare alla directory seguente: /network.  
  
 L'accesso a questo sito FTP dal browser Web potrebbe non funzionare. Se si verificano problemi, provare a utilizzare un client FTP "tradizionale" o utilizzare il prompt dei comandi DOS.  
  
> [!NOTE]  
>  Poiché Oracle corregge i bug nelle versioni correnti e quindi li adatta alle versioni precedenti utilizzando patch software, si consiglia di scaricare la patch più recente disponibile. Ciò è particolarmente vero per i componenti di Oracle Server Client. In caso di domande sull'installazione di queste patch, contattare il supporto Oracle.
