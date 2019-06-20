---
title: Proprietà database (pagina File) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.files.f1
ms.assetid: 3c030e51-db82-4b43-b1e5-8547ddd3de87
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 36b0d8b5d91b18ad4b97ac873ad3073ca97b133e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871987"
---
# <a name="database-properties-files-page"></a>Proprietà database (pagina File)
  Utilizzare questa pagina per creare un nuovo database oppure per visualizzare o modificare le proprietà del database selezionato. Questo argomento si applica a **Proprietà database (pagina File)** per i database esistenti e a **Nuovo database (pagina Generale)** .  
  
## <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Nome database**  
 È possibile aggiungere o visualizzare il nome del database.  
  
 **Proprietario**  
 È possibile specificare il proprietario del database selezionandolo nell'elenco.  
  
 **Usa indicizzazione full-text**  
 Questa casella di controllo è selezionata e disabilitata perché l'indicizzazione full-text è sempre abilitata in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per altre informazioni, vedere [Ricerca full-text](../search/full-text-search.md).  
  
 **File di database**  
 È possibile aggiungere, visualizzare, modificare o rimuovere file del database associato. I file di database dispongono delle proprietà seguenti:  
  
 **Nome logico**  
 È possibile immettere o modificare il nome del file.  
  
 **Tipo di file**  
 È possibile selezionare il tipo di file nell'elenco. Il tipo di file può essere **Dati**, **Log**o **Dati FILESTREAM**. Non è possibile modificare il tipo di file di un file esistente.  
  
 Selezionare **Dati FILESTREAM** se si aggiungono file (contenitori) a un filegroup ottimizzato per la memoria.  
  
 Per aggiungere file (contenitori) a un filegroup di dati FILESTREAM, FILESTREAM deve essere abilitato. È possibile abilitare FILESTREAM usando la finestra di dialogo [Proprietà server (pagina Avanzate)](../../database-engine/configure-windows/server-properties-advanced-page.md) .  
  
 **Filegroup**  
 È possibile selezionare il filegroup per il file nell'elenco. Per impostazione predefinita, il filegroup è PRIMARY. È possibile creare un nuovo filegroup selezionando **\<nuovo filegroup>** e immettendo informazioni sul filegroup nella finestra di dialogo **Nuovo filegroup**. Anche nella pagina **Filegroup** è possibile creare un nuovo filegroup. Non è possibile modificare il filegroup di un file esistente.  
  
 Quando si aggiungono file (contenitori) a un filegroup ottimizzato per la memoria, il campo **Filegroup** viene popolato con il nome del filegroup ottimizzato per la memoria del database.  
  
 **Dimensioni iniziali**  
 È possibile immettere o modificare le dimensioni iniziali in megabyte del file. Per impostazione predefinita, questo valore corrisponde a quello del database **model** .  
  
 Questo campo non è valido per i file FILESTREAM.  
  
 Per i file nei filegroup ottimizzati per la memoria, questo campo non può essere modificato.  
  
 **Aumento automatico**  
 È possibile selezionare o visualizzare le proprietà dell'aumento automatico per il file. Queste proprietà controllano l'espansione del file al raggiungimento delle dimensioni massime. Per modificare i valori di aumento automatico fare clic sul pulsante di modifica accanto alle proprietà di aumento automatico relative al file desiderato e modificare i valori nella finestra di dialogo **Cambia aumento automatico dimensioni** . Per impostazione predefinita, questi valori corrispondono a quelli del database **model** .  
  
 Questo campo non è valido per i file FILESTREAM.  
  
 Per i file nei filegroup ottimizzati per la memoria, questo campo deve essere **Senza limiti**.  
  
 **Percorso**  
 È possibile visualizzare il percorso del file selezionato. Per specificare il percorso di un nuovo file fare clic sul pulsante di modifica accanto al percorso del file e passare alla cartella di destinazione. Non è possibile modificare il percorso di un file esistente.  
  
 Per i file FILESTREAM, il percorso è una cartella. Il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] creerà i file sottostanti in questa cartella.  
  
 **Nome file**  
 È possibile visualizzare il nome del file.  
  
 Questo campo non è valido per i file FILESTREAM, inclusi i file nei filegroup ottimizzati per la memoria.  
  
 **Aggiungi**  
 È possibile aggiungere un nuovo file al database.  
  
 **Rimuovi**  
 È possibile eliminare il file selezionato dal database. È possibile eliminare solo file vuoti. Non è possibile eliminare i file di dati e di log primari.  
  
 Per altre informazioni sui file, vedere [Filegroup e file di database](database-files-and-filegroups.md).  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
  
