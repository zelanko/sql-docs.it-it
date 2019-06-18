---
title: Problemi noti in questa versione del driver per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- known issues
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 86b87d03a5b0a66ba1e77260a0ec0b43125fa98b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798760"
---
# <a name="known-issues-in-this-version-of-the-driver"></a>Problemi noti in questa versione del driver

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Questo argomento contiene un elenco di problemi noti relativi a Microsoft ODBC Driver for SQL Server 13, 13.1 e 17 in Linux e macOS.

Altri problemi verranno pubblicati nel [blog del team di Microsoft ODBC Driver](https://blogs.msdn.com/b/sqlnativeclient/).  

- Windows, Linux e macOS convertono i caratteri provenienti dall'Area uso privato (PUA) o i caratteri definiti dall'utente finale (EUDC) in modo diverso. Per le conversioni eseguite sul server all'interno di [!INCLUDE[tsql](../../../includes/tsql-md.md)] viene usata la libreria di conversione Windows. Le conversioni eseguite nel driver usano le librerie di conversione Windows, Linux o macOS. Le conversioni eseguite con le due librerie possono produrre risultati diversi. Per altre informazioni, vedere [End-User-Defined and Private Use Area Characters](/windows/desktop/Intl/end-user-defined-characters) (Caratteri definiti dall'utente finale e caratteri di area uso privato).

- Se la codifica del client è UTF-8, Gestione driver non esegue sempre correttamente la conversione da UTF-8 a UTF-16. Attualmente se uno o più caratteri della stringa non sono caratteri UTF-8 validi, i dati vengono danneggiati. I caratteri ASCII vengono mappati correttamente. Gestione driver tenta questa conversione quando si chiamano le versioni SQLCHAR dell'API ODBC (ad esempio, SQLDriverConnectA). Gestione driver non tenterà questa conversione quando si chiamano le versioni SQLWCHAR dell'API ODBC (ad esempio, SQLDriverConnectW).  

- Il parametro *ColumnSize* di **SQLBindParameter** fa riferimento al numero di caratteri nel tipo SQL, mentre *BufferLength* è il numero di byte nel buffer dell'applicazione. Tuttavia, se il tipo di dati SQL è `varchar(n)` o `char(n)`, se l'applicazione associa il parametro come SQL_C_CHAR o SQL_C_VARCHAR e se la codifica dei caratteri del client è UTF-8, è possibile che si verifichi un errore "Troncamento a destra della stringa di dati" nel driver anche se il valore di *ColumnSize* è allineato con la dimensione del tipo di dati nel server. Questo errore si verifica perché le conversioni tra codifiche di caratteri possono cambiare la lunghezza dei dati. Ad esempio un carattere virgoletta singola destra (U+2019) è codificato in CP-1252 come 0x92 a byte singolo, mentre in UTF-8 è codificato come sequenza a tre byte 0xe2 0x80 0x99.

Ad esempio se la codifica è UTF-8 e si specifica 1 sia per *BufferLength* sia per *ColumnSize* in **SQLBindParameter** per un parametro out, quindi si prova a recuperare il carattere precedente archiviato in una colonna `char(1)` nel server (usando CP-1252), il driver tenta di convertirlo alla codifica UTF-8 a 3 byte, ma non può adattare il risultato in un buffer di 1 byte. Nella direzione opposta, *ColumnSize* viene confrontato con *BufferLength* in **SQLBindParameter** prima della conversione tra le diverse tabelle codici su client e server. Poiché il valore 1 di *ColumnSize* è minore di un valore *BufferLength* di 3 (ad esempio), il driver genera un errore. Per evitare questo errore, verificare che la lunghezza dei dati dopo la conversione si adatti correttamente al buffer o alla colonna specificati. Si noti che *ColumnSize* non può essere maggiore di 8000 per il tipo `varchar(n)`.

## <a name="see-also"></a>Vedere anche  
[Linee guida per la programmazione](../../../connect/odbc/linux-mac/programming-guidelines.md)  
[Note sulla versione](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  

