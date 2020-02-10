---
title: MSSQLSERVER_8992 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8992 (Database Engine error)
ms.assetid: 68467e6a-09d8-478f-8bd9-3bb09453ada3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8ad75e136c4bef59f24b451b84f03e06d71a32ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62912545"
---
# <a name="mssqlserver_8992"></a>MSSQLSERVER_8992
    
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|8992|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|DBCC3_CHECK_CATALOG|  
|Testo del messaggio|Messaggio di controllo del catalogo ERROR, stato STATE: MESSAGE.|  
  
## <a name="explanation"></a>Spiegazione  
 DBCC CHECKCATALOG o DBCC CHECKDB ha rilevato un'incoerenza nelle tabelle di metadati di sistema per l'oggetto specificato. Ciò significa che vi è un'incoerenza tra l'ID dell'oggetto registrato e l'oggetto specificato nel messaggio di errore.  
  
 Questo errore può verificarsi quando una o più tabelle di sistema sono state aggiornate manualmente in modo da creare un'incoerenza nei metadati di sistema. Un utente, ad esempio, può avere manualmente eliminato un oggetto dalla tabella **sysobjects** senza rimuovere le righe associate in altre tabelle, quali **sysindexes** e **syscolumns**.  
  
 Questo errore può verificarsi quando si esegue DBCC CHECKDB su un database aggiornato da SQL Server 2000 a SQL Server 2005 o versione successiva. Poiché in SQL Server 2000 DBCC CHECKDB non include la funzionalità DBCC CHECKCATALOG, l'errore non viene rilevato prima dell'aggiornamento a meno di non eseguire DBCC CHECKCATALOG in modo specifico sul database.  
  
 È possibile che venga visualizzato uno degli errori seguenti insieme all'errore 8992:  
  
 Messaggio 3851 - Trovata una riga non valida (%ls) nella tabella di sistema sys.%ls%ls.  
  
 Messaggio 3852 - Per la riga (%ls) di sys.%ls%ls non esiste una riga corrispondente (%ls) in sys.%ls%ls.  
  
 Messaggio 3853 - Per l'attributo (%ls) della riga (%ls) di sys.%ls%ls non esiste una riga corrispondente (%ls) in sys.%ls%ls.  
  
 Messaggio 3854 - Per l'attributo (%ls) della riga (%ls) di sys.%ls%ls esiste una riga corrispondente (%ls) in sys.%ls%ls che non è valida.  
  
 Messaggio 3855 - L'attributo (%ls) esiste senza una riga (%ls) in sys.%ls%ls.  
  
 Messaggio 3856 - L'attributo (%ls) esiste, ma non dovrebbe esistere per la riga (%ls) in sys.%ls%ls.  
  
 Messaggio 3857 - L'attributo (%ls) è necessario ma è assente per la riga (%ls) in sys.%ls%ls.  
  
 Messaggio 3858 - Il valore dell'attributo (%ls) della riga (%ls) in sys.%ls%ls non è valido.  
  
## <a name="user-action"></a>Azione dell'utente  
  
### <a name="drop-and-re-create-the-specified-object"></a>Rimuovere e ricreare l'oggetto specificato  
 Se possibile, rimuovere e ricreare l'oggetto specificato. Se, ad esempio, l'oggetto è una stored procedure di tipo definito dall'utente (UDT), una nuova creazione dell'oggetto potrebbe risolvere il problema.  
  
### <a name="restore-from-backup"></a>Eseguire un ripristino da backup  
 Se il problema non è correlato all'hardware ed è disponibile un backup valido noto, ripristinare il database dal backup. Questa azione è utile solo se il backup non contiene errori dei metadati.  
  
### <a name="export-the-data-to-a-new-database"></a>Esportare i dati in un nuovo database  
 Se nel backup sono contenuti anche metadati incoerenti, è necessario creare un nuovo database in cui esportare il contenuto di quello esistente.  
  
### <a name="dbcc-checkdb-cannot-repair-this-error"></a>Impossibile correggere questo errore con DBCC CHECKDB  
 Impossibile correggere questo errore.  Se non è possibile ripristinare il database da un backup, contattare il Servizio Supporto Tecnico Clienti [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
### <a name="do-not-manually-update-system-tables"></a>Non aggiornare manualmente le tabelle di sistema  
 Non effettuare aggiornamenti manuali alle tabelle di sistema. SQL Server non supporta alcuna modifica manuale ai database di sistema. Se si aggiorna una tabella di sistema in un database di SQL Server, vengono registrati due eventi, evento ID 17659 ed evento ID 3859. Per ulteriori informazioni, vedere l'articolo della Knowledge Base 2688307 relativo agli eventi ID 17659 e ID 3859 registrati durante l'aggiornamento di tabelle di sistema in un database di SQL Server.  
  
## <a name="see-also"></a>Vedere anche  
 [Gli eventi con ID 17659 e ID 3859 vengono registrati durante l'aggiornamento delle tabelle di sistema in un database di SQL Server](https://support.microsoft.com/kb/2688307/EN-US)  
  
  
