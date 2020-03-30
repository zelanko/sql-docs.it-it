---
title: Ottenere il dump della memoria completo per risolvere i problemi di SSMS
Description: Risoluzione dei problemi relativi a un blocco o un arresto anomalo del sistema di SSMS tramite la raccolta di un dump completo della memoria
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: markingmyname
ms.author: maghan
ms.reviewer: dineth, sstein
ms.custom: seo-lt-2019
ms.date: 05/17/2019
ms.openlocfilehash: 95e88b8bbf61e04251ce17ad0a4fcd5aff91cc9e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75247167"
---
# <a name="get-full-memory-dump"></a>Ottenere il dump completo della memoria

[!INCLUDE[Applies to](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

Questo articolo descrive come acquisire le informazioni di diagnostica per risolvere i problemi relativi a un arresto anomalo del sistema o a un blocco riscontrato in SQL Server Management Studio (SSMS).

Per acquisire le informazioni di diagnostica per la risoluzione dei problemi, seguire questa procedura.

1. Scaricare [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Decomprimere il download in una cartella.

3. Aprire un prompt dei comandi (come `cmd.exe`) ed eseguire il comando seguente.

    ```
    <PathToProcDumpFolder>\procdump.exe -e -h -ma -w ssms.exe
    ```

    Se viene richiesto di accettare un contratto di licenza, selezionare **Accetto**.

4. Avviare SQL Server Management Studio (SSMS), se non è ancora stato avviato.

5. Riprodurre il problema.

6. Il testo verrà visualizzato nel prompt dei comandi relativo alla scrittura del file di dump. Attendere il completamento dell'operazione.

7. Creare una nuova cartella e copiare il file *.dmp di cui è stata eseguita la scrittura in tale cartella.

8. Copiare i file seguenti nella stessa cartella.

    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Comprimere la cartella.

## <a name="outofmemoryexception"></a>OutOfMemoryException

È anche possibile ottenere il dump completo della memoria di SSMS quando restituisce un'eccezione di tipo OutOfMemoryException (può trattarsi di qualsiasi eccezione gestita).

Per acquisire le informazioni di diagnostica per la risoluzione dei problemi di un'eccezione di tipo OutOfMemoryException in SSMS, seguire questa procedura.

1. Scaricare [ProcDump](https://technet.microsoft.com/sysinternals/dd996900.aspx).

2. Decomprimere il download in una cartella.

3. Aprire il prompt dei comandi ed eseguire il comando seguente.

    ```cmd
    <PathToProcDumpFolder>\procdump.exe -e 1 -f System.OutOfMemoryException -ma -w ssms.exe
    ```

    Se viene richiesto di accettare un contratto di licenza, selezionare **Accetto**.

4. Avviare SQL Server Management Studio, se non è ancora stato avviato.

5. Riprodurre il problema.

6. Il testo verrà visualizzato nel prompt dei comandi relativo alla scrittura del file di dump. Attendere il completamento dell'operazione.

7. Creare una nuova cartella e copiare il file *.dmp di cui è stata eseguita la scrittura in tale cartella.

8. Copiare i file seguenti nella stessa cartella.

    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\mscordacwks.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\SOS.dll"
    * "C:\Windows\Microsoft.NET\Framework\v4.0.30319\clr.dll"

9. Comprimere la cartella.

## <a name="share-the-information"></a>Condividere le informazioni

1. Per condividere le informazioni con il team di SSMS, registrare il problema all'indirizzo https://aka.ms/sqlfeedback.

2. Quindi condividere il file di dump della memoria raccolto in OneDrive (o una soluzione equivalente) dove il file può essere raccolto.

    > [!Important]
    > I file di dump della memoria possono contenere informazioni sensibili.

## <a name="next-steps"></a>Passaggi successivi

[SQL Server Management Studio](../sql-server-management-studio-ssms.md)