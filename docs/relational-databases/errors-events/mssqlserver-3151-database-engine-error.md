---
title: MSSQLSERVER_3151 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3151 (Database Engine error)
ms.assetid: a8657a91-ec75-4649-a09a-21920e0030ff
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d0d4c51bd7f4e1eca3bf57fbcfa89aec93357fb0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723738"
---
# <a name="mssqlserver_3151"></a>MSSQLSERVER_3151
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|3151|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|LDDB_MASTER_LOAD_FAILED|  
|Testo del messaggio|Impossibile ripristinare il database master. SQL Server verrà chiuso. Controllare i log degli errori e ricompilare il database master. Per ulteriori informazioni sulla ricompilazione del database master, vedere la documentazione online di SQL Server.|  
  
## <a name="explanation"></a>Spiegazione  
Si tratta di un messaggio di errore generale che indica vari problemi relativi al database **master**.  
  
## <a name="user-action"></a>Azione dell'utente  
Per ulteriori informazioni esaminare i log degli errori. Per creare un database **master** utilizzabile, eseguire Setup.exe con l'opzione REBUILDDATABASE. Per altre informazioni, vedere "Procedura: Installare SQL Server dal prompt dei comandi" nella documentazione online di SQL Server.  
  
