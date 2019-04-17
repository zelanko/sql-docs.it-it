---
title: Scaricare e installare sqlpackage | Microsoft Docs
description: Scaricare e installare sqlpackage per Windows, macOS o Linux
ms.custom: tools|sos
ms.date: 06/20/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.prod_service: sql-tools
ms.topic: conceptual
author: pensivebrian
ms.author: broneill
manager: craigg
ms.openlocfilehash: 7b909df2e97149019d70af49085cc5f1e212f5ee
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2019
ms.locfileid: "59240409"
---
# <a name="download-and-install-sqlpackage"></a>Scaricare e installare sqlpackage

sqlpackage viene eseguito in Windows, macOS e Linux.

Scaricare e installare la versione più recente per .NET Framework e le anteprime per macOS e Linux:

|Piattaforma|Scarica|Data di rilascio|Versione|Compilazione
|:---|:---|:---|:---|:---|
|Windows|[Programma di installazione MSI](https://go.microsoft.com/fwlink/?linkid=2069405)|1 febbraio 2019|18.1|15.0.4316.1|
|macOS .NET Core (anteprima)|[File ZIP](https://go.microsoft.com/fwlink/?linkid=2069126)|1 febbraio 2019 | 18.1 |15.0.4316.1|
|Linux .NET Core (anteprima)|[File ZIP](https://go.microsoft.com/fwlink/?linkid=2069122)|1 febbraio 2019 | 18.1 |15.0.4316.1|

Per informazioni dettagliate sulla versione più recente, vedere le [note sulla versione](release-notes-sqlpackage.md).

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="get-sqlpackage-for-windows"></a>Ottenere sqlpackage per Windows

Questa versione di sqlpackage include un'esperienza di installazione Windows standard e un file ZIP: 

1. Scaricare ed eseguire il [programma di installazione DacFramework.msi per Windows](https://go.microsoft.com/fwlink/?linkid=2069405).
2. Aprire una nuova finestra del prompt dei comandi ed eseguire sqlpackage.exe
    - sqlpackage viene installato nella cartella ```C:\Program Files\Microsoft SQL Server\150\DAC\bin```
    - Installando la versione x86 in un computer x64, sqlpackage viene installato nella cartella ```C:\Program Files (x86)\Microsoft SQL Server\150\DAC\bin```

## <a name="get-sqlpackage-preview-for-macos"></a>Ottenere sqlpackage (anteprima) per macOS

1. Scaricare [sqlpackage per macOS](https://go.microsoft.com/fwlink/?linkid=2069126).
2. Per estrarre il file e avviare sqlpackage, aprire una nuova finestra del terminale e digitare i comandi seguenti:

   **Installazione file con estensione zip:**

   ```bash
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-osx-<version string>.zip ~/sqlpackage 
   echo 'export PATH="$PATH:~/sqlpackage"' >> ~/.bash_profile
   source ~/.bash_profile
   sqlpackage
   ```

## <a name="get-sqlpackage-preview-for-linux"></a>Ottenere sqlpackage (anteprima) per Linux

1. Scaricare [sqlpackage per Linux](https://go.microsoft.com/fwlink/?linkid=2069122) usando uno dei programmi di installazione o l'archivio tar.gz:
2. Per estrarre il file e avviare sqlpackage, aprire una nuova finestra del terminale e digitare i comandi seguenti:

   **Installazione file con estensione zip:**

   ```bash
   cd ~
   mkdir sqlpackage
   unzip ~/Downloads/sqlpackage-linux-<version string>.zip -d ~/sqlpackage 
   echo "export PATH=\"\$PATH:$HOME/sqlpackage\"" >> ~/.bashrc
   chmod a+x ~/sqlpackage/sqlpackage
   source ~/.bashrc
   sqlpackage
   ```

   > [!NOTE]
   > In Debian, Red Hat e Ubuntu potrebbero mancare alcune dipendenze. Usare i comandi seguenti per installare queste dipendenze a seconda della versione di Linux:

   **Debian:**

   ```bash
   sudo apt-get install libunwind8
   ```

   **Redhat:**

   ```bash
   yum install libunwind
   yum install libicu
   ```

   **Ubuntu:**

   ```bash
   sudo apt-get install libunwind8

   # install the libicu library based on the Ubuntu version
   sudo apt-get install libicu52      # for 14.x
   sudo apt-get install libicu55      # for 16.x
   sudo apt-get install libicu57      # for 17.x
   sudo apt-get install libicu60      # for 18.x
   ```

## <a name="uninstall-sqlpackage-preview"></a>Disinstallare sqlpackage (anteprima)

Se sqlpackage è stato installato usando il programma di installazione di Windows, disinstallarlo così come si rimuove qualsiasi applicazione Windows.

Se sqlpackage è stato installato con un file ZIP o un altro archivio, è sufficiente eliminare i file.

## <a name="supported-operating-systems"></a>Sistemi operativi supportati

sqlpackage viene eseguito in Windows, macOS e Linux ed è supportato nelle piattaforme seguenti:

### <a name="windows"></a>Windows

- Windows 10
- Windows 8.1
- Windows 8
- Windows 7 SP1
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2

### <a name="macos"></a>macOS

- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux-x64"></a>Linux (x64)

- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="next-steps"></a>Next Steps

- Altre informazioni su [sqlpackage](sqlpackage.md)

[Informativa sulla privacy di Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839)
