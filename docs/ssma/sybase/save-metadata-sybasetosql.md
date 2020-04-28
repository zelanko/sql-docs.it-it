---
title: Salvare i metadati (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: b2517735-dd19-449f-8cee-08e68ca89d3a
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 3a8cde296fd0a47c407752977f5e41269a05354e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "68020974"
---
# <a name="save-metadata--sybasetosql"></a>Salvare i metadati (SybaseToSQL)
La finestra di dialogo **Salva metadati** richiede di caricare i metadati nel progetto SSMA prima di salvarli. In questo modo è possibile disporre di un file di progetto completo che può essere utilizzato offline e inviato ad altri utenti, ad esempio il personale del supporto tecnico.  
  
Per accedere alla finestra di dialogo **Salva metadati** , salvare il progetto. Se mancano metadati, in SSMA verrà visualizzata la finestra di dialogo **Salva metadati** .  
  
## <a name="options"></a>Opzioni  
**Nome**  
Nome di ogni database nel progetto.  
  
**Stato**  
Indica se i metadati vengono caricati nel progetto SSMA o se i metadati risultano mancanti.  
  
SSMA carica i metadati nel progetto, se necessario. I metadati vengono caricati automaticamente quando si esplorano i metadati e si convertono gli schemi.  
  
**Seleziona tutto**  
Seleziona tutti i database elencati.  
  
**Deselezionare**  
Deseleziona la casella di controllo per tutti i database con metadati mancanti. Non è possibile deselezionare la casella di controllo se i metadati sono stati caricati.  
  
**Salva**  
Salva il progetto, caricando i metadati per i database selezionati che contengono metadati mancanti.  
  
**Annulla**  
Annulla l'operazione di salvataggio. I metadati mancanti non vengono caricati nel progetto.  
  
