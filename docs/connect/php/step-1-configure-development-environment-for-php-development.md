---
title: "Passaggio 1: Configurare l'ambiente per PHP"
description: Il passaggio 1 di questa guida introduttiva prevede l'installazione di PHP, Microsoft ODBC Driver for SQL Server e la configurazione dell'ambiente di sviluppo.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 0bce6022-00bd-45c6-9671-eaa9dfa395a8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 88eb2c2c67eac3ecd9fba2c79c143de28cf60d22
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2020
ms.locfileid: "81633172"
---
# <a name="step-1-configure-environment-for-php-development"></a>Passaggio 1: Configurare l'ambiente per lo sviluppo di PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]




* Identificare la versione del driver PHP da usare, a seconda dell'ambiente, come indicato di seguito:  [Requisiti di sistema dei driver Microsoft per PHP per SQL Server](system-requirements-for-the-php-sql-driver.md)
* Scaricare e installare il driver PHP applicabile qui: [Scaricare il driver Microsoft per PHP](https://www.microsoft.com/download/details.aspx?id=20098)  
* Scaricare e installare il driver ODBC applicabile qui:  [Microsoft ODBC Driver per SQL Server](../odbc/download-odbc-driver-for-sql-server.md)  
* Configurare il driver PHP e il server Web per il sistema operativo specifico:

### <a name="windows"></a>Windows  
  

* Configurare il caricamento del driver PHP, come indicato di seguito: [Caricamento dei Driver Microsoft per PHP per SQL Server](../../connect/php/loading-the-php-sql-driver.md) 
* Configurare IIS per l'hosting di applicazioni PHP, come indicato di seguito: [Configurazione di IIS per i driver Microsoft per PHP per SQL Server](../../connect/php/configuring-iis-for-php-sql-driver.md)

### <a name="linux-and-macos"></a>Linux e macOS


*   Configurare il caricamento del driver PHP e configurare il server Web per l'hosting di applicazioni PHP, come indicato di seguito: [Esercitazione sull'installazione dei driver PHP in Linux e macOS](../../connect/php/installation-tutorial-linux-mac.md)
