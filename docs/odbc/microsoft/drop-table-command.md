---
title: Comando DROP TABLE Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 779c519f720027aea3a6f6cf2587d3c6e0b59b52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303422"
---
# <a name="drop-table-command"></a>DROP TABLE (comando)
Rimuove una tabella dal database specificato con l'origine dati e la elimina dal disco.  
  
 Il driver ODBC di Visual FoxPro supporta la sintassi nativa del linguaggio Visual FoxPro per questo comando. Per informazioni specifiche del driver, vedere la pagina Osservazioni.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>Impostazioni  
 *Tablename*  
 Specifica la tabella da rimuovere dal database specificato con l'origine dati e da eliminare dal disco.  
  
 *Filename*  
 Specifica una tabella libera da eliminare dal disco.  
  
 ?  
 Visualizza la finestra di dialogo Rimuovi da cui è possibile scegliere una tabella da rimuovere dal database specificato con l'origine dati ed eliminare dal disco.  
  
## <a name="remarks"></a>Osservazioni  
 Quando viene emesso DROP TABLE, vengono rimossi anche tutti gli indici primari, i valori predefiniti e le regole di convalida associate alla tabella. DROP TABLE influisce anche sulle altre tabelle del database specificato con l'origine dati se tali tabelle hanno regole o relazioni associate alla tabella da rimuovere. Le regole e le relazioni non sono più valide quando la tabella viene rimossa dal database.  
  
## <a name="driver-remarks"></a>Osservazioni del conducente  
 Quando l'applicazione invia l'istruzione SQL ODBC DROP TABLE all'origine dati, il driver ODBC di Visual FoxPro converte il comando nel comando Table di Visual FoxProDROP utilizzando la sintassi illustrata nella tabella seguente.  
  
|Sintassi ODBC|Origine dati|Sintassi di Visual FoxPro|  
|-----------------|-----------------|--------------------------|  
|NOME *tabella di base* DROP TABLE|Database (file con estensione dbc)|REMOVE *TABLEName NOMECAN*|  
||Directory delle tabelle libere (file con estensione dbf)|Nome *dbf* ERASE<br /><br /> NOME *cdx* ERASE<br /><br /> ERASE *fptName*|
