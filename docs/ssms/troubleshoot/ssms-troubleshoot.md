---
title: Risoluzione dei problemi relativi a un blocco o un arresto anomalo con SQL Server Management Studio (SSMS)
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: dnethi
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
manager: jroth
ms.custom: ''
ms.date: 07/01/2019
ms.openlocfilehash: 424b0863da9d0d2cfb56676bed5c368efc4d9349
ms.sourcegitcommit: 0b0f5aba602732834c8439c192d95921149ab4c3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2019
ms.locfileid: "67501188"
---
# <a name="get-diagnostic-data-after-a-sql-server-management-studio-ssms-crash"></a>Ottenere dati di diagnostica dopo un arresto anomalo di SQL Server Management Studio (SSMS)

[!INCLUDE[Si applica a](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)

## <a name="get-full-memory-dump-of-sql-server-management-studio-ssms-when-it-hangs-or-crashes"></a>Ottenere il dump della memoria completo di SQL Server Management Studio (SSMS) in seguito a un blocco o un arresto anomalo

Per acquisire le informazioni di diagnostica per risolvere i problemi di un arresto anomalo o un blocco di SSMS, seguire questa procedura.

1. Scaricare [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Decomprimere il download in una cartella.

3. Aprire il prompt dei comandi ed eseguire il comando seguente.

    ```prompt dei comandi  <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    If it prompts you to accept a license agreement, select *Agree*.

4. Start SSMS, if it hasn't started already.

5. Reproduce the issue.

6. The text should appear in the cmd prompt about writing the dump file, wait for that to finish.

7. Create a new folder and copy the *.dmp file that is written out to that folder.

8. Copy the following files into the same folder.

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Zip up the folder

## Get full memory dump of SSMS when it throws an OutOfMemoryException

You can get a full memory dump with any managed exception.

To capture diagnostic information to troubleshoot an OutOfMemoryException from SSMS, follow the steps below.

1. Download [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Unzip the download into a folder.

3. Open Command Prompt and run the following command.

    ```command prompt
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    Se viene richiesto di accettare un contratto di licenza, selezionare *Accetto*.

4. Avviare SQL Server Management Studio, se non è ancora stato avviato.

5. Riprodurre il problema.

6. Il testo verrà visualizzato nel prompt dei comandi relativo alla scrittura del file di dump. Attendere il completamento dell'operazione.

7. Creare una nuova cartella e copiare il file *.dmp di cui è stata eseguita la scrittura in tale cartella.

8. Copiare i file seguenti nella stessa cartella.

    "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"  "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Comprimere la cartella.