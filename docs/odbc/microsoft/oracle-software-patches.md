---
title: Patch software Oracle | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292951"
---
# <a name="oracle-software-patches"></a>Patch del software Oracle
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Per il corretto funzionamento di diversi prodotti e tecnologie Microsoft, tra cui Microsoft ODBC driver for Oracle, provider Microsoft OLE DB per Oracle, Internet Information Services (IIS), Servizi componenti (o Microsoft Transaction Server, se si utilizza Windows NT) e così via, sono necessarie patch per i prodotti server Oracle e per il relativo componente client.  
  
> [!NOTE]  
>  Le istruzioni seguenti potrebbero non essere completamente accurate perché il sito FTP Oracle è soggetto a modifiche.  
  
### <a name="to-download-the-oracle-software-patches"></a>Per scaricare le patch del software Oracle  
  
1.  Connettersi al sito FTP pubblico in oracle-ftp.oracle.com. L'ID utente è "anonimo" e la password è l'indirizzo di posta elettronica.  
  
2.  Passare alla directory seguente:/server/wgt_tech/server/windowsNT.  
  
3.  Per scaricare le patch più rilevanti per Windows 95, Windows 98 e Windows NT/Windows 2000, passare alla sottodirectory per la versione di Oracle-7,3 o 8,0. Le due sottodirectory sono/73patchsets e/80patchsets.  
  
4.  Per scaricare le patch per la tecnologia di rete di Oracle, ovvero SQL * NET o Net8, passare alla directory seguente:/Network.  
  
 L'accesso a questo sito FTP dalla Web browser potrebbe non funzionare. Se si verificano problemi, provare a usare un client FTP "tradizionale" o usare il prompt dei comandi DOS.  
  
> [!NOTE]  
>  Poiché Oracle corregge i bug nelle versioni correnti e li aggiorna alle versioni precedenti usando le patch software, è consigliabile scaricare la patch più recente disponibile. Questa operazione è particolarmente valida per i componenti client di Oracle Server. Per domande sull'installazione di queste patch, contattare il supporto tecnico Oracle.
