---
title: Installing the Driver Manager (Driver ODBC per SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Driver Manager, installing
ms.assetid: 7c4b6fb4-f45a-4973-adb9-a4d83f0a2a7a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 78eaf77064fb96c024c548c320ca9feeec10ce02
ms.sourcegitcommit: 7d4a3fc0f2622cbc6930d792be4a9b3fcac4c4b6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 03/21/2019
ms.locfileid: "58305809"
---
# <a name="installing-the-driver-manager"></a>Installazione di Gestione driver
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Questo articolo contiene istruzioni per installare Gestione Driver unixODBC per l'uso con tutte le versioni del Driver ODBC di Microsoft per SQL Server in Linux e macOS.  

> [!IMPORTANT]  
> Eliminare tutti i pacchetti di gestione dei driver installati nel computer prima di installare Gestione driver unixODBC. L'installazione di Gestione driver unixODBC potrebbe interrompere l'esecuzione di un programma di gestione dei driver esistente.  

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-13-131-and-17"></a>Installazione di Gestione driver per Microsoft ODBC Driver 13, 13.1 e 17
La dipendenza di Gestione driver viene risolta automaticamente dal sistema di gestione pacchetti quando si installa Microsoft ODBC Driver 17 for SQL Server in Linux o macOS, 13.1 o 13 seguendo le istruzioni riportate in [installazione di Microsoft ODBC Driver per SQL Server in Linux o macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md). 

## <a name="installing-the-driver-manager-for-microsoft-odbc-driver-11-for-sql-server"></a>Installazione di Gestione driver per Microsoft ODBC Driver 11 for SQL Server  

(SUSE e Red Hat Linux solo).

**Uso dello script di installazione**  
  
> [!IMPORTANT]  
> Queste istruzioni fanno riferimento a `msodbcsql-11.0.2270.0.tar.gz`, il file di installazione per Red Hat Linux. Se si sta installando l'anteprima per SUSE Linux, il nome del file è `msodbcsql-11.0.2260.0.tar.gz`.  

Per installare Gestione driver:  
  
1.  Assicurarsi di disporre dell'autorizzazione di radice.  
  
2.  Passare alla directory in cui il download del driver ODBC di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ha inserito il file denominato `msodbcsql-11.0.2270.0.tar.gz`. Verificare di avere il file \*.tar.gz corrispondente alla versione di Linux in uso. Per estrarre i file, eseguire il comando seguente: **tar xvzf msodbcsql-11.0.2270.0.tar.gz**.  

3.  Passare alla directory `msodbcsql-11.0.2270.0` contenente un file denominato `build_dm.sh`. È possibile eseguire `build_dm.sh` per installare Gestione Driver unixODBC.

4.  Per visualizzare un elenco delle opzioni disponibili, eseguire il comando seguente: **./build_dm.sh --help**.  
  
5.  Quando si è pronti per l'installazione e il computer può accedere a un sito esterno tramite FTP, eseguire il comando seguente: **./build_dm.sh**.

Se il computer non può accedere a un sito esterno tramite FTP, scaricare `unixODBC-2.3.0.tar.gz`. È possibile ottenere `unixODBC-2.3.0.tar.gz` dal [ http://www.unixodbc.org ](http://www.unixodbc.org/). Fare clic sul collegamento **Download** a sinistra nella pagina per passare alla pagina di download. Fare clic sul collegamento appropriato per scaricare unixODBC-2.3.0 (non unixODBC-2.3.1). unixODBC-2.3.1 non è supportato con questa versione di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Eseguire il comando seguente per iniziare l'installazione di gestione Driver unixODBC: **./build_dm.sh --download-url=file://unixODBC-2.3.0.tar.gz**.  

6.  Digitare **SÌ** per procedere all'estrazione dei file. Questa fase del processo può richiedere fino a cinque minuti.  

7.  Al termine dell'esecuzione dello script, seguire le istruzioni visualizzate per installare Gestione driver unixODBC.

A questo punto si è pronti per l'installazione del driver. Per altre informazioni, vedere [installazione di Microsoft ODBC Driver for SQL Server in Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).  

**Installazione manuale**

Se l'esecuzione dello script di installazione non viene completata, configurare e creare il programma di gestione dei driver manualmente.

1.  Rimuovere qualsiasi versione precedente di unixODBC, ad esempio unixODBC 2.2.11. In Red Hat Enterprise Linux 5 o 6, eseguire il comando seguente: **yum remove unixODBC**. In SUSE Linux Enterprise, **zypper rimuovere unixODBC**.  
  
2.  Passare a [http://www.unixodbc.org](http://www.unixodbc.org/). Fare clic sul collegamento **Download** a sinistra nella pagina per passare alla pagina di download. Fare clic sul collegamento appropriato per salvare il file unixODBC-2.3.0.tar.gz nel computer. UnixODBC-2.3.1 non è supportato con questa versione di [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
3.  Nel computer Linux, eseguire il comando: **tar xvzf unixODBC-2.3.0.tar.gz**.  
  
4.  Passare alla directory unixODBC-2.3.0.  
  
5.  Un prompt dei comandi, eseguire il comando: **CPPFLAGS = "-DSIZEOF_LONG_INT = 8"**.  
  
6.  Un prompt dei comandi, eseguire il comando: **export CPPFLAGS**.  
  
7.  Un prompt dei comandi, eseguire il comando: **"./configure --prefix=/usr --libdir=/usr/lib64 --sysconfdir=/etc --enable-gui=no --enable-drivers=no --enable-iconv --with-iconv-char-enc=UTF8 --with-iconv-ucode-enc=UTF16LE"**.  
  
8.  Al prompt dei comandi (connesso come radice), eseguire il comando: **make**.  
  
9. Al prompt dei comandi (connesso come radice), eseguire il comando: **make install**.  

A questo punto si è pronti per l'installazione del driver. Per altre informazioni, vedere [installazione di Microsoft ODBC Driver for SQL Server in Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche
[Installazione di Microsoft ODBC Driver for SQL Server in Linux e macOS](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

[Problemi noti in questa versione del driver](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Note sulla versione](../../../connect/odbc/linux-mac/release-notes.md)
