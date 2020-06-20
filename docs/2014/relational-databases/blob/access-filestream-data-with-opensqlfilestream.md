---
title: Accedere a dati FILESTREAM con OpenSqlFilestream | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
api_name:
- OpenSqlFilestream
api_location:
- sqlncli11.dll
helpviewer_keywords:
- OpenSqlFilestream
ms.assetid: d8205653-93dd-4599-8cdf-f9199074025f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1a1416c0104e07c7bd228a723192ecb35bbe9216
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84955991"
---
# <a name="access-filestream-data-with-opensqlfilestream"></a>Accesso ai dati FILESTREAM con OpenSqlFilestream
  L'API OpenSqlFilestream ottiene un handle di file compatibile con Win32 per un BLOB (Binary Large Object) FILESTREAM archiviato nel file system. L'handle può essere passato a una qualsiasi delle API Win32 seguenti: [ReadFile](https://go.microsoft.com/fwlink/?LinkId=86422), [WriteFile](https://go.microsoft.com/fwlink/?LinkId=86423), [TransmitFile](https://go.microsoft.com/fwlink/?LinkId=86424), [SetFilePointer](https://go.microsoft.com/fwlink/?LinkId=86425), [SetEndOfFile](https://go.microsoft.com/fwlink/?LinkId=86426)o [FlushFileBuffers](https://go.microsoft.com/fwlink/?LinkId=86427). Se si passa questo handle a qualsiasi altra API Win32, viene restituito l'errore ERROR_ACCESS_DENIED. L'handle deve essere chiuso passandolo all'API [CloseHandle](https://go.microsoft.com/fwlink/?LinkId=86428) Win32 prima che venga eseguito il commit o il rollback della transazione. La mancata chiusura dell'handle provoca perdite di risorse sul lato server.  
  
 L'accesso al contenitore di tutti i dati FILESTREAM deve essere eseguito in una transazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[tsql](../../includes/tsql-md.md)] Anche le istruzioni possono essere eseguite nella stessa transazione. In questo modo viene mantenuta la coerenza tra i dati SQL e dati BLOB FILESTREAM.  
  
 Per accedere al BLOB FILESTREAM usando Win32, è necessario abilitare l' [autorizzazione Windows](../security/choose-an-authentication-mode.md) .  
  
> [!IMPORTANT]  
>  Quando il file è aperto per l'accesso in scrittura, la transazione è di proprietà dell'agente FILESTREAM. Finché non viene rilasciata la transazione è consentito solo l'I/O dei file Win32. Per rilasciare la transazione, è necessario chiudere l'handle di scrittura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
  HANDLE OpenSqlFilestream (  
  LPCWSTR  
  FilestreamPath  
  ,  
  SQL_FILESTREAM_DESIRED_ACCESS  
  DesiredAccess,  
ULONGOpenOptions,LPBYTEFilestreamTransactionContext,SIZE_TFilestreamTransactionContextLength,PLARGE_INTEGERAllocationSize);  
```  
  
#### <a name="parameters"></a>Parametri  
 *FilestreamPath*  
 in `nvarchar(max)`Percorso restituito dalla funzione [pathname](/sql/relational-databases/system-functions/pathname-transact-sql) . La funzione PathName deve essere chiamata dal contesto di un account che dispone dell'autorizzazione SELECT o UPDATE di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per la tabella e la colonna FILESTREAM.  
  
 *DesiredAccess*  
 [in] Imposta la modalità utilizzata per accedere ai dati BLOB FILESTREAM. Questo valore viene passato alla [funzione DeviceIoControl](https://go.microsoft.com/fwlink/?LinkId=105527).  
  
|Nome|valore|Significato|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_READ|0|I dati possono essere letti dal file.|  
|SQL_FILESTREAM_WRITE|1|I dati possono essere scritti nel file.|  
|SQL_FILESTREAM_READWRITE|2|I dati possono essere scritti e letti dal file.|  
  
> [!NOTE]  
>  Questi valori vengono definiti nell'enumerazione SQL_FILESTREAM_DESIRED_ACCESS in sqlncli.h.  
  
 *OpenOptions*  
 [in] Attributi e flag del file. Questo parametro può includere inoltre qualsiasi combinazione dei flag seguenti.  
  
|Flag|valore|Significato|  
|----------|-----------|-------------|  
|SQL_FILESTREAM_OPEN_NONE|0x00000000:|Il file è aperto o creato senza opzioni speciali.|  
|SQL_FILESTREAM_OPEN_FLAG_ASYNC|0x00000001L|Il file è aperto o creato per gli I/O asincroni.|  
|SQL_FILESTREAM_OPEN_FLAG_NO_BUFFERING|0x00000002L|Il sistema apre il file senza utilizzare la memorizzazione nella cache di sistema.|  
|SQL_FILESTREAM_OPEN_FLAG_NO_WRITE_THROUGH|0x00000004L|Il sistema scrive senza utilizzare alcuna cache intermedia, ma accede direttamente al disco.|  
|SQL_FILESTREAM_OPEN_FLAG_SEQUENTIAL_SCAN|0x00000008L|L'accesso a un file viene eseguito in sequenza, partendo dall'inizio e fino alla fine. Il sistema può interpretare questa situazione come hint per l'ottimizzazione della memorizzazione del file nella cache. Se un'applicazione sposta il puntatore del file per l'accesso casuale, potrebbe non essere possibile ottimizzare la memorizzazione nella cache.|  
|SQL_FILESTREAM_OPEN_FLAG_RANDOM_ACCESS|0x00000010L|L'accesso al un file viene eseguito in modo casuale. Il sistema può interpretare questa situazione come hint per l'ottimizzazione della memorizzazione del file nella cache.|  
  
 *FilestreamTransactionContext*  
 [in] Valore restituito dalla funzione [GET_FILESTREAM_TRANSACTION_CONTEXT](/sql/t-sql/functions/get-filestream-transaction-context-transact-sql) .  
  
 *FilestreamTransactionContextLength*  
 [in] Numero di byte nei dati `varbinary(max)` restituiti dalla funzione GET_FILESTREAM_TRANSACTION_CONTEXT. La funzione restituisce una matrice di N byte. Il valore N è determinato dalla funzione e costituisce una proprietà della matrice di byte restituita.  
  
 *AllocationSize*  
 [in] Specifica le dimensioni dell'allocazione iniziale del file di dati in byte. In modalità di lettura viene ignorato. Questo parametro può essere Null nel caso in cui venga utilizzato il comportamento del file system predefinito.  
  
## <a name="return-value"></a>Valore restituito  
 Se la funzione viene eseguita correttamente, il valore restituito è un handle aperto per il file specificato. Se la funzione ha esito negativo, il valore restituito è INVALID_HANDLE_VALUE. Per informazioni dettagliate sull'errore, chiamare GetLastError().  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti viene illustrato come utilizzare l'API `OpenSqlFilestream` per ottenere un handle Win32.  
  
 [!code-csharp[FILESTREAM#FS_CS_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cs/filestream.cs#fs_cs_readandwriteblob)]  
  
 [!code-vb[FILESTREAM#FS_VB_ReadAndWriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/vb/filestream.vb#fs_vb_readandwriteblob)]  
  
 [!code-cpp[FILESTREAM#FS_CPP_WriteBLOB](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_writeblob)]  
  
## <a name="remarks"></a>Osservazioni  
 Per utilizzare questa API, è necessario che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sia installato. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client viene installato con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o con gli strumenti client di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni, vedere [Installazione di SQL Server Native Client](../native-client/applications/installing-sql-server-native-client.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Dati BLOB (Binary Large Object) (SQL Server)](binary-large-object-blob-data-sql-server.md)   
 [Esecuzione di aggiornamenti parziali di dati FILESTREAM](make-partial-updates-to-filestream-data.md)   
 [Evitare conflitti con le operazioni del database nelle applicazioni di FILESTREAM](avoid-conflicts-with-database-operations-in-filestream-applications.md)  
  
  
